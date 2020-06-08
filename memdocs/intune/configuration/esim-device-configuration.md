---
title: 'Aktivieren von eSIM-Datenverbindungen in Microsoft Intune: Azure | Microsoft-Dokumentation'
description: Sie können eSIM hinzufügen oder verwenden, um mithilfe verschiedener Datentarife Internet- und Datenzugriff zu erhalten. Fügen Sie in Intune Aktivierungscodes hinzu oder importieren Sie diese, und weisen Sie diese Aktivierungscodes anschließend über ein Konfigurationsprofil zu. Sie können auch die eSIM-Profile überwachen und den Status der eSIM-fähigen Geräte überprüfen.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/26/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ericor
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 17c0c83452f7b67ad2fef660e8f0c81bc6d4b78f
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989151"
---
# <a name="configure-esim-cellular-profiles-in-intune-public-preview"></a>Konfigurieren von eSIM-Mobilfunkprofilen in Intune (öffentliche Vorschau)

eSIM ist ein eingebetteter SIM-Chip, mit dem Sie auf einem eSIM-fähigen Gerät, wie z.B. dem [Surface LTE Pro](https://www.microsoft.com/surface/business/surface-pro), über Mobilfunk eine Verbindung mit dem Internet herstellen können. Mit einer eSIM müssen Sie keine SIM-Karte von Ihrem Mobilfunkanbieter erhalten. Wenn Sie viel reisen, können Sie zwischen den Mobilfunkanbietern und Datentarifen wechseln, um stets verbunden zu sein.

Sie haben beispielsweise einen Mobilfunktarif für Ihre Arbeit und einen Datentarif bei einem anderen Mobilfunkanbieter für den persönlichen Gebrauch. Bei Reisen erhalten Sie Zugang zum Internet, indem nach Mobilfunkanbietern mit Datentarifen in diesem Gebiet gesucht wird.

Diese Funktion gilt für:

- Windows 10 und höher

In Intune können Sie einmalige Aktivierungscodes importieren, die von Ihrem Mobilfunkanbieter bereitgestellt werden. Für die Konfiguration von Mobilfunktarifen auf dem eSIM-Modul müssen Sie diese Aktivierungscodes auf Ihren eSIM-fähigen Geräten bereitstellen. Wenn Intune den Aktivierungscode installiert, nimmt das eSIM-Hardwaremodul mithilfe der Daten im Aktivierungscode Kontakt zum Mobilfunkanbieter auf. Nach Abschluss dieses Vorgangs wird das eSIM-Profil auf dem Gerät heruntergeladen und für die Aktivierung der Mobilfunkverbindung konfiguriert.

Für die Bereitstellung von eSIM auf Ihren Geräten mithilfe von Intune ist Folgendes erforderlich:

- **eSIM-fähige Geräte**, z.B. das Surface LTE: Überprüfen Sie, [ob Ihr Gerät eSIM unterstützt](https://support.microsoft.com/help/4020763/windows-10-use-esim-for-cellular-data). Alternativ können Sie eine Liste [einiger der bekannten eSIM-fähigen Geräte](#esim-capable-devices) anzeigen (in diesem Artikel).
- **PC mit Windows 10 Fall Creators Update** (ab 1709), der registriert ist und von Intune MDM-verwaltet wird
- Von Ihrem Mobilfunkanbieter bereitgestellte **Aktivierungscodes**. Diese einmaligen Aktivierungscodes werden zu Intune hinzugefügt und auf Ihren eSIM-fähigen Geräten bereitgestellt. eSIM-Aktivierungscodes können Sie bei Ihrem Mobilfunkanbieter erwerben.

## <a name="deploy-esim-to-devices---overview"></a>Übersicht: Bereitstellen von eSIM auf Geräten

Ein Administrator muss zur Bereitstellung von eSIM auf Geräten die folgenden Schritte ausführen:

1. Importieren der von Ihrem Mobilfunkanbieter bereitgestellten Aktivierungscodes
2. Erstellen einer Azure Active Directory-Gerätegruppe (Azure AD), die Ihre eSIM-fähigen Geräte enthält
3. Zuweisen der Azure AD-Gruppe zu Ihrem importierten Abonnementpool
4. Überwachen der Bereitstellung

In diesem Artikel finden Sie eine Anleitung zur Ausführung dieser Schritte.

## <a name="esim-capable-devices"></a>eSIM-fähige Geräte

Wenn Sie sich nicht sicher sind, ob Ihre Geräte eSIM unterstützen, wenden Sie sich an den Gerätehersteller. Auf Windows-Geräten können Sie die Unterstützbarkeit von eSIM bestätigen. Weitere Informationen finden Sie unter [Verwenden von eSIM zum Abrufen einer Mobilfunk-Datenverbindung auf Ihrem Windows 10-PC](https://support.microsoft.com/help/4020763/windows-10-use-esim-for-cellular-data).

## <a name="step-1-add-cellular-activation-codes"></a>Schritt 1: Hinzufügen von Aktivierungscodes für Mobilfunkverbindungen

Aktivierungscodes für Mobilfunkverbindungen werden von Ihrem Mobilfunkanbieter in einer durch Trennzeichen getrennten Datei (CSV) bereitgestellt. Wenn Sie über diese Datei verfügen, fügen Sie diese zu Intune hinzu, indem Sie die folgenden Schritte ausführen:

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **eSIM-Mobilfunkprofile** > **Hinzufügen** aus.
3. Wählen Sie die CSV-Datei mit Ihren Aktivierungscodes aus.
4. Klicken Sie auf **OK**, um die Änderungen zu speichern.

### <a name="csv-file-requirements"></a>CSV-Dateianforderungen

Stellen Sie bei der Arbeit mit der CSV-Datei, welche die Aktivierungscodes enthält, sicher, dass Sie oder Ihr Mobilfunkanbieter folgende Anforderungen erfüllen:

- Die Datei muss das CSV-Format („Dateiname.csv“) aufweisen.
- Die Dateistruktur muss einem festen Format entsprechen. Andernfalls schlägt der Import fehl. Intune überprüft die Datei beim Import und schlägt fehl, wenn Fehler gefunden werden.
- Aktivierungscodes werden nur einmal verwendet. Von einem Import zuvor importierter Aktivierungscodes wird abgeraten, da dies bei der Bereitstellung auf demselben oder einem anderen Gerät möglicherweise Probleme verursacht.
- Jede Datei sollte für einen Mobilfunkanbieter spezifisch sein, und sämtliche Aktivierungscodes sollten für den gleichen Abrechnungsplan spezifisch sein. Intune verteilt die Aktivierungscodes nach dem Zufallsprinzip an die Zielgeräte. Es gibt keine Garantie dafür, welchem Gerät ein bestimmter Aktivierungscode zugeordnet wird.
- In einer CSV-Datei können maximal 1.000 Aktivierungscodes importiert werden.

### <a name="csv-file-example"></a>CSV-Beispieldatei

1. Die erste Zeile und Zelle der CSV-Datei enthält die URL des eSIM-Aktivierungsdiensts des Mobilfunkanbieters, der als SM-DP+ (Server des Abonnement-Managers für die Datenaufbereitung) bezeichnet wird. Bei der URL sollte es sich um einen vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) ohne Kommas handeln.
2. Die zweite und alle weiteren Zeilen enthalten eindeutige, einmalige Aktivierungscodes mit zwei Werten:

    1. Die erste Spalte enthält die ICCID (Bezeichner des SIM-Chips)
    2. Die zweite Spalte enthält die entsprechende ID, die nur durch ein Komma von der ICCID getrennt ist (kein Komma am Ende). Dieser Schritt wird im folgenden Beispiel dargestellt:

        :::image type="content" source="./media/esim-device-configuration/url-activation-code-examples.png" alt-text="CSV-Beispieldatei mit Aktivierungscodes des Mobilfunkanbieters.":::

3. Der Name der CSV-Datei wird im Endpoint Manager Admin Center als Name für den Abonnementpool der Mobilfunkverbindung verwendet. In der vorherigen Abbildung lautet der Dateiname `UnlimitedDataSkynet.csv`. Folglich gibt Intune dem Abonnementpool den Namen `UnlimitedDataSkynet.csv`:

    :::image type="content" source="./media/esim-device-configuration/subscription-pool-name-csv-file.png" alt-text="Der Abonnementpool der Mobilfunkverbindung wird nach dem Namen der CSV-Beispieldatei mit dem Aktivierungscode benannt.":::

## <a name="step-2-create-an-azure-ad-device-group"></a>Schritt 2: Erstellen einer Azure AD-Gerätegruppe

Erstellen Sie eine Gerätegruppe, welche die eSIM-fähigen Geräte enthält. Unter [Hinzufügen von Gruppen](../fundamentals/groups-add.md) werden die einzelnen Schritte aufgeführt.

> [!NOTE]
> - Es gibt nur Zielgeräte, keine Zielbenutzer.
> - Es wird empfohlen, eine statische Azure AD-Gerätegruppe zu erstellen, die Ihre eSIM-Geräte enthält. Durch die Verwendung einer Gruppe wird bestätigt, dass Sie nur über eSIM-Zielgeräte verfügen.

## <a name="step-3-assign-esim-activation-codes-to-devices"></a>Schritt 3: Zuweisen von eSIM Aktivierungscodes zu Geräten

Weisen Sie der Azure AD-Gruppe mit Ihren eSIM-Geräten das Profil zu.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **eSIM-Mobilfunkprofile** aus.
3. Wählen Sie in der Liste der Profile den Abonnementpool der eSIM-Mobilfunkverbindung aus, der zugewiesen werden soll. Wählen Sie anschließend **Zuweisungen** aus.
4. Wählen Sie aus, ob Sie Gruppen **einschließen** oder **ausschließen** möchten, und wählen Sie die Gruppen anschließend aus.

    :::image type="content" source="./media/esim-device-configuration/include-exclude-groups.png" alt-text="Einschließen der Gerätegruppen für die Zuweisung des Profils in Microsoft Intune.":::

5. Wenn Sie Ihre Gruppen auswählen, wählen Sie eine Azure AD-Gruppe aus. Drücken Sie für die Auswahl mehrerer Gruppen die **STRG**-Taste, und wählen Sie die Gruppen aus.
6. **Speichern** Sie anschließend Ihre Änderungen.

eSIM-Aktivierungscodes werden nur einmal verwendet. Nachdem Intune einen Aktivierungscode auf einem Gerät installiert hat, nimmt das eSIM-Modul Kontakt zum Mobilfunkanbieter auf, um das Mobilfunkprofil herunterzuladen. Mit diesem Kontakt ist die Registrierung des Geräts beim Netzwerk des Mobilfunkanbieters abgeschlossen.

## <a name="step-4-monitor-deployment"></a>Schritt 4: Überwachen der Bereitstellung

### <a name="review-the-deployment-status"></a>Überprüfen des Bereitstellungsstatus

Nachdem Sie das Profil zugewiesen haben, können Sie den Bereitstellungsstatus eines Abonnementspools überwachen.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **eSIM-Mobilfunkprofile** aus. Alle vorhandenen Abonnementpools für eSIM-Mobilfunkverbindungen werden aufgeführt.
3. Wählen Sie ein Abonnement aus, und überprüfen Sie den **Bereitstellungsstatus**.

### <a name="check-the-profile-status"></a>Überprüfen des Profilstatus

Nachdem Sie Ihr Geräteprofil erstellt haben, bietet Intune grafische Diagramme. Diese Diagramme zeigen den Status eines Profils an, etwa ob es erfolgreich Geräten zugewiesen wurde, oder ob das Profil einen Konflikt aufweist.

1. Wählen Sie **Geräte** > **eSIM-Mobilfunkprofile** und dann ein vorhandenes Abonnement aus.
2. Auf der Registerkarte **Übersicht** wird im oberen grafischen Diagramm die Anzahl der Geräte angezeigt, die der Bereitstellung des Abonnementpools für das bestimmte eSIM-Mobilfunknetz zugewiesen wurden.

    Es zeigt auch die Anzahl der Geräte anderer Plattformen an, die dem gleichen Geräteprofil zugewiesen sind.

    Intune zeigt den Bereitstellungs- und den Installationsstatus für den Aktivierungscode der Zielgeräte an.

    - **Gerät nicht synchronisiert:** Das Zielgerät hat seit der Erstellung der eSIM-Bereitstellungsrichtlinie keinen Kontakt zu Intune aufgenommen
    - **Aktivierung steht aus:** Ein vorübergehender Zustand, in dem Intune den Aktivierungscode auf dem Gerät installiert
    - **Aktiv:** Die Installation des Aktivierungscodes war erfolgreich
    - **Fehler bei der Aktivierung:** Die Installation des Aktivierungscodes ist fehlgeschlagen. Weitere Informationen finden Sie im Leitfaden zur Problembehandlung.

#### <a name="view-the-detailed-device-status"></a>Anzeigen des detaillierten Gerätestatus

Sie können eine detaillierte Liste der Geräte überwachen und anzeigen, die unter „Gerätestatus“ angezeigt werden.**

1. Wählen Sie **Geräte** > **eSIM-Mobilfunkprofile** und dann ein vorhandenes Abonnement aus.
2. Wählen Sie **Gerätestatus** aus. Intune zeigt weitere Details zu dem Gerät an:

    - **Gerätename:** Der Name des Zielgeräts
    - **Benutzer:** Der Benutzer des registrierten Geräts
    - **ICCID:** Ein eindeutiger Code, der vom Mobilfunkanbieter im Aktivierungscode des Geräts bereitgestellt wird
    - **Aktivierungsstatus:** Der Bereitstellungs- und Installationsstatus des Aktivierungscodes auf dem Gerät von Intune
    - **Mobilfunkstatus:** Der vom Mobilfunkanbieter bereitgestellte Status Befassen Sie sich zur Fehlerbehebung näher mit dem Mobilfunkanbieter.
    - **Letztes Einchecken:** Das Datum, an dem das Gerät zuletzt mit Intune kommuniziert hat

### <a name="monitor-esim-profile-details-on-the-actual-device"></a>Überwachen von eSIM-Profildetails auf dem aktuellen Gerät

1. Öffnen Sie auf Ihrem Gerät **Einstellungen** > wechseln Sie zu **Netzwerk und Internet**.
2. Wählen Sie **Mobilfunk** > **eSIM-Profile verwalten** aus.
3. Die eSIM-Profile werden aufgeführt:

    :::image type="content" source="./media/esim-device-configuration/device-settings-cellular-profiles.png" alt-text="Anzeigen der eSIM-Profile in Ihren Geräteeinstellungen.":::

## <a name="remove-the-esim-profile-from-device"></a>Entfernen des eSIM-Profils von dem Gerät

Wenn Sie das Gerät aus der Azure AD-Gruppe entfernen, wird das eSIM-Profil ebenfalls entfernt. Stellen Sie Folgendes sicher:

1. Vergewissern Sie sich, dass Sie die Azure AD-Gruppe der eSIM-Geräte verwenden.
2. Wechseln Sie zur Azure AD-Gruppe, und entfernen Sie das Gerät aus der Gruppe.
3. Wenn das entfernte Geräte Kontakt zu Intune aufnimmt, wird die aktualisierte Richtlinie ausgewertet und das eSIM-Profil entfernt.

Das eSIM-Profil wird auch entfernt, wenn der Benutzer das Gerät [außer Betrieb nimmt](../remote-actions/devices-wipe.md#retire) oder dessen Registrierung aufhebt, oder wenn der [Remotevorgang zum Zurücksetzen des Geräts](../remote-actions/devices-wipe.md#wipe) auf dem Gerät ausgeführt wird.

> [!NOTE]
> Durch das Entfernen des Profils wird die Abrechnung möglicherweise nicht beendet. Wenden Sie sich an Ihren Mobilfunkanbieter, um den Abrechnungsstatus für Ihr Gerät zu überprüfen.

## <a name="best-practices--troubleshooting"></a>Bewährte Methoden und Problembehandlung

- Achten Sie darauf, dass Ihre CSV-Datei ordnungsgemäß formatiert ist. Vergewissern Sie sich, dass die Datei weder doppelte Codes noch mehrere Mobilfunkanbieter oder unterschiedliche Datentarife enthält. Beachten Sie, dass jede Datei für einen Mobilfunkbetreiber und einen Datenverbindungstarif eindeutig sein muss.
- Erstellen Sie eine statische Azure AD-Gruppe, die nur die vorgesehenen eSIM-Geräte enthält.
- Überprüfen Sie Folgendes, wenn bei dem Bereitstellungsstatus ein Problem vorliegt:
  - **File format not proper** (Nicht unterstütztes Dateiformat): Weitere Informationen erhalten Sie unter **Schritt 1: Hinzufügen von Aktivierungscodes für Mobilfunkverbindungen** (in diesem Artikel), um in Erfahrung zu bringen, wie Sie Ihre Datei ordnungsgemäß formatieren.
  - **Cellular activation failure, contact mobile operator** (Die Aktivierung der Mobilfunkverbindung ist fehlgeschlagen, wenden Sie sich an den Mobilfunkanbieter): Möglicherweise ist der Aktivierungscode nicht im Netzwerk aktiviert. Alternativ können auch das Herunterladen des Profils und die Aktivierung der Mobilfunkverbindung fehlschlagen.

## <a name="next-steps"></a>Nächste Schritte

[Konfigurieren von Geräteprofilen](device-profiles.md)
