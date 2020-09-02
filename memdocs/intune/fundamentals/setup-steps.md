---
title: Microsoft Intune einrichten
description: Anforderungen und erforderliche Komponenten für den Beginn der Verwendung Ihres Intune-Abonnements
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d158503c-1276-422b-ab81-5f66c1cd7e7a
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: c0a71ba59a1704e0f6369f611a2922212a2aa8c6
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911339"
---
# <a name="set-up-intune"></a>Einrichten von Intune

Diese Einrichtungsschritte helfen Ihnen, die mobile Geräteverwaltung (Mobile Device Management, MDM) mit Intune zu aktivieren. Geräte müssen verwaltet werden, bevor Sie Benutzern Zugriff auf Unternehmensressourcen gewähren oder Einstellungen auf diesen Geräten verwalten können.

Einige Schritte wie die Einrichtung eines Intune-Abonnements und der MDM-Autorität sind in den meisten Szenarios erforderlich. Andere Schritte wie das Konfigurieren einer benutzerdefinierten Domäne oder das Hinzufügen von Apps sind optional, je nach den Anforderungen Ihres Unternehmens.

Wenn Sie Microsoft Configuration Manager derzeit zum Verwalten von Computern und Servern verwenden, können Sie [Configuration Manager über die Co-Verwaltung mit der Cloud verknüpfen](/configmgr/comanage/overview).

>[!TIP]
>Sie können das *FastTrack Center-Leistungsangebot* nutzen, wenn Sie mindestens 150 Lizenzen für Intune in einem berechtigten Plan erwerben. Bei diesem Dienst unterstützen Sie Microsoft-Spezialisten bei der Vorbereitung Ihrer Umgebung für Intune. Informationen hierzu finden Sie unter [FastTrack Center-Leistungsangebot für Enterprise Mobility Suite (EMS)](/enterprise-mobility-security/Solutions/enterprise-mobility-fasttrack-program).

| Schritte | Status  |
|---|---|
|   1   | [Unterstützte Konfigurationen:](supported-devices-browsers.md) Wichtige Informationen, bevor Sie beginnen. Dies beinhaltet die unterstützten Konfigurationen und Netzwerkanforderungen.|
|   2   |  [Anmelden bei Intune:](account-sign-up.md) Melden Sie sich bei Ihrem Testabonnement an, oder erstellen Sie ein neues Intune-Abonnement. |
|   3   | [Konfigurieren des Domänennamens:](custom-domain-name-configure.md) Legen Sie die DNS-Registrierung fest, um den Domänennamen Ihres Unternehmens mit Intune zu verbinden. Dies bietet Benutzern eine vertraute Domäne beim Herstellen einer Verbindung zu Intune und beim Verwenden von Ressourcen. |
|   4   | [Hinzufügen von Benutzern](users-add.md) und [Gruppen](groups-add.md): Fügen Sie Benutzer und Gruppen hinzu, oder verbinden Sie Active Directory Domain Services für die Synchronisierung mit Intune. Erforderlich, es sei denn, Ihre Geräte sind „benutzerlose“ Kiosk-Geräte. Gruppen werden verwendet, um Apps, Einstellungen und andere Ressourcen zuzuweisen.|
|   5   | [Zuweisen von Lizenzen:](licenses-assign.md) Erteilen Sie Benutzern die Berechtigung, Intune zu verwenden. Jeder Benutzer oder jedes benutzerlose Gerät benötigt eine Lizenz für Intune, um auf den Dienst zuzugreifen. |
|   6   | [Festlegen der MDM-Autorität:](mdm-authority-set.md) Verwenden Sie Benutzer- und Gerätegruppen, um Verwaltungsaufgaben zu vereinfachen. Gruppen werden verwendet, um Apps, Einstellungen und andere Ressourcen zuzuweisen. |
|   7   | [Hinzufügen von Apps:](../apps/apps-add.md) Apps können Gruppen zugewiesen und automatisch oder optional installiert werden. |
|   8   | [Konfigurieren von Geräten:](../configuration/device-profiles.md) Richten Sie Profile ein, die Einstellungen für Geräte verwalten. Mit Geräteprofilen können Einstellungen für E-Mail-, VPN-, WLAN- und Gerätefunktionen vorkonfiguriert werden. Sie können auch Geräte zum Schutz von Geräten und Daten einschränken. |
|   9   |  [Anpassen des Unternehmensportals:](../apps/company-portal-app.md) Passen Sie das Intune-Unternehmensportal an, mit dem Benutzer Geräte registrieren und Apps installieren. Diese Einstellungen werden in der Unternehmensportal-App und auf der Intune-Unternehmensportal-Website angezeigt.       |
|  10   | [Aktivieren der Geräteregistrierung:](mdm-authority-set.md) Aktivieren Sie die Intune-Verwaltung auf iOS/iPadOS-, Windows-, Android- und Mac-Geräten, indem Sie die MDM-Autorität festlegen und bestimmte Plattformen aktivieren. |
|  11   |  [Konfigurieren der App-Richtlinien:](../apps/app-protection-policy.md) Legen Sie bestimmte Einstellungen anhand der App-Schutzrichtlinien in Microsoft Intune fest. |