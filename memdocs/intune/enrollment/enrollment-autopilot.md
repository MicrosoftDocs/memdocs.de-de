---
title: Registrieren von Geräten mithilfe von Autopilot
titleSuffix: Microsoft Intune
description: Erfahren Sie, wie Sie Windows 10-Geräte mithilfe des Windows Autopilot registrieren.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/15/2020
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a2dc5594-a373-48dc-ba3d-27aff0c3f944
ms.reviewer: spshumwa
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: e87b9aaffc9a6252f8d14645fb477588479a684e
ms.sourcegitcommit: 01c1ca337e82c5e8e92153079ed89f79e20bde9e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/09/2020
ms.locfileid: "86157891"
---
# <a name="enroll-windows-devices-in-intune-by-using-the-windows-autopilot"></a>Registrieren von Windows-Geräten in Intune mithilfe von Windows Autopilot  
Windows Autopilot vereinfacht das Registrieren von Geräten in Intune. Das Erstellen und Warten von benutzerdefinierten Images des Betriebssystems ist ein langwieriger Prozess. Es kann ebenfalls Zeit in Anspruch nehmen, diese benutzerdefinierten Images von Betriebssystemen auf neue Geräte anzuwenden, um diese für die Verwendung vorzubereiten, bevor Sie sie Ihren Benutzern zur Verfügung stellen. Mit Microsoft Intune und Autopilot können Sie Ihren Benutzern neue Geräte geben, ohne die benutzerdefinierten Images des Betriebssystems auf den Geräten erstellen, verwalten und auf diese anwenden zu müssen. Wenn Sie Intune zum Verwalten von Autopilot-Geräten verwenden, können Sie Richtlinien, Profile und Apps usw. verwalten, nachdem diese registriert sind. Eine Übersicht über die Vorteile, Szenarios und Voraussetzungen finden Sie unter [Übersicht über Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot).

Es gibt vier Arten der Autopilot-Bereitstellung:

- [Self-Deployment-Modus](https://docs.microsoft.com/windows/deployment/windows-autopilot/self-deploying) für Kiosks, digitale Signaturen oder ein freigegebenes Gerät
- [White Glove](https://docs.microsoft.com/windows/deployment/windows-autopilot/white-glove) ermöglicht Partnern und IT-Mitarbeitern, einen Windows 10-PC vorab bereitzustellen, sodass dieser bereits vollständig konfiguriert und betriebsbereit ist.
- Mit [Autopilot für vorhandene Geräte](https://docs.microsoft.com/windows/deployment/windows-autopilot/existing-devices) können Sie die neueste Version von Windows 10 mühelos auf Ihren vorhandenen Geräten installieren.
- [Benutzergesteuerter Modus](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) für herkömmliche Benutzer.

In diesem Artikel wird das Einrichten von Autopilot für Windows-PCs erläutert. Weitere Informationen zu Autopilot und HoloLens finden Sie unter [Windows Autopilot für HoloLens 2](https://docs.microsoft.com/hololens/hololens2-autopilot).

## <a name="prerequisites"></a>Voraussetzungen

- [Intune-Abonnement](../fundamentals/licenses.md)
- [Die automatische Windows-Registrierung muss aktiviert sein](windows-enroll.md#enable-windows-10-automatic-enrollment).
- [Azure Active Directory Premium-Abonnement](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) <!--&#40;[trial subscription](https://go.microsoft.com/fwlink/?LinkID=816845)&#41;-->

## <a name="how-to-get-the-csv-for-import-in-intune"></a>Abrufen der CSV-Datei für den Import in Intune

Weitere Informationen finden Sie über das Cmdlet zu den Grundlagen von PowerShell.

- [Get-WindowsAutoPilotInfo](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo)

## <a name="add-devices"></a>Hinzufügen von Geräten

Sie können Windows Autopilot-Geräte durch Importieren einer CSV-Datei mit ihren Informationen hinzufügen.

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Geräte** > **Windows** > **Windows-Registrierung** > **Geräte** (unter **Windows AutoPilot Deployment-Programm** > **Importieren**).

    ![Screenshot von Windows Autopilot-Geräten](./media/enrollment-autopilot/autopilot-import-device.png)

2. Navigieren Sie unter **Windows AutoPilot-Geräte hinzufügen** zu einer CSV-Datei, die allen Geräte aufführt, die Sie hinzufügen möchten. Die CSV-Datei sollte die Seriennummern, die Windows-Produkt-IDs, die Hardware-Hashes, optionale Gruppentags und den optional zugewiesenen Benutzer auflisten. Die Liste kann bis zu 500 Zeilen enthalten. Informationen zum Abrufen von Geräteinformationen finden Sie unter [Hinzufügen von Geräten zu Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/add-devices#device-identification). Verwenden Sie das unten gezeigte Format für Header und Zeilen:

    `Device Serial Number,Windows Product ID,Hardware Hash,Group Tag,Assigned User`</br>
    `<serialNumber>,<ProductID>,<hardwareHash>,<optionalGroupTag>,<optionalAssignedUser>`

    ![Screenshot zum Hinzufügen von Windows Autopilot-Geräten](./media/enrollment-autopilot/autopilot-import-device2.png)

    >[!IMPORTANT]
    > Wenn Sie zum Zuweisen eines Benutzers einen CSV-Upload verwenden, stellen Sie sicher, dass Sie gültige UPNs zuweisen. Wenn Sie einen ungültigen UPN (einen falschen Benutzernamen) verwenden, wird Ihr Gerät möglicherweise unzugänglich, bis Sie die ungültige Zuweisung entfernen. Während eines CSV-Uploads wird nur überprüft, ob die Spalte **Zugewiesener Benutzer** einen gültigen Domänennamen enthält. Es kann keine individuelle UPN-Validierung durchgeführt werden, um sicherzustellen, dass Sie einen vorhandenen oder korrekten Benutzer zuweisen.

3. Wählen Sie **Importieren** aus, um mit dem Importieren von Informationen zu den Geräten zu beginnen. Der Import kann mehrere Minuten dauern.

4. Klicken Sie nach Abschluss des Imports unter **Windows Autopilot Deployment-Programm** > **Synchronisieren** auf **Geräte** > **Windows** > **Windows-Registrierung** > **Geräte**. Eine Meldung zeigt an, dass die Synchronisierung ausgeführt wird. Der Prozess kann ein paar Minuten in Anspruch nehmen, je nachdem, wie viele Geräte synchronisiert werden.

5. Aktualisieren Sie die Ansicht, um neue Geräte anzuzeigen.

## <a name="create-an-autopilot-device-group"></a>Erstellen einer Autopilot-Gerätegruppe

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf die Option **Gruppen** > **Neue Gruppe**.
2. Auf dem Blatt **Gruppe**:
    1. Wählen Sie für **Gruppentyp** die Option **Sicherheit**.
    2. Geben Sie einen **Gruppennamen** und eine **Gruppenbeschreibung** ein.
    3. Für **Mitgliedschaftstyp** wählen Sie entweder **Zugewiesen** oder **Dynamisches Gerät**.
3. Wenn Sie **Zugewiesen** als **Mitgliedschaftstyp** im vorherigen Schritt ausgewählt haben, wählen Sie anschließend auf dem Blatt **Gruppe** die Option **Mitglieder**, und fügen Sie Autopilot-Geräte zur Gruppe hinzu.
    Autopilot-Geräte, die noch nicht registriert sind, sind Geräte, deren Name der Seriennummer des Geräts entspricht.
4. Wenn Sie oben **Dynamisches Geräte** als **Mitgliedschaftstyp** ausgewählt haben,wählen Sie anschließend auf dem Blatt **Gruppe** die Option **Dynamische Gerätemitglieder**, und geben Sie einen der folgenden Codes in das Feld **Erweiterte Regel** ein. Nur Autopilot-Geräte werden von diesen Regeln erfasst, da sie auf Attribute abzielen, die nur Autopilot-Geräte aufweisen. Das Erstellen einer Gruppe, die auf Nicht-Autopilot-Attributen basiert, garantiert nicht, dass die in der Gruppe enthaltenen Geräte tatsächlich bei Autopilot registriert sind.
    - Wenn Sie eine Gruppe mit all Ihren Autopilot-Geräten erstellen möchten, geben Sie ein: `(device.devicePhysicalIDs -any (_ -contains "[ZTDId]"))`
    - Das Intune-Feld „Gruppentag“ wird dem Attribut „OrderID“ auf Azure AD-Geräten zugeordnet. Wenn Sie eine Gruppe erstellen möchten, die all Ihre Autopilot-Geräte mit einem bestimmten Gruppentag (der OrderID der Azure AD-Geräte) enthält, müssen Sie Folgendes eingeben: `(device.devicePhysicalIds -any _ -eq "[OrderID]:179887111881")`
    - Wenn Sie eine Gruppe mit all Ihren Autopilot-Geräten mit einer bestimmten Bestellungs-ID erstellen möchten, geben Sie `(device.devicePhysicalIds -any _ -eq "[PurchaseOrderId]:76222342342")` ein.
    
    Wählen Sie nach dem Hinzufügen des Codes im Feld **Erweiterte Regel** die Option **Speichern**.
5. Wählen Sie **Erstellen** aus.  

## <a name="create-an-autopilot-deployment-profile"></a>Erstellen eines Autopilot-Bereitstellungsprofils
Autopilot-Bereitstellungsprofile werden verwendet, um die Autopilot-Geräte zu konfigurieren. Sie können bis zu 350 Profile pro Mandant erstellen.
1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Geräte** > **Windows** > **Windows-Registrierung** > **Deployment Profiles** (Bereitstellungsprofile) > **Profil erstellen** > **Wählen-PC** oder **HoloLens**. In diesem Artikel wird das Einrichten von Autopilot für Windows-PCs erläutert. Weitere Informationen zu Autopilot und HoloLens finden Sie unter [Windows Autopilot für HoloLens 2](https://docs.microsoft.com/hololens/hololens2-autopilot).
2. Geben Sie auf der Seite **Grundlagen** einen Wert in **Name** und eine optionale **Beschreibung** ein.

    ![Screenshot der Seite „Grundlagen“](./media/enrollment-autopilot/create-profile-basics.png)

3. Wenn Sie möchten, dass alle Geräte in den zugewiesenen Gruppen automatisch in Autopilot konvertiert werden, legen Sie für **Alle Zielgeräte in Autopilot-Geräte konvertieren** den Wert **Ja** fest. Alle unternehmenseigenen, Nicht-Autopilot-Geräte in zugewiesenen Gruppen werden mit dem Autopilot-Bereitstellungsdienst registriert. Private Geräte werden nicht in Autopilot konvertiert. Die Verarbeitung der Registrierung kann 48 Stunden dauern. Wenn die Registrierung des Geräts aufgehoben und es zurückgesetzt ist, registriert Autopilot es. Nachdem ein Gerät auf diese Weise registriert wurde, wird das Gerät durch Deaktivieren dieser Option oder Entfernen der Profilzuordnung nicht aus dem Autopilot-Bereitstellungsdienst entfernt. Sie müssen stattdessen [das Gerät direkt entfernen](enrollment-autopilot.md#delete-autopilot-devices).
4. Wählen Sie **Weiter** aus.
5. Wählen Sie auf der Seite **Out-of-Box-Experience (OOBE)** als **Bereitstellungsmodus** eine der beiden folgenden Optionen aus:
    - **Benutzergesteuert**: Geräte mit diesem Profil werden dem Benutzer zugeordnet, der das Gerät registriert. Für die Registrierung des Geräts sind Benutzeranmeldeinformationen erforderlich.
    - **Selbstbereitstellend (Vorschauversion)** : (Windows 10, Version 1809 oder höher, erforderlich) Geräte mit diesem Profil werden nicht dem Benutzer zugeordnet, der das Gerät registriert. Für die Registrierung des Geräts sind keine Anmeldeinformationen erforderlich. Wenn einem Gerät kein Benutzer zugeordnet ist, gelten keine benutzerbasierten Kompatibilitätsrichtlinien. Wenn Sie den Self-Deployment-Modus verwenden, werden nur Kompatibilitätsrichtlinien angewendet, die auf das Gerät abzielen.

    ![Screenshot der Seite „OOBE“](./media/enrollment-autopilot/create-profile-outofbox.png)

   > [!NOTE]
   > Optionen, die abgeblendet oder schattiert angezeigt werden, werden derzeit vom ausgewählten Bereitstellungsmodus nicht unterstützt.

6. Wählen Sie im Feld **Verknüpfen mit Azure AD als** die Option **In Azure AD eingebunden**.
7. Konfigurieren Sie die folgenden Optionen:
    - **Microsoft-Software-Lizenzbedingungen**: (Windows 10, Version 1709 oder höher) Wählen Sie aus, ob die Lizenzbedingungen den Benutzern angezeigt werden sollen.
    - **Datenschutzeinstellungen**: Wählen Sie aus, ob die Datenschutzeinstellungen den Benutzern angezeigt werden.
    >[!IMPORTANT]
    >Der Standardwert für die Diagnosedateneinstellung variiert je nach Windows-Version. Bei Geräten unter Windows 10, Version 1903, wird der Standardwert während der Out-of-Box-Funktion auf „Full“ festgelegt. Weitere Informationen finden Sie unter [Windows-Diagnosedaten](https://docs.microsoft.com/windows/privacy/windows-diagnostic-data). <br>
    
    - **Optionen zur Kontoänderung ausblenden (Windows 10, Version 1809 oder höher, erforderlich)** : Wählen Sie **Ausblenden** aus, um zu verhindern, dass Optionen zum Ändern des Kontos auf der Anmeldeseite des Unternehmens und den Domänenfehlerseiten angezeigt werden. Für diese Option muss das [Unternehmensbranding in Azure Active Directory konfiguriert](https://docs.microsoft.com/azure/active-directory/fundamentals/customize-branding) sein.
    - **Art des Benutzerkontos**: Wählen Sie den Kontotyp des Benutzers aus (**Administrator** oder **Standardbenutzer**). Der Benutzer, der dem Gerät beitritt, kann ein lokaler Administrator werden, indem er zur lokalen Administratorgruppe hinzugefügt wird. Wir aktivieren den Benutzer nicht als Standardadministrator auf dem Gerät.
    - **Willkommensseite ohne Benutzerauthentifizierung zulassen** (erfordert Windows 10, Version 1903 oder höher; [zusätzliche physische Anforderungen](https://docs.microsoft.com/windows/deployment/windows-autopilot/white-glove#prerequisites)): Wählen Sie **Ja** aus, um die intensive Benutzerunterstützung zuzulassen.
    - **Vorlage für Gerätenamen anwenden** (erfordert Windows 10, Version 1809 oder höher und Azure AD-Verknüpfungstyp): Klicken Sie auf **Ja**, um eine Vorlage für die Benennung eines Geräts während der Registrierung zu erstellen. Namen dürfen höchstens 15 Zeichen lang sein und können Buchstaben, Zahlen und Bindestriche enthalten. Ein Name darf nicht nur aus Zahlen bestehen. Verwenden Sie das [%SERIAL%-Makro](https://docs.microsoft.com/windows/client-management/mdm/accounts-csp), um eine hardwarespezifische Seriennummer hinzuzufügen. Verwenden Sie alternativ das [%RAND:x%-Makro](https://docs.microsoft.com/windows/client-management/mdm/accounts-csp), um eine zufällige Zeichenfolge von Zahlen hinzuzufügen, bei der x der Anzahl der hinzuzufügenden Ziffern entspricht. Sie können nur in einem [Domänenbeitrittsprofil](windows-autopilot-hybrid.md#create-and-assign-a-domain-join-profile) ein Präfix für Hybridgeräte bereitstellen. 
    - **Sprache (Region)** \*: Wählen Sie die Sprache aus, die für das Gerät verwendet werden soll. Diese Option ist nur verfügbar, wenn Sie **Selbstbereitstellend** als **Bereitstellungsmodus** ausgewählt haben.
    - **Tastatur automatisch konfigurieren**\*: Wenn **Sprache (Region)** ausgewählt ist, können Sie mit **Ja** die Tastaturauswahlseite überspringen. Diese Option ist nur verfügbar, wenn Sie **Selbstbereitstellend** als **Bereitstellungsmodus** ausgewählt haben.
8. Wählen Sie **Weiter** aus.
9. Fügen Sie auf der Seite **Bereichsmarkierungen** optional die Bereichsmarkierungen hinzu, die Sie auf dieses Profil anwenden möchten. Weitere Informationen zu Bereichsmarkierungen finden Sie unter [Use role-based access control and scope tags for distributed IT (Verwenden der rollenbasierten Zugriffssteuerung und von Bereichsmarkierungen für verteilte IT)](../fundamentals/scope-tags.md).
10. Wählen Sie **Weiter** aus.
11. Wählen Sie auf der Seite **Zuweisungen** für **Zuweisen an** die Option **Ausgewählte Gruppen** aus.

    ![Screenshot der Seite „Zuweisungen“](./media/enrollment-autopilot/create-profile-assignments.png)

12. Wählen Sie **Einzuschließende Gruppen auswählen** und dann die Gruppen aus, die Sie in dieses Profil einbeziehen möchten.
13. Wenn Sie Gruppen ausschließen möchten, wählen Sie **Auszuschließende Gruppen auswählen** und dann die Gruppen aus, die Sie ausschließen möchten.
14. Wählen Sie **Weiter** aus.
15. Wählen Sie auf der Seite **Überprüfen + Erstellen** den Befehl **Erstellen** aus, um das Profil zu erstellen.

    ![Screenshot der Seite „Überprüfen“](./media/enrollment-autopilot/create-profile-review.png)

> [!NOTE]
> Intune führt regelmäßig eine Überprüfung auf neuen Geräten in den zugewiesenen Gruppen durch und beginnt dann mit der Zuweisung von Profilen zu diesen Geräten. Dieser Vorgang kann einige Minuten dauern. Vor der Bereitstellung eines Geräts stellen Sie sicher, dass der Vorgang abgeschlossen ist.  Unter **Windows Autopilot Deployment Program** (Windows Autopilot Deployment-Programm) können Sie über **Geräte** > **Windows** > **Windows enrollment** > **Geräte** (Windows-Registrierung) überprüfen, ob der Profilstatus von „Nicht zugewiesen“ in „Assigning“ (Wird zugewiesen) und dann schließlich in „Zugewiesen“ geändert wird.

## <a name="edit-an-autopilot-deployment-profile"></a>Bearbeiten eines Autopilot-Bereitstellungsprofils
Nachdem Sie ein Autopilot-Bereitstellungsprofil erstellt haben, können Sie bestimmte Teile des Bereitstellungsprofils bearbeiten.   

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Geräte** > **Windows** > **Windows-Registrierung** > **Deployment Profiles** (Bereitstellungsprofile).
2. Wählen Sie das Profil aus, das Sie bearbeiten möchten.
3. Klicken Sie auf der linken Seite auf **Eigenschaften**, um den Namen oder die Beschreibung des Bereitstellungsprofils zu ändern. Klicken Sie auf **Speichern**, wenn Sie Änderungen vorgenommen haben.
5. Klicken Sie auf **Einstellungen**, um Änderungen an den OOBE-Einstellungen vorzunehmen. Klicken Sie auf **Speichern**, wenn Sie Änderungen vorgenommen haben.

> [!NOTE]
> Änderungen am Profil werden für die diesem Profil zugewiesenen Geräte angewendet. Das aktualisierte Profil wird jedoch nicht auf ein Gerät angewendet, das bereits bei Intune registriert ist, bis das Gerät zurückgesetzt und erneut registriert wurde.

## <a name="edit-autopilot-device-attributes"></a>Bearbeiten von Autopilot-Geräteattributen
Nachdem Sie ein Autopilot-Gerät hochgeladen haben, können Sie bestimmte Geräteattribute bearbeiten.

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Geräte** > **Windows** > **Windows-Registrierung** > **Geräte** (unter **Windows AutoPilot Deployment-Programm**).
2. Wählen Sie das Gerät aus, das Sie bearbeiten möchten.
3. Im rechten Bereich des Bildschirms können Sie den Gerätenamen, das Gruppentag oder den benutzerfreundlichen Namen bearbeiten (sofern Sie einen Benutzer zugewiesen haben).
4. Wählen Sie **Speichern** aus.

> [!NOTE]
> Gerätenamen können für alle Geräte konfiguriert werden, werden aber bei mit Azure AD Hybrid im Zusammenhang stehenden Bereitstellungen ignoriert. Der Gerätename stammt weiterhin aus dem Domänenbeitrittsprofil für Azure AD Hybrid-Geräte.

## <a name="alerts-for-windows-autopilot-unassigned-devices-----163236---"></a>Warnungen für nicht zugewiesene Windows Autopilot-Geräte  <!-- 163236 -->  

Warnungen zeigen an, wie viele Autopilot-Programmgeräte keine Autopilot-Bereitstellungsprofile aufweisen. Verwenden Sie die Informationen aus der Warnung, um Profile zu erstellen und sie den nicht zugeordneten Geräten zuzuweisen. Wenn Sie auf die Warnung klicken, sehen Sie die vollständige Liste der Windows Autopilot-Geräte zusammen mit detaillierten Informationen.

Um Warnungen zu nicht zugewiesenen Geräten anzuzeigen, klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Geräte** > **Übersicht** > **Registrierungswarnungen** > **Nicht zugewiesene Geräte**.  

## <a name="autopilot-deployments-report"></a>Bericht über Autopilot-Bereitstellungen
Sie können Details zu jedem Gerät, das über Windows Autopilot bereitgestellt wird, anzeigen.
Navigieren Sie zum [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431), und klicken Sie auf **Geräte** > **Überwachen** > **Autopilot-Bereitstellungen**, um den Bericht anzuzeigen.
Die Daten sind für 30 Tage nach der Bereitstellung verfügbar.

Dieser Bericht befindet sich in der Vorschau. Gerätebereitstellungsdatensätze werden zurzeit nur durch neue Intune-Registrierungsereignisse ausgelöst. Dies bedeutet, dass alle Bereitstellungen, die keine neue Intune-Registrierung auslösen, von diesem Bericht nicht erfasst werden. Dies schließt jede Art von Zurücksetzung ein, die die Registrierung und den Benutzeranteil der intensiven Autopilot-Benutzerunterstützung beibehält.

## <a name="assign-a-user-to-a-specific-autopilot-device"></a>Hinzufügen eines Benutzers zu einem bestimmten Autopilot-Gerät

Sie können einen Benutzer zu einem bestimmten Autopilot-Gerät hinzufügen. Durch diese Zuweisung werden während der Windows-Einrichtung auf der [unternehmensspezifischen](https://docs.microsoft.com/azure/active-directory/fundamentals/customize-branding) Anmeldeseite schon vorab die Informationen für einen Benutzer eingetragen, der in Azure Active Directory verwaltet wird. Sie können auch eine benutzerdefinierte Begrüßung festlegen. Die Windows-Anmeldung wird nicht vorab ausgefüllt oder geändert. Nur lizenzierte Intune-Benutzer können so zugewiesen werden.

Voraussetzungen: Das Azure Active Directory-Unternehmensportal wurde konfiguriert und verfügt über Windows 10, Version 1809 oder höher.

> [!NOTE]
> Das Zuweisen eines Benutzers zu einem spezifischen Autopilot-Gerät funktioniert nicht, wenn Sie ADFS verwenden.

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Geräte** > **Windows** > **Windows-Registrierung** > **Geräte** (unter **Windows AutoPilot Deployment-Programm**). Wählen Sie anschließend das Gerät aus, und klicken Sie auf **Assign user** (Benutzer zuweisen).

    ![Screenshot von „Benutzer zuweisen“](./media/enrollment-autopilot/assign-user.png)

2. Wählen Sie einen für Intune lizenzierten Azure-Benutzer aus, und klicken Sie auf **Auswählen**.

    ![Screenshot der Benutzerauswahl](./media/enrollment-autopilot/select-user.png)

3. Geben Sie im Feld **User Friendly Name** (Anzeigename) einen Anzeigenamen ein, oder akzeptieren Sie die Standardeinstellung. Diese Zeichenfolge ist der Anzeigename, der angezeigt wird, wenn sich der Benutzer während des Windows-Setups anmeldet.

    ![Screenshot von Anzeigename](./media/enrollment-autopilot/friendly-name.png)

4. Klicken Sie auf **OK**.


## <a name="delete-autopilot-devices"></a>Löschen von Autopilot-Geräten

Sie können Windows Autopilot-Geräte, die in Intune nicht registriert sind, folgendermaßen löschen:

- Löschen Sie unter **Windows Autopilot Deployment Program** (Windows Autopilot Deployment-Programm) die Geräte über **Geräte** > **Windows** > **Windows enrollment** > **Geräte** (Windows-Registrierung) aus Windows Autopilot. Wählen Sie die Geräte, die Sie löschen möchten, und dann **Löschen** aus. Die Gerätelöschung in Windows Autopilot kann ein paar Minuten lang dauern.

Für die vollständige Entfernung eines Geräts von Ihrem Mandanten müssen Sie das Intune-Gerät, das Azure Active Directory-Gerät und die Windows Autopilot-Geräteeinträge löschen. Dies lässt sich alles über Intune erledigen:

1. Wenn die Geräte bei Intune registriert sind, müssen Sie sie zuerst [aus dem Intune-Blatt „Alle Geräte“ löschen](../remote-actions/devices-wipe.md#delete-devices-from-the-azure-active-directory-portal).

2. Löschen Sie die Geräte in den Azure Active Directory-Geräten über **Geräte** > **Azure AD-Geräte**.

3. Löschen Sie unter **Windows Autopilot Deployment Program** (Windows Autopilot Deployment-Programm) die Geräte über **Geräte** > **Windows** > **Windows enrollment** > **Geräte** (Windows-Registrierung) aus Windows Autopilot. Wählen Sie die Geräte, die Sie löschen möchten, und dann **Löschen** aus. Die Gerätelöschung in Windows Autopilot kann ein paar Minuten lang dauern.

## <a name="using-autopilot-in-other-portals"></a>Verwenden von Autopilot in anderen Portalen
Wenn die mobile Geräteverwaltung für Sie nicht von Interesse ist, können Sie Autopilot in anderen Portalen verwenden. Die Verwendung von anderen Portalen ist ebenfalls möglich, es wird jedoch empfohlen, ausschließlich Intune zum Verwalten Ihrer Autopilot-Bereitstellungen zu verwenden. Wenn Sie Intune und ein anderes Portal verwenden, kann Intune folgende Funktionen nicht verwenden:  

- Anzeigen von Änderungen an Profilen, die in Intune erstellt, aber in einem anderen Portal bearbeitet wurden
- Synchronisieren von Profilen, die in einem anderen Portal erstellt wurden
- Anzeigen von Profilzuweisungen, die in einem anderen Portal vorgenommen wurden
- Synchronisieren von Profilzuweisungen, die in einem anderen Portal vorgenommen wurden
- Anzeigen von Änderungen an der Geräteliste, die in einem anderen Portal vorgenommen wurden

## <a name="windows-autopilot-for-existing-devices"></a>Windows Autopilot für vorhandene Geräte

Sie können Windows-Geräte nach einer Korrelator-ID gruppieren, wenn sie mit [Autopilot für bestehende Geräte](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) über Configuration Manager registriert werden. Die Korrelator-ID ist ein Parameter der Autopilot-Konfigurationsdatei. Das Azure AD-Geräteattribut [enrollmentProfileName](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices) ist standardmäßig auf „OfflineAutopilotprofile-\<correlator ID\>“ festgelegt. Dadurch können beliebige dynamische Azure AD-Gruppen basierend auf der Korrelator-ID über das Attribut „enrollmentprofileName“ erstellt werden.

>[!WARNING] 
> Da die Korrelator-ID nicht in Intune aufgelistet ist, kann das Gerät eine beliebige Korrelator-ID melden. Wenn der Benutzer eine Korrelator-ID erstellt, die dem Autopilot- oder Apple-ADE-Profilnamen entspricht, wird das Gerät basierend auf dem Attribut „enrollmentProfileName“ einer beliebigen dynamischen Azure AD-Gerätegruppe hinzugefügt. Um einen solchen Konflikt zu vermeiden, gehen Sie wie folgt vor:
> - Erstellen Sie stets dynamische Gruppenregeln für den *gesamten* enrollmentProfileName-Wert.
> - Vergeben Sie niemals Namen für Autopilot- oder Apple-ADE-Profile, die mit „OfflineAutopilotprofile-“ beginnen.

## <a name="next-steps"></a>Nächste Schritte
Nachdem Sie Windows Autopilot für registrierte Windows 10-Geräte konfiguriert haben, erfahren Sie mehr über die Verwaltung dieser Geräte. Weitere Informationen finden Sie unter [Was ist die Microsoft Intune-Geräteverwaltung?](../remote-actions/device-management.md).
