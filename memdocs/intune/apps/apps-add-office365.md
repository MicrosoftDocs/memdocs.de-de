---
title: Hinzufügen von Office 365-Apps zu Windows 10-Geräten mit Microsoft Intune
titleSuffix: ''
description: Erfahren Sie, wie Sie Microsoft Intune verwenden können, um Office 365-Apps auf Windows 10-Geräten zu installieren.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/10/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3292671a-5f5a-429e-90f7-b20019787d22
ms.reviewer: craigma
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, seoapril2019
ms.collection: M365-identity-device-management
ms.openlocfilehash: d411950dce117aa9c99f806d2ef80796a2a2fc50
ms.sourcegitcommit: fb84a87e46f9fa126c1c24ddea26974984bc9ccc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2020
ms.locfileid: "82023264"
---
# <a name="add-office-365-apps-to-windows-10-devices-with-microsoft-intune"></a>Hinzufügen von Office 365-Apps zu Windows 10-Geräten mit Microsoft Intune

Bevor Sie Apps zuweisen, überwachen, konfigurieren oder schützen können, müssen Sie sie zu Intune hinzufügen. Zu den verfügbaren [App-Typen](apps-add.md#app-types-in-microsoft-intune) gehören Office 365-Apps für Windows 10-Geräte. Wenn Sie den App-Typ in Intune auswählen, können Sie Office 365-Apps zuweisen und auf Geräten mit Windows 10 installieren. Sie können auch Apps für den Microsoft Project Online-Desktopclient und Microsoft Visio Online Plan 2 zuweisen und installieren, wenn Sie über die entsprechenden Lizenzen verfügen. Die verfügbaren Office 365-Apps werden in Azure in der Intune-Konsole als einzelne Einträge in der App-Liste angezeigt.

> [!NOTE]
> Microsoft Office 365 ProPlus wurde in **Microsoft 365 Apps for Enterprise** umbenannt. In unserer Dokumentation wird üblicherweise **Microsoft 365-Apps** verwendet.
> 
> Sie müssen Microsoft 365-Apps-Lizenzen verwenden, um Microsoft 365-Apps zu aktivieren, die über Microsoft Intune bereitgestellt wurden. Die Microsoft 365-Apps for Business-Edition wird von Intune unterstützt. Sie müssen jedoch die App-Suite der Microsoft 365-Apps for Business-Edition mithilfe von XML-Daten konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren der App-Suite mithilfe von XML-Daten](apps-add-office365.md#step-2---option-2-configure-app-suite-using-xml-data).

## <a name="before-you-start"></a>Vorbereitung

> [!IMPORTANT]
> Wenn es auf dem Endbenutzergerät MSI-Office-Apps gibt, müssen Sie diese Apps mit dem Feature **MSI entfernen** sicher deinstallieren. Andernfalls schlägt die Installation der von Intune bereitgestellten Office 365-Apps fehl.

- Auf den Geräten, auf denen Sie diese Apps bereitstellen, muss das Windows 10 Creators Update oder höher ausgeführt werden.
- Intune unterstützt nur das Hinzufügen von Office-Apps aus der Microsoft 365-Apps-Suite.
- Falls Office-Apps geöffnet sind, wenn Intune die App-Suite installiert, kann bei der Installation ein Fehler auftreten, und Benutzer verlieren möglicherweise Daten aus nicht gespeicherten Dateien.
- Diese Installationsmethode wird auf Windows Home-, Windows Team-, Windows Holographic- oder Windows Holographic for Business-Geräten nicht unterstützt.
- Intune unterstützt nicht das Installieren von Office 365-Desktop-Apps aus dem Microsoft Store (sogenannte Office Centennial-Apps) auf einem Gerät, für das bereits Office 365-Apps mit Intune bereitgestellt wurden. Wenn Sie diese Konfiguration installieren, kann sie zu Datenverlusten oder -beschädigungen führen.
- Mehrere erforderliche oder verfügbare App-Zuweisungen sind nicht additiv. Eine spätere App-Zuweisung überschreibt bereits vorhandene installierte App-Zuweisungen. Wenn z.B. der erste Satz von Office-Apps Word enthält und der spätere nicht, wird Word deinstalliert. Diese Bedingung gilt nicht für Visio- oder Project-Anwendungen.
- Mehrere Office 365-Bereitstellungen werden derzeit nicht unterstützt. Es wird nur eine Bereitstellung an das Gerät übermittelt.
- **Office-Version:** Wählen Sie aus, ob Sie die 32-Bit- oder die 64-Bit-Version von Office zuweisen möchten. Sie können die 32-Bit-Version sowohl auf 32-Bit- als auch auf 64-Bit-Geräten installieren. Die 64-Bit-Version lässt sich jedoch nur auf 64-Bit-Geräten installieren.
- **Remove MSI from end-user devices** (MSI von Endbenutzergeräten entfernen): Wählen Sie aus, ob Sie vorhandene Office-MSI-Apps von Endbenutzergeräten entfernen möchten. Die Installation kann nicht erfolgreich durchgeführt werden, wenn bereits MSI-Apps auf den Endbenutzergeräten vorhanden sind. Die zu deinstallierenden Apps sind nicht auf die Apps beschränkt, die in **App-Suite konfigurieren** zur Installation ausgewählt wurden, sondern es werden sämtliche Office-(MSI)-Apps vom Endbenutzergerät entfernt. Weitere Informationen finden Sie unter [Remove existing MSI versions of Office when upgrading to Office 365 ProPlus (Entfernen vorhandener MSI-Versionen von Office beim Upgrade auf Microsoft 365-Apps)](https://docs.microsoft.com/deployoffice/upgrade-from-msi-version). Wenn Intune Office auf den Computern Ihrer Endbenutzer neu installiert, erhalten sie automatisch dieselben Sprachpakete wie bei früheren MSI-Office-Installationen.

## <a name="select-microsoft-365-apps"></a>Auswählen von Microsoft 365-Apps

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Apps** > **Alle Apps** > **Hinzufügen** aus.
3. Wählen Sie **Windows 10** im Abschnitt **Microsoft 365-Apps** des Bereichs **App-Typ auswählen** aus.
4. Klicken Sie auf **Auswählen**. Die Schritte für **Microsoft 365-Apps hinzufügen** werden angezeigt.


## <a name="step-1---app-suite-information"></a>Schritt 1: Informationen zur App-Suite

In diesem Schritt stellen Sie Informationen über die App-Suite bereit. Diese Informationen helfen Ihnen dabei, die App-Suite in Intune zu identifizieren. Außerdem können Benutzer sie im Unternehmensportal leichter finden.

1. Auf der Seite **Informationen zur App-Suite** können Sie die Standardwerte bestätigen oder ändern:
    - **Name der Suite**: Geben Sie den Namen der App-Suite so ein, wie er im Unternehmensportal angezeigt wird. Stellen Sie sicher, dass alle Suitenamen eindeutig sind. Wenn ein Sammlungsname zweimal vergeben wird, wird den Benutzern im Unternehmensportal nur eine der Apps angezeigt.
    - **Beschreibung der Suite**: Geben Sie eine Beschreibung der App-Suite ein. Sie können die Apps auflisten, die Sie einschließen möchten.
    - **Herausgeber**: Als Herausgeber wird Microsoft angezeigt.
    - **Kategorie**: Wählen Sie optional eine oder mehrere der integrierten oder von Ihnen erstellten App-Kategorien aus. Diese Einstellung erleichtert den Benutzern die Suche nach der App-Suite im Unternehmensportal.
    - **Diese App als ausgewählte App im Unternehmensportal anzeigen**: Wählen Sie diese Option, um die App-Suite auf der Hauptseite des Unternehmensportals hervorgehoben anzuzeigen, wenn die Benutzer nach Apps suchen.
    - **Informations-URL**: Geben Sie optional eine URL zu einer Website ein, die Informationen über diese App enthält. Diese URL wird Benutzern im Unternehmensportal angezeigt.
    - **URL zu den Datenschutzbestimmungen**: Geben Sie optional eine URL zu einer Website ein, die Datenschutzinformationen für diese App enthält. Diese URL wird Benutzern im Unternehmensportal angezeigt.
    - **Entwickler**: Als Entwickler wird Microsoft angezeigt.
    - **Besitzer**: Als Besitzer wird Microsoft angezeigt.
    - **Anmerkungen**: Geben Sie Hinweise zu dieser App ein.
    - **Logo**: Das Logo von Microsoft 365-Apps wird gemeinsam mit der App angezeigt, wenn der Benutzer das Unternehmensportal durchsucht.
2. Klicken Sie auf **Weiter**, um die Seite **App-Suite konfigurieren** anzuzeigen.

## <a name="step-2---option-1-configure-app-suite-using-the-configuration-designer"></a>Schritt 2 (**Option 1**): Konfigurieren der App-Suite mithilfe des Konfigurations-Designers 

Sie können eine Methode zum Konfigurieren von App-Einstellungen auswählen, indem Sie das **Format der Konfigurationseinstellungen** auswählen. Es stehen die folgenden Einstellungsformate zur Verfügung:
- Konfigurations-Designer
- Eingeben von XML-Daten

Wenn Sie **Konfigurations-Designer** auswählen, ändert sich der Bereich **App hinzufügen**, und es werden drei weitere Einstellungsbereiche angezeigt:
- Konfigurieren der App-Suite
- Informationen zur App-Suite
- Eigenschaften

<img alt="Add Microsoft 365 Apps - Configuration designer" src="./media/apps-add-office365/apps-add-office365-02.png" width="700">

1. Wählen Sie auf der Seite **App-Suite konfigurieren** die Option **Konfigurations-Designer** aus.
   - **Office-Apps auswählen**: Wählen Sie in der Dropdownliste die Standard-Office-Apps aus, die Sie Geräten zuweisen möchten.
   - **Weitere Office-Apps auswählen (Lizenz erforderlich)** : Wählen Sie in der Dropdownliste zusätzliche Office-Apps aus, die Sie Geräten zuweisen möchten und für die Sie über Lizenzen verfügen. Hierzu gehören lizenzierte Apps wie der Microsoft Project Online-Desktopclient und Microsoft Visio Online (Plan 2).
   - **Architektur**: Wählen Sie aus, ob Sie die **32-Bit**- oder **64-Bit**-Version von Microsoft 365-Apps zuweisen möchten. Sie können die 32-Bit-Version sowohl auf 32-Bit- als auch auf 64-Bit-Geräten installieren. Die 64-Bit-Version lässt sich jedoch nur auf 64-Bit-Geräten installieren.
    - **Updatekanal**: Wählen Sie aus, wie Office auf Geräten aktualisiert wird. Informationen zu den unterschiedlichen Updatekanälen finden Sie in der [Übersicht der Updatekanäle für Office 365 ProPlus](https://docs.microsoft.com/DeployOffice/overview-of-update-channels-for-office-365-proplus). Es stehen die folgenden Optionen zur Auswahl:
        - **Monatlich**
        - **Monatlich (Ziel)**
        - **Halbjährlich**
        - **Halbjährlich (Ziel)**

        Nach der Auswahl eines Kanals stehen folgende Optionen zur Verfügung:
        - **Andere Versionen entfernen**: Klicken Sie auf **Ja**, um andere Office-Versionen (MSI) von Benutzergeräten zu entfernen. Wählen Sie diese Option aus, wenn Sie vorhandene Office-MSI-Apps von Endbenutzergeräten entfernen möchten. Die Installation kann nicht erfolgreich durchgeführt werden, wenn bereits MSI-Apps auf den Endbenutzergeräten vorhanden sind. Die zu deinstallierenden Apps sind nicht auf die Apps beschränkt, die in **App-Suite konfigurieren** zur Installation ausgewählt wurden, sondern es werden sämtliche Office-(MSI)-Apps vom Endbenutzergerät entfernt. Weitere Informationen finden Sie unter [Remove existing MSI versions of Office when upgrading to Office 365 ProPlus (Entfernen vorhandener MSI-Versionen von Office beim Upgrade auf Microsoft 365-Apps)](https://docs.microsoft.com/deployoffice/upgrade-from-msi-version). Wenn Intune Office auf den Computern Ihrer Endbenutzer neu installiert, erhalten sie automatisch dieselben Sprachpakete wie bei früheren MSI-Office-Installationen. 
        - **Zu installierende Version**: Wählen Sie die Office-Version aus, die installiert werden soll.
        - **Bestimmte Version**: Wenn Sie in der Einstellung oben **Bestimmte Version** als Option für **Zu installierende Version** ausgewählt haben, können Sie eine bestimmte Version von Office für den ausgewählten Kanal auf Endbenutzergeräten installieren. 
            
            Die verfügbaren Versionen werden im Laufe der Zeit geändert. Wenn Sie eine neue Bereitstellung erstellen, können deshalb die verfügbaren Versionen aktueller sein, und bestimmte ältere Versionen sind möglicherweise nicht mehr verfügbar. Für aktuelle Bereitstellungen sind weiterhin die älteren Versionen verfügbar, jedoch wird die Liste mit den Versionen nicht ständig pro Kanal aktualisiert.
            
            Der Berichtsstatus für Geräte, deren angeheftete Version (oder andere Eigenschaften) aktualisiert wurde und die als verfügbar bereitgestellt wurden, lautet „Installiert“, wenn die vorherige Version vor dem Check-In des Geräts installiert wurde. Wenn das Gerät eingecheckt wird, ändert sich der Status vorübergehend in „Unbekannt“. Dies wird dem Benutzer nicht angezeigt. Wenn der Benutzer die Installation der neuesten verfügbaren Version startet, wird der Status als „Installiert“ angezeigt.
            
            Weitere Informationen finden Sie unter [Übersicht über die Updatekanäle für Microsoft 365-Apps](https://docs.microsoft.com/DeployOffice/overview-of-update-channels-for-office-365-proplus).
    - **Aktivierung gemeinsam genutzter Computer verwenden**: Wählen Sie diese Option aus, wenn sich mehrere Benutzer einen Computer teilen. Weitere Informationen finden Sie in der [Übersicht über die Aktivierung gemeinsam genutzter Computer für Microsoft 365-Apps](https://docs.microsoft.com/DeployOffice/overview-of-shared-computer-activation-for-office-365-proplus).
    - **Microsoft-Software-Lizenzbedingungen automatisch akzeptieren**: Wählen Sie diese Option aus, wenn es nicht erforderlich ist, dass Endbenutzer die Lizenzvereinbarung akzeptieren. Intune akzeptiert daraufhin die automatisch die Vereinbarung.
    - **Sprachen**: Office wird automatisch in allen unterstützen Sprachen installiert, die mit Windows auf Endbenutzergeräten installiert wurden. Wählen Sie diese Option, wen Sie zusätzliche Sprachen mit der App-Sammlung installieren möchten. <p></p>
        Sie können zusätzliche Sprachen für Office 365 Pro Plus-Apps bereitstellen, die über Intune verwaltet werden. In der Liste der verfügbaren Sprachpakete ist auch der **Typ** der Sprachpakete angegeben (grundlegende Sprachunterstützung, Sprache teilweise unterstützt und Sprachkorrekturhilfen). Wählen Sie im Azure-Portal Bereich **Microsoft Intune** > **Apps** > **Alle Apps** > **Hinzufügen** aus. Wählen Sie im Bereich **App hinzufügen** in der Liste **App-Typ** unter **Microsoft 365-Apps** den Eintrag **Windows 10** aus. Wählen Sie im Bereich **Einstellungen der App-Suite** die Option **Sprachen** aus. Weitere Informationen finden Sie unter [Übersicht über die Bereitstellung von Sprachen in Microsoft 365-Apps](https://docs.microsoft.com/deployoffice/overview-of-deploying-languages-in-office-365-proplus).
2. Klicken Sie auf **Weiter**, um die Seite **Bereichsmarkierungen** anzuzeigen.

## <a name="step-2---option-2-configure-app-suite-using-xml-data"></a>Schritt 2 (**Option 2**): Konfigurieren der App-Suite mithilfe von XML-Daten 

Wenn Sie auf der Seite **App-Suite konfigurieren** unter dem Dropdownfeld **Einstellungsformat** die Option **XML-Daten eingeben** ausgewählt haben, können Sie die Office-App-Suite mithilfe einer benutzerdefinierten Konfigurationsdatei konfigurieren.

![Konfigurations-Designer für Office 365 hinzufügen](./media/apps-add-office365/apps-add-office365-01.png)

1. Fügen Sie Ihre XML-Konfigurationsdatei hinzu.

    > [!NOTE]
    > Die Produkt-ID kann entweder Business (`O365BusinessRetail`) oder ProPlus (`O365ProPlusRetail`) sein. Sie können jedoch nur die App-Suite von Microsoft 365-Apps für Business-Edition mithilfe von XML-Daten konfigurieren. Beachten Sie, dass Microsoft Office 365 ProPlus in **Microsoft 365 Apps for Enterprise** umbenannt wurde.

2. Klicken Sie auf **Weiter**, um die Seite **Bereichsmarkierungen** anzuzeigen.

Weitere Informationen zum Eingeben von XML-Daten finden Sie unter [Konfigurationsoptionen für das Office-Bereitstellungstool](https://docs.microsoft.com/DeployOffice/configuration-options-for-the-office-2016-deployment-tool).

## <a name="step-3---select-scope-tags-optional"></a>Schritt 3: Auswählen von Bereichsmarkierungen (optional)
Sie können Bereichsmarkierungen verwenden, um zu bestimmen, wer Client-App-Informationen in Intune anzeigen kann. Ausführliche Informationen zu Bereichsmarkierungen finden Sie unter [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md) (Verwenden der rollenbasierten Zugriffssteuerung und von Bereichsmarkierungen für verteilte IT).

1. Klicken Sie auf **Bereichstags auswählen**, um optional Bereichsmarkierungen für die App-Suite hinzuzufügen.
2. Klicken Sie auf **Weiter**, um die Seite **Zuweisungen** anzuzeigen.

## <a name="step-4---assignments"></a>Schritt 4: Zuweisungen

1. Wählen Sie die Gruppenzuweisungen **Erforderlich**, **Für registrierte Geräte verfügbar** oder **Deinstallieren** für die App-Suite aus. Weitere Informationen finden Sie unter [Hinzufügen von Gruppen zum Organisieren von Benutzern und Geräten](../fundamentals/groups-add.md) und [Zuweisen von Apps zu Gruppen mit Microsoft Intune](apps-deploy.md).
2. Klicken Sie auf **Weiter**, um die Seite **Überprüfen + erstellen** anzuzeigen.

## <a name="step-5---review--create"></a>Schritt 5: Überprüfen und Erstellen

1. Überprüfen Sie die Werte und Einstellungen, die Sie für die App-Suite eingegeben haben.
2. Klicken Sie abschließend auf **Erstellen**, um Intune die App hinzuzufügen.

    Das Blatt **Übersicht** wird angezeigt.

## <a name="deployment-details"></a>Bereitstellungsdetails

Nachdem die Bereitstellungsrichtlinie von Intune über [Office-Konfigurationsdienstanbieter (CSP)](https://docs.microsoft.com/windows/client-management/mdm/office-csp) den Zielcomputern zugewiesen wurde, lädt das Endgerät automatisch das Installationspaket aus dem Speicherort *officecdn.microsoft.com* herunter. Im Verzeichnis *Programme* werden zwei Verzeichnisse angezeigt:

![Office-Installationspakete im Verzeichnis „Programme“](./media/apps-add-office365/office-folder.png)

Im Verzeichnis *Microsoft Office* wird ein neuer Ordner erstellt, in dem die Installationsdateien gespeichert werden:

![Neu erstellter Ordner im Microsoft Office-Verzeichnis](./media/apps-add-office365/created-folder.png)

Im Verzeichnis *Microsoft Office 15* werden die Office-Klick-und-Los-Installationsstartdateien gespeichert. Die Installation wird automatisch gestartet, wenn der Zuweisungstyp erforderlich ist:

![Klicken, um Installationsstartdateien auszuführen](./media/apps-add-office365/clicktorun-files.png)

Die Installation wird im unbeaufsichtigten Modus ausgeführt, wenn die Zuweisung der O365 Suite entsprechend konfiguriert ist. Die heruntergeladenen Installationsdateien werden gelöscht, nachdem die Installation erfolgreich abgeschlossen wurde. Wenn die Zuweisung als **Verfügbar** konfiguriert ist, werden die Office-Anwendungen in der Unternehmensportal-App angezeigt, damit Endbenutzer die Installation manuell initiieren können.

## <a name="troubleshooting"></a>Problembehandlung
Intune verwendet das [Office-Bereitstellungstool](https://docs.microsoft.com/DeployOffice/overview-of-the-office-2016-deployment-tool) zum Herunterladen und Bereitstellen von Office 365 ProPlus auf Ihren Clientcomputern über das [Office 365-CDN](https://docs.microsoft.com/office365/enterprise/content-delivery-networks). Sehen Sie sich die Best Practices in [Verwalten von Office 365-Endpunkten](https://docs.microsoft.com/office365/enterprise/managing-office-365-endpoints) an, um sicherzustellen, dass Ihre Netzwerkkonfiguration Clients den Zugriff auf das CDN erlaubt, anstatt den CDN-Datenverkehr über zentrale Proxys weiterzuleiten, um unnötige Latenzen zu vermeiden.

Führen Sie den [Microsoft Support- und Wiederherstellungs-Assistenten für Office 365](https://diagnostics.office.com) auf einem Zielgerät aus, falls Installations- oder Laufzeitprobleme auftreten.

### <a name="additional-troubleshooting-details"></a>Zusätzliche Informationen zur Fehlerbehebung

Wenn Sie O365-Apps nicht auf einem Gerät installieren können, müssen Sie herausfinden, ob das Problem im Zusammenhang mit Intune oder dem Betriebssystem/Office steht. Wenn die beiden Ordner *Microsoft Office* und *Microsoft Office 15* im Verzeichnis *Programme* des Geräts angezeigt werden, können Sie überprüfen, ob die Bereitstellung erfolgreich von Intune initiiert wurde. Wenn diese beiden Ordner nicht im Verzeichnis *Programme* angezeigt werden, sollten Sie Folgendes überprüfen:

- Das Gerät ist ordnungsgemäß bei Microsoft Intune registriert. 
- Auf dem Gerät ist eine aktive Netzwerkverbindung vorhanden. Wenn sich das Gerät im Flugmodus befindet, ausgeschaltet ist oder sich an einem Ort ohne Empfang befindet, wird die Richtlinie erst angewendet, wenn die Netzwerkverbindung hergestellt wurde.
- Sowohl Intune- als auch Office 365-Netzwerkanforderungen sind erfüllt und die zugehörigen IP-Adressbereiche sind wie in den folgenden Artikeln beschrieben zugänglich:

  - [Bandbreiten- und andere Anforderungen an die Netzwerkkonfiguration für Intune](https://docs.microsoft.com/intune/network-bandwidth-use)
  - [URLs und IP-Adressbereiche für Office 365](https://docs.microsoft.com/office365/enterprise/urls-and-ip-address-ranges)

- Der O365-App Suite wurden die richtigen Gruppen zugewiesen. 

Überprüfen Sie zusätzlich die Größe des Verzeichnisses *C:\Programme\Microsoft Office\Updates\Download*. Das aus der Intune-Cloud heruntergeladene Installationspaket wird an diesem Speicherort gespeichert. Wenn die Größe gar nicht oder nur langsam zunimmt, wird empfohlen, die Netzwerkkonnektivität und Bandbreite zu überprüfen.

Sobald Sie sicher sein können, dass sowohl Intune als auch die Netzwerkinfrastruktur erwartungsgemäß funktionieren, sollten Sie das Problem im Hinblick auf das Betriebssystem genauer analysieren. Überprüfen Sie die folgenden Bedingungen:

- Das Zielgerät muss unter Windows 10 Creators Update oder höher ausgeführt werden.
- Wenn Intune die Anwendungen bereitstellt, sind keine vorhandenen Office-Apps geöffnet.
- Vorhandene MSI-Versionen von Office wurden ordnungsgemäß vom Gerät entfernt. Intune verwendet Office-Klick-und-Los, das nicht mit der Office-MSI kompatibel ist. Dieses Verhalten wird weiter unten in diesem Dokument erwähnt:<br>
  [Die Installation von Office mit Klick-und-Los und Windows Installer auf dem gleichen Computer wird nicht unterstützt.](https://support.office.com/article/office-installed-with-click-to-run-and-windows-installer-on-same-computer-isn-t-supported-30775ef4-fa77-4f47-98fb-c5826a6926cd)
- Der Anmeldebenutzer muss über die Berechtigung zum Installieren von Anwendungen auf dem Gerät verfügen.
- Vergewissern Sie sich, dass keine Probleme im Zusammenhang mit dem Protokoll der Windows-Ereignisanzeige vorliegen (**Windows-Protokolle** -> **Anwendungen**).
- Erfassen Sie während der Installation ausführliche Protokolle der Office-Installation. Gehen Sie hierzu folgendermaßen vor:<br>
    1. Aktivieren Sie die ausführliche Protokollierung für Office-Installationen auf den Zielcomputern. Führen Sie hierzu den folgenden Befehl aus, um die Registrierung zu ändern:<br>
        `reg add HKLM\SOFTWARE\Microsoft\ClickToRun\OverRide /v LogLevel /t REG_DWORD /d 3`<br>
    2. Stellen Sie die Microsoft 365-Apps erneut für die Zielgeräte bereit.<br>
    3. Warten Sie ungefähr 15 bis 20 Minuten, und navigieren Sie dann zu den Ordnern **%temp%** und **%windir%\temp**, sortieren Sie nach **Änderungsdatum**, und wählen Sie die Dateien *{Machine Name}-{TimeStamp}.log* aus, die gemäß Ihrer Reproduktionszeit geändert werden.<br>
    4. Führen Sie den folgenden Befehl aus, um das ausführliche Protokoll zu deaktivieren:<br>
        `reg delete HKLM\SOFTWARE\Microsoft\ClickToRun\OverRide /v LogLevel /f`<br>
        Die ausführlichen Protokolle bieten weitere Informationen zum Installationsvorgang.

## <a name="errors-during-installation-of-the-app-suite"></a>Fehler während der Installation der App-Suite

Informationen zum Anzeigen ausführlicher Installationsprotokolle finden Sie im Blogbeitrag [How to enable Microsoft 365 Apps ULS logging](/office/troubleshoot/diagnostic-logs/how-to-enable-office-365-proplus-uls-logging) (Aktivieren der ULS-Protokollierung von Microsoft 365-Apps).

In den nachstehenden Tabellen sind die häufigsten Fehlercodes aufgeführt, die auftreten können, sowie deren Bedeutung.

### <a name="status-for-office-csp"></a>Status für Office CSP

| Status | Phase | Beschreibung |
|--------------------------------------------------|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1460 (ERROR_TIMEOUT) | Herunterladen | Das Office-Bereitstellungstool konnte nicht heruntergeladen werden |
| 13 (ERROR_INVALID_DATA) | - | Die Signatur des heruntergeladenen Office-Bereitstellungstools konnte nicht überprüft werden. |
| Fehlercode aus CertVerifyCertificateChainPolicy | - | Fehlgeschlagene Zertifizierungsprüfung für das heruntergeladene Office-Bereitstellungstool. |
| 997 | WIP | Installation |
| 0 | Nach der Installation | Die Installation war erfolgreich |
| 1603 (ERROR_INSTALL_FAILURE) | - | Fehler bei Voraussetzungsprüfungen, z.B.:SxS (beim Installationsversuch war 2016 MSI installiert)Nicht übereinstimmende VersionSonstiges |
| 0x8000ffff (E_UNEXPECTED) | - | Beim Versuch, eine Deinstallation durchzuführen, war keine Klick-und-Los-Version von Office auf dem Computer vorhanden. |
| 17002 | - | Das Szenario (Installation) konnte nicht abgeschlossen werden. Mögliche Gründe:Installation durch Benutzer abgebrochen Installation durch andere Installation abgebrochen Fehlender Speicherplatz auf dem Datenträger während der Installation Unbekannte Sprach-ID |
| 17004 | - | Unbekannte SKUs |


### <a name="office-deployment-tool-error-codes"></a>Fehlercodes der Office-Bereitstellungstools

| Szenario | Rückgabecode | Benutzeroberfläche | Hinweis |
|------------------------------------------------------------------------------------------------------------------|---------------------------------------|----------------------------------------------------|------------------------------------|
| Deinstallationsaufwand, wenn keine aktive Klick-und-Los-Installation vorhanden ist | – 2147418113, 0x8000ffff oder 2147549183 | Fehlercode: 30088-1008Fehlercode: 30125-1011 (404) | Office-Bereitstellungstool |
| Installieren, wenn eine MSI-Version installiert wird | 1603 | - | Office-Bereitstellungstool |
| Die Installation wurde vom Benutzer oder einer anderen Installation abgebrochen | 17002 | - | Klick-und-Los |
| Versuch, eine 64-Bit-Version auf einem Gerät mit installierter 32-Bit-Version zu installieren | 1603 | - | Rückgabecode der Office-Bereitstellungstools |
| Versuch, eine unbekannte SKU zu installieren (kein zulässiger Anwendungsfall für Office CSP, da nur gültige SKUs übergeben werden sollen) | 17004 | - | Klick-und-Los |
| Nicht genügend Speicherplatz | 17002 | - | Klick-und-Los |
| Der Klick-und-Los-Client konnte nicht gestartet werden (unerwartet) | 17000 | - | Klick-und-Los |
| Der Klick-und-Los-Client konnte das Szenario nicht in die Warteschlange einreihen (unerwartet) | 17001 | - | Klick-und-Los |

## <a name="next-steps"></a>Nächste Schritte

- Informationen zum Zuweisen der App-Suite zu weiteren Gruppen finden Sie unter [Zuweisen von Apps zu Gruppen](/mem/intune/apps/apps-deploy).
