---
title: 'Tutorial: Schützen des Exchange Online-E-Mail-Diensts auf nicht verwalteten Geräten'
titleSuffix: Microsoft Intune
description: Erfahren Sie, wie Sie Office 365 Exchange Online mit Intune-App-Schutzrichtlinien und dem bedingten Zugriff von Azure AD sichern.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/21/2019
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f8be97edbbba9a998dd223a5a0e9c8982c1a16a1
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80326594"
---
# <a name="tutorial-protect-exchange-online-email-on-unmanaged-devices"></a>Tutorial: Schützen des Exchange Online-E-Mail-Diensts auf nicht verwalteten Geräten

Erfahren Sie, wie Sie App-Schutzrichtlinien mit bedingtem Zugriff zum Schutz von Exchange Online verwenden, auch wenn Geräte nicht in einer Geräteverwaltungslösung wie Intune registriert sind. In diesem Tutorial lernen Sie Folgendes:

> [!div class="checklist"]
> * Erstellen einer Intune-App-Schutzrichtlinie für die Outlook-App. Sie schränken die möglichen Aktivitäten von Benutzern für App-Daten ein, indem Sie „Speichern unter“-Aktionen ganz verhindern und Optionen zum Ausschneiden, Kopieren und Einfügen begrenzen.
> * Erstellen Sie Richtlinien für bedingten Zugriff in Azure Active Directory (Azure AD), die dafür sorgen, dass die Outlook-App in Exchange Online nur auf Unternehmens-E-Mails zugreifen darf. Sie fordern auch die mehrstufige Authentifizierung (Multi-Factor Authentication, MFA) für Clients mit moderner Authentifizierung wie Outlook für iOS und Android an.

## <a name="prerequisites"></a>Voraussetzungen

Sie benötigen für dieses Tutorial einen Testmandanten mit den folgenden Abonnements:

- Azure Active Directory Premium ([kostenlose Testversion](https://azure.microsoft.com/free/?WT.mc_id=A261C142F))
- Intune-Abonnement ([kostenlose Testversion](../fundamentals/free-trial-sign-up.md))
- Office 365 Business-Abonnement, das Exchange Server ([kostenlose Testversion](https://go.microsoft.com/fwlink/p/?LinkID=510938)) umfasst

## <a name="sign-in-to-intune"></a>Anmelden bei Intune

Melden Sie sich für dieses Tutorial beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) als [globaler Administrator](../fundamentals/users-add.md#types-of-administrators) oder [Intune-Dienstadministrator](../fundamentals/users-add.md#types-of-administrators) an. Wenn Sie ein Testabonnement für Intune erstellt haben, besitzt das Konto, mit dem Sie das Abonnement erstellt haben, die Rolle des Unternehmensadministrators.

## <a name="create-the-app-protection-policy"></a>Erstellen der App-Schutzrichtlinie

In diesem Tutorial richten wir eine Intune-App-Schutzrichtlinie für iOS für die Outlook-App ein, mit der Schutzfunktionen auf App-Ebene aktiviert werden. Wir fordern eine PIN zum Öffnen einer App in einem geschäftlichen Kontext an. Wir beschränken auch die gemeinsame Datennutzung von Apps und verhindern, dass Unternehmensdaten in privaten Speicherorten gespeichert werden.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Klicken Sie auf **Apps** > **App-Schutzrichtlinien** > **Richtlinie erstellen**, und wählen Sie für die Plattform **iOS/iPadOS** aus.

3. Konfigurieren Sie auf der Seite **Basics** (Grundlagen) die folgenden Einstellungen:

   - **Name:** Geben Sie **Outlook-App-Richtlinientest** ein.
   - **Beschreibung:** Geben Sie **Outlook-App-Richtlinientest** ein.

   Der Wert für die **Plattform** wird auf die vorherige Auswahl festgelegt.

   Klicken Sie zum Fortfahren auf **Weiter** .

4. Auf der Seite **Apps** können Sie auswählen, wie Sie diese Richtlinie auf Apps auf verschiedenen Geräten anwenden möchten. Konfigurieren Sie die folgenden Optionen:

   - Für **Target to all app types** (Auf alle App-Typen ausrichten): Wählen Sie **Kein** aus, und aktivieren Sie bei **App-Typen** das Kontrollkästchen für **Apps auf nicht verwalteten Geräten**.
   - Klicken Sie auf **Select public apps** (Öffentliche Apps auswählen). Wählen Sie in der Liste der Apps den Eintrag **Outlook** und dann **Auswählen** aus.  Outlook wird jetzt unter *Public apps* (Öffentliche Apps) angezeigt.

   Klicken Sie zum Fortfahren auf **Weiter** .

5. Auf der Seite **Datenschutz** finden Sie Einstellungen, die bestimmen, wie Benutzer mit den Daten in den Apps interagieren, für die diese App-Schutzrichtlinie gilt. Konfigurieren Sie die folgenden Optionen:

   Konfigurieren Sie unter *Datenübertragung* die folgenden Einstellungen, und behalten Sie für alle anderen Einstellungen die Standardwerten bei:

   - Wählen Sie für **Send org data to other apps** (Organisationsdaten an andere Apps senden) die Option **Keine** aus.  
   - Wählen Sie für **Daten von anderen Apps empfangen** die Option **Keine** aus.  
   - Wählen Sie für **Save copies of org data** (Kopien von Organisationsdaten speichern) die Option **Blockieren** aus.  
   - Wählen Sie für **Ausschneiden, Kopieren und Einfügen zwischen anderen Apps einschränken** die Option **Blockiert** aus. 

   ![Auswählen der Einstellungen für die Datenverschiebung im Rahmen der Outlook-App-Schutzrichtlinie](./media/tutorial-protect-email-on-unmanaged-devices/data-protection-settings.png)

   Wählen Sie **Weiter** aus, um den Vorgang fortzusetzen.

6. Auf der Seite **Access requirements** (Erforderliche Zugriffsberechtigungen) finden Sie Einstellungen, mit denen Sie die PIN und die Anforderungen bezüglich der Anmeldeinformationen konfigurieren können, die Benutzer für den Zugriff auf Apps in einem Arbeitskontext erfüllen müssen. Konfigurieren Sie die folgenden Einstellungen, und behalten Sie für alle anderen Einstellungen die Standardwerten bei:

   - Wählen Sie für **PIN für Zugriff** die Option **Anfordern** aus.
   - Wählen Sie für **Anmeldeinformationen für Geschäfts-, Schul- oder Unikonto für Zugriff** die Option **Anfordern** aus.

   ![Auswählen der Zugriffsaktionen im Rahmen der Outlook-App-Schutzrichtlinie](./media/tutorial-protect-email-on-unmanaged-devices/access-requirements-settings.png)

   Wählen Sie **Weiter** aus, um den Vorgang fortzusetzen.

7. Auf der Seite **Conditional launch** (Bedingter Start) finden Sie Einstellungen zum Festlegen der Sicherheitsanforderungen für Anmeldeinformationen für die App-Schutzrichtlinien. Für dieses Tutorial müssen Sie diese Einstellungen nicht konfigurieren.

   Klicken Sie zum Fortfahren auf **Weiter** .

8. Verwenden Sie die Seite **Zuweisungen**, um die App-Schutzrichtlinie bestimmten Gruppen von Benutzern zuzuweisen. In diesem Tutorial weisen Sie diese Richtlinie keiner Gruppe zu.  
 Sie müssen diese Einstellungen nicht konfigurieren.

   Klicken Sie zum Fortfahren auf **Weiter** .

9. Überprüfen Sie auf der Seite **Next: Review and create** (Weiter: Überprüfen und erstellen) die Werte und Einstellungen, die Sie für diese App-Schutzrichtlinie eingegeben haben. Klicken Sie auf **Erstellen**, um die App-Schutzrichtlinie in Intune zu erstellen.

Die App-Schutzrichtlinie für Outlook wird erstellt. Als Nächstes richten Sie den bedingten Zugriff ein, um zu erzwingen, dass Geräte die Outlook-App verwenden.

## <a name="create-conditional-access-policies"></a>Erstellen von Richtlinien für bedingten Zugriff

Nun erstellen wir zwei Richtlinien für bedingten Zugriff, um alle Geräteplattformen abzudecken.  

- Die erste Richtlinie erfordert, dass Clients mit moderner Authentifizierung die genehmigte Outlook-App und mehrstufige Authentifizierung (Multi-Factor Authentication, MFA) verwenden. Clients mit moderner Authentifizierung enthalten Outlook für iOS und Outlook für Android.  

- Die zweite Richtlinie erfordert, dass Exchange ActiveSync-Clients die genehmigte Outlook-App verwenden. (Zurzeit unterstützt Exchange Active Sync keine anderen Bedingungen als die Geräteplattform). Sie können Richtlinien für bedingten Zugriff im Azure AD-Portal oder im Intune-Portal konfigurieren. Da wir uns bereits im Intune-Portal befinden, erstellen wir die Richtlinie über dieses Portal.  

### <a name="create-an-mfa-policy-for-modern-authentication-clients"></a>Erstellen einer MFA-Richtlinie für Clients mit moderner Authentifizierung  

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Endpunktsicherheit** >  **Bedingter Zugriff** > **Neue Richtlinie** aus.  

3. Geben Sie **Testrichtlinie für Clients mit moderner Authentifizierung** als **Name** ein.  

4. Klicken Sie unter **Zuweisungen** auf **Benutzer und Gruppen**. Klicken Sie auf der Registerkarte **Einschließen** auf **Alle Benutzer** und dann auf **Fertig**.

5. Wählen Sie unter **Zuweisungen** die Option **Cloud-Apps oder -aktionen** aus. Da wir den Office 365 Exchange Online-E-Mail-Dienst schützen möchten, wählen wir diese in den folgenden Schritten aus:

   1. Klicken Sie auf der Registerkarte **Einschließen** auf **Apps auswählen**.
   2. Klicken Sie auf **Auswählen**.
   3. Wählen Sie in der Anwendungsliste **Office 365 Exchange Online** und dann **Auswählen** aus.
   4. Wählen Sie **Fertig** aus, um zum Bereich „Neue Richtlinie“ zurückzukehren.

   ![Auswählen der Office 365 Exchange Online-App](./media/tutorial-protect-email-on-unmanaged-devices/modern-auth-policy-cloud-apps.png)

6. Klicken Sie unter **Zuweisungen** auf **Bedingungen** > **Geräteplattformen**.

   1. Klicken Sie unter **Konfigurieren** auf **Ja**.
   2. Wählen Sie auf der Registerkarte **Einschließen** die Option **Jedes Gerät** aus.
   3. Wählen Sie **Fertig** aus.

7. Wählen Sie im Bereich **Bedingungen** die Option **Client-Apps** aus.

   1. Klicken Sie unter **Konfigurieren** auf **Ja**.
   2. Wählen Sie **Mobile Apps und Desktopclients** und **Clients mit moderner Authentifizierung** aus.
   3. Deaktivieren Sie alle anderen Kontrollkästchen.
   4. Wählen Sie **Fertig** > **Fertig** aus, um zum Bereich „Neue Richtlinie“ zurückzukehren.

   ![Auswählen von Mobile-Apps und -Clients](./media/tutorial-protect-email-on-unmanaged-devices/modern-auth-policy-client-apps.png)

8. Klicken Sie unter **Zugriffssteuerungen** auf **Gewähren**.

   1. Klicken Sie im Bereich **Gewähren** auf **Zugriff gewähren**.
   2. Wählen Sie **Mehrstufige Authentifizierung erforderlich** aus.
   3. Klicken Sie auf **Genehmigte Client-App erforderlich**.
   4. Klicken Sie unter **Für mehrere Steuerelemente** auf **Alle ausgewählten Kontrollen anfordern**. Durch diese Einstellung wird sichergestellt, dass beide Anforderungen, die Sie ausgewählt haben, erzwungen werden, wenn ein Gerät versucht, auf E-Mails zuzugreifen.
   5. Klicken Sie auf **Auswählen**.

   ![Auswählen von Zugriffssteuerungen](./media/tutorial-protect-email-on-unmanaged-devices/modern-auth-policy-mfa.png)

9. Wählen Sie unter **Richtlinie aktivieren** die Option **Ein** und dann **Erstellen** aus.

   ![Erstellen von Richtlinien](./media/tutorial-protect-email-on-unmanaged-devices/enable-policy.png)  

Die Richtlinie für bedingten Zugriff für Clients mit moderner Authentifizierung wird erstellt. Jetzt können Sie eine Richtlinie für Exchange Active Sync-Clients erstellen.

### <a name="create-a-policy-for-exchange-active-sync-clients"></a>Erstellen einer Richtlinie für Exchange Active Sync-Clients

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Endpunktsicherheit** > **Bedingter Zugriff** > **Neue Richtlinie** aus.

3. Geben Sie **Testrichtlinie für EAS-Clients** als **Name** ein.

4. Klicken Sie unter **Zuweisungen** auf **Benutzer und Gruppen**. Klicken Sie auf der Registerkarte *Einschließen* auf **Alle Benutzer** und dann auf **Fertig**.

5. Wählen Sie unter **Zuweisungen** die Option **Cloud-Apps oder -aktionen** aus. Wählen Sie die Option für Office 365 Exchange Online-E-Mail folgendermaßen aus:

   1. Klicken Sie auf der Registerkarte *Einschließen* auf **Apps auswählen**.
   2. Klicken Sie auf **Auswählen**.
   3. Wählen Sie in der Liste der *Anwendungen* die Option **Office 365 Exchange Online**, anschließend **Auswählen** und dann **Fertig** aus.
  
6. Klicken Sie unter **Zuweisungen** auf **Bedingungen** > **Geräteplattformen**.

   1. Klicken Sie unter **Konfigurieren** auf **Ja**.
   2. Wählen Sie auf der Registerkarte **Einschließen** die Option **Alle Benutzer** und dann **Fertig** aus.

7. Wählen Sie im Bereich **Bedingungen** die Option **Client-Apps** aus.

   1. Klicken Sie unter **Konfigurieren** auf **Ja**.
   2. Wählen Sie **Mobile Apps und Desktopclients** aus.
   3. Wählen Sie **Exchange ActiveSync-Clients** und **Richtlinie nur auf unterstützte Plattformen anwenden** aus.  
   4. Deaktivieren Sie alle anderen Kontrollkästchen.  
   5. Klicken Sie auf **Fertig** und dann erneut auf **Fertig**.  

   ![Anwenden auf unterstützte Plattformen](./media/tutorial-protect-email-on-unmanaged-devices/eas-client-apps.png)  

8. Klicken Sie unter **Zugriffssteuerungen** auf **Gewähren**.

   1. Klicken Sie im Bereich **Gewähren** auf **Zugriff gewähren**.
   2. Klicken Sie auf **Genehmigte Client-App erforderlich**. Deaktivieren Sie alle anderen Kontrollkästchen.
   3. Klicken Sie auf **Auswählen**.

   ![Voraussetzen genehmigter Client-Apps](./media/tutorial-protect-email-on-unmanaged-devices/eas-grant-access.png)

9. Wählen Sie unter **Richtlinie aktivieren** die Option **Ein** und dann **Erstellen** aus.

Die App-Schutzrichtlinien und der bedingte Zugriff sind jetzt eingerichtet und können getestet werden.

## <a name="try-it-out"></a>Probieren Sie es aus

Mit den von Ihnen erstellten Richtlinien müssen Geräte sich bei Intune registrieren und die mobile Outlook-App verwenden, um auf Office 365-E-Mails zuzugreifen. Um dieses Szenario auf iOS-Geräten zu testen, melden Sie sich bei Exchange Online mit den Anmeldeinformationen für einen Benutzer auf Ihrem Testmandanten an.

1. Um dies auf einem iPhone zu testen, navigieren Sie zu **Einstellungen** > **Kennwörter & Konten** > **Konto hinzufügen** > **Exchange**.

2. Geben Sie die E-Mail-Adresse für einen Benutzer auf Ihrem Testmandanten ein, und klicken Sie dann auf **Weiter**.  
3. Klicken Sie auf **Anmelden**.

4. Geben Sie das Kennwort des Testbenutzers ein, und klicken Sie auf **Anmelden**.

5. Die Meldung **Es sind weitere Informationen erforderlich** wird angezeigt, mit der Sie aufgefordert werden, die mehrstufige Authentifizierung einzurichten. Richten Sie eine zusätzliche Überprüfungsmethode ein.

6. Danach werden Sie in einer Meldung darüber informiert, dass Sie versuchen, diese Ressource mit einer App zu öffnen, die von Ihrer IT-Abteilung nicht genehmigt ist. Die Meldung bedeutet, dass die Nutzung der nativen Mail-App für Sie gesperrt ist. Brechen Sie die Anmeldung ab.

7. Öffnen Sie die Outlook-App, und klicken Sie auf **Einstellungen** > **Konto hinzufügen** > **E-Mail-Konto hinzufügen**.

8. Geben Sie die E-Mail-Adresse für einen Benutzer auf Ihrem Testmandanten ein, und klicken Sie dann auf **Weiter**.

9. Klicken Sie auf **Mit Office 365 anmelden**. Sie werden aufgefordert, weitere Authentifizierungs- und Registrierungsinformationen anzugeben. Nachdem Sie sich angemeldet haben, können Sie Aktionen wie „Ausschneiden“, „Kopieren“, „Einfügen“ und „Speichern unter“ testen.

## <a name="clean-up-resources"></a>Bereinigen der Ressourcen

Wenn die Testrichtlinien nicht mehr benötigt werden, können Sie diese entfernen.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Geräte** und dann **Kompatibilitätsrichtlinien** aus.

3. Rufen Sie in der Liste **Richtlinienname** das Kontextmenü ( **...** ) für Ihre Testrichtlinie auf, und klicken Sie dann auf **Löschen**. Wählen Sie zum Bestätigen **OK** aus.

4. Klicken Sie auf **Endpoint security** > **Bedingter Zugriff** (Endpunktsicherheit).

5. Öffnen Sie in der Liste **Richtlinienname** das Kontextmenü ( **...** ) für jede Ihrer Testrichtlinien, und klicken Sie dann auf **Löschen**. Klicken Sie zum Bestätigen auf **Ja**.

## <a name="next-steps"></a>Nächste Schritte
In diesem Tutorial haben Sie App-Schutzrichtlinien erstellt, um die Aktionen einzuschränken, die ein Benutzer in der Outlook-App ausführen kann. Sie haben zudem Richtlinien für bedingten Zugriff erstellt, um die Outlook-App sowie die mehrstufige Authentifizierung für Clients mit moderner Authentifizierung zu erzwingen. Weitere Informationen zur Verwendung von Intune mit bedingtem Zugriff zum Schutz von anderen Apps und Diensten finden Sie unter [Was ist bedingter Zugriff?](conditional-access.md).
