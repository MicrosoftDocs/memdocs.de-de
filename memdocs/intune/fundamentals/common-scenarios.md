---
title: Häufige Verwendungsarten von Microsoft Intune
description: Erhalten Sie Informationen zu den sechs gängigsten Aufgaben, die Sie mit Microsoft Intune verwalten können.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 11/29/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1f37d4ff-b5a7-4a89-8884-a6184908b09c
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: b5ed8b6974971e3e2e8182d32cad39a5481331b2
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88994122"
---
# <a name="common-ways-to-use-microsoft-intune"></a>Häufige Verwendungsarten von Microsoft Intune

Bevor die Implementierungsaufgaben behandelt werden, ist es wichtig, dass die Enterprise Mobility-Beteiligten Ihres Unternehmens in Bezug auf die Verwendung von Intune die gleichen Geschäftsziele verfolgen. Hierbei spielt es keine Rolle, ob Enterprise Mobility für Sie neu ist oder Sie von einem anderen Produkt migrieren.  

Die Anforderungen in Bezug auf Enterprise Mobility entwickeln sich dynamisch und die Ansätze von Microsoft zur Behandlung dieser Anforderungen können sich manchmal von anderen Lösungen am Markt unterscheiden. Die beste Methode zum Ausrichten von Geschäftszielen besteht darin, die Ziele in Bezug auf die Szenarios auszudrücken, die Sie für Mitarbeiter, Partner und die IT-Abteilung ermöglichen möchten.  

Nachfolgend finden Sie eine kurze Einführung zu den sechs häufigsten, auf Intune beruhenden Szenarios sowie Links zu weiteren Informationen, wie diese jeweils geplant und bereitgestellt werden.

>[!NOTE]
>Möchten Sie wissen, wie die Microsoft IT Intune verwendet, um Microsoft-Mitarbeitern den Zugriff auf Unternehmensressourcen auf ihren mobilen Geräten zu ermöglichen, während dabei auch die Unternehmensdaten geschützt bleiben? [Lesen Sie diese technische Fallstudie](https://www.microsoft.com/itshowcase/Article/Content/588), um ausführlich zu erfahren, wie Microsoft IT Intune und andere Dienste dazu verwendet, um Identitäten, Geräte, Apps und Daten zu verwalten.  

>[!IMPORTANT]
>Wir möchten sicherstellen, dass Mobilgeräte angesichts der aktuellen „Trident“-Malware-Angriffe auf iOS/iPadOS-Geräte aktuell sind. Lesen Sie daher unseren Blogbeitrag [Ensuring mobile devices are up to date using Microsoft Intune (Verwenden von Microsoft Intune, um sicherzustellen, dass mobile Geräte auf dem neuesten Stand sind)](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/26/ensuring-mobile-devices-are-up-to-date-using-microsoft-intune/). Er bietet Informationen zu den verschiedenen Methoden, mit denen Intune Ihre Geräte sicher und auf dem neuesten Stand halten kann.

## <a name="protecting-your-on-premises-email-and-data-so-it-can-be-safely-accessed-by-mobile-devices"></a>Schützen Ihrer lokalen E-Mails und Daten für den sicheren Zugriff über mobile Geräte

Die meisten Enterprise Mobility-Strategien beginnen mit einem Plan, um Mitarbeitern mit mobilen Geräten den sicheren Zugriff auf E-Mails über das Internet zu ermöglichen. Viele Unternehmen verwenden weiterhin lokale Daten- und Anwendungsserver wie Microsoft Exchange, die im Unternehmensnetzwerk gehostet werden.

Intune und Microsoft Enterprise Mobility + Security (EMS) bieten eine einzigartig integrierte [Lösung für den bedingten Zugriff](../protect/conditional-access.md) für Exchange Server, die sicherstellt, dass mobile Apps nur dann auf E-Mails zugreifen können, wenn das Gerät bei Intune registriert ist. Sie können diese Art des E-Mail-Zugriffs implementieren, ohne einen weiteren Gatewaycomputer am Rand Ihres Unternehmensnetzwerks bereitstellen zu müssen.

Neben E-Mails unterstützt Intune auch das Ermöglichen des Zugriffs auf mobile Apps, die den sicheren Zugriff auf lokale Daten erfordern, z.B. ein branchenspezifischer Anwendungsserver. Dieser Zugriffstyp erfolgt in der Regel mithilfe von [Zertifikaten die von Intune verwaltet werden](../protect/certificates-configure.md), in Kombination mit einem VPN-Standardgateway oder -proxy im Umkreis, z.B. dem Microsoft Azure Active Directory-Anwendungs-Proxy.

In diesen Fällen besteht die einzige Möglichkeit für den Zugriff auf Unternehmensdaten in der Registrierung des Geräts für die Verwaltung. Nach der Registrierung stellt das Verwaltungssystem sicher, dass Geräte, die auf Unternehmensdaten zugreifen möchten, Ihren Richtlinien entsprechen. Darüber hinaus können das [App Wrapping Tool und App SDK](../developer/apps-prepare-mobile-application-management.md) von Intune dabei helfen, dass die Daten, auf die zugegriffen wird, in der branchenspezifischen App verbleiben und diese App keine Unternehmensdaten an Verbraucher-Apps oder -Dienste übergeben kann.

<!-- Learn more about how to plan and deploy Intune to help secure on-premises email and data. -->

## <a name="protecting-your-microsoft-365-email-and-data-so-it-can-be-safely-accessed-by-mobile-devices"></a>Schützen von Microsoft 365-E-Mails und -Daten für den sicheren Zugriff über mobile Geräte

Das Schützen von Unternehmensdaten in Microsoft 365 (E-Mails, Dokumente, Sofortnachrichten, Kontakte) könnte für Sie nicht einfacher oder für Ihre Benutzer nicht problemloser verlaufen.

Intune und Microsoft Enterprise Mobility + Security bieten eine auf einzigartige Weise integrierte Lösung für den bedingten Zugriff, die sicherstellt, dass Benutzer, Apps oder Geräte nur auf Microsoft 365-Daten zugreifen können, die den Complianceanforderungen Ihres Unternehmens entsprechen (ausgeführte [mehrstufige Authentifizierung](../enrollment/multi-factor-authentication.md), Registrierung bei Intune, Verwenden der verwalteten App, der unterstützten Betriebssystemversion, der Geräte-PIN, des Benutzerprofils mit geringem Risiko usw.).

Die mobilen Office-Apps in ihren jeweiligen App-Stores sind bereit, Datenbeschränkungsrichtlinien einzuhalten, die Sie über Intune konfigurieren können. Mit diesen Funktionen können Sie verhindern, dass Daten für nicht von der IT verwaltete Apps (beispielsweise eine native E-Mail-App) und Speicherorte (beispielsweise Dropbox) freigegeben werden. Diese Funktionalität ist in Microsoft 365 und EMS vollständig integriert. Sie müssen keine zusätzliche Infrastruktur bereitstellen, um dies zu erreichen.

Eine gängige Microsoft 365-Bereitstellungsmethode besteht darin, dass sich Geräte bei der Verwaltung registrieren müssen, wenn sie vollständig mit App-/Zertifikat-/WLAN- oder VPN-Konfigurationen im Unternehmen bereitgestellt werden müssen, was bei firmeneigenen Geräten ein häufig vorkommendes Szenario ist.  

Wenn Ihr Benutzer jedoch einfach Zugriff auf die E-Mails und Dokumente des Unternehmens benötigt, was häufig bei Geräten der Fall ist, die sich im privaten Besitz befinden, können Sie festlegen, dass der Benutzer die mobilen Office-Apps nutzen (auf die Sie [App-Schutzrichtlinien](../apps/app-protection-policies.md) 
angewendet haben) und die Registrierung des Geräts überspringen muss.  

In beiden Fällen werden die Microsoft 365-Daten durch von Ihnen definierte Richtlinien geschützt.

<!-- Learn more about how to plan and deploy Intune to help secure Microsoft 365 email and data. -->

## <a name="offer-a-bring-your-own-device-program-to-all-employees"></a>Anbieten eines BYOD-Programms (Bring Your Own Device) für alle Mitarbeiter

Die Beliebtheit von BYOD nimmt in Unternehmen als Mittel zum Reduzieren von Hardwareausgaben oder zum Erhöhen von mobilen Produktivitätsoptionen für Mitarbeiter weiter zu. Fast jeder verfügt heutzutage über ein eigenes Smartphone, warum also sollten die Mitarbeiter mit einem zusätzlichen Smartphone ausgestattet werden? Die wesentliche Herausforderung ist dabei immer gewesen, die Mitarbeiter davon zu überzeugen, ihr privates Gerät bei der Verwaltung zu registrieren, da sie unsicher sind, was die IT-Abteilung mit ihren Geräten anzeigen oder machen kann.  

Wenn die Registrierung des Geräts nicht realisierbar ist, bietet Intune einen alternativen BYOD-Ansatz, bei dem einfach nur die [Apps verwaltet werden, die Unternehmensdaten enthalten](../apps/app-protection-policies.md). Intune schützt die Unternehmensdaten, auch wenn die betreffende Anwendung sowohl auf Unternehmens- als auch auf private Daten zugreift, wie es bei mobilen Office-Apps der Fall ist.  

Als Administrator können Sie festlegen, dass Benutzer über die mobilen Office-Apps auf Microsoft 365 zugreifen müssen. Zudem können Sie die Apps mit Richtlinien konfigurieren, die dafür sorgen, dass die Daten geschützt bleiben (Verschlüsselung, durch PIN geschützt usw.). Diese App-Schutzrichtlinien verhindern den Datenverlust durch nicht verwaltete Apps und Speicherorte – innerhalb oder außerhalb dieser Apps. Die Richtlinien hindern z.B. einen Benutzer daran, Text aus einem E-Mail-Profil im Unternehmen in das E-Mail-Profil eines Verbrauchers zu kopieren, auch wenn beide Profile in Outlook Mobile konfiguriert sind. Ähnliche Konfigurationen können für andere Dienste und Anwendungen bereitgestellt werden, die für Ihre BYOD-Benutzer erforderlich sind.

<!-- Learn more about how to plan and deploy Intune to support BYOD.-->

## <a name="issue-corporate-owned-phones-to-your-employees"></a>Ausgeben firmeneigener Smartphones für Mitarbeiter

Viele Mitarbeiter sind heutzutage mobil, wodurch Produktivität auf mobilen Geräten unverzichtbar wird, um wettbewerbsfähig zu bleiben. Diese Mitarbeiter benötigen jederzeit und überall den problemlosen Zugriff auf alle Apps und Daten im Unternehmen. Sie müssen sicherstellen, dass die Unternehmensdaten sicher und die Verwaltungskosten gering sind.  

Intune bietet die [Massenbereitstellung sowie Verwaltungslösungen](../enrollment/device-enrollment.md), die in die wesentlichen Verwaltungsplattformen für Unternehmensgeräte integriert sind, die heute am Markt verfügbar sind, einschließlich dem Programm zur Geräteregistrierung von Apple und der mobilen Knox-Sicherheitsplattform von Samsung. Die zentrale Erstellung von Gerätekonfigurationen mit Intune trägt dazu bei, die Bereitstellung von firmeneigenen Geräten zu einem Vorgang zu machen, der umfassend automatisiert werden kann.  

Stellen Sie sich Folgendes vor: Überreichen Sie einem Mitarbeiter ein ungeöffnetes iPhone-Produktpaket. Der Mitarbeiter schaltet das Gerät ein und wird durch ein Setup mit Firmenbranding geleitet, bei dem er sich selbst authentifizieren muss. Das iPhone ist nahtlos mit [Sicherheitsrichtlinien](../configuration/device-profiles.md) konfiguriert.

Dann startet der Mitarbeiter die Windows Intune-Unternehmensportal-App für den Zugriff auf optionale Unternehmens-Apps, die zur Verfügung stehen.

<!-- Learn more about how to plan and deploy Intune to support corporate owned devices. -->

## <a name="issue-limited-use-shared-tablets-to-your-employees"></a>Ausgeben gemeinsam genutzter Tablets mit eingeschränkter Verwendung an Ihre Mitarbeiter

Mitarbeiter nutzen zunehmend mobile Technologien. Freigegebene Tablets sind z.B. für Mitarbeiter im Einzelhandel jetzt üblich.  Ob Verkaufsvorgang oder unmittelbare Bestandsprüfung, Tablets ermöglichen eine hervorragende Interaktion mit Kunden.

In diesem Fall ist die Einfachheit der Benutzererfahrung entscheidend. Daher werden die Tablets den Mitarbeitern in der Regel in einem Modus mit eingeschränkter Nutzung übergeben, damit die Mitarbeiter nur mit einzelnen branchenspezifischen Apps interagieren können. Mit Intune können Sie für diese freigegebenen [iOS- und Android](../configuration/device-profiles.md)-Tablets, die für die Ausführung in diesem Modus mit eingeschränkter Nutzung konfiguriert werden können, eine Massenbereitstellung durchführen, sie sichern und zentral verwalten.

<!-- Learn more about how to plan and deploy Intune to support shared tablets. -->

## <a name="enable-your-employees-to-securely-access-microsoft-365-from-an-unmanaged-public-kiosk"></a>Ermöglichen des sicheren Zugriffs für Mitarbeiter auf Microsoft 365 von einem nicht verwalteten, öffentlichen Kiosk aus

Mitunter müssen Ihre Mitarbeiter Geräte, Apps oder Browser verwenden, die von Ihnen nicht verwaltet werden können, z. B. öffentliche Computer auf Messen und in Hotellobbys.

Sollten Sie es den Mitarbeitern gestatten, dass sie über diese öffentlichen Computer auf E-Mails im Unternehmen zugreifen? Mit Intune und Microsoft Enterprise Mobility + Security können Sie diese Frage einfach mit „Nein“ beantworten, indem Sie den [E-Mail-Zugriff auf Geräte beschränken, die von Ihrer Organisation verwaltet werden](../protect/conditional-access.md). Dadurch wird sichergestellt, dass streng authentifizierte Mitarbeiter nicht versehentlich Unternehmensdaten auf nicht vertrauenswürdigen Computern hinterlassen.
