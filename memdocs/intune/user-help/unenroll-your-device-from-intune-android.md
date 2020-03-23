---
title: Entfernen der Registrierung Ihres Android-Geräts aus Intune | Microsoft-Dokumentation
description: Entfernen Ihres Android-Geräts aus dem Intune-Unternehmensportal
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/19/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: f40aab26-7613-48cc-a74e-de83df9465a4
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 77c8a972020113b36b57c992b64a6965f733d119
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79335470"
---
# <a name="unenroll-your-android-device-from-management"></a>Aufheben der Registrierung Ihres Android-Geräts für die Verwaltung  

Entfernen Sie Android-Geräte, deren Registrierung aufgehoben wurde, damit diese nicht mehr von Ihrer Organisation verwaltet werden. In diesem Artikel wird beschrieben, wie Sie das Gerät aus der Unternehmensportal-App entfernen. Es hat folgende Konsequenzen, wenn das Gerät entfernt wird:  

* Dem Gerät wird der Zugriff auf die geschützten Daten und Ressourcen Ihrer Organisation entzogen.
* Das Gerät wird nicht mehr im Unternehmensportal angezeigt.
* Sie können keine Apps mehr über das Unternehmensportal installieren.
* Alle Einstellungen, die beim Hinzufügen des Geräts auf diesem geändert wurden, z.B. das Deaktivieren der Kamera oder die Anforderung einer bestimmten Kennwortlänge, werden unwirksam.  

> [!NOTE]
> Sie können die Registrierung Ihres unternehmenseigenen Geräts nicht aus der Microsoft Intune-App aufheben. Das Gerät wurde während der Ersteinrichtung registriert und muss für den Zugriff auf die Ressourcen Ihrer Organisation registriert werden.  

1. Tippen Sie im Unternehmensportal auf die drei vertikal angeordneten Punkte in der oberen rechten Ecke. Dann öffnet sich das Menü „Aktion“.

   ![Screenshot der Android-Unternehmensportal-App mit geöffnetem Aktionsmenü in der oberen rechten Ecke Die neue Option „Unternehmensportal entfernen“ steht als die dritte Option unter „Mein Profil“ und „Einstellungen“ und über „Nutzungsbedingungen“, „Hilfe und Feedback“ und „Info“ zur Verfügung.](./media/android_remove_cp_menu_action_after_1705.png)

2. Tippen Sie auf **Unternehmensportal entfernen**.  

3. Dann wird eine Nachricht mit Informationen darüber angezeigt, was geschieht, wenn Sie die Registrierung Ihres Geräts aufheben. Tippen Sie auf **OK**, um zu bestätigen, dass Sie das Gerät aus dem Unternehmensportal entfernen möchten.

   ![Ein Screenshot der Bestätigung, die nach Auswahl der neuen Option „Unternehmensportal entfernen“ im Aktionsmenü verfügbar ist](./media/android_remove_cp_menu_confirmation_after_1705.png)

## <a name="remove-data-collected-by-the-company-portal-app"></a>Entfernen von Daten, die von der Unternehmensportal-App gesammelt wurden  

So entfernen Sie alle Daten, die die Unternehmensportal-App für Android auf Ihrem Gerät gespeichert hat:

- Löschen Sie die App-Daten, indem Sie auf **Anwendungen** > **[*Name der App*]**  > **Daten löschen** tippen.
- Löschen Sie den folgenden Ordner: \storage\internal storage\Android\data\com.microsoft.windowsintune.companyportal

## <a name="uninstall-the-company-portal-app"></a>Deinstallieren der Unternehmensportal-App

Das Unternehmensportal ist eine App für die Geräteverwaltung. Daher kann diese erst deinstalliert werden, wenn Sie die Registrierung für die Verwaltung des Geräts aufheben. Wenn dies geschehen ist, tippen Sie auf das Symbol für die Unternehmensportal-App und halten Sie dieses so lange gedrückt, bis die Option **Deinstallieren** angezeigt wird. Tippen Sie auf **Deinstallieren**, um die App von Ihrem Gerät zu entfernen.  

Stattdessen können Sie auch auf **Einstellungen** > **Apps** > **Unternehmensportal** > **Deinstallieren** tippen.  

### <a name="remove-the-company-portal-app-as-a-device-administrator"></a>Entfernen der Unternehmensportal-App als Geräteadministrator

Als letzte Alternative können Sie die App über das Gerät als Geräteadministrator deinstallieren.  

Wenn Sie ein unternehmenseigenes Gerät besitzen, setzt Ihre Organisation möglicherweise voraus, dass das Unternehmensportal immer auf dem Gerät installiert ist. Wenn Sie es deinstallieren, könnten Sie den Zugriff auf geschützte Unternehmensressourcen wie E-Mails, Apps, WLAN-Netzwerke oder VPNs verlieren, bis die App neu installiert wird. Weitere Informationen zum Installieren, Aktualisieren und Entfernen erforderlicher Apps finden Sie unter [Hinzufügen von Apps zu Microsoft Intune](/intune/apps/apps-add#apps-that-are-added-automatically-by-intune).

Im Folgenden erfahren Sie, wie Sie das Unternehmensportal als Geräteadministrator deaktivieren. Die tatsächlichen Namen der einzelnen Einstellungen können je nach Android-Gerät variieren.  

**Option 1**:  

1. Klicken Sie auf **Einstellungen** > **Sicherheit** > **Andere Sicherheitseinstellungen** > **Geräteadministratoren**.  
2. Deaktivieren Sie die Option **Unternehmensportal**.  

**Option 2**:

1. Klicken Sie auf **Einstellungen** > **Sperrbildschirm und Sicherheit** > **Andere Sicherheitseinstellungen** > **Geräteadministratoren**.
2. Deaktivieren Sie die Option **Unternehmensportal**.

Benötigen Sie weitere Unterstützung? Kontaktieren Sie den Support Ihres Unternehmens. Die entsprechenden Kontaktinformationen finden Sie auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980).
