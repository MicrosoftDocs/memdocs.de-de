---
title: Pfade zur Co-Verwaltung
titleSuffix: Configuration Manager
description: Verstehen Sie die Voraussetzungen für die beiden wichtigsten Methoden, wie Sie Co-Verwaltung einrichten können.
ms.date: 06/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 5beb5564-2fdf-4f0a-8801-d0cec8214c43
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7a670660bcf7b3f5cb8209aaf6d0b59eb0f343e4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691238"
---
# <a name="paths-to-co-management"></a>Pfade zur Co-Verwaltung

Es gibt zwei primäre Methoden zum Einrichten der Co-Verwaltung. Es ist wichtig, die Voraussetzungen für jeden dieser Pfade zu verstehen. Jeder von ihnen erfordert eine Kombination aus Azure Active Directory (Azure AD), Configuration Manager, Microsoft Intune und Windows 10. 

1. [Automatische Registrierung von vorhandenen, von Configuration Manager verwalteten Geräten in Intune](#bkmk_path1)  
2. [Starten des Configuration Manager-Clients mit moderner Bereitstellung](#bkmk_path2)  

![Abbildung zu den Pfaden für die Co-Verwaltung](media/co-management-paths.png)



## <a name="path-1-auto-enroll-existing-clients"></a><a name="bkmk_path1"></a>Pfad 1: Automatische Registrierung vorhandener Clients

Wenn Sie diesen Pfad einschlagen, können Sie Ihre vorhandenen, durch Configuration Manager verwalteten Geräte schnell in Intune registrieren lassen. Die Verwaltung dieser Geräte aus Configuration Manager unterscheidet sich nicht von der Verwaltung vor dem Aktivieren der Co-Verwaltung. Jetzt können Sie alle cloudbasierten Vorteile nutzen. Dieser Pfad ist für Ihre Benutzer transparent.

Gehen Sie für die Einrichtung wie folgt vor:
- Hybrid-Azure AD
    - Eine der folgenden [Optionen für Azure AD-Hybrididentität](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin):  
       - [Kennworthashsynchronisierung](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#password-hash-synchronization) mit [nahtlosem einmaligen Anmelden (SSO)](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)
       - [Pass-Through-Authentifizierung](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta) mit [nahtlosem einmaligen Anmelden (SSO)](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)
       - [Einmaliges Anmelden (SSO) im Verbund (mit Active Directory-Verbunddienste [AD FS])](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-user-signin#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)
    - Azure AD Connect
    - Azure AD Premium-Lizenz
    - Konfigurieren der Hybrid-Azure AD-Einbindung (wählen Sie eine Option aus):
        - Für verwaltete Domänen
        - Für Verbunddomänen
- Client-Agent-Einstellungen für Hybrid-Azure AD-Einbindung
- Konfigurieren der automatischen Registrierung von Geräten in Intune
- Zuweisen von Intune-Benutzerlizenzen
- Aktivieren der Co-Verwaltung in Configuration Manager

Ein Tutorial zu diesem Pfad finden Sie unter [Tutorial: Aktivieren der Co-Verwaltung für vorhandene Configuration Manager-Clients](tutorial-co-manage-clients.md).



## <a name="path-2-bootstrap-with-modern-provisioning"></a><a name="bkmk_path2"></a>Pfad 2: Starten mit moderner Bereitstellung

Gehen Sie für die Einrichtung wie folgt vor:

1. [Einrichten von erweitertem HTTP](../core/plan-design/hierarchy/enhanced-http.md)  
2. [Erstellen der Clouddienste in Azure](../core/servers/deploy/configure/azure-services-wizard.md)  
3. [Konfigurieren des Verwaltungspunkts und der Clients für die Verwendung des Cloudverwaltungsgateways (CMG)](../core/clients/manage/cmg/setup-cloud-management-gateway.md)  
4. [Verwenden von Intune zum Bereitstellen des Configuration Manager-Clients](how-to-prepare-Win10.md)  

> [!Note]  
> Ein Tutorial für diesen Pfad wird in Kürze verfügbar sein.
