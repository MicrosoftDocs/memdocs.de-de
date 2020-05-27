---
title: Windows Information Protection-App-Schutzrichtlinien (WIP)
titleSuffix: Microsoft Intune
description: Erstellen und Bereitstellen von WIP-Richtlinien (Windows Information Protection) in Microsoft Intune
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/25/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 4e3627bd-a9fd-49bc-b95e-9b7532f0ed55
ms.reviewer: joglocke
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 66ea84d8defa1d1d5b79f686537b391452cf3c30
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990283"
---
# <a name="create-and-deploy-windows-information-protection-wip-policy-with-intune"></a>Erstellen und Bereitstellen von WIP-Richtlinien (Windows Information Protection) in Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Sie können WIP-Richtlinien (Windows Information Protection) bei Windows 10-Apps verwenden, um Apps ohne Geräteregistrierung zu schützen.

## <a name="before-you-begin"></a>Vorbereitung

Sie müssen mit einigen Konzepten vertraut sein, wenn Sie eine WIP-Richtlinie hinzufügen:

### <a name="list-of-allowed-and-exempt-apps"></a>Liste der zulässigen und ausgenommenen Apps

- **Geschützte Apps:** Diese Apps müssen die Richtlinie einhalten.

- **Ausgenommene Apps:** Diese Apps sind von dieser Richtlinie ausgenommen und können ohne Einschränkungen auf Unternehmensdaten zugreifen.

### <a name="types-of-apps"></a>App-Typen

- **Empfohlene Apps:** Eine vorab aufgefüllte Liste von Apps (hauptsächlich Microsoft Office), die Ihnen einen einfachen Import in die Richtlinie ermöglicht.
- **Store-Apps:** Sie können der Richtlinie eine beliebige App aus dem Windows Store hinzufügen.
- **Windows Desktop-Apps:** Sie können der Richtlinie traditionelle Windows Desktop-Apps hinzufügen (z. B. .exe, .dll usw.)

## <a name="prerequisites"></a>Voraussetzungen

Sie müssen den MAM-Anbieter konfigurieren, bevor Sie eine WIP-Richtlinie erstellen können. Weitere Informationen finden Sie unter [Konfigurieren Ihres MAM-Anbieters in Intune](app-protection-policies-configure-windows-10.md).  

> [!IMPORTANT]
> WIP unterstützt nicht mehrere Identitäten; nur jeweils eine verwaltete Identität darf vorhanden sein. Weitere Informationen zu den Möglichkeiten und Grenzen von WIP finden Sie unter [Schützen Ihrer Unternehmensdaten mit Windows Information Protection (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip).

Darüber hinaus benötigen Sie folgende Lizenz und folgendes Update:

- [Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium)-Lizenz
- [Windows Creators Update](https://blogs.windows.com/windowsexperience/2017/04/11/how-to-get-the-windows-10-creators-update/#o61bC2PdrHslHG5J.97)





## <a name="to-add-a-wip-policy"></a>Hinzufügen einer WIP-Richtlinie

Nachdem Sie Intune in Ihrer Organisation eingerichtet haben, können Sie eine WIP-spezifische Richtlinie erstellen.

> [!TIP]  
> Weitere Informationen zum Erstellen von WIP-Richtlinien für Intune, einschließlich der verfügbaren Einstellungen und deren Konfiguration, finden Sie in der Bibliothek mit der Dokumentation zur Windows-Sicherheit unter [Erstellen einer Windows Information Protection-Richtlinie (WIP) mit MAM mithilfe des Azure-Portals für Microsoft Intune](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-mam-intune-azure). 


1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Apps** > **App-Schutzrichtlinien** > **Richtlinie erstellen** aus.
3. Fügen Sie die folgenden Werte hinzu:
    - **Name:** Geben Sie einen Namen für Ihre neue Richtlinie ein (erforderlich).
    - **Beschreibung:** Geben Sie eine Beschreibung ein (optional).
    - **Plattform:** Wählen Sie **Windows 10** als unterstützte Plattform für Ihre WIP-Richtlinie aus.
    - **Registrierungsstatus:** Wählen Sie **Ohne Registrierung** als Registrierungsstatus für Ihre Richtlinie aus.
4. Wählen Sie **Erstellen** aus. Die Richtlinie wird erstellt und in der Tabelle im Bereich **App-Schutzrichtlinien** angezeigt.

## <a name="to-add-recommended-apps-to-your-protected-apps-list"></a>Hinzufügen von empfohlenen Apps zur Liste der geschützten Apps

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Apps** > **App-Schutzrichtlinien** aus.
3. Wählen Sie im Bereich **App-Schutzrichtlinien** die Richtlinie aus, die Sie ändern möchten. Der Bereich **Intune-App-Schutz** wird angezeigt.
4. Wählen Sie im Bereich **Intune-App-Schutz** die Option **Geschützte Apps** aus. Der Bereich **Geschützte Apps** wird geöffnet und zeigt alle Apps an, die bereits in der Liste für diese App-Schutzrichtlinie enthalten sind.
5. Klicken Sie auf **Apps hinzufügen**. Die Informationen bei **Apps hinzufügen** zeigen eine gefilterte Liste von Apps. Mit der Liste oben im Bereich können Sie den Listenfilter ändern.
6. Wählen Sie alle Apps aus, denen Sie Zugriff auf Ihre Unternehmensdaten gewähren möchten.
7. Klicken Sie auf **OK**. Der Bereich **Geschützte Apps** wird aktualisiert und zeigt alle ausgewählten Apps an.
8. Klicken Sie auf **Speichern**.

## <a name="add-a-store-app-to-your-protected-apps-list"></a>Hinzufügen einer Store-App zur Liste der geschützten Apps

**Hinzufügen eine Store-App**

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Apps** > **App-Schutzrichtlinien** aus.
3. Wählen Sie im Bereich **App-Schutzrichtlinien** die Richtlinie aus, die Sie ändern möchten. Der Bereich **Intune-App-Schutz** wird angezeigt.
4. Wählen Sie im Bereich **Intune-App-Schutz** die Option **Geschützte Apps** aus. Der Bereich **Geschützte Apps** wird geöffnet und zeigt alle Apps an, die bereits in der Liste für diese App-Schutzrichtlinie enthalten sind.
5. Klicken Sie auf **Apps hinzufügen**. Die Informationen bei **Apps hinzufügen** zeigen eine gefilterte Liste von Apps. Mit der Liste oben im Bereich können Sie den Listenfilter ändern.
6. Wählen Sie **Store-Apps** aus der Liste aus.
7. Geben Sie Werte für **Name**, **Herausgeber**, **Produktname** und **Aktion** ein. Stellen Sie sicher, dass der Wert für **Aktion** auf **Zulassen** festgelegt ist, damit die App auf Ihre Unternehmensdaten zugreifen kann.
9. Klicken Sie auf **OK**. Der Bereich **Geschützte Apps** wird aktualisiert und zeigt alle ausgewählten Apps an.
10. Klicken Sie auf **Speichern**.

## <a name="add-a-desktop-app-to-your-protected-apps-list"></a>Hinzufügen einer Desktop-App zur Liste der geschützten Apps

**So fügen Sie eine Desktop-App hinzu**
1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Apps** > **App-Schutzrichtlinien** aus.
3. Wählen Sie im Bereich **App-Schutzrichtlinien** die Richtlinie aus, die Sie ändern möchten. Der Bereich **Intune-App-Schutz** wird angezeigt.
4. Wählen Sie im Bereich **Intune-App-Schutz** die Option **Geschützte Apps** aus. Der Bereich **Geschützte Apps** wird geöffnet und zeigt alle Apps an, die bereits in der Liste für diese App-Schutzrichtlinie enthalten sind.
5. Klicken Sie auf **Apps hinzufügen**. Die Informationen bei **Apps hinzufügen** zeigen eine gefilterte Liste von Apps. Mit der Liste oben im Bereich können Sie den Listenfilter ändern.
6. Wählen Sie **Desktop-Apps** aus der Liste aus.
7. Geben Sie Werte für **Name**, **Herausgeber**, **Produktname**, **Datei**, **Mindestversion**, **Maximale Version** und **Aktion** ein. Stellen Sie sicher, dass der Wert für **Aktion** auf **Zulassen** festgelegt ist, damit die App auf Ihre Unternehmensdaten zugreifen kann.
9. Klicken Sie auf **OK**. Der Bereich **Geschützte Apps** wird aktualisiert und zeigt alle ausgewählten Apps an.
10. Klicken Sie auf **Speichern**.

## <a name="wip-learning"></a>WIP Learning
Nachdem Sie die Apps hinzugefügt haben, die durch WIP geschützt werden sollen, müssen Sie mittels **WIP Learning** einen Schutzmodus anwenden.

### <a name="before-you-begin"></a>Vorbereitung

WIP Learning ist ein Bericht, mit dem Sie Ihre WIP-tauglichen und WIP-unbekannten Apps überwachen können. Unbekannte Apps sind Apps, die nicht von der IT-Abteilung Ihrer Organisation bereitgestellt wurden. Sie können diese Apps vor der Erzwingung von WIP im Modus „Blockieren“ über den Bericht exportieren und zu Ihren WIP-Richtlinien hinzufügen, um Produktivitätseinbußen zu verhindern.

<!-- 1631908 -->
Neben der Anzeige von Informationen über WIP-fähige Apps können Sie eine Zusammenfassung der Geräte anzeigen, die Arbeitsdaten für Websites freigegeben haben. Anhand dieser Informationen können Sie festlegen, welche Websites zu WIP-Gruppen- und Benutzerrichtlinien hinzugefügt werden sollen. Die Zusammenfassung zeigt, auf welche Website-URLs von WIP-aktivierten Apps zugegriffen werden kann.

Beim Arbeiten mit WIP-tauglichen und WIP-unbekannten Apps sollten Sie mit **Automatisch** oder **Außerkraftsetzungen zulassen** beginnen und bei einer kleinen Gruppe überprüfen, ob die Liste der geschützten Apps die richtigen Apps enthält. Wenn Sie fertig sind, können Sie Ihre endgültige Erzwingungsrichtlinie in **Blockieren** ändern.

### <a name="what-are-the-protection-modes"></a>Was sind Schutzmodi?

#### <a name="block"></a>Blockieren
WIP prüft auf ungeeignete Datenfreigabeverfahren und hindert den Benutzer an der Durchführung der Aktion. Blockierte Aktionen können die Freigabe von Informationen über nicht geschützte Unternehmens-Apps hinweg sowie die Freigabe von Unternehmensdaten zwischen anderen Personen und Geräten außerhalb Ihrer Organisation einschließen.

#### <a name="allow-overrides"></a>Außerkraftsetzungen zulassen
WIP prüft auf ungeeignete Datenfreigabeverfahren, bei dem Benutzer gewarnt werden, wenn sie einen potenziell unsicheren Vorgang durchführen. In diesem Modus können Benutzer jedoch die Richtlinie überschreiben und die Daten freigeben. Die Aktion wird dabei in Ihrem Überwachungsprotokoll protokolliert.

#### <a name="silent"></a>Automatisch
WIP wird automatisch ausgeführt, wobei ungeeignete Datenfreigabeverfahren protokolliert werden. Dabei werden im Modus „Außerkraftsetzungen zulassen“ keine Vorgänge blockiert, die zu einer Mitarbeiterinteraktion auffordern würden. Unzulässige Aktionen wie bei Apps, die unzulässigerweise versuchen, auf eine Netzwerkressource oder auf WIP-geschützte Daten zuzugreifen, werden trotzdem angehalten.

#### <a name="off-not-recommended"></a>Inaktiv (nicht empfohlen)
WIP ist deaktiviert und unterstützt nicht beim Schutz oder der Überwachung Ihrer Daten.

Nachdem Sie WIP deaktiviert haben, wird versucht, WIP-getaggte Dateien auf den lokalen Laufwerken zu entschlüsseln. Denken Sie daran, dass Ihre vorherigen Informationen zu Entschlüsselungen und Richtlinien nicht automatisch erneut angewendet werden, wenn Sie den WIP-Schutz wieder aktivieren.

### <a name="add-a-protection-mode"></a>Hinzufügen eines Schutzmodus

1. Wählen Sie im Bereich **App-Richtlinie** den Namen Ihrer Richtlinie und anschließend die Option **Erforderliche Einstellungen** aus.

    ![Screenshot des Bereichs „Trainingsmodus“](./media/windows-information-protection-policy-create/learning-mode-sc1.png)

1. Wählen Sie eine Einstellung aus, und klicken Sie auf **Speichern**.

### <a name="use-wip-learning"></a>Verwenden von WIP Learning

1. Öffnen Sie das [Azure-Portal](https://portal.azure.com). Wählen Sie **Alle Dienste** aus. Geben Sie **Intune** in das Filtertextfeld ein.

3. Wählen Sie **Intune** > **Apps** aus.

4. Klicken Sie anschließend auf **Status des App-Schutzes** > **Berichte** > **Windows Information Protection-Tutorial**.  

    Wenn dann die Apps im WIP Learning-Protokollierungsbericht angezeigt werden, können Sie sie zu Ihren App-Schutzrichtlinien hinzufügen.

## <a name="allow-windows-search-indexer-to-search-encrypted-items"></a>Der Windows Search-Indexerstellung die Suche nach verschlüsselten Elementen gestatten
Hiermit wird die Indizierung von Elementen zugelassen oder verweigert. Diese Option ist für die Windows Search-Indexerstellung bestimmt und steuert, ob verschlüsselte Elemente wie beispielsweise WIP-geschützte Dateien (Windows Information Protection) indiziert werden.

Diese App-Schutzrichtlinienoption befindet sich in den **erweiterten Einstellungen** der WIP-Richtlinie (Windows Information Protection). Für die App-Schutzrichtlinie muss die *Windows 10*-Plattform und für die App-Richtlinie **Registrierungsstatus** muss **Mit Registrierung** festgelegt werden.

Wenn die Richtlinie aktiviert ist, werden WIP-geschützte Elemente indiziert und die zugehörigen Metadaten werden an einem nicht verschlüsselten Speicherort gespeichert. Die Metadaten umfassen beispielsweise den Dateipfad und das Änderungsdatum.

Wenn die Richtlinie deaktiviert ist, werden WIP-geschützte Elemente nicht indiziert und sie werden nicht in den Ergebnissen in Cortana oder im Datei-Explorer angezeigt. Ferner sind bei Fotos und Groove-Apps Leistungseinbußen möglich, wenn sich auf dem Gerät große Mengen an WIP-geschützten Mediendateien befinden.

## <a name="add-encrypted-file-extensions"></a>Hinzufügen von verschlüsselten Dateierweiterungen

Sie können nicht nur die Option **Der Windows Search-Indexerstellung die Suche nach verschlüsselten Elementen gestatten** festlegen, sondern auch eine Liste mit Dateierweiterungen angeben. Dateien mit diesen Erweiterungen werden beim Kopieren aus einer SMB-Freigabe innerhalb der Unternehmensgrenzen (gemäß Definition in der Liste mit Netzwerkstandorten) verschlüsselt. Wenn diese Richtlinie nicht festgelegt ist, wird das vorhandene Verhalten zur automatischen Verschlüsselung angewendet. Wenn diese Richtlinie konfiguriert ist, werden nur Dateien mit den in der Liste enthaltenen Erweiterungen verschlüsselt.

## <a name="deploy-your-wip-app-protection-policy"></a>Bereitstellen der WIP-App-Schutzrichtlinie

> [!IMPORTANT]
> Diese Informationen gelten für WIP ohne Geräteregistrierung.

<!---not sure why you need the Important note. Isn't this what the topic is about? app protection w/o enrollment?--->

Nachdem Sie Ihre WIP-App-Schutzrichtlinie erstellt haben, müssen Sie sie Ihrer Organisation über MAM bereitstellen.

1. Wählen Sie im Bereich **App-Richtlinie** die neu erstellte App-Schutzrichtlinie aus. Wählen Sie anschließend **Benutzergruppen** > **Benutzergruppe hinzufügen** aus.

    Im Bereich **Benutzergruppe hinzufügen** wird eine Liste von Benutzergruppen geöffnet, die aus allen Sicherheitsgruppen in Azure Active Directory besteht.

2. Wählen Sie die Gruppe aus, auf die Ihre Richtlinie angewendet werden soll, und klicken Sie dann auf **Auswählen**, um die Richtlinie bereitzustellen.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu Windows Information Protection finden Sie unter [Protect your enterprise data using Windows Information Protection (WIP) (Schützen Ihrer Unternehmensdaten mit Windows Information Protection (WIP))](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip).
