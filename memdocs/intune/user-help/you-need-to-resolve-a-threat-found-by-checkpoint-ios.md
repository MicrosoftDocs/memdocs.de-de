---
title: Vorgehen gegen von SandBlast Mobile Protect erkannte Bedrohungen unter iOS | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie eine Bedrohung beheben, die von SandBlast Mobile Protect für iOS gefunden wurde.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/05/2018
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 5b2a69e7-cc86-4f1b-81d9-35b8b23b937b
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 9ef18bc6554f5db364eaf320c66da12e7a5ffe7d
ms.sourcegitcommit: 2ee50bfc416182362ae0b8070b096e1cc792bf68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87866161"
---
# <a name="resolve-a-threat-found-by-sandblast-mobile-protect-on-ios"></a>Beheben einer von SandBlast Mobile Protect erkannten Bedrohung unter iOS

SandBlast Mobile Protect ist ein Mobile Threat Defender-Dienst, der potenzielle Bedrohungen auf Ihren iOS-Geräten identifiziert und analysiert. Anschließend wird ein Bericht über die Bedrohungen erstellt, sodass Sie sich diese in der Unternehmensportal-App ansehen können. Bedrohungen werden in der App als ungelöste Probleme angezeigt, die auf fehlende Konformität hinweisen. Solange diese Bedrohungen vorhanden sind, können Sie folgende Aktionen möglicherweise nicht ausführen:   

* Herstellen einer Verbindung mit Unternehmens-E-Mail
* Herstellen einer Verbindung mit Unternehmens-WLAN
* Herstellen einer Verbindung mit SharePoint Online
* Synchronisieren von Unternehmensdateien mit OneDrive
* Zugreifen auf Unternehmens-Apps

In diesem Artikel wird beschrieben, wie Sandblast Mobile Protect-Benachrichtigungen zu Bedrohungen zu verstehen sind und wie diese gelöst werden können.  

## <a name="troubleshoot-virus-or-security-threat"></a>Problembehandlung bei Viren- oder Sicherheitsbedrohungen  
Wenn eine Viren- oder Sicherheitsbedrohung erkannt wird, verfährt die SandBlast Mobile Protect-App gemäß den Zugriffsrichtlinien Ihrer Organisation. Zugriffsrichtlinien könnten Sie am Zugriff auf das Netzwerk, die Apps und die E-Mails hindern, die Sie für Ihre Arbeit benötigen.  

![Beispielscreenshot einer Warnmeldung der SEP Mobile-App.](./media/skycure-list-of-potential-issues-android.png)  
SandBlast Mobile Protect fordert Sie dazu auf, Maßnahmen zu ergreifen, um den Zugang zu diesen Ressourcen wiederherzustellen. Wählen Sie die Bedrohung aus, und führen Sie zur Problembehebung die Anweisungen in der App aus.

Da die App in den MDM-Anbieter Ihres Unternehmens integriert ist, wird auch eine Warnung über den eingeschränkten Zugriff in der Unternehmensportal-App angezeigt. In der Warnmeldung werden Sie aufgefordert, Sandblast Mobile Protect zu öffnen, um die Viren- bzw. Sicherheitsbedrohung zu beheben.  

  ![Beispielscreenshot der Geräteseite des Unternehmensportals, auf der die Sandblast Mobile Protect-Warnung angezeigt wird](./media/CP-lookout-virus-banner-1808.png)  

## <a name="troubleshoot-an-app-threat"></a>Problembehandlung bei einer App-Bedrohung  

Wenn Sie eine App installieren, die als Bedrohung für Ihr Gerät angesehen wird, erhalten Sie eine Benachrichtigung in SandBlast Mobile Protect. Solange die betroffene App auf Ihrem Gerät verbleibt, können Sie nicht auf Unternehmensressourcen zugreifen.  

Zum Auflösen der Warnung wählen Sie die App in der Liste der Bedrohungen in SandBlast Mobile Protect aus. Folgen Sie dann den Anweisungen, um die App zu entfernen und zu deinstallieren.  

Benötigen Sie weitere Unterstützung? Kontaktieren Sie den Support Ihres Unternehmens. Sie finden entsprechende Kontaktinformationen auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980).  
