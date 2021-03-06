---
title: Veilige communicatie voor services in Azure Service Fabric Help | Microsoft Docs
description: Overzicht van hoe u kunt beveiligde communicatie voor betrouwbare services die worden uitgevoerd in een Azure Service Fabric-cluster.
services: service-fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: ''
ms.service: service-fabric
ms.devlang: java
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/30/2017
ms.author: pakunapa
ms.openlocfilehash: 624d9d358145fb8b41013d686821cb157693d3c6
ms.sourcegitcommit: eb75f177fc59d90b1b667afcfe64ac51936e2638
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/16/2018
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a>Veilige communicatie van de Help voor services in Azure Service Fabric
> [!div class="op_single_selector"]
> * [C# op Windows](service-fabric-reliable-services-secure-communication.md)
> * [Java op Linux](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a>Beveiligen van een service als u service voor externe toegang
We gebruiken hiervoor een bestaande [voorbeeld](service-fabric-reliable-services-communication-remoting-java.md) waarin wordt uitgelegd hoe instellen van externe toegang voor betrouwbare services. Ter beveiliging van een service, wanneer u externe toegang de service de volgende stappen uit:

1. Maken van een interface `HelloWorldStateless`, die definieert de methoden die beschikbaar zijn voor een externe procedureaanroep voor uw service. Uw service maakt gebruik van `FabricTransportServiceRemotingListener`, die is gedeclareerd in de `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` pakket. Dit is een `CommunicationListener` -implementatie mogelijkheden voor externe toegang biedt.

    ```java
    public interface HelloWorldStateless extends Service {
        CompletableFuture<String> getHelloWorld();
    }

    class HelloWorldStatelessImpl extends StatelessService implements HelloWorldStateless {
        @Override
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
        return listeners;
        }

        public CompletableFuture<String> getHelloWorld() {
            return CompletableFuture.completedFuture("Hello World!");
        }
    }
    ```
2. Instellingen voor listener en beveiligingsreferenties toevoegen.

    Zorg ervoor dat het certificaat dat u wilt gebruiken om te helpen beveiligen van uw servicecommunicatie is geïnstalleerd op alle knooppunten in het cluster. Er zijn twee manieren waarop u instellingen voor listener en beveiligingsreferenties kunt opgeven:

   1. Ze bieden met behulp van een [configuratiepakket](service-fabric-application-and-service-manifests.md):

       Voeg een `TransportSettings` sectie in het bestand settings.xml.

       ```xml
       <!--Section name should always end with "TransportSettings".-->
       <!--Here we are using a prefix "HelloWorldStateless".-->
        <Section Name="HelloWorldStatelessTransportSettings">
            <Parameter Name="MaxMessageSize" Value="10000000" />
            <Parameter Name="SecurityCredentialsType" Value="X509_2" />
            <Parameter Name="CertificatePath" Value="/path/to/cert/BD1C71E248B8C6834C151174DECDBDC02DE1D954.crt" />
            <Parameter Name="CertificateProtectionLevel" Value="EncryptandSign" />
            <Parameter Name="CertificateRemoteThumbprints" Value="BD1C71E248B8C6834C151174DECDBDC02DE1D954" />
        </Section>

       ```

       In dit geval de `createServiceInstanceListeners` methode ziet er als volgt:

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        Als u een `TransportSettings` sectie in het bestand settings.xml zonder voorvoegsel, `FabricTransportListenerSettings` alle instellingen in deze sectie standaard wordt geladen.

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        In dit geval de `CreateServiceInstanceListeners` methode ziet er als volgt:

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. Wanneer u methoden aanroepen voor een beveiligde service met behulp van de stack voor externe toegang, in plaats van de `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` klasse te maken van een serviceproxy, gebruikt u `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.

    Als de clientcode wordt uitgevoerd als onderdeel van een service, kunt u laden `FabricTransportSettings` uit het bestand settings.xml. Maak een sectie TransportSettings die vergelijkbaar is met de servicecode, zoals eerder besproken. De volgende wijzigingen aanbrengen in de clientcode:

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
