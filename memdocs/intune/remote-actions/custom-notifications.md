---
title: Senden benutzerdefinierter Benachrichtigungen an Benutzer mit Microsoft Intune
titleSuffix: Microsoft Intune
description: Verwenden von Intune zum Erstellen und Senden benutzerdefinierter Pushbenachrichtigungen an Benutzer von iOS-/iPadOS- und Android-Geräten
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: jinyoon
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0ef8989c9f4de0211a7636c747ff9a01111842f6
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80325317"
---
# <a name="send-custom-notifications-in-intune"></a>Senden benutzerdefinierter Benachrichtigungen in Intune

Verwenden Sie Microsoft Intune zum Senden benutzerdefinierter Benachrichtigungen an die Benutzer von verwalteten iOS-/iPadOS- und Android-Geräten. Diese Nachrichten werden wie auch Benachrichtigungen von anderen Anwendungen auf dem Gerät als Standardpushbenachrichtigungen von der Unternehmensportal-App und der Microsoft Intune-App auf dem Gerät eines Benutzers angezeigt. Benutzerdefinierte Intune-Benachrichtigungen werden von macOS- und Windows-Geräten nicht unterstützt.

Benutzerdefinierte Benachrichtigungsnachrichten enthalten einen kurzen Titel und einen Nachrichtentext mit maximal 500 Zeichen. Diese Nachrichten können für jeden allgemeinen Kommunikationszweck angepasst werden.

### <a name="what-the-notification-looks-like-on-an-iosipados-device"></a>So sieht die Benachrichtigung auf einem iOS-/iPadOS-Gerät aus

Wenn Sie die Unternehmensportal-App auf einem iOS-/iPadOS-Gerät geöffnet haben, ähnelt die Benachrichtigung dem folgenden Screenshot:

> [!div class="mx-imgBorder"]
> ![Unternehmensportal: iOS-/iPadOS-Testbenachrichtigung](./media/custom-notifications/105046-1.png)

Wenn das Gerät gesperrt ist, ähnelt die Benachrichtigung dem folgenden Screenshot:

> [!div class="mx-imgBorder"]
> ![iOS-/iPadOS-Testbenachrichtigung für gesperrte Geräte](./media/custom-notifications/105046-2.png)

### <a name="what-the-notification-looks-like-on-an-android-device"></a>So sieht die Benachrichtigung auf einem Android-Gerät aus

Wenn Sie die Unternehmensportal-App auf einem Android-Gerät geöffnet haben, ähnelt die Benachrichtigung dem folgenden Screenshot:

> [!div class="mx-imgBorder"]
> ![Android-Testbenachrichtigung](./media/custom-notifications/105046-3.png)

## <a name="common-scenarios-for-sending-custom-notifications"></a>Allgemeine Szenarios für das Senden von benutzerdefinierten Benachrichtigungen  

- Informieren Sie alle Mitarbeiter über eine Änderung des Zeitplans, z. B. bei Schließungen von Gebäuden aufgrund schwieriger Wetterbedingungen.
- Senden Sie eine Benachrichtigung an Benutzer einzelner Geräte, um eine dringende Anforderung mitzuteilen, beispielsweise zum Neustart des Geräts, um die Installation eines Updates abzuschließen.

## <a name="considerations-for-using-custom-notifications"></a>Überlegungen zur Verwendung benutzerdefinierter Benachrichtigungen

**Gerätekonfiguration**

- Bevor Benutzer benutzerdefinierte Benachrichtigungen erhalten können, muss die Unternehmensportal-App oder Microsoft Intune-App auf Geräten installiert sein. Außerdem müssen sie über Berechtigungen verfügen, damit die Unternehmensportal-App oder Microsoft Intune-App Pushbenachrichtigungen senden kann. Bei Bedarf können die Unternehmensportal-App und die Microsoft Intune-App Benutzer auffordern, Benachrichtigungen zuzulassen.
- Unter Android ist Google Play Services eine erforderliche Abhängigkeit.
- Auf dem Gerät muss MDM registriert sein.

**Berechtigungen**:

- Um Benachrichtigungen an Gruppen zu senden, muss Ihr Konto über folgende RBAC-Berechtigungen (Role-Based Access Control, rollenbasierte Zugriffssteuerung) in Intune verfügen: *Organisation* > **Update**.
- Um Benachrichtigungen an ein Gerät zu senden, muss Ihr Konto über folgende RBAC-Berechtigungen in Intune verfügen: *Remoteaufgaben* > **Benutzerdefinierte Benachrichtigungen senden**.

**Erstellen von Benachrichtigungen:**
 
- Für das Erstellen von Meldungen muss ein Konto verwendet werden, dem eine Intune-Rolle mit der richtigen Berechtigung zugewiesen ist, wie oben im Abschnitt *Berechtigungen* beschrieben. Informationen zum Zuweisen von Berechtigungen für einen Benutzer finden Sie unter [Rollenzuweisungen](../fundamentals/role-based-access-control.md#role-assignments).
- Benutzerdefinierte Benachrichtigungen sind auf 50 Zeichen lange Titel und 500 Zeichen lange Nachrichten beschränkt.  
- Intune speichert den Text bereits gesendeter benutzerdefinierter Benachrichtigungen nicht. Sie müssen eine Nachricht noch mal erstellen, um sie noch mal zu senden.  
- Sie können maximal 25 Nachrichten pro Stunde an Gruppen senden. Diese Einschränkung gilt für die Mandantenebene. Diese Einschränkung gilt nicht beim Senden von Benachrichtigungen an Einzelpersonen.
- Wenn Sie Nachrichten an einzelne Geräte senden, können Sie nur bis zu 10 Nachrichten pro Stunde an ein und dasselbe Gerät senden.
- Sie können Benachrichtigungen an Gruppen von Benutzern senden. Beim Senden von Benachrichtigungen an Gruppen kann jede Benachrichtigung direkt an bis zu 25 Gruppen gerichtet werden. Verschachtelte Gruppen zählen nicht zu dieser Gesamtanzahl. Benachrichtigungen, die an Gruppen gesendet werden, richten sich nur nach den Benutzern in der jeweiligen Gruppe und werden an alle registrierten iOS-/iPadOS- und Android-Geräte dieser Benutzer gesendet. Die Geräte in der Gruppe werden beim Bestimmen der Benachrichtigungsempfänger nicht berücksichtigt.
- Sie können Benachrichtigungen an einzelne Geräte senden. Anstatt Gruppen zu verwenden, wählen Sie ein Gerät aus und verwenden dann remote eine [Geräteaktion](device-management.md#available-device-actions), um die benutzerdefinierte Benachrichtigung zu senden.

**Lieferung:**

- Intune sendet Nachrichten an die Unternehmensportal-App oder Microsoft Intune-App der Benutzer, die dann die Pushbenachrichtigung erstellt. Benutzer müssen nicht in der App angemeldet sein, damit die Benachrichtigung an das Gerät übermittelt wird, aber das Gerät muss vom Zielbenutzer registriert worden sein.
- Weder Intune noch die Unternehmensportal-App oder die Microsoft Intune-App kann die Zustellung von benutzerdefinierten Benachrichtigungen garantieren. Nach mehreren Stunden Verzögerung werden möglicherweise benutzerdefinierte Benachrichtigungen angezeigt, die dann nicht für dringende Nachrichten verwendet werden sollten.
- Benutzerdefinierte Benachrichtigungsnachrichten von Intune werden auf Geräten als Standardpushbenachrichtigungen angezeigt. Wenn die Unternehmensportal-App auf einem iOS/iPadOS-Gerät beim Empfang der Benachrichtigung geöffnet ist, wird anstelle einer Systempushbenachrichtigung eine Benachrichtigung in der App angezeigt.  
- Benutzerdefinierte Benachrichtigungen können je nach Geräteeinstellungen sowohl auf iOS-/iPadOS- als auch auf Android-Geräten auf dem Sperrbildschirm sichtbar sein.  
- Auf Android-Geräten haben andere Apps möglicherweise Zugriff auf die Daten in Ihren benutzerdefinierten Benachrichtigungen. Verwenden Sie diese nicht für vertrauliche Kommunikation.  
- Benutzer von Geräten, deren Registrierung vor kurzem aufgehoben wurde, und aus einer Gruppe entfernte Benutzer erhalten möglicherweise trotzdem eine benutzerdefinierte Benachrichtigung, die später an diese Gruppe gesendet wurde.  Gleiches gilt, wenn Sie einen Benutzer zu einer Gruppe hinzufügen, nachdem eine benutzerdefinierte Benachrichtigung an die Gruppe gesendet wurde: Es ist möglich, dass der neu hinzugefügte Benutzer diese zuvor gesendete Benachrichtigung empfängt.  

## <a name="send-a-custom-notification-to-groups"></a>Senden einer benutzerdefinierten Benachrichtigung an Gruppen

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) mit einem Konto mit Berechtigung zum Erstellen und Senden von Benachrichtigungen an, und navigieren Sie zu **Mandantenverwaltung** > **Benutzerdefinierte Benachrichtigungen**.  

2. Geben Sie auf der Registerkarte „Basics“ (Grundlagen) das Folgende an, und klicken Sie dann auf **Weiter**, um fortzufahren.  
   - **Titel:** Geben Sie einen Titel für diese Benachrichtigung an. Titel sind auf 50 Zeichen beschränkt.  
   - **Body** (Text): Geben Sie die Nachricht an. Nachrichten sind auf 500 Zeichen beschränkt.

   ![Erstellen einer benutzerdefinierten Benachrichtigung](./media/custom-notifications/custom-notifications.png)  

3. Klicken Sie auf der Registerkarte **Zuweisungen** zuerst auf die Gruppen, an die Sie diese benutzerdefinierte Benachrichtigung senden möchten, und anschließend auf „Weiter“, um fortzufahren. Benachrichtigungen, die an Gruppen gesendet werden, richten sich nur nach den Benutzern in der jeweiligen Gruppe. Die Benachrichtigung wird an alle registrierten iOS-/iPadOS- und Android-Geräte dieser Benutzer gesendet.

4. Überprüfen Sie auf der Registerkarte **Review + Create** (Überprüfen und Erstellen) die Informationen, und klicken Sie dann auf **Erstellen**, wenn Sie zum Senden der Benachrichtigung bereit sind.  

Von Ihnen erstellte Nachrichten werden von Intune sofort verarbeitet. Die einzige Bestätigung für das Senden der Nachricht ist die Intune-Benachrichtigung, die bestätigt, dass die benutzerdefinierte Benachrichtigung gesendet wurde.  

![Bestätigung einer gesendeten Benachrichtigung](./media/custom-notifications/notification-sent.png)  

Intune verfolgt die von Ihnen gesendeten benutzerdefinierten Benachrichtigungen nicht, und der Empfang wird außerhalb des Benachrichtigungscenters des Geräts nicht protokolliert. Die Benachrichtigung kann allerdings in einem temporären Diagnoseprotokoll enthalten sein, wenn ein Benutzer in der Unternehmensportal- oder der Intune-App eine Supportanfrage gestellt hat.

## <a name="send-a-custom-notification-to-a-single-device"></a>Senden einer benutzerdefinierten Benachrichtigung an ein einzelnes Gerät

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) mit einem Konto mit Berechtigung zum Erstellen und Senden von Benachrichtigungen an, und navigieren Sie zu **Geräte** > **Alle Geräte**.

2. Doppelklicken Sie auf den Namen des verwalteten Geräts, an das Sie eine Benachrichtigung senden möchten, um die Seite *Übersicht* für dieses Gerät zu öffnen.

3. Klicken Sie auf der Seite **Übersicht** für das Gerät auf die Geräteaktion **Benutzerdefinierte Benachrichtigung senden**, um den Bereich *Benutzerdefinierte Benachrichtigung senden* zu öffnen. Wenn diese Option nicht verfügbar ist, wählen Sie oben rechts auf der Seite die Option **...** (drei Auslassungspunkte) aus, und klicken Sie dann auf **Benutzerdefinierte Benachrichtigung senden**.

4. Geben Sie im Bereich **Benutzerdefinierte Benachrichtigung senden** die folgenden Details zur Nachricht an:  

   - **Titel:** Geben Sie einen Titel für diese Benachrichtigung an. Titel sind auf 50 Zeichen beschränkt.  
   - **Body** (Text): Geben Sie die Nachricht an. Nachrichten sind auf 500 Zeichen beschränkt.  

5. Wählen Sie **Senden** aus, um die benutzerdefinierte Benachrichtigung an das Gerät zu senden. Im Gegensatz zu Benachrichtigungen, die Sie an Gruppen senden, konfigurieren Sie keine Zuordnung oder überprüfen die Nachricht vor dem Senden.  

Intune verarbeitet die Nachricht sofort. Die einzige Bestätigung dafür, dass die Nachricht gesendet wurde, besteht in der Intune-Benachrichtigung, die Sie in der Konsole erhalten und die den Text der gesendeten Nachricht anzeigt.  

## <a name="receive-a-custom-notification"></a>Empfangen einer benutzerdefinierten Benachrichtigung

Benutzern werden auf einem Gerät benutzerdefinierte Benachrichtigungsnachrichten angezeigt, die von Intune als Standardpushbenachrichtigung von der Unternehmensportal-App oder Microsoft Intune-App gesendet werden. Diese Benachrichtigungen ähneln den Pushbenachrichtigungen, die Benutzer von anderen Apps auf dem Gerät erhalten.  

Wenn die Unternehmensportal-App auf iOS-/iPadOS-Geräten beim Empfang der Benachrichtigung geöffnet ist, wird in der App anstelle einer Pushbenachrichtigung eine Benachrichtigung angezeigt.  

Die Benachrichtigung bleibt so lange erhalten, bis Sie vom Benutzer geschlossen wird.  

## <a name="next-steps"></a>Nächste Schritte

[Verwalten von Geräten](device-management.md)
