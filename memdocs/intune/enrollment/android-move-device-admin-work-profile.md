---
title: Verschieben von Android-Geräten aus dem Geräteadministrator in die Arbeitsprofilverwaltung
titleSuffix: Microsoft Intune
description: Verschieben Sie Android-Geräte aus dem Geräteadministrator in die Arbeitsprofilverwaltung in Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b66777e9c108ab4a6b84e4d4fa0942532685912f
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086727"
---
# <a name="move-android-devices-from-device-administrator-to-work-profile-management"></a>Verschieben von Android-Geräten aus dem Geräteadministrator in die Arbeitsprofilverwaltung

Sie können Benutzer dabei unterstützen, ihre Android-Geräte aus dem Geräteadministrator in die Arbeitsprofilverwaltung zu verschieben, indem Sie die Konformitätseinstellung **Mit dem Geräteadministrator verwaltete Geräte blockieren** verwenden. Mit dieser Einstellung können Sie Geräte als nicht konform einstufen, wenn diese über den Geräteadministrator verwaltet werden. 

Wenn Benutzer bemerken, dass ihr Gerät aus diesem Grund nicht mehr konform ist, können sie auf **Auflösen** tippen. Den Benutzern wird eine Prüfliste angezeigt, die sie durch folgende Aufgaben führt:
1. Aufheben der Registrierung in der Geräteadministratorverwaltung
2. Registrieren bei der Arbeitsprofilverwaltung
3. Lösen von Konformitätsproblemen 

## <a name="prerequisites"></a>Voraussetzungen

- Benutzer müssen über [beim Android-Geräteadministrator registrierte Geräte](android-enroll-device-administrator.md) mit dem Android-Unternehmensportal der Version 5.0.4720.0 oder höher verfügen.
- Richten Sie die Android-Arbeitsprofilverwaltung ein, indem Sie [eine Verbindung von Ihrem Intune-Mandantenkonto mit Ihrem Android Enterprise-Konto herstellen](connect-intune-android-enterprise.md).
- Legen Sie die [Android Enterprise-Arbeitsprofilregistrierung](android-work-profile-enroll.md) für die Gruppe von Benutzern fest, die zum Android-Arbeitsprofil wechseln.
- Erhöhen Sie ggf. die Limits für Benutzergeräte. Wenn Sie die Registrierung von Geräten bei der Geräteadministratorverwaltung aufheben, werden Datensätze für Geräte u. U. nicht sofort entfernt. Um für diesen Zeitraum über genügend Puffer zu verfügen, müssen Sie möglicherweise das Gerätelimit erhöhen, sodass die Benutzer sich bei der Arbeitsprofilverwaltung registrieren können.
  - [Konfigurieren Sie die Azure Active Directory-Geräteeinstellungen](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal.md#configure-device-settings) für die maximale Anzahl von Geräten pro Benutzer.
  - Passen Sie die [Intune-Gerätelimiteinschränkungen](enrollment-restrictions-set.md#create-a-device-limit-restriction) an, indem Sie das Gerätelimit festlegen. 

## <a name="create-device-compliance-policy"></a>Erstellen einer Gerätekonformitätsrichtlinie

1. Wählen Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) die Option **Geräte** > **Konformitätsrichtlinien** > **Richtlinien** > **Richtlinie erstellen** aus.

    ![Erstellen von Richtlinien](./media/android-move-device-admin-work-profile/create-policy.png)

2. Legen Sie auf der Seite **Richtlinie erstellen** die Option **Plattform** auf **Android-Geräteadministrator** fest, und klicken Sie auf **Erstellen**.
3. Geben Sie auf der Seite **Grundlagen** den **Namen** und eine **Beschreibung** ein, und klicken Sie auf **Weiter**.

    ![Seite „Grundlagen“](./media/android-move-device-admin-work-profile/basics.png)
    
4. Legen Sie auf der Seite **Konformitätseinstellungen** im Abschnitt **Geräteintegrität** die Option **Mit dem Geräteadministrator verwaltete Geräte blockieren** auf **Ja** fest, und klicken Sie auf **Weiter**.

    ![Blockieren von Geräten](./media/android-move-device-admin-work-profile/block-devices.png)

5. Auf der Seite **Standorte** können Sie bei Bedarf Standorte hinzufügen. Klicken Sie dann auf **Weiter**.
6. Bei den **Aktionen bei Nichtkonformität** können Sie die Aktion **E-Mail an Endbenutzer senden** festlegen.

    ![Senden von E-Mails](./media/android-move-device-admin-work-profile/send-email.png)


    In der E-Mail-Nachricht an Benutzer können Sie die folgende URL angeben. Mit dieser URL wird das Android-Unternehmensportal auf der Seite **Geräteeinstellungen aktualisieren** geöffnet. Auf dieser Seite startet der Flow für den Wechsel zur Arbeitsprofilverwaltung.
    - [https://portal.manage.microsoft.com/UpdateSettings.aspx](https://portal.manage.microsoft.com/UpdateSettings.aspx).
    - Für US-Regierungsorganisationen können Sie stattdessen diesen Link verwenden: [https://portal.manage.microsoft.us/UpdateSettings.aspx](https://portal.manage.microsoft.us/UpdateSettings.aspx).
  
    > [!NOTE]
    > - Natürlich können Sie in Ihren Mitteilungen an Benutzer auch benutzerfreundlichen Hypertext für die Links verwenden. Verkürzen Sie URLs jedoch nicht, da die Links in diesem Fall möglicherweise nicht funktionieren.
    > - Wenn das Android-Unternehmensportal im Hintergrund offen ist und der Benutzer auf den Link tippt, wird er möglicherweise auf die zuletzt im Portal geöffnete Seite weitergeleitet.

    Wählen Sie **Weiter** aus.

7. Wählen Sie auf der Seite **Bereichstags** alle Bereichstags aus, die Sie einschließen möchten.
8. Weisen Sie die Richtlinie auf der Seite **Zuweisungen** einer Gruppe zu, für die Geräte in der Geräteadministratorverwaltung registriert sind. Klicken Sie dann auf **Weiter**.
9. Bestätigen Sie auf der Seite **Überprüfen + erstellen** alle Einstellungen, und wählen Sie dann **Erstellen** aus.

## <a name="troubleshooting"></a>Problembehandlung

Der [Endbenutzerflow zum Wechsel in die neue Geräteverwaltung](https://docs.microsoft.com/mem/intune/user-help/move-to-new-device-management-setup.md) leitet Benutzer durch den Prozess zum Aufheben der Registrierung bei der Geräteadministratorverwaltung und zum Einrichten der Arbeitsprofilverwaltung. Benutzer müssen über [beim Android-Geräteadministrator registrierte Geräte](android-enroll-device-administrator.md) mit dem Android-Unternehmensportal der Version 5.0.4720.0 oder höher verfügen.

### <a name="user-sees-an-error-after-tapping-resolve"></a>Benutzern wird nach dem Tippen auf „Auflösen“ ein Fehler angezeigt
Wenn Benutzern nach dem Tippen auf die Schaltfläche **Auflösen**n ein Fehler angezeigt wird, liegt wahrscheinlich einer der folgenden Gründe vor:
- Die Registrierung des Arbeitsprofils ist nicht ordnungsgemäß eingerichtet (ein Android Enterprise-Konto ist nicht verbunden, oder die Registrierungseinschränkungen sind so festgelegt, dass die Arbeitsprofilregistrierung blockiert wird).
- Auf dem Gerät wird Android 4.4 oder früher ausgeführt – diese Version unterstützt die Registrierung von Arbeitsprofilen nicht. 
- Der Gerätehersteller unterstützt die Registrierung von Arbeitsprofilen auf dem Gerätemodell nicht.

### <a name="resolve-button-doesnt-appear-on-the-users-device"></a>Die Schaltfläche zum Auflösen wird auf dem Benutzergerät nicht angezeigt
Die Schaltfläche **Auflösen** wird auf dem Gerät des Benutzers nicht angezeigt, wenn der Benutzer sich bei der Geräteadministratorverwaltung registriert, nachdem die oben erläuterte Gerätekonformitätsrichtlinie für den Benutzer eingerichtet wurde.

Damit die Schaltfläche **Auflösen** angezeigt wird, muss der Benutzer die Einrichtung verschieben und den Prozess aus der Benachrichtigung erneut starten.

Um diese Situation zu vermeiden, verwenden Sie Registrierungsbeschränkungen, um die Registrierung bei der Gerätadministratorverwaltung zu blockieren.

### <a name="user-sees-an-error-after-tapping-url-to-update-device-settings-page"></a>Benutzern wird nach dem Tippen auf die URL zur Seite „Geräteeinstellungen aktualisieren“ ein Fehler angezeigt
Wenn Benutzer auf die URL tippen, die sie zur Seite **Geräteeinstellungen aktualisieren** im Android-Unternehmensportal leitet, wird möglicherweise im Browser eine Fehlerseite angezeigt. Für diesen Fehler können folgende Ursachen vorliegen:
- Das Gerät ist kein Android-Gerät.
- Auf dem Android-Gerät ist die Unternehmensportal-App nicht installiert.
- Die Version des Android-Unternehmensportals ist niedriger als 5.0.4720.0.
- Das Gerät verwendet Android 6 oder früher. 

## <a name="next-steps"></a>Nächste Schritte
[Endbenutzerflow](https://docs.microsoft.com/mem/intune/user-help/move-to-new-device-management-setup.md)

[Verwalten von Android-Arbeitsprofilgeräten mit Intune](android-enterprise-overview.md)

