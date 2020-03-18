---
title: Überwachen, Exportieren und Löschen von personenbezogenen Daten
titleSuffix: Microsoft Intune
description: Erfahren Sie mehr über das Überwachen, Exportieren und Löschen von personenbezogenen Daten.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 96990be0-eb1e-43a4-a0e4-09c7dbdc2bf4
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: db3146bbaae3362e97c8c076823b58dbcd57c4af
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79339071"
---
# <a name="audit-export-or-delete-personal-data-in-intune"></a>Überwachen, Exportieren und Löschen von personenbezogenen Daten in Intune

Intune-Administratoren können Überwachungsprotokolle verwenden, um Aktivitäten in Zusammenhang mit personenbezogenen Daten nachzuverfolgen. Administratoren können personenbezogene Daten darüber hinaus exportieren und löschen.

[!INCLUDE [GDPR-related guidance](../includes/gdpr-intro-sentence.md)]

## <a name="audit-personal-data"></a>Überwachen von personenbezogenen Daten

Überwachungsprotokolle stellen Mandantenadministratoren einen Datensatz von Aktivitäten zur Verfügung, die eine Änderung in Microsoft Intune bewirken. Überwachungsprotokoll sind für viele Verwaltungsaktivitäten verfügbar und erstellen, aktualisieren (bearbeiten), löschen und weisen Aktionen zu. Remotetasks, die Überwachungsereignisse generieren, können ebenfalls überprüft werden. Diese Überwachungsprotokolle können personenbezogene Daten von Benutzern enthalten, deren Geräte in Intune registriert sind.  

Aus Sicherheitsgründen kann Intune Überwachungsprotokolle für Benutzer- und Geräteaktionen für ein Jahr aufbewahren. Diese Protokolle werden nach der Aufbewahrungsdauer von einem Jahr automatisch gelöscht.

Wenn Sie die Überwachungsprotokolle überprüfen möchten, finden Sie weitere Informationen unter [Überwachungsprotokolle für Intune-Aktivitäten](../fundamentals/monitor-audit-logs.md). 

Überwachungsprotokolle können von Administratoren nicht gelöscht werden.

Diese Überwachungsereignisse werden für ein Jahr aufbewahrt. Mandantenadministratoren können Überwachungsprotokoll mithilfe [dieses Formulars für Supportanfragen](https://privacy.microsoft.com/en-US/privacy-questions?) anfordern.

## <a name="export-personal-data"></a>Exportieren von personenbezogenen Daten

Administratoren können die personenbezogenen Daten von Endbenutzern exportieren, einschließlich Konten, Dienstdaten und zugeordneten Protokollen, um DSR-Anforderungen (Data Subject Rights) zu erfüllen. Es liegt an Ihnen und Ihrer Organisation, zu entscheiden, ob Sie dem Datensubjekt eine Kopie der personenbezogenen Daten bereitstellen oder ob eine legitime geschäftliche Veranlassung vorliegt, die Daten einzubehalten. Wenn Sie die Daten bereitstellen, können Sie dies durch eine Kopie des echten Dokuments, eine entsprechend bearbeitete Version oder einen Screenshot der Teile, die freigegeben werden können, tun.

Sie können Folgendes verwenden, um die personenbezogenen Daten eines Benutzers zu exportieren: 
- Das Intune-Blatt „MDM-Gerät“, um eine Liste der Geräte zu exportieren. Sie können die Gerätedaten auch direkt kopieren.
- Das Skript [Export-IntuneData.ps1](https://aka.ms/intunedataexport).

## <a name="delete-end-user-personal-data"></a>Löschen personenbezogener Daten von Endbenutzern

Es gibt drei Möglichkeiten, um personenbezogene Daten aus der Intune-Verwaltung zu entfernen:
- Löschen Sie den Benutzer aus Azure Active Directory.
- Setzen Sie das Gerät auf die Werkseinstellungen zurück.
- Der Benutzer löscht sich selbst.

### <a name="delete-a-user-from-intune"></a>Löschen eines Benutzers aus Intune

Ein Administrator muss [den Benutzer aus Azure Active Directory (AAD) löschen](https://docs.microsoft.com/azure/active-directory/fundamentals/add-users-azure-active-directory#delete-a-user), um die personenbezogenen Daten eines Endbenutzers aus Intune zu löschen. Wenn der Benutzer aus AAD gelöscht wird (dauerhaft), empfängt Intune den Löschbefehl von AAD und beginnt automatisch damit, alle personenbezogenen Daten des Benutzers aus dem Intune-Dienst zu löschen. Die Benutzerinformationen werden aus dem Intune-Dienst innerhalb von 30 Tagen nach dem Löschvorgang gelöscht.

### <a name="reset-device-to-factory-settings"></a>Zurücksetzen des Geräts auf die Werkseinstellung
Beim Zurücksetzen auf Werkseinstellungen werden alle geschäftlichen und personenbezogenen Daten und Einstellungen auf die Werkseinstellungen zurückgesetzt. Dies ist nützlich, um ein Gerät für den nächsten Mitarbeiter bereitzustellen. Benutzerdateien, von Benutzern installierte Anwendungen und vom Standard abweichende Einstellungen werden entfernt, und diese Daten werden innerhalb von 30 Tagen nach dem Löschvorgang aus dem Intune-Dienst gelöscht.

### <a name="user-self-removal-from-intune-management"></a>Selbstständige Entfernung des Benutzers aus der Intune-Verwaltung
Benutzer können ihre persönlichen [Android-, Apple- oder Windows-Geräte](https://docs.microsoft.com/user-help/unenroll-your-device-from-intune-android) aus der Intune-Verwaltung ohne Unterstützung durch den Administrator entfernen.   

### <a name="retire"></a>Außerkraftsetzen
Mit der Aktion **Abkoppeln** werden in Intune bereitgestellte Daten wie Unternehmensanwendungen, Daten zu von Intune verwalteten Apps, Richtlinieneinstellungen und E-Mail-Profile entfernt. Dabei bleiben die personenbezogenen Daten des Benutzers auf dem Gerät erhalten.

### <a name="delete-a-tenant-from-microsoft-intune"></a>Löschen eines Mandanten aus Microsoft Intune

Wenn ein Intune-Mandantenkunde sein Intune-Konto löscht, werden alle Mandantendaten innerhalb von 180 Tagen, nachdem der Benutzer sein Intune-Konto geschlossen hat, gelöscht. Wenn der AAD-Mandant anderen Microsoft-Unternehmensabonnements (Azure, Office 365) zugeordnet ist, werden nur die Intune-Kundendaten gelöscht. Die AAD-Mandantenressource wird für die Verwendung durch die anderen Abonnements beibehalten. Wenn es sich beim Intune-Konto um das einzige Abonnement handelt, das dem AAD-Mandanten zugeordnet ist, wird der Mandant gelöscht, und alle Ressourcen und Kundendaten werden ebenfalls gelöscht.

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie, wie Sie personenbezogene Daten in Intune [überwachen, exportieren oder löschen](privacy-data-audit-export-delete.md) können.
