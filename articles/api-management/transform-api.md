---
title: Uw API transformeren en beveiligen met Azure API Management | Microsoft Docs
description: Informatie over het beveiligen van uw API met beleidsregels voor quota en (frequentie)beperking.
services: api-management
documentationcenter: ''
author: vladvino
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.custom: mvc
ms.topic: tutorial
ms.date: 11/19/2017
ms.author: apimpm
ms.openlocfilehash: bebfabfa2c9012fa55bfc6964dc0b638cb7ab3f1
ms.sourcegitcommit: d98d99567d0383bb8d7cbe2d767ec15ebf2daeb2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/10/2018
---
# <a name="transform-and-protect-your-api"></a>Uw API transformeren en beveiligen 

In de zelfstudie ziet u hoe u uw API kunt transformeren zodat deze geen persoonlijke back-endgegevens vrijgeeft. U kunt bijvoorbeeld de gegevens verbergen over de technologiestack die op de back-end wordt uitgevoerd. U kunt ook de oorspronkelijke URL's verbergen die worden weergegeven in de hoofdtekst van het HTTP-antwoord van de API, en deze in plaats hiervan omleiden naar de APIM-gateway.

In deze zelfstudie kunt u ook zien hoe eenvoudig het is om beveiliging toe te voegen voor uw back-end-API door de frequentielimiet te configureren met Azure API Management. U kunt bijvoorbeeld het aantal aanroepen voor de API beperken, zodat deze niet wordt overbelast door ontwikkelaars. Zie [API Management-beleid](api-management-policies.md) voor meer informatie

In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Een API transformeren om antwoordheaders te verwijderen
> * Oorspronkelijke URL's in de hoofdtekst van het API-antwoord vervangen door APIM-gateway-URL's
> * Een API beveiligen door beleid voor frequentielimieten toe te voegen
> * De transformaties testen

![Beleidsregels](./media/transform-api/api-management-management-console.png)

## <a name="prerequisites"></a>Vereisten

+ Lees de volgende snelstartgids: [Een Azure API Management-exemplaar maken](get-started-create-service-instance.md).
+ Voltooi tevens de volgende zelfstudie: [Uw eerste API importeren en publiceren](import-and-publish.md).
 
[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-navigate-to-instance.md)]

## <a name="transform-an-api-to-strip-response-headers"></a>Een API transformeren om antwoordheaders te verwijderen

In deze sectie wordt beschreven hoe u de HTTP-headers kunt verbergen die u niet wilt weergeven aan gebruikers. In dit voorbeeld worden de volgende headers in het HTTP-antwoord verwijderd:

* **X-Powered-By**
* **X-AspNet-Version**

### <a name="test-the-original-response"></a>Het oorspronkelijke antwoord testen

Het oorspronkelijke antwoord zien:

1. Selecteer het tabblad **API**.
2. Klik in de API-lijst op **Demo Conference API**.
3. Selecteer de bewerking **GetSpeakers**.
4. Klik bovenaan het scherm op het tabblad **Testen**.
5. Klik onderaan het scherm op de knop **Verzenden**. 

    Zoals u kunt zien, ziet het oorspronkelijke antwoord er als volgt uit:

    ![Beleidsregels](./media/transform-api/original-response.png)

### <a name="set-the-transformation-policy"></a>Transformatiebeleid instellen

1. Blader naar de APIM-instantie.
2. Selecteer het tabblad **API**.
3. Klik in de API-lijst op **Demo Conference API**.
4. Selecteer **Alle bewerkingen**.
5. Selecteer boven in het scherm het tabblad **Ontwerp**.
6. Klik in het venster **Uitgaande verwerking** op het driehoekje (naast het potlood).
7. Selecteer **Code-editor**.
    
     ![Beleid bewerken](./media/set-edit-policies/set-edit-policies01.png)
9. Plaats de cursor in het **&lt;uitgaande&gt;** element.
10. Klik in het rechtervenster onder **Transformatiebeleid** twee keer op **+ HTTP-header instellen** (om twee beleidsfragmenten in te voegen).

    ![Beleidsregels](./media/transform-api/transform-api.png)
11. Wijzig de code **<outbound>** zodat deze er als volgt uitziet:

        <set-header name="X-Powered-By" exists-action="delete" />
        <set-header name="X-AspNet-Version" exists-action="delete" />
                
## <a name="replace-original-urls-in-the-body-of-the-api-response-with-apim-gateway-urls"></a>Oorspronkelijke URL's in de hoofdtekst van het API-antwoord vervangen door APIM-gateway-URL's

In deze sectie ziet u hoe u de oorspronkelijke URL's kunt verbergen die worden weergegeven in de hoofdtekst van het HTTP-antwoord van de API, en deze in plaats hiervan kunt omleiden naar de APIM-gateway.

### <a name="test-the-original-response"></a>Het oorspronkelijke antwoord testen

Het oorspronkelijke antwoord zien:

1. Selecteer het tabblad **API**.
2. Klik in de API-lijst op **Demo Conference API**.
3. Selecteer de bewerking **GetSpeakers**.
4. Klik bovenaan het scherm op het tabblad **Testen**.
5. Klik onderaan het scherm op de knop **Verzenden**. 

    Zoals u kunt zien, ziet het oorspronkelijke antwoord er als volgt uit:

    ![Beleidsregels](./media/transform-api/original-response2.png)

### <a name="set-the-transformation-policy"></a>Transformatiebeleid instellen

1. Blader naar de APIM-instantie.
2. Selecteer het tabblad **API**.
3. Klik in de API-lijst op **Demo Conference API**.
4. Selecteer **Alle bewerkingen**.
5. Selecteer boven in het scherm het tabblad **Ontwerp**.
6. Klik in het venster **Uitgaande verwerking** op het driehoekje (naast het potlood).
7. Selecteer **Code-editor**.
8. Plaats de cursor in het **&lt;uitgaande&gt;** element.
9. Klik in het rechtervenster onder **Transformatiebeleid** twee keer op **+ Tekenreeks in hoofdtekst zoeken en vervangen**.
10. Wijzig de code **<find-and-replace** (in het element **<outbound>**) om de URL te vervangen zodat deze overeenkomt met de APIM-gateway. Bijvoorbeeld:

        <find-and-replace from="://conferenceapi.azurewebsites.net" to="://apiphany.azure-api.net/conference"/>

## <a name="protect-an-api-by-adding-rate-limit-policy-throttling"></a>Een API beveiligen door beleid voor frequentielimieten toe te voegen

In deze sectie wordt beschreven hoe u beveiliging voor uw back-end-API kunt toevoegen door frequentielimieten te configureren. U kunt bijvoorbeeld het aantal aanroepen voor de API beperken, zodat deze niet wordt overbelast door ontwikkelaars. In dit voorbeeld is de limiet ingesteld op 3 aanroepen per 15 seconden voor elke abonnements-id. Na 15 seconden kan een ontwikkelaar de API opnieuw proberen aan te roepen.

1. Blader naar de APIM-instantie.
2. Selecteer het tabblad **API**.
3. Klik in de API-lijst op **Demo Conference API**.
4. Selecteer **Alle bewerkingen**.
5. Selecteer boven in het scherm het tabblad **Ontwerp**.
6. Klik in het venster **Binnenkomende verwerking** op het driehoekje (naast het potlood).
7. Selecteer **Code-editor**.
8. Plaats de cursor in het **&lt;binnenkomende&gt;** element.
9. Klik in het rechtervenster onder **Toegang tot beperkingsbeleid** op **+ Aantal oproepen per sleutel beperken**.
10. Wijzig de code **< rate-limit-by-key** (in het element **<inbound>**) in de volgende code:

        <rate-limit-by-key calls="3" renewal-period="15" counter-key="@(context.Subscription.Id)" />

## <a name="test-the-transformations"></a>De transformaties testen
        
Op dit moment ziet uw beleidscode er ongeveer als volgt uit:

    <policies>
        <inbound>
            <rate-limit-by-key calls="3" renewal-period="15" counter-key="@(context.Subscription.Id)" />
            <base />
        </inbound>
        <backend>
            <base />
        </backend>
        <outbound>
            <set-header name="X-Powered-By" exists-action="delete" />
            <set-header name="X-AspNet-Version" exists-action="delete" />
            <find-and-replace from="://conferenceapi.azurewebsites.net" to="://apiphany.azure-api.net/conference"/>
            <base />
        </outbound>
        <on-error>
            <base />
        </on-error>
    </policies>

In de rest van deze sectie worden de beleidstransformaties getest die u in dit artikel hebt ingesteld.

### <a name="test-the-stripped-response-headers"></a>De verwijderde anwoordheaders testen

1. Blader naar de APIM-instantie.
2. Selecteer het tabblad **API**.
3. Klik in de API-lijst op **Demo Conference API**.
4. Selecteer de bewerking **GetSpeakers**.
5. Selecteer het tabblad **Testen**.
6. Druk op **Verzenden**.

    Zoals u ziet, zijn de headers verwijderd:

    ![Beleidsregels](./media/transform-api/final-response1.png)

### <a name="test-the-replaced-url"></a>De vervangen URL testen

1. Blader naar de APIM-instantie.
2. Selecteer het tabblad **API**.
3. Klik in de API-lijst op **Demo Conference API**.
4. Selecteer de bewerking **GetSpeakers**.
5. Selecteer het tabblad **Testen**.
6. Druk op **Verzenden**.

    Zoals u ziet, is de URL vervangen.

    ![Beleidsregels](./media/transform-api/final-response2.png)

### <a name="test-the-rate-limit-throttling"></a>De frequentielimiet testen

1. Blader naar de APIM-instantie.
2. Selecteer het tabblad **API**.
3. Klik in de API-lijst op **Demo Conference API**.
4. Selecteer de bewerking **GetSpeakers**.
5. Selecteer het tabblad **Testen**.
6. Druk drie keer achter elkaar op **Verzenden**.

    Nadat de aanvraag 3 keer is verzonden, ontvangt u het antwoord **429 Te veel aanvragen**.
7. Wacht ongeveer 15 seconden en druk opnieuw op **Verzenden**. Deze keer ontvangt u, als het goed is, het antwoord **200 OK**.

    ![Beperking](./media/transform-api/test-throttling.png)

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie heeft u het volgende geleerd:

> [!div class="checklist"]
> * Een API transformeren om antwoordheaders te verwijderen
> * Oorspronkelijke URL's in de hoofdtekst van het API-antwoord vervangen door APIM-gateway-URL's
> * Een API beveiligen door beleid voor frequentielimieten toe te voegen
> * De transformaties testen

Ga door naar de volgende zelfstudie:

> [!div class="nextstepaction"]
> [Uw API controleren](api-management-howto-use-azure-monitor.md)
