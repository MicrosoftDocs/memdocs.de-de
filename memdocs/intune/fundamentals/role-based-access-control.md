---
title: Rollenbasierte Zugriffssteuerung für Microsoft Intune
description: Erfahren Sie, wie Sie mithilfe der rollenbasierten Zugriffssteuerung (Role-Based Access Control, RBAC) steuern können, wer in Microsoft Intune Aktionen ausführen und Änderungen vornehmen kann.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/22/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ca3de752-3caa-46a4-b4ed-ee9012ccae8e
ms.reviewer: pjain
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5cb4631b31d33e53b6ef172f142735d24a5c3cb6
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80220165"
---
# <a name="role-based-access-control-rbac-with-microsoft-intune"></a>Rollenbasierte Zugriffssteuerung für Microsoft Intune

Mithilfe der rollenbasierten Zugriffssteuerung (Role-Based Access Control, RBAC) können Sie verwalten, wer Zugriff auf die Ressourcen Ihrer Organisation hat und wozu diese verwendet werden können.  Wenn Sie Ihren Intune-Benutzern [Rollen zuweisen](assign-role.md), können Sie einschränken, welche Elemente diese sehen und ändern können. Jeder Rolle sind Berechtigungen zugewiesen, die festlegen, auf welche Elemente Benutzer mit dieser Rolle innerhalb Ihrer Organisation zugreifen können und welche Elemente sie ändern können.

Für das Erstellen, Bearbeiten oder Zuweisen von Rollen muss das Konto in Azure AD über eine der folgenden Berechtigungen verfügen:
- **Globaler Administrator**
- **Intune-Dienstadministrator** (auch als **Intune-Administrator** bezeichnet)

Wenn Sie Tipps und Vorschläge zu Intune RBAC benötigen, können Sie sich diese Reihe von fünf Videos mit Beispielen und exemplarischen Vorgehensweisen ansehen: [1](https://www.youtube.com/watch?v=5deXLMLcnKY), [2](https://www.youtube.com/watch?v=38dnMBLuxbQ), [3](https://www.youtube.com/watch?v=6vqg9cAkMbY), [4](https://www.youtube.com/watch?v=5yOLajFFMHE), [5](https://www.youtube.com/watch?v=P5DDvsSF4Wk).

## <a name="roles"></a>Rollen
Eine Rolle definiert die Berechtigungen, die den ihr zugewiesenen Benutzern gewährt werden.
Sie können sowohl integrierte als auch benutzerdefinierte Rollen verwenden. Integrierte Rollen decken einige häufige Szenarios in Intune ab. Sie können aber auch Ihre [eigenen benutzerdefinierten Rollen](create-custom-role.md) mit den gewünschten Berechtigungen erstellen. Mehrere Azure Active Directory-Rollen beinhalten den Zugriff auf Intune.
Wenn Sie eine Rolle abrufen möchten, klicken Sie auf **Intune** > **Rollen** > **Alle Rollen**, und wählen Sie eine Rolle aus. Dann werden die folgenden Seiten angezeigt:

- **Eigenschaften:** der Name, die Beschreibung, der Typ, die Zuweisungen und die Bereichsmarkierungen für die Rolle 
- **Berechtigungen**: Listet eine Reihe von Optionen auf, die die Berechtigungen der jeweiligen Rolle definieren
- **Zuweisungen:** Eine Liste mit [Rollenzuweisungen]( assign-role.md), in der definiert wird, welche Benutzer Zugriff auf welche Benutzer/Geräte haben. Eine Rolle kann mehrere Zuweisungen aufweisen, und ein Benutzer kann Teil mehrerer Zuweisungen sein.

### <a name="built-in-roles"></a>Integrierte Rollen
Sie können Gruppen ohne weitere Konfiguration integrierte Rollen zuweisen. Sie können den Namen, die Beschreibung, den Typ oder die Berechtigungen einer integrierten Rolle löschen oder bearbeiten.

- **Helpdesk-Operator**: Führt Remoteaufgaben für Benutzer und Geräte durch und kann Anwendungen oder Richtlinien Benutzern oder Geräten zuweisen.
- **Richtlinien- und Profil-Manager**: Verwaltet Konformitätsrichtlinien, Konfigurationsprofile, die Apple-Registrierung, unternehmensbezogene Geräte-IDs und Sicherheitsbaselines.
- **Schreibgeschützter Operator**: Kann Benutzer-, Geräte-, Registrierungs-, Konfigurations- und Anwendungsinformationen anzeigen. Kann keine Änderungen in Intune vornehmen.
- **Anwendungs-Manager**: Verwaltet mobile und verwaltete Anwendungen und kann Geräteinformationen lesen sowie Gerätekonfigurationsprofile anzeigen.
- **Intune-Rollenadministrator**: Verwaltet benutzerdefinierte Intune-Rollen und fügt integrierten Intune-Rollen Aufgaben hinzu. Dies ist die einzige Intune-Rolle, die Administratoren Berechtigungen zuweisen kann.
- **Schuladministrator**: Verwaltet Windows 10-Geräte in [Intune for Education](introduction-intune-education.md).
- **Endpunktsicherheits-Manager**: Verwaltet Sicherheits- und Konformitätsfeatures, wie z. B. Sicherheitsbaselines, Gerätekonformität, bedingter Zugriff und Microsoft Defender ATP.

### <a name="custom-roles"></a>Benutzerdefinierte Rollen
Sie können mithilfe von benutzerdefinierten Berechtigungen Ihre eigenen Rollen erstellen. Weitere Informationen zu benutzerdefinierten Rollen finden Sie unter [Create a custom role (Erstellen von benutzerdefinierten Rollen)](create-custom-role.md).

### <a name="azure-active-directory-roles-with-intune-access"></a>Azure Active Directory-Rollen mit Zugriff auf Intune
| Azure Active Directory-Rolle | Alle Intune-Daten | Intune-Überwachungsdaten |
| --- | :---: | :---: |
| Globaler Administrator | Lesen + Schreiben | Lesen + Schreiben |
| Intune-Dienstadministrator | Lesen + Schreiben | Lesen + Schreiben |
| Administrator für bedingten Zugriff | Keine | Keine |
| Sicherheitsadministrator | Schreibgeschützt (vollständige Administratorberechtigungen für den Endpunkt-Sicherheitsknoten) | Schreibgeschützt |
| Sicherheitsoperator | Schreibgeschützt | Schreibgeschützt |
| Sicherheitsleseberechtigter | Schreibgeschützt | Schreibgeschützt |
| Complianceadministrator | Keine | Schreibgeschützt |
| Administrator für Konformitätsdaten | Keine | Schreibgeschützt |
| Globaler Leser | Schreibgeschützt | Schreibgeschützt |

> [!TIP]
> Intune zeigt außerdem drei Azure AD-Erweiterungen an: **Benutzer**, **Gruppen** und **Bedingter Zugriff**, die mithilfe der rollenbasierten Zugriffssteuerung von Azure AD gesteuert werden. Darüber hinaus führt der **Benutzerkontoadministrator** lediglich auf AAD-Benutzer- und Gruppen bezogene Aktivitäten aus und verfügt nicht über Vollzugriffsberechtigungen zum Ausführen aller Aktivitäten in Intune. Weitere Informationen finden Sie unter [Berechtigungen der Administratorrolle in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles).

## <a name="role-assignments"></a>Rollenzuweisungen
Eine Rollenzuweisung definiert Folgendes:

- die einer Rolle zugewiesenen Benutzer
- die Ressourcen, die diese sehen können
- die Ressourcen, die diese ändern können

Sie können Ihren Benutzern sowohl benutzerdefinierte als auch integrierte Rollen zuweisen. Um einer Intune-Rolle zugewiesen zu werden, muss der Benutzer über eine Intune-Lizenz verfügen.
Wenn Sie eine Rollenzuweisung abrufen möchten, klicken Sie auf **Intune** > **Rollen** > **Alle Rollen**, und wählen Sie erst eine Rolle und dann eine Zuweisung aus. Dann werden die folgenden Seiten angezeigt:

- **Eigenschaften:** der Name, die Beschreibung, die Rolle, die Mitglieder, die Bereiche und die Markierungen einer Zuweisung
- **Mitglieder**: Alle Benutzer in den aufgelisteten Azure-Sicherheitsgruppen haben die Berechtigung, die Benutzer/Geräte zu verwalten, die in „Bereich (Gruppen)“ aufgelistet sind.
- **Bereich (Gruppen)** : Alle Benutzer/Geräte in diesen Azure-Sicherheitsgruppen können von den Benutzern verwaltet werden, die unter „Mitglieder“ aufgeführt sind.
- **[Bereich (Tags)](scope-tags.md)** : Benutzer, die unter „Mitglieder“ aufgeführt sind, können die Ressourcen sehen, die dieselben Bereichsmarkierungen aufweisen.

### <a name="multiple-role-assignments"></a>Mehrere Rollenzuweisungen
Hat ein Benutzer mehrere Rollenzuweisungen, Berechtigungen und Bereichsmarkierungen, erstrecken sich diese Rollenzuweisungen wie folgt auf verschiedene Objekte:

- Zuweisungsberechtigungen und Bereichsmarkierungen gelten nur für die Objekte (etwa Richtlinien oder Apps), die in „Bereich (Gruppen)“ dieser Gruppe zugewiesen sind. Zuweisungsberechtigungen und Bereichsmarkierungen gelten nicht für Objekte in anderen Rollenzuweisungen, es sei denn, sie werden in einer anderen Zuweisung explizit erteilt.
- Andere Berechtigungen (etwa Erstellen, Lesen, Aktualisieren und Schreiben) und Bereichsmarkierungen gelten für alle Objekte desselben Typs (etwa alle Richtlinien oder alle Apps) in den Zuweisungen des Benutzers.
- Berechtigungen und Bereichsmarkierungen für Objekte anderer Typen (etwa Richtlinien oder Apps) gelten nicht gegenseitig. Eine Leseberechtigung für eine Richtlinie umfasst beispielsweise keine Leseberechtigung für Apps in den Zuweisungen des Benutzers.

## <a name="next-steps"></a>Nächste Schritte
- [Assign a role to a user (Zuweisen einer Rolle an einen Benutzer)](assign-role.md)
- [Create a custom role (Erstellen einer benutzerdefinierten Rolle)](create-custom-role.md)
