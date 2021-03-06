---
title: Installieren von Microsoft 365-Apps auf macOS-Geräten mit Microsoft Intune
titleSuffix: ''
description: Hier lernen Sie, wie Sie Microsoft Intune verwenden können, um Microsoft 365-Apps auf macOS-Geräten installieren zu können.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 2372332a-7e3a-4a9c-91a9-86654e0fabe2
ms.reviewer: aiwang
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2eb8ea29739e2478df68e3b9926f111f2ee8d0e4
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996485"
---
# <a name="assign-microsoft-365-to-macos-devices-with-microsoft-intune"></a>Zuweisen von Microsoft 365 zu macOS-Geräten mit Microsoft Intune

Dieser App-Typ macht es Ihnen einfach, Microsoft 365-Apps macOS-Geräten zuzuweisen. Dieser App-Typ ermöglicht Ihnen die Installation von Word, Excel, PowerPoint, Outlook, OneNote und Teams. Diese Apps sind auch im Lieferumfang von Microsoft AutoUpdate (MAU) enthalten, um die Apps sicherer und auf dem neuesten Stand zu halten. Die gewünschten Apps werden in der Intune-Konsole als einzelne App in der App-Liste angezeigt.

> [!NOTE]
> Microsoft Office 365 ProPlus wurde in **Microsoft 365 Apps for Enterprise** umbenannt. In unserer Dokumentation wird üblicherweise **Microsoft 365-Apps** verwendet.

## <a name="before-you-start"></a>Vorbereitung

Bevor Sie damit beginnen, macOS-Geräten Microsoft 365-Apps hinzuzufügen, sollten Sie sich Folgendes bewusst machen:

- Auf Geräten, für die Sie diese Apps bereitstellen, muss macOS 10.10 oder höher ausgeführt werden.
- Intune unterstützt nur das Hinzufügen von Office-Apps, die in der Office 2016 für Mac-Suite enthalten sind.
- Wenn Office-Apps geöffnet sind, wenn Intune die App-Suite installiert, verlieren Benutzer möglicherweise Daten aus nicht gespeicherten Dateien.

## <a name="select-microsoft-365-apps"></a>Auswählen von Microsoft 365-Apps

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Apps** > **Alle Apps** > **Hinzufügen** aus.
3. Wählen Sie **macOS** im Abschnitt **Microsoft 365-Apps** des Bereichs **App-Typ auswählen** aus.
4. 4. Klicken Sie auf **Auswählen**. Die Schritte für **Microsoft 365-Apps hinzufügen** werden angezeigt.

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
2. Klicken Sie auf **Weiter**, um die Seite **Bereichsmarkierungen** anzuzeigen.

## <a name="step-2---select-scope-tags-optional"></a>Schritt 2: Auswählen von Bereichsmarkierungen (optional)
Sie können Bereichsmarkierungen verwenden, um zu bestimmen, wer Client-App-Informationen in Intune anzeigen kann. Ausführliche Informationen zu Bereichsmarkierungen finden Sie unter [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md) (Verwenden der rollenbasierten Zugriffssteuerung und von Bereichsmarkierungen für verteilte IT).

1. Klicken Sie auf **Bereichstags auswählen**, um optional Bereichsmarkierungen für die App-Suite hinzuzufügen. 
2. Klicken Sie auf **Weiter**, um die Seite **Zuweisungen** anzuzeigen.

## <a name="step-3---assignments"></a>Schritt 3: Zuweisungen

1. Wählen Sie die Gruppenzuweisungen **Erforderlich** oder **Für registrierte Geräte verfügbar** für die App-Suite aus. Weitere Informationen finden Sie unter [Hinzufügen von Gruppen zum Organisieren von Benutzern und Geräten](../fundamentals/groups-add.md) und [Zuweisen von Apps zu Gruppen mit Microsoft Intune](apps-deploy.md).

    >[!Note]
    > Sie können die „Microsoft 365-Apps für macOS“-App-Suite nicht über Intune deinstallieren.

2. Klicken Sie auf **Weiter**, um die Seite **Überprüfen + erstellen** anzuzeigen. 

## <a name="step-4---review--create"></a>Schritt 4: Überprüfen und Erstellen

1. Überprüfen Sie die Werte und Einstellungen, die Sie für die App-Suite eingegeben haben.
2. Klicken Sie abschließend auf **Erstellen**, um Intune die App hinzuzufügen.

    Das Blatt **Übersicht** wird angezeigt. Die Suite wird in der Liste der Apps als einzelnen Eintrag angezeigt.

## <a name="next-steps"></a>Nächste Schritte

- Weitere Informationen zum Hinzufügen von Microsoft 365-Apps zu Windows 10-Geräten finden Sie unter [Hinzufügen von Microsoft 365-Apps zu Windows 10-Geräten mit Microsoft Intune](apps-add-office365.md).
- Informationen zum Ein- und Ausschließen von App-Zuweisungen für Gruppen finden Sie unter [Einschließen und Ausschließen von App-Zuweisungen in Microsoft Intune](apps-inc-exl-assignments.md).
