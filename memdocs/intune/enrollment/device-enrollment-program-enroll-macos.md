---
title: 'Registrieren von macOS-Geräten: Apple Business Manager oder Apple School Manager'
titleSuffix: ''
description: Informieren Sie sich, wie Sie unternehmenseigene macOS-Geräte registrieren.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 12/06/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1070c7b396ac3c19c340a69b6e2eb8db9d6707b6
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80327196"
---
# <a name="automatically-enroll-macos-devices-with-the-apple-business-manager-or-apple-school-manager"></a>Automatisches Registrieren von macOS-Geräten mit Apple Business Manager oder Apple School Manager

> [!IMPORTANT]
> Apple hat vor Kurzem vom Programm zur Geräteregistrierung (DEP, Device Enrollment Program) auf die automatische Geräteregistrierung (ADE, Automated Device Enrollment) umgestellt. Die Benutzeroberfläche von Intune wird derzeit entsprechend aktualisiert. Bis diese Änderungen abgeschlossen sind, wird im Intune-Portal weiterhin der Begriff *Programm zur Geräteregistrierung* verwendet. Überall, wo dieser steht, wird nun die automatische Geräteregistrierung verwendet.

Sie können die Intune-Registrierung für macOS-Geräte einrichten, die über [Apple Business Manager](https://business.apple.com/) oder [Apple School Manager](https://school.apple.com/) von Apple erworben wurden. Sie können jedes dieser Programme zur Geräteregistrierung für eine große Anzahl von Geräten verwenden, ohne diese physisch berühren zu müssen. Sie können macOS-Geräte direkt an Benutzer senden. Wenn ein Benutzer das Gerät einschaltet, wird der Setup-Assistent mit vordefinierten Einstellungen ausgeführt, und das Gerät wird bei der Intune-Verwaltung registriert.

Zum Einrichten der Registrierung können Sie sowohl das Intune-Portal als auch das Apple-Portal verwenden. Sie erstellen Registrierungsprofile, die Einstellungen enthalten, die für Geräte während der Registrierung gelten.

Weder die Registrierung mit Apple Business Manager noch mit Apple School Manager funktioniert mit dem [Geräteregistrierungs-Manager](device-enrollment-manager-enroll.md).

<!--
**Steps to enable enrollment programs from Apple**
1. [Get an Apple DEP token and assign devices](#get-the-apple-dep-token)
2. [Create an enrollment profile](#create-an-apple-enrollment-profile)
3. [Synchronize DEP-managed devices](#sync-managed-device)
4. [Assign DEP profile to devices](#assign-an-enrollment-profile-to-devices)
5. [Distribute devices to users](#end-user-experience-with-managed-devices)
-->
## <a name="prerequisites"></a>Voraussetzungen

- Geräte, die unter [Apple School Manager](https://school.apple.com/) oder dem [Programm zur Geräteregistrierung von Apple](http://deploy.apple.com) erworben werden.
- Eine Liste mit Seriennummern oder eine Auftragsnummer.
- [MDM-Autorität](../fundamentals/mdm-authority-set.md)
- [Apple-MDM-Push-Zertifikat](../enrollment/apple-mdm-push-certificate-get.md)

## <a name="get-an-apple-ade-token"></a>Abrufen eines Apple-ADE-Tokens

Bevor Sie macOS-Geräte mit ADE oder Apple School Manager registrieren können, benötigen Sie eine Tokendatei (P7M-Datei) von Apple. Mit diesem Token kann Intune Informationen zu den Geräten synchronisieren, die Ihrem Unternehmen gehören. Zudem ermöglicht es Intune das Hochladen von Registrierungsprofilen bei Apple und das Zuweisen dieser Profile zu Geräten.

Verwenden Sie das Apple-Portal, um ein Token zu erstellen. Sie verwenden das Apple-Portal auch, um in Intune Geräte für die Verwaltung zuzuweisen.

> [!NOTE]
> Wenn Sie das Token vor der Migration zu Azure aus dem klassischen Intune-Portal löschen, stellt Intune womöglich ein gelöschtes Apple-Token wieder her. Sie können das Token erneut aus dem Azure-Portal löschen.

### <a name="step-1-download-the-intune-public-key-certificate-required-to-create-the-token"></a>Schritt 1: Laden Sie das Intune-Zertifikat mit öffentlichem Schlüssel herunter, das zum Erstellen des Tokens erforderlich ist.

1. Navigieren Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) zu **Geräte** > **macOS** > **macOS-Registrierung** > **Registrierungsprogrammtoken** > **Hinzufügen**.

    ![Rufen Sie ein Registrierungsprogrammtoken ab.](./media/device-enrollment-program-enroll-macos/image01.png)

2. Erteilen Sie Microsoft die Berechtigung, Benutzer- und Geräteinformationen an Apple zu senden, indem Sie auf **Ich stimme zu** klicken.

   ![Screenshot des Bereichs „Registrierungsprogrammtoken“ im Arbeitsbereich „Apple-Zertifikate“ zum Herunterladen des öffentlichen Schlüssels](./media/device-enrollment-program-enroll-macos/add-enrollment-program-token-pane.png)

3. Wählen Sie **Laden Sie Ihr Zertifikat mit öffentlichem Schlüssel herunter** aus, um die Verschlüsselungsschlüsseldatei (PEM) herunterzuladen und lokal zu speichern. Die PEM-Datei wird verwendet, um ein Vertrauensstellungszertifikat vom Apple-Portal anzufordern.

### <a name="step-2-use-your-key-to-download-a-token-from-apple"></a>Schritt 2: Verwenden Sie Ihren Schlüssel, um ein Token von Apple herunterzuladen.

1. Wählen Sie **Token für das Programm zur Geräteregistrierung von Apple erstellen** oder **Token über Apple School Manager erstellen** aus, um das Portal des Bereitstellungsprogramms von Apple zu öffnen. Melden Sie sich mit der Apple-ID Ihres Unternehmens an. Diese Apple-ID kann später zum Erneuern Ihres Tokens verwendet werden.
2. Wählen Sie im Apple-Portal für DEP **Get Started (Einstieg)** für **Device Enrollment Program (Programm zur Geräteregistrierung)**  > **Manage Servers (Server verwalten)**  > **Add MDM Server (MDM-Server hinzufügen)** aus.
3. Wählen Sie im Apple-Portal für Apple School Manager **MDM Servers (MDM-Server)**  > **Add MDM Server (MDM-Server hinzufügen)** aus.
4. Geben Sie den **MDM-Servernamen** ein, und wählen Sie anschließend **Weiter** aus. Der Servername dient als Referenz zum Identifizieren des MDM-Servers (mobile device management, Verwaltung mobiler Geräte). Es handelt sich nicht um den Namen oder die URL des Microsoft Intune-Servers.

5. Das Dialogfeld **&lt;Servername&gt; hinzufügen** wird geöffnet, und die Meldung **Laden Sie Ihren öffentlichen Schlüssel hoch** wird angezeigt. Wählen Sie **Datei auswählen** aus, um die PEM-Datei hochzuladen, und wählen Sie anschließend **Weiter** aus.

6. Wechseln Sie zu **Bereitstellungsprogramm** &gt; **Programm zur Geräteregistrierung** &gt; **Geräte verwalten**.
7. Geben Sie unter **Geräte auswählen nach** an, wie die Geräte identifiziert werden sollen:
    - **Seriennummer**
    - **Reihenfolge**
    - **Upload der CSV-Datei**

   ![Screenshot bei Festlegen von „Geräte auswählen nach“ auf „Seriennummer“, der Einstellung „Aktion auswählen“ auf „Zu Server zuweisen“ und der Auswahl des Servernamens.](./media/device-enrollment-program-enroll-macos/enrollment-program-token-specify-serial.png)

8. Wählen Sie als Nächstes für **Aktion auswählen** die Option **Zu Server zuweisen** aus. Wählen Sie den für Microsoft Intune angegebenen &lt;Servernamen&gt; und anschließend **OK** aus. Das Apple-Portal weist die angegebenen Geräte dem Intune-Server für die Verwaltung zu und zeigt dann **Zuweisung abgeschlossen** an.

### <a name="step-3-save-the-apple-id-used-to-create-this-token"></a>Schritt 3: Speichern der zum Erstellen dieses Tokens verwendeten Apple-ID

Geben Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) die Apple-ID zur späteren Verwendung an.

![Screenshot der Angabe der Apple-ID zur Erstellung des Registrierungsprogrammtokens und Navigieren zu diesem Token](./media/device-enrollment-program-enroll-macos/image03.png)

### <a name="step-4-upload-your-token"></a>Schritt 4: Hochladen des Tokens
Navigieren Sie im Feld **Apple-Token** zur Zertifikatsdatei (PEM), und wählen Sie **Öffnen** und dann **Erstellen** aus. Mit dem Pushzertifikat kann Intune macOS-Geräte registrieren und verwalten, indem die Richtlinie per Push auf registrierte Geräte übertragen wird. Intune führt eine automatische Synchronisierung mit Apple durch, um Ihr Registrierungsprogrammkonto anzuzeigen.

## <a name="create-an-apple-enrollment-profile"></a>Erstellen eines Apple-Registrierungsprofils

Da Sie nun Ihr Token installiert haben, können Sie ein Registrierungsprofil für Geräte erstellen. Ein Geräteregistrierungsprofil definiert die Einstellungen, die während der Registrierung auf eine Gruppe von Geräten angewendet werden.

1. Navigieren Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) zu **Geräte** > **macOS** > **macOS-Registrierung** > **Registrierungsprogrammtoken**.
2. Wählen Sie ein Token aus, und wählen Sie dann **Profile** und **Profil erstellen** aus.

    ![Screenshot „Profil erstellen“](./media/device-enrollment-program-enroll-macos/image04.png)

3. Geben Sie zu administrativen Zwecken unter **Profil erstellen** einen **Namen** und eine **Beschreibung** für das Profil ein. Benutzer können diese Informationen nicht sehen. Sie können das Feld **Name** zum Erstellen einer dynamischen Gruppe in Azure Active Directory verwenden. Verwenden Sie den Profilnamen, um den Parameter „enrollmentProfileName“ zu definieren, um Geräte mit diesem Registrierungsprofil zuzuweisen. Erfahren Sie mehr über [dynamische Gruppen in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices).

    ![Profilname und Beschreibung](./media/device-enrollment-program-enroll-macos/createprofile.png)

4. Wählen Sie als **Plattform** die Option **macOS** aus.

5. Wählen Sie unter **Benutzeraffinität** aus, ob sich Geräte mit diesem Profil mit oder ohne einen zugewiesenen Benutzer registrieren müssen.
    - **Mit Benutzeraffinität registrieren**: Wählen Sie diese Option für Geräte aus, die Benutzern gehören und das Unternehmensportal verwenden sollen, um Dienste wie z.B. die Installation von Apps nutzen zu können. Bei ADFS ist für Benutzeraffinität [Endpunkt WS-Trust 1.3 Username/Mixed](https://technet.microsoft.com/library/adfs2-help-endpoints) erforderlich. [Hier erhalten Sie weitere Informationen](https://technet.microsoft.com/itpro/powershell/windows/adfs/get-adfsendpoint). Auf macOS-Geräten mit Benutzeraffinität, die über ADE registriert wurden, wird die mehrstufige Authentifizierung nicht unterstützt.

    - **Ohne Benutzeraffinität registrieren**: Wählen Sie diese Option für Geräte aus, die keinem einzelnen Benutzer zugeordnet sind. Verwenden Sie diese Option für Geräte, die Aufgaben ohne den Zugriff auf lokale Benutzerdaten ausführen. Apps wie die Unternehmensportal-App funktionieren nicht.

6. Wählen Sie **Geräteverwaltungseinstellungen** aus, und geben Sie an, ob für Geräte mit diesem Profil die gesperrte Registrierung verwendet werden soll. Die **gesperrte Registrierung** deaktiviert die macOS-Einstellungen, mit denen das Verwaltungsprofil aus dem Menü **Einstellungen** oder über das **Terminal** entfernt werden kann. Nach der Geräteregistrierung können Sie diese Einstellung ändern, ohne das Gerät zurückzusetzen.

    ![Screenshot der Geräteverwaltungseinstellungen](./media/device-enrollment-program-enroll-macos/devicemanagementsettingsblade-macos.png)

7. Wählen Sie **OK** aus.

8. Wählen Sie **Einstellungen des Einrichtungs-Assistenten** aus, um die folgenden Profileinstellungen zu konfigurieren:  ![Anpassung des Setup-Assistenten](./media/device-enrollment-program-enroll-macos/setupassistantcustom-macos.png)

    | Abteilungseinstellungen | Beschreibung |
    |---|---|
    | <strong>Abteilungsname</strong> | Wird angezeigt, wenn der Benutzer während der Aktivierung auf <strong>Info zur Konfiguration</strong> tippt. |
    | <strong>Abteilungstelefonnummer</strong> | Wird angezeigt, wenn der Benutzer während der Aktivierung auf die Schaltfläche <strong>Benötigen Sie Hilfe?</strong> klickt. |

    Sie können entscheiden, ob ein Bildschirm des Setup-Assistenten auf dem Gerät angezeigt oder ausgeblendet wird, während der Benutzer es einrichtet.
    - Wenn Sie auf **Ausblenden** klicken, wird der Bildschirm nicht während des Setups angezeigt. Nach dem Setup des Geräts kann der Benutzer weiterhin zum Menü **Einstellungen** navigieren, um das Feature einzurichten.
    - Wenn Sie auf **Anzeigen** klicken, wird der Bildschirm während des Setups angezeigt. Gelegentlich kann der Benutzer den Bildschirm überspringen, ohne weitere Maßnahmen ergreifen zu müssen. Er kann aber später zum Gerätemenü **Einstellungen** navigieren, um das Feature einzurichten. 

    | Bildschirmeinstellungen des Setup-Assistenten | Wenn Sie während des Setups des Geräts auf **Anzeigen** klicken, führt das Gerät die folgenden Aktionen durch: |
    |------------------------------------------|------------------------------------------|
    | <strong>Kennung</strong> | Es fordert den Benutzer auf, eine Kennung einzugeben. Fordern Sie immer eine Kennung an, es sei denn, das Gerät und der Zugriff darauf werden auf andere Weise geschützt (d.h. im Kioskmodus zum Einschränken des Geräts auf eine App). |
    | <strong>Standortdienste</strong> | Es fordert den Benutzer auf, seinen Standort anzugeben. |
    | <strong>Wiederherstellen</strong> | Es zeigt den Bildschirm „Apps & Daten“ an. Über diesen Bildschirm hat der Benutzer die Möglichkeit, Daten aus der iCloud-Sicherung wiederherzustellen oder aus dieser zu übertragen, wenn er das Gerät einrichtet. |
    | <strong>iCloud und Apple-ID</strong> | Es lässt zu, dass der Benutzer sich mit seiner **Apple-ID** anmelden und **iCloud** verwenden kann.                         |
    | <strong>Geschäftsbedingungen</strong> | Es verlangt, dass der Benutzer die Nutzungsbedingungen von Apple akzeptiert. |
    | <strong>Touch ID</strong> | Es lässt zu, dass der Benutzer die Identifikation per Fingerabdruck für das Gerät einrichtet. |
    | <strong>Apple Pay</strong> | Es lässt zu, dass der Benutzer Apple Pay auf dem Gerät einrichtet. |
    | <strong>Zoom</strong> | Es lässt zu, dass der Benutzer die Anzeige vergrößern bzw. verkleinern kann, während er das Gerät einrichtet. |
    | <strong>Siri</strong> | Es lässt zu, dass der Benutzer Siri einrichtet. |
    | <strong>Diagnosedaten</strong> | Zeigt dem Benutzer den Bildschirm „Diagnose“ an. Über diesen Bildschirm kann der Benutzer Diagnosedaten an Apple senden. |
    | <strong>FileVault</strong> | Es lässt zu, dass der Benutzer FileVault-Verschlüsselung einrichtet. |
    | <strong>iCloud Diagnostics</strong> | Es lässt zu, dass der Benutzer iCloud-Diagnosedaten an Apple sendet. |
    | <strong>iCloud-Speicher</strong> | Ermöglicht dem Benutzer, iCloud-Speicher zu verwenden. |    
    | <strong>Displayfarbton</strong> | Geben Sie dem Benutzer die Möglichkeit, den Anzeigefarbton zu aktivieren. |
    | <strong>Darstellung</strong> | Zeigen Sie den Bildschirm „Darstellung“ für den Benutzer an. |
    | <strong>Registrierung</strong>| Es verlangt, dass der Benutzer das Gerät registriert. |
    | <strong>Datenschutz</strong>| Lassen Sie den Benutzer auf den Bildschirm Privatsphäre zugreifen. |
    | <strong>Bildschirmzeit</strong>| Aktivieren Sie den Bildschirm „Bildschirmzeit“ für den Benutzer. |

9. Wählen Sie **OK** aus.

10. Wählen Sie **Erstellen** aus, um das Profil zu speichern.

## <a name="sync-managed-devices"></a>Synchronisieren verwalteter Geräte

Nachdem Intune nun die Berechtigung zum Verwalten Ihrer Geräte besitzt, können Sie Intune mit Apple synchronisieren, um Ihre verwalteten Geräte in Intune im Azure-Portal anzuzeigen.

1. Navigieren Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) zu **Geräte** > **macOS** > **macOS-Registrierung** > **Registrierungsprogrammtoken**, wählen Sie ein Token aus der Liste aus, und klicken Sie auf **Geräte** > **Synchronisieren**. ![Screenshot des ausgewählten Knotens „Geräte des Registrierungprogramms“ und des ausgewählten Links „Synchronisierung“](./media/device-enrollment-program-enroll-macos/image06.png)

   Zur Einhaltung der Apple-Bedingungen für zulässigen Datenverkehr des Registrierungsprogramms erzwingt Intune die folgenden Einschränkungen:
   - Eine vollständige Synchronisation kann nicht öfter als einmal alle sieben Tage erfolgen. Während einer vollständigen Synchronisierung ruft Intune die vollständig aktualisierte Liste der Seriennummern auf, die dem mit Intune verbundenen Apple MDM-Server zugewiesen sind. Nachdem ein Registrierungsprogrammgerät aus dem Intune-Portal gelöscht wurde, ohne dass es vom Apple MDM-Server im Apple-Portal entfernt wurde, wird es erst wieder in Intune importiert, wenn die vollständige Synchronisierung ausgeführt wurde.   
   - Die Synchronisierung wird automatisch alle 24 Stunden ausgeführt. Sie können eine Synchronisierung ebenfalls durchführen, indem Sie auf die Schaltfläche **Synchronisierung** klicken (nicht öfter als einmal alle 15 Minuten). Alle Synchronisierungsanforderungen müssen innerhalb von 15 Minuten abgeschlossen werden. Die Schaltfläche **Synchronisierung** bleibt bis zum Abschluss der Synchronisierung deaktiviert. Durch diese Synchronisierung werden vorhandene Gerätestatus aktualisiert und neue Geräte importiert, die dem Apple MDM-Server zugewiesen sind.

## <a name="assign-an-enrollment-profile-to-devices"></a>Zuweisen eines Registrierungsprofils an Geräte

Sie müssen Geräten ein Profil des Registrierungsprogramms zuweisen, bevor Sie mit der Registrierung beginnen können.

1. Navigieren Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) zu **Geräte** > **macOS** > **macOS-Registrierung** > **Registrierungsprogrammtoken**, und wählen Sie ein Token aus der Liste aus.
2. Wählen Sie **Geräte** aus, wählen Sie in der Liste die Geräte aus, und wählen Sie dann **Profil zuweisen** aus.
3. Wählen Sie unter **Profil zuweisen** ein Profil für die Geräte aus, und klicken Sie dann auf **Zuweisen**.

### <a name="assign-a-default-profile"></a>Zuweisen eines Standardprofils

Sie können ein macOS- und iOS-/iPadOS-Standardprofil auswählen, das auf alle Geräte angewendet wird, die sich mit einem bestimmten Token registrieren. 

1. Navigieren Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) zu **Geräte** > **macOS** > **macOS-Registrierung** > **Registrierungsprogrammtoken**, und wählen Sie ein Token aus der Liste aus.
2. Wählen Sie **Standardprofil festlegen** aus, wählen Sie ein Profil in der Dropdownliste aus, und wählen Sie dann **Speichern** aus. Dieses Profil wird auf alle Geräte angewendet, die sich mit dem Token registrieren.

## <a name="distribute-devices"></a>Verteilen von Geräten

Sie haben die Verwaltung und Synchronisierung zwischen Apple und Intune aktiviert und haben ein Profil zugewiesen, damit Ihre Geräte registriert werden können. Sie können jetzt Geräte an Benutzer verteilen. Für Geräte mit Benutzeraffinität muss jedem Benutzer eine Intune-Lizenz zugewiesen werden. Geräte ohne Benutzeraffinität benötigen eine Gerätelizenz. Ein aktiviertes Gerät kann kein Registrierungsprofil anwenden, bis das Gerät zurückgesetzt wurde.

## <a name="renew-an-ade-token"></a>Erneuern eines ADE-Tokens

1. Wechseln Sie zu deploy.apple.com.  
2. Wählen Sie unter **Server verwalten** Ihren MDM-Server aus, der der Tokendatei zugeordnet ist, die Sie erneuern möchten.
3. Klicken Sie auf **Neues Token generieren**.

    ![Screenshot von „Neues Token generieren“](./media/device-enrollment-program-enroll-macos/generatenewtoken.png)

4. Klicken Sie auf **Ihr Servertoken**.  
5. Navigieren Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) zu **Geräteregistrierung** > **Apple-Registrierung** > **Registrierungsprogrammtoken**, und wählen Sie das Token aus.
    ![Screenshot der Registrierungsprogrammtoken.](./media/device-enrollment-program-enroll-macos/enrollmentprogramtokens.png)

6. Wählen Sie **Token erneuern** aus, und geben Sie die Apple-ID ein, die zum Erstellen des ursprünglichen Tokens verwendet wurde.  
    ![Screenshot von „Token erneuern“](./media/device-enrollment-program-enroll-macos/renewtoken.png)

7. Laden Sie das neu heruntergeladene Token hoch.  
8. Klicken Sie auf **Token erneuern**. Es wird eine Bestätigung angezeigt, dass das Token erneuert wurde.
    ![Screenshot der Bestätigung](./media/device-enrollment-program-enroll-macos/confirmation.png)

## <a name="next-steps"></a>Nächste Schritte

Sie können macOS-Geräte [verwalten](../remote-actions/device-management.md), nachdem Sie sie registriert haben.
