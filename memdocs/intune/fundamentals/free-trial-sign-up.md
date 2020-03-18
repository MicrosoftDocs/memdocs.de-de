---
title: 'Schnellstart: Testen Sie Microsoft Intune kostenlos'
titleSuffix: ''
description: In diesem Schnellstart erstellen Sie ein kostenloses Testabonnement, können unterstützte Konfigurationen und Netzwerkanforderungen nachvollziehen und optional Ihren Domänennamen konfigurieren.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/16/2020
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 195931c0-8208-43bd-b0af-b1f8e469a32c
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 83107121b05b2126e4c6b2b377baf57ee069f917
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79343985"
---
# <a name="quickstart-try-microsoft-intune-for-free"></a>Schnellstart: Testen Sie Microsoft Intune kostenlos

Mit Microsoft Intune können Sie die Unternehmensdaten Ihrer Mitarbeiter durch die Verwaltung von Geräten und Apps schützen. In diesem Schnellstart erstellen Sie ein kostenloses Abonnement, um Intune in einer Testumgebung zu testen.

Intune bietet die Verwaltung mobiler Geräte (Mobile Device Management, MDM) und mobiler Apps (Mobile App Management, MAM) über einen sicheren cloudbasierten Dienst, der mithilfe des Microsoft Endpoint Manager Admin Centers verwaltet wird. Durch die Verwendung von Intune stellen Sie sicher, dass die Unternehmensressourcen Ihrer Mitarbeiter (Daten, Geräte und Apps) ordnungsgemäß konfiguriert und aktualisiert werden und dass ordnungsgemäß darauf zugegriffen werden kann. Dabei wird darauf geachtet, dass die Konformitätsrichtlinien und Anforderungen Ihres Unternehmens eingehalten werden.

## <a name="prerequisites"></a>Voraussetzungen
Prüfen Sie vor der Einrichtung von Microsoft Intune die folgenden Anforderungen:

- [Unterstützte Betriebssysteme und Browser](supported-devices-browsers.md)
- [Bandbreite und Anforderungen an die Netzkonfiguration](network-bandwidth-use.md)

## <a name="sign-up-for-a-microsoft-intune-free-trial"></a>Registrieren für eine kostenlose Testversion von Microsoft Intune

Sie können Intune 30 Tage lang kostenlos testen. Wenn Sie bereits über ein Arbeits- oder Schulkonto verfügen, **melden Sie sich mit diesem Konto an**, und fügen Sie Intune Ihrem Abonnement hinzu. Sie können sich auch für ein neues Konto **registrieren**, um Intune für Ihre Organisation zu verwenden.

> [!IMPORTANT]
> Sie können kein bestehendes Arbeits- oder Schulkonto nach der Registrierung für ein neues Konto kombinieren.

1. Wechseln Sie zur Seite [Microsoft Intune-Testversion](https://go.microsoft.com/fwlink/?linkid=2019088), und füllen Sie das Formular aus.

    ![Screenshot der Website für die Registrierung für das Microsoft Intune-Testkonto](./media/free-trial-sign-up/account-sign-up-site-full-browser.png)

    Wenn sich der Großteil Ihres IT-Betriebs und Ihrer Benutzer in einem anderen Gebietsschema als Sie befindet, sollten Sie dieses Gebietsschema unter **Land oder Region** auswählen. Azure bietet Ihnen aufgrund Ihrer regionalen Informationen die richtigen Dienste an. Diese Einstellung kann später nicht mehr geändert werden.

2. Erstellen Sie ein Konto mit dem Namen Ihres Unternehmens gefolgt von **.onmicrosoft.com**. 

    ![Screenshot des Prozesses für neue Anmeldeinformationen für das Intune-Testkonto](./media/free-trial-sign-up/account-sign-up-site-user-id.png)

    Wenn Ihre Organisation über eine eigene benutzerdefinierte Domäne verfügt, die Sie ohne **.onmicrosoft.com** verwenden möchten, können Sie diese im Microsoft 365 Admin Center ändern. Näheres hierzu wird später in diesem Artikel erläutert.

3. Am Ende des Registrierungsvorgangs werden Ihre neuen Kontoinformationen angezeigt.

    ![Abbildung Ihrer Kontoinformationen](./media/free-trial-sign-up/intune-end-of-sign-up-process.png) 

## <a name="sign-in-to-intune-in-the-microsoft-endpoint-manager"></a>Anmelden bei Intune im Microsoft Endpoint Manager

Wenn Sie noch nicht beim Portal angemeldet sind, führen Sie die folgenden Schritte aus:

1. Öffnen Sie ein neues Browserfenster, und geben Sie **https://devicemanagement.microsoft.com** in die Adressleiste ein. 
2. Verwenden Sie die Benutzer-ID, die Sie in den obigen Schritten erhalten haben, um sich anzumelden ( *yourID@yourdomain* .onmicrosoft.com).

    ![Abbildung der Anmeldeseite des Portals](./media/free-trial-sign-up/azure-portal-signin.png)

Wenn Sie sich für eine Testversion registrieren, wird eine E-Mail mit Ihren Kontoinformationen an die von Ihnen bei der Registrierung angegebene E-Mail-Adresse gesendet. Diese E-Mail bestätigt, dass Ihre Testversion aktiv ist.

> [!TIP]
> Wenn Sie mit dem Microsoft Endpoint Manager, erzielen Sie bessere Ergebnisse, wenn Sie nicht im privaten, sondern im normalen Modus mit Ihrem Browser arbeiten.

## <a name="confirm-the-mdm-authority-in-intune"></a>Bestätigen der MDM-Autorität in Intune

Standardmäßig wird die MDM-Autorität festgelegt, wenn Sie Ihre kostenlose Testversion erstellen. Um sicherzustellen, dass die MDM-Autorität festgelegt ist, gehen Sie folgendermaßen vor:

1. Wenn Sie noch nicht angemeldet sind, melden Sie sich beim Microsoft Endpoint Manager an.
2. Klicken Sie auf **Mandantenverwaltung**.
3. Zeigen Sie die Mandantendetails an. Die **MDM-Autorität** sollte nun auf **Microsoft Intune** festgelegt sein.

Wenn Sie nach der Anmeldung beim Microsoft Endpoint Manager ein orangefarbenes Banner sehen, das anzeigt, dass Sie die MDM-Autorität noch nicht festgelegt haben, können Sie sie zu diesem Zeitpunkt aktivieren. Die Einstellung für die Autorität für die Verwaltung mobiler Geräte (Mobile Device Management, MDM) bestimmt, wie Sie Ihre Geräte verwalten. Die MDM-Autorität muss festgelegt werden, bevor Benutzer Geräte für die Verwaltung registrieren können.

### <a name="to-set-the-mdm-authority-to-intune-follow-these-steps"></a>Führen Sie die folgenden Schritte aus, um die MDM-Autorität in Intune festzulegen:

1. Öffnen Sie ein neues Browserfenster, und geben Sie **https://portal.azure.com** in die Adressleiste ein. 
2. Wählen Sie **Alle Dienste** > **Microsoft Intune** aus.
3. Klicken Sie auf den Banner, in dem darauf hingewiesen wird, dass Sie die Geräteverwaltung nicht aktiviert haben. Wenn der Banner nicht direkt angezeigt wird, klicken Sie auf **Geräteregistrierung**. Wenn Sie die Geräteverwaltung noch nicht aktiviert haben, wird das Blatt **MDM-Autorität wählen** angezeigt.

    > [!NOTE]
    > Wenn Sie die MDM-Autorität festgelegt haben, können Sie den Wert der MDM-Autorität auf dem Blatt **Geräteregistrierung** sehen. Der orangefarbene Banner wird nur angezeigt, wenn Sie die MDM-Autorität noch nicht festgelegt haben. 

    ![Bild des Blatts „MDM-Autorität wählen“](./media/free-trial-sign-up/choose-mdm-authority.png) 

4. Wenn Ihre MDM-Autorität nicht festgelegt ist, legen Sie Ihre MDM-Autorität unter **MDM-Autorität wählen** auf **Intune-MDM-Autorität** fest.

Informationen zum Festlegen der MDM-Autorität finden Sie unter [Festlegen der Autorität für die Verwaltung mobiler Geräte](mdm-authority-set.md).

## <a name="configure-your-custom-domain-name-optional"></a>Konfigurieren des Namens Ihrer benutzerdefinierten Domäne (optional)

Wie vorstehend erwähnt, können Sie eine benutzerdefinierte Domäne im Microsoft 365 Admin Center ändern, wenn Ihre Organisation über eine eigene benutzerdefinierte Domäne verfügt, die Sie ohne **.onmicrosoft.com** verwenden möchten. Sie können Ihren benutzerdefinierten Domänennamen mithilfe der folgenden Schritte hinzufügen, überprüfen und konfigurieren.  

> [!IMPORTANT]
> Sie können den *ursprünglichen* **onmicrosoft.com**-Teil des Domänennamens nicht umbenennen oder entfernen. Jedoch können Sie in Intune verwendete *benutzerdefinierte* Domänennamen hinzufügen, überprüfen oder entfernen, damit Ihre Geschäftsidentität eindeutig bleibt. Weitere Informationen finden Sie unter [Konfigurieren eines benutzerdefinierten Domänennamens](custom-domain-name-configure.md).

1. Wechseln Sie zum [Microsoft 365 Admin Center](https://admin.microsoft.com), und melden Sie sich über Ihr Administratorkonto an.

2. Wählen Sie im Navigationsbereich **Einrichtung** > **Domänen** > **Domäne hinzufügen** aus.

3. Geben Sie den Namen Ihrer benutzerdefinierten Domäne ein. Wählen Sie anschließend **Weiter** aus.

   ![Screenshot von Microsoft 365 Admin Center: Domäne hinzufügen](./media/free-trial-sign-up/domain-custom-add.png)

4. Überprüfen Sie, ob Sie Besitzer der im vorherigen Schritt eingegebenen Domäne sind. 
    
    Durch das Auswählen von **Send Code via Email** (Code per E-Mail senden) wird an den registrierten Kontakt Ihrer Domäne eine E-Mail gesendet. Kopieren Sie nach dem Empfang der E-Mail den Code, und geben Sie diesen in das Feld **Type your verification code here** (Geben Sie Ihren Prüfcode hier ein) ein. Stimmt der Prüfcode überein, wird die Domäne zu Ihrem Mandanten hinzugefügt. Die angezeigte E-Mail kommt Ihnen möglicherweise nicht bekannt vor. Einige Registrierungsstellen verbergen die reale E-Mail-Adresse. Ferner kann die E-Mail-Adresse von der abweichen, die bei der Registrierung der Domäne zur Verfügung gestellt wurde.

   ![Screenshot von Microsoft 365 Admin Center: Domäne überprüfen](./media/free-trial-sign-up/domain-custom-verify.png)

   > [!NOTE]
   > Einzelheiten zur Überprüfung von TXT-Datensätzen finden Sie unter [Erstellen von DNS-Datensätzen bei jedem DNS-Hostinganbieter für Office 365](https://support.office.com/article/Create-DNS-records-at-any-DNS-hosting-provider-for-Office-365-7B7B075D-79F9-4E37-8A9E-FB60C1D95166).

## <a name="admin-experiences"></a>Verwaltungsoberfläche

Es gibt zwei Portale, die Sie am meisten verwenden werden:
- Im Microsoft Endpoint Manager Admin Center ([https://devicemanagement.microsoft.com/](https://devicemanagement.microsoft.com/)) können Sie die [Funktionen von Intune](what-is-intune.md)untersuchen. An dieser Stelle arbeiten Administratoren in der Regel mit Intune.
- Das Microsoft 365 Admin Center ([https://admin.microsoft.com](https://admin.microsoft.com)) ist der Ort, an dem Sie Benutzer hinzufügen und verwalten können, wenn Sie dazu nicht Azure Active Directory verwenden. Sie können auch andere Aspekte Ihres Kontos verwalten, einschließlich Abrechnung und Support.

## <a name="next-steps"></a>Nächste Schritte

In diesem Schnellstart wurde erläutert, wie Sie ein kostenloses Abonnement abschließen, um Intune in einer Testumgebung zu testen. Weitere Informationen zum Einrichten von Intune finden Sie unter [Einrichten von Intune](setup-steps.md).

Weitere Informationen zu Intune erhalten Sie im nächsten Schnellstart.

> [!div class="nextstepaction"]
> [Schnellstart: Erstellen eines Benutzers und Zuweisen einer Lizenz zu diesem Benutzer](quickstart-create-user.md)
