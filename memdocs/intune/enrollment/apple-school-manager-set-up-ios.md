---
title: Apple School Manager-Programm zur Registrierung von iOS-/iPadOS-Geräten
titleSuffix: Microsoft Intune
description: Erfahren Sie, wie Sie das Apple School Manager-Programm für die Registrierung von unternehmenseigenen iOS-/iPadOS-Geräten bei Intune einrichten.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 4c35a23e-0c61-11e8-ba89-0ed5f89f718b
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: e919ac336532e8b641908b02c0e282ae9e1711e7
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093970"
---
# <a name="set-up-iosipados-device-enrollment-with-apple-school-manager"></a>Einrichten der iOS-/iPadOS-Geräteregistrierung mit Apple School Manager

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Sie können Intune für die Registrierung von iOS-/iPadOS-Geräten einrichten, die über das [Apple School Manager](https://school.apple.com/)-Programm erworben wurden. Wenn Sie Intune mit Apple School Manager verwenden, können Sie eine große Zahl von iOS-/iPadOS-Geräten registrieren, ohne sie in die Hand nehmen zu müssen. Wenn ein Schüler oder ein Lehrer das Gerät anschaltet, wird der Setup-Assistent mit vordefinierten Einstellungen ausgeführt, und das Gerät wird für die Verwaltung registriert.

Um die Registrierung mit Apple School Manager möglich zu machen, müssen Sie die Portale von Intune und Apple School Manager verwenden. Sie benötigen auch eine Liste von Seriennummern oder eine Bestellnummer, um Geräte in Intune zur Verwaltung zuweisen zu können. Sie erstellen ADE-Registrierungsprofile (automatische Geräteregistrierung), die Einstellungen enthalten, die für Geräte während der Registrierung gelten.

Die Registrierung von Apple School Manager kann nicht mit der [automatischen Geräteregistrierung von Apple](device-enrollment-program-enroll-ios.md) oder dem [Geräteregistrierungs-Manager](device-enrollment-manager-enroll.md) verwendet werden.

**Voraussetzungen**
- [Pushzertifikat für Apple-MDM (Mobile Device Management, Verwaltung mobiler Geräte)](apple-mdm-push-certificate-get.md)
- [MDM-Autorität](../fundamentals/mdm-authority-set.md)
- Bei ADFS ist für Benutzeraffinität [Endpunkt WS-Trust 1.3 Username/Mixed](https://technet.microsoft.com/library/adfs2-help-endpoints) erforderlich. [Weitere Informationen](https://technet.microsoft.com/itpro/powershell/windows/adfs/get-adfsendpoint)
- Geräte, die über das Programm [Apple School Management](http://school.apple.com) erworben wurden

## <a name="get-an-apple-token-and-assign-devices"></a>Abrufen eines Apple-Tokens und Zuweisen von Geräten

Damit Sie unternehmenseigene iOS-/iPadOS-Geräte mit dem Apple School Manager registrieren können, benötigen Sie eine Tokendatei (P7M) von Apple. Mit diesem Token kann Intune Informationen zu Geräten synchronisieren, die zum Apple School Manager-Programm gehören. Damit kann Intune außerdem Registrierungsprofile an Apple übermitteln und diesen Profilen Geräte zuweisen. Im Apple-Portal können Sie auch Geräteseriennummern für die Verwaltung zuweisen.

### <a name="step-1-download-the-intune-public-key-certificate-required-to-create-an-apple-token"></a>Schritt 1: Herunterladen des Intune-Zertifikats mit öffentlichem Schlüssel, das zum Erstellen eines Apple-Tokens erforderlich ist

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment Program Tokens** > **Add** (Geräte > iOS/iPadOS > iOS/iPadOS-Registrierung > Registrierungsprogrammtoken > Hinzufügen).

   ![Rufen Sie ein Registrierungsprogrammtoken ab.](./media/apple-school-manager-set-up-ios/image01.png)

2. Wählen Sie auf dem Blatt **Registrierungsprogrammtoken** die Option **Laden Sie Ihr Zertifikat mit öffentlichem Schlüssel herunter** aus, um die Verschlüsselungsschlüsseldatei (PEM) herunterzuladen und lokal zu speichern. Die PEM-Datei wird verwendet, um ein Vertrauensstellungszertifikat vom Apple School Manager-Portal anzufordern.
     ![Blatt „Registrierungsprogrammtoken“](./media/apple-school-manager-set-up-ios/image02.png)

### <a name="step-2-download-a-token-and-assign-devices"></a>Schritt 2: Herunterladen eines Tokens und Zuweisen von Geräten
1. Wählen Sie **Token über Apple School Manager erstellen** aus, und melden Sie sich mit Ihrer Apple-Unternehmens-ID bei Apple School an. Sie können diese Apple-ID auch zum Erneuern Ihres Apple School Manager-Tokens verwenden.
2. Wechseln Sie im [Apple School Manager-Portal](https://school.apple.com) zu **MDM-Server**, und klicken Sie auf **MDM-Server hinzufügen** (oben rechts).
3. Geben Sie den **MDM-Servernamen** ein. Der Servername dient als Referenz zum Identifizieren des MDM-Servers (mobile device management, Verwaltung mobiler Geräte). Es handelt sich nicht um den Namen oder die URL des Microsoft Intune-Servers.
   ![Screenshot des Apple School Manager-Portals mit der ausgewählter Option „Seriennummer“](./media/apple-school-manager-set-up-ios/asm-server-assignment.png)

4. Wählen Sie im Apple-Portal die Option **Datei hochladen...** , navigieren Sie zur PEM-Datei, und wählen Sie **MDM-Server speichern** (unten rechts).
5. Klicken Sie auf **Token abrufen**, und laden Sie die Servertokendatei (P7M) auf Ihren Computer herunter.
6. Wechseln Sie zu **Gerätezuweisungen**, und verwenden Sie die Option **Gerät auswählen**, indem Sie **Seriennummern** oder **Bestellnummer** manuell eingeben oder eine **CSV-Datei hochladen**.
     ![Screenshot des Apple School Manager-Portals mit der ausgewählter Option „Seriennummer“](./media/apple-school-manager-set-up-ios/asm-device-assignment.png)
7. Wählen Sie die Aktion **Zu Server zuweisen**, und wählen Sie den von Ihnen erstellten **MDM-Server** aus.
8. Geben Sie an Sie **Geräte ausgewählt werden**, und stellen Sie dann Geräteinformationen sowie Details bereit.
9. Wählen Sie **Zu Server zuweisen** aus. Wählen Sie den für Microsoft Intune angegebenen &lt;Servernamen&gt; und anschließend **OK** aus.

### <a name="step-3-save-the-apple-id-used-to-create-this-token"></a>Schritt 3: Speichern der zum Erstellen dieses Tokens verwendeten Apple-ID

Geben Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) die Apple-ID zur späteren Verwendung an.

![Screenshot der Angabe der Apple-ID zur Erstellung des Registrierungsprogrammtokens und Navigieren zu diesem Token](./media/apple-school-manager-set-up-ios/image03.png)

### <a name="step-4-upload-your-token"></a>Schritt 4: Hochladen des Tokens
Navigieren Sie im Feld **Apple-Token** zur Zertifikatsdatei (PEM), und wählen Sie **Öffnen** und dann **Erstellen** aus. Mit dem Pushzertifikat kann Intune iOS-/iPadOS-Geräte registrieren und verwalten, indem die Richtlinie auf registrierte mobile Geräte gepusht wird. Intune synchronisiert Ihre Apple School Manager-Geräte automatisch mit Apple.

## <a name="create-an-apple-enrollment-profile"></a>Erstellen eines Apple-Registrierungsprofils
Da Sie nun Ihr Token installiert haben, können Sie ein Registrierungsprofil für Apple School-Geräte erstellen. Ein Geräteregistrierungsprofil definiert die Einstellungen, die während der Registrierung auf eine Gruppe von Geräten angewendet werden.

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment program tokens** (Geräte > iOS/iPadOS > iOS/iPadOS-Registrierung > Registrierungsprogrammtoken).
2. Wählen Sie ein Token aus, und wählen Sie dann **Profile** und **Profil erstellen** aus.

3. Geben Sie zu administrativen Zwecken unter **Profil erstellen** einen **Namen** und eine **Beschreibung** für das Profil ein. Benutzer können diese Informationen nicht sehen. Sie können das Feld **Name** zum Erstellen einer dynamischen Gruppe in Azure Active Directory verwenden. Verwenden Sie den Profilnamen, um den Parameter „enrollmentProfileName“ zu definieren, um Geräte mit diesem Registrierungsprofil zuzuweisen. Erfahren Sie mehr über [dynamische Gruppen in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal#rules-for-devices).

    ![Profilname und Beschreibung](./media/apple-school-manager-set-up-ios/image05.png)

4. Wählen Sie unter **Benutzeraffinität** aus, ob sich Geräte mit diesem Profil mit oder ohne einen zugewiesenen Benutzer registrieren müssen.
    - **Mit Benutzeraffinität registrieren**: Wählen Sie diese Option für Geräte aus, die Benutzern gehören und das Unternehmensportal verwenden sollen, um Dienste wie z. B. die Installation von Apps nutzen zu können. Mit dieser Option können Benutzer ihre Geräte auch über das Unternehmensportal authentifizieren. Bei ADFS ist für Benutzeraffinität [Endpunkt WS-Trust 1.3 Username/Mixed](https://technet.microsoft.com/library/adfs2-help-endpoints) erforderlich. [Weitere Informationen](https://technet.microsoft.com/itpro/powershell/windows/adfs/get-adfsendpoint)   Der Apple School Manager-Modus „Gemeinsam genutztes iPad“ erfordert, dass Benutzer sich ohne Affinität zwischen Benutzer und Gerät registrieren.

    - **Ohne Benutzeraffinität registrieren**: Wählen Sie diese Option für Geräte aus, die keinem einzelnen Benutzer zugeordnet sind, z. B. ein gemeinsam genutztes Gerät. Verwenden Sie diese Option für Geräte, die Aufgaben ohne Zugriff auf lokale Benutzerdaten ausführen. Apps wie die Unternehmensportal-App funktionieren nicht.

5. Wenn Sie **Mit Benutzeraffinität registrieren** ausgewählt haben, können Sie es Benutzern ermöglichen, sich über das Unternehmensportal statt über den Apple-Setup-Assistenten zu authentifizieren.

    ![Authentifizieren über das Unternehmensportal](./media/apple-school-manager-set-up-ios/authenticatewithcompanyportal.png)

    > [!NOTE]
    > Wenn Sie einen der folgenden Schritte ausführen möchten, legen Sie **Über das Unternehmensportal statt über den Setup-Assistenten authentifizieren** auf **Ja** fest.
    >    - Sie möchten die mehrstufige Authentifizierung verwenden.
    >    - Sie möchten Benutzer zum Ändern ihres Kennworts auffordern, wenn sie sich zum ersten Mal anmelden.
    >    - Sie möchten Benutzer dazu auffordern, ihre abgelaufenen Kennwörter bei der Registrierung zurückzusetzen.
    >
    > Diese Optionen werden nicht unterstützt, wenn die Authentifizierung über den Setup-Assistenten von Apple erfolgt.

6. Klicken Sie auf **Geräteverwaltungseinstellungen**, und geben Sie an, ob Geräte mit diesem Profil überwacht werden sollen.
    Bei **überwachten** Geräten stehen mehr Verwaltungsfunktionen zur Verfügung, und die Aktivierungssperre ist standardmäßig deaktiviert. Microsoft empfiehlt, ADE als Mechanismus zur Aktivierung des überwachten Modus von Intune zu verwenden. Dies gilt insbesondere für Organisationen, die eine große Anzahl von iOS-/iPadOS-Geräten bereitstellen.

    Die Benutzer werden auf zweierlei Weise benachrichtigt, dass ihre Geräte überwacht werden:

   - Auf dem Sperrbildschirm wird Folgendes angezeigt: „This iPhone is managed by Contoso“ (Dieses iPhone wird von Contoso verwaltet).
   - Auf dem Bildschirm **Settings** > **General** > **About** (Einstellungen > Allgemein > Info) wird Folgendes angezeigt: „This iPhone is supervised. „This iPhone is supervised. Contoso can monitor your Internet traffic and locate this device“ (Dieses iPhone wird überwacht. Contoso kann Ihren Internetdatenverkehr überwachen und dieses Gerät suchen.)

     > [!NOTE]
     > Ein Gerät, das ohne Überwachung registriert wurde, kann nur mithilfe von Apple Configurator auf den Status „Überwacht“ zurückgesetzt werden. Wenn Sie das Gerät auf diese Weise zurücksetzen möchten, müssen Sie ein iOS-/iPadOS-Gerät über ein USB-Kabel mit einem Mac verbinden. Erfahren Sie mehr über dieses Thema in der [Dokumentation zu Apple Configurator](http://help.apple.com/configurator/mac/2.3).

7. Wählen Sie aus, ob für Geräte mit diesem Profil die gesperrte Registrierung verwendet werden soll. Wenn **Gesperrte Registrierung** aktiviert ist, sind die iOS-/iPadOS-Einstellungen deaktiviert, mit denen das Verwaltungsprofil aus dem Menü **Einstellungen** entfernt werden kann. Nach der Geräteregistrierung können Sie diese Einstellung nicht ändern, ohne das Gerät zurückzusetzen. Bei solchen Geräten muss der Verwaltungsmodus **Überwacht** auf *Ja* eingestellt sein. 

8. Mithilfe einer verwalteten Apple-ID können Sie mehreren Benutzern ermöglichen, sich bei registrierten iPads anzumelden. Wählen Sie dazu **Ja** unter **Gemeinsam genutztes iPad**. (Diese Option erfordert den Modus **Ohne Benutzeraffinität registrieren** und **Überwacht**, der auf **Ja** eingestellt ist.) Verwaltete Apple-IDs werden im Apple School Manager-Portal erstellt. Weitere Informationen zu [gemeinsam genutzten iPads](../fundamentals/education-settings-configure-ios-shared.md) finden Sie in den [entsprechenden Apple-Anforderungen](https://help.apple.com/classroom/ipad/2.0/#/cad7e2e0cf56).

9. Wählen Sie aus, ob für Geräte, für die dieses Profil verwendet wird, die Option **Mit Computern synchronisieren** verfügbar sein soll. **Alle verweigern** bedeutet, dass alle Geräte, die dieses Profil verwenden, keine Daten mit Daten auf einem beliebigen Computer synchronisieren können. Wenn Sie **Apple Configurator nach Zertifikat zulassen** auswählen, müssen Sie unter **Apple Configurator-Zertifikate** ein Zertifikat auswählen.

10. Wenn Sie im vorherigen Schritt **Apple Configurator nach Zertifikat zulassen** ausgewählt haben, müssen Sie ein Apple Configurator-Zertifikat zum Importieren auswählen.

11. Sie können ein Benennungsformat für Geräte angeben, das bei deren Registrierung automatisch angewendet wird. Wählen Sie hierzu unter **Vorlage für Gerätenamen anwenden** die Option **Ja** aus. Geben Sie dann in das Feld **Vorlage für Gerätenamen** den Namen der Vorlage ein, die für die Geräte verwendet werden soll, für die dieses Profil verwendet wird. Sie können ein Vorlagenformat angeben, das den Gerätetyp und die Seriennummer enthält.

12. Wählen Sie **OK** aus.

13. Wählen Sie **Einstellungen des Einrichtungs-Assistenten** aus, um die folgenden Profileinstellungen zu konfigurieren: ![Anpassung des Setup-Assistenten](./media/apple-school-manager-set-up-ios/setupassistantcustom.png)


    |                 Einstellung                  |                                                                                               Beschreibung                                                                                               |
    |------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    |     <strong>Abteilungsname</strong>     |                                                             Wird angezeigt, wenn der Benutzer während der Aktivierung auf <strong>Info zur Konfiguration</strong> tippt.                                                              |
    |    <strong>Abteilungstelefonnummer</strong>     |                                                          Wird angezeigt, wenn der Benutzer während der Aktivierung auf die Schaltfläche <strong>Benötigen Sie Hilfe?</strong> klickt.                                                          |
    | <strong>Setup-Assistent-Optionen</strong> |                                                     Die folgenden optionalen Einstellungen können später im iOS-/iPadOS-Menü <strong>Einstellungen</strong> eingerichtet werden.                                                      |
    |        <strong>Kennung</strong>         | Fordert während der Aktivierung zur Eingabe der Kennung auf. Verlangen Sie immer eine Kennung (Passcode) für ungeschützte Geräte, es sei denn, der Zugriff ist auf andere Weise geschützt (etwa im Kioskmodus, in dem das Gerät auf eine App beschränkt wird). |
    |    <strong>Standortdienste</strong>    |                                                                 Falls aktiviert, fordert der Setup-Assistent während der Aktivierung zur Ausführung dieses Dienstes auf.                                                                  |
    |         <strong>Wiederherstellen</strong>         |                                                                Falls aktiviert, fordert der Setup-Assistent während der Aktivierung die iCloud-Sicherung an.                                                                 |
    |   <strong>iCloud und Apple-ID</strong>   |                         Falls aktiviert, fordert der Setup-Assistent den Benutzer auf, sich mit einer Apple-ID anzumelden, und im Bildschirm „Apps und Daten“ kann das Gerät von einer iCloud-Sicherung wiederhergestellt werden.                         |
    |  <strong>Geschäftsbedingungen</strong>   |                                                   Falls aktiviert, fordert der Setup-Assistenten während der Aktivierung den Benutzer auf, die Apple-Geschäftsbedingungen zu akzeptieren.                                                   |
    |        <strong>Touch ID</strong>         |                                                                 Falls aktiviert, fordert der Setup-Assistent während der Aktivierung zur Ausführung dieses Dienstes auf.                                                                 |
    |        <strong>Apple Pay</strong>        |                                                                 Falls aktiviert, fordert der Setup-Assistent während der Aktivierung zur Ausführung dieses Dienstes auf.                                                                 |
    |          <strong>Zoom</strong>           |                                                                 Falls aktiviert, fordert der Setup-Assistent während der Aktivierung zur Ausführung dieses Dienstes auf.                                                                 |
    |          <strong>Siri</strong>           |                                                                 Falls aktiviert, fordert der Setup-Assistent während der Aktivierung zur Ausführung dieses Dienstes auf.                                                                 |
    |     <strong>Diagnosedaten</strong>     |                                                                 Falls aktiviert, fordert der Setup-Assistent während der Aktivierung zur Ausführung dieses Dienstes auf.                                                                 |


14. Wählen Sie **OK** aus.

15. Wählen Sie **Erstellen** aus, um das Profil zu speichern.

## <a name="connect-school-data-sync"></a>Verbinden mit School Data Sync
(Optional) Apple School Manager unterstützt die Synchronisierung von Kursplandaten mit Azure Active Directory (AD) über Microsoft School Data Sync (SDS). Sie können nur ein Token mit SDS synchronisieren. Wenn Sie ein anderes Token mit School Data Sync einrichten, wird SDS aus dem bisherigen Token entfernt. Das aktuelle Token wird durch eine neue Verbindung ersetzt. Führen Sie die folgenden Schritte aus, um SDS zum Synchronisieren von Schul- bzw. Unidaten zu verwenden.

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment program tokens** (Geräte > iOS/iPadOS > iOS/iPadOS-Registrierung > Registrierungsprogrammtoken).
2. Wählen Sie ein Apple School Manager-Token und dann **School Data Sync** aus.
3. Wählen Sie unter **School Data Sync** die Option **Zulassen** aus. Mit dieser Einstellung kann Intune in Office 365 eine Verbindung mit SDS herstellen.
4. Um eine Verbindung zwischen Apple School Manager und Azure AD zu ermöglichen, klicken Sie auf **Microsoft-Synchronisierung von Schul-/Unidaten einrichten**. Erfahren Sie mehr über [das Einrichten von School Data Sync](https://support.office.com/article/Install-the-School-Data-Sync-Toolkit-8e27426c-8c46-416e-b0df-c29b5f3f62e1).
5. Klicken Sie auf **Speichern** > **OK**.

## <a name="sync-managed-devices"></a>Synchronisieren verwalteter Geräte

Nachdem Intune die Berechtigung zum Verwalten Ihrer Apple School Manager-Geräte zugewiesen wurde, synchronisieren Sie Intune mit dem Apple-Dienst, um Ihre verwalteten Geräte in Intune anzuzeigen.

Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment Program Tokens** (Geräte > iOS/iPadOS > iOS/iPadOS-Registrierung > Registrierungsprogrammtoken), wählen Sie in der Liste ein Token aus, und klicken Sie auf **Geräte** > **Synchronisieren**. ![Screenshot des Knotens „Geräte des Registrierungprogramms“ und des Links „Synchronisierung“](./media/device-enrollment-program-enroll-ios/image06.png)

Zur Befolgung der Apple-Bedingungen für zulässigen Datenverkehr des Registrierungsprogramms erzwingt Intune die folgenden Einschränkungen:
- Eine vollständige Synchronisation kann nicht öfter als einmal alle sieben Tage erfolgen. Während einer vollständigen Synchronisierung aktualisiert Intune jede Seriennummer von Apple, die Intune zugewiesen ist. Wenn eine vollständige Synchronisierung innerhalb von sieben Tagen nach der vorherigen vollständigen Synchronisierung versucht wird, aktualisiert Intune nur Seriennummern, die nicht bereits in Intune aufgeführt werden.
- Synchronisierungsanforderungen müssen innerhalb von 15 Minuten abgeschlossen sein. Während dieser Zeit oder bis zum erfolgreichen Erfüllen der Anforderung wird die Schaltfläche **Synchronisieren** deaktiviert.
- Intune synchronisiert alle 24 Stunden neue und entfernte Geräte für Apple.

>[!NOTE]
>Sie können auch über das Blatt **Geräte des Registrierungsprogramms** Apple School Manager-Seriennummern zu Geräten zuweisen.

## <a name="assign-a-profile-to-devices"></a>Zuweisen eines Profils zu Geräten
Apple School Manager-Geräten, die von Intune verwaltet werden, muss vor der Registrierung ein Registrierungsprofil zugewiesen werden.

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment Program Tokens** (Geräte > iOS/iPadOS > iOS/iPadOS-Registrierung > Registrierungsprogrammtoken), und wählen Sie in der Liste ein Token aus.
2. Wählen Sie **Geräte** aus, wählen Sie in der Liste die Geräte aus, und wählen Sie dann **Profil zuweisen** aus.
3. Wählen Sie unter **Profil zuweisen** ein Profil für die Geräte aus, und wählen Sie dann **Zuweisen** aus.

## <a name="distribute-devices-to-users"></a>Verteilen von Geräten an Benutzer

Sie haben die Verwaltung und Synchronisierung zwischen Apple und Intune aktiviert und ein Profil zugewiesen, damit Ihre Apple School-Geräte registriert werden können. Sie können jetzt Geräte an Benutzer verteilen. Wenn ein iOS-/iPadOS-Apple School Manager-Gerät eingeschaltet wird, wird es für die Verwaltung durch Intune registriert. Profile können nicht auf aktivierten Geräten angewendet werden, die derzeit verwendet werden, bis das Gerät gelöscht wird.
