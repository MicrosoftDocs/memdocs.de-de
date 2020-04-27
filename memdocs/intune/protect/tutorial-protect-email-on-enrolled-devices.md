---
title: 'Tutorial: Schützen des Exchange Online-E-Mail-Diensts auf verwalteten Geräten'
titleSuffix: Microsoft Intune
description: Erfahren Sie, wie Sie Exchange Online durch Intune-Konformitätsrichtlinien für iOS und den bedingten Azure AD-Zugriff schützen können, indem Sie die Verwendung von verwalteten Geräten und der Outlook-App als obligatorisch festlegen.
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
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 24bdaf71f90e3da84fb26c4b69d9b81f43413c69
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079058"
---
# <a name="tutorial-protect-exchange-online-email-on-managed-devices"></a>Tutorial: Schützen des Exchange Online-E-Mail-Diensts auf verwalteten Geräten

In diesem Artikel erfahren Sie, wie Sie mithilfe von Gerätekonformitätsrichtlinien mit bedingtem Zugriff sicherstellen können, dass iOS-Geräte nur dann auf Exchange Online-E-Mails zugreifen können, wenn sie von Intune verwaltet werden und eine genehmigte E-Mail-App verwenden.

In diesem Tutorial lernen Sie Folgendes:

> [!div class="checklist"]
> * Erstellen einer Intune-iOS-Gerätekonformitätsrichtlinie zum Festlegen der Bedingungen, die ein Gerät erfüllen muss, um als konform angesehen zu werden
> * Erstellen einer Azure Active Directory-Richtlinie (Azure AD) für bedingten Zugriff, die erzwingt, dass iOS-Geräte bei Intune registriert werden, Intune-Richtlinien erfüllen und die genehmigte mobile Outlook-App verwenden, um auf Exchange Online-E-Mails zugreifen zu können

Wenn Sie über kein Intune-Abonnement verfügen, [registrieren Sie sich für eine kostenlose Testversion](../fundamentals/free-trial-sign-up.md).

## <a name="prerequisites"></a>Voraussetzungen

Sie benötigen für dieses Tutorial einen Testmandanten mit den folgenden Abonnements:

- Azure Active Directory Premium ([kostenlose Testversion](https://azure.microsoft.com/free/?WT.mc_id=A261C142F))

- Microsoft 365-Apps für Unternehmen-Abonnement, das Exchange Server ([kostenlose Testversion](https://go.microsoft.com/fwlink/p/?LinkID=510938)) umfasst

Bevor Sie beginnen, erstellen Sie ein Testgeräteprofil für iOS-Geräte, indem Sie die Schritte unter [Schnellstart: Erstellen eines E-Mail-Geräteprofils für iOS/iPadOS](../configuration/quickstart-email-profile.md).

## <a name="sign-in-to-intune"></a>Anmelden bei Intune

Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) als [globaler Administrator](../fundamentals/users-add.md#types-of-administrators) oder [Intune-Dienstadministrator](../fundamentals/users-add.md#types-of-administrators) an. Wenn Sie ein Testabonnement für Intune erstellt haben, besitzt das Konto, mit dem Sie das Abonnement erstellt haben, die Rolle des globalen Administrators.

## <a name="create-the-ios-device-compliance-policy"></a>Erstellen der iOS-Gerätekonformitätsrichtlinie

Richten Sie eine Intune-Gerätekonformitätsrichtlinie ein, um die Bedingungen festzulegen, die ein Gerät erfüllen muss, um als konform angesehen zu werden. Für dieses Tutorial erstellen wir eine Gerätekonformitätsrichtlinie für iOS-Geräte. Konformitätsrichtlinien sind plattformspezifisch, weshalb Sie eine separate Konformitätsrichtlinie für jede Geräteplattform benötigen, die Sie auswerten möchten.

1. Klicken Sie in Intune auf **Geräte** > **Konformitätsrichtlinien** > **Richtlinie erstellen**.

2. Geben Sie als **Namen** **Test für iOS-Konformitätsrichtlinie** ein.

3. Geben Sie als **Beschreibung** **Test für iOS-Konformitätsrichtlinie** ein.

4. Wählen Sie als **Plattform** die Option **iOS/iPadOS** aus.

5. Klicken Sie auf **Einstellungen** > **E-Mail**.

   1. Klicken Sie neben **Verlangen, dass Mobilgeräte über ein verwaltetes E-Mail-Profil verfügen** auf **Erfordern**.

   2. Klicken Sie auf **OK**.

   ![Festlegen der E-Mail-Konformitätsrichtlinie, um ein verwaltetes E-Mail-Profil zu erfordern](./media/tutorial-protect-email-on-enrolled-devices/ios-compliance-policy-email.png)

6. Klicken Sie auf **Geräteintegrität**. Klicken Sie neben **Geräte mit Jailbreak** auf **Blockieren** und dann auf **OK**.

7. Klicken Sie auf **Systemsicherheit**, und geben Sie die **Kennwort**-Einstellungen an. Legen Sie für dieses Tutorial die folgenden empfohlenen Einstellungen fest:

   - Wählen Sie für **Ein Kennwort zum Entsperren von Mobilgeräten anfordern** **Erfordern** aus.

   - Wählen Sie für **Einfache Kennwörter** **Blockieren** aus.

   - Wählen Sie für **Minimale Kennwortlänge** **4** aus.

     > [!TIP]
     > Standardwerte, die ausgegraut und kursiv sind, stellen nur Empfehlungen dar. Sie müssen Empfehlungswerte ersetzen, um Einstellungen zu konfigurieren.

   - Wählen Sie für **Erforderlicher Kennworttyp** **Alphanumerisch** aus.

   - Wählen Sie für **Maximaler Zeitraum, bevor ein Kennwort erforderlich ist** **Sofort** aus.

   - Geben Sie für **Kennwortablauf (Tage)** **41** ein.

   - Geben Sie für **Anzahl vorheriger Kennwörter zum Verhindern der Wiederverwendung** **5** ein.
 
   ![Festlegen der Kennworteinstellungen für die E-Mail-Konformitätsrichtlinie](./media/tutorial-protect-email-on-enrolled-devices/ios-compliance-policy-system-security.png)

8. Klicken Sie auf **OK** und erneut auf **OK**.

9. Wählen Sie **Erstellen** aus.

## <a name="create-the-conditional-access-policy"></a>Erstellen der Richtlinie für bedingten Zugriff

Jetzt erstellen wir eine Richtlinie für bedingten Zugriff, die erzwingt, dass alle Geräteplattformen bei Intune registriert werden und unsere Intune-Konformitätsrichtlinie erfüllen, bevor die Geräte auf Exchange Online zugreifen dürfen. Zudem wird auch die Outlook-App für den E-Mail-Zugriff verlangt. Richtlinien für bedingten Zugriff können im Azure AD-Portal oder im Intune-Portal konfiguriert werden. Da wir uns bereits im Intune-Portal befinden, erstellen wir die Richtlinie über dieses Portal.

1. Klicken Sie in Intune auf **Endpunktsicherheit** > **Bedingter Zugriff** > **Neue Richtlinie**.

2. Geben Sie unter **Name** Folgendes ein: **Testrichtlinie für Office 365-E-Mail**.

3. Klicken Sie unter **Zuweisungen** auf **Benutzer und Gruppen**. Klicken Sie auf der Registerkarte **Einschließen** auf **Alle Benutzer** und dann auf **Fertig**.

4. Wählen Sie unter **Zuweisungen** die Option **Cloud-Apps oder -aktionen** aus. Da wir den Office 365 Exchange Online-E-Mail-Dienst schützen möchten, wählen wir diese in den folgenden Schritten aus:

   1. Klicken Sie auf der Registerkarte **Einschließen** auf **Apps auswählen**.

   2. Klicken Sie auf **Auswählen**. 

   3. Klicken Sie in der Anwendungsliste auf **Office 365 Exchange Online** und dann auf **Auswählen**. 

   4. Wählen Sie **Fertig** aus.
  
   ![Auswählen der Office 365 Exchange Online-App](./media/tutorial-protect-email-on-enrolled-devices/ios-ca-policy-cloud-apps.png)

5. Klicken Sie unter **Zuweisungen** auf **Bedingungen** > **Geräteplattformen**.

   1. Klicken Sie unter **Konfigurieren** auf **Ja**.

   2. Wählen Sie auf der Registerkarte **Einschließen** die Option **Alle Benutzer** und dann **Fertig** aus. 

   3. Klicken Sie erneut auf **Fertig**.

   ![Einschließen beliebiger Geräte](./media/tutorial-protect-email-on-enrolled-devices/ios-ca-policy-cloud-device-platforms.png)

6. Klicken Sie unter **Zuweisungen** auf **Bedingungen** > **Client-Apps**.

   1. Klicken Sie unter **Konfigurieren** auf **Ja**.

   2. Klicken Sie für dieses Tutorial auf **Mobile Apps und Desktopclients** und auf **Clients mit moderner Authentifizierung** (bezieht sich auf Apps wie Outlook für iOS und Outlook für Android). Deaktivieren Sie alle anderen Kontrollkästchen.

   3. Klicken Sie auf **Fertig** und dann erneut auf **Fertig**.

   ![Auswählen von Apps und Clients](./media/tutorial-protect-email-on-enrolled-devices/ios-ca-policy-client-apps.png)

7. Klicken Sie unter **Zugriffssteuerungen** auf **Gewähren**.

   1. Klicken Sie im Bereich **Gewähren** auf **Zugriff gewähren**.

   2. Klicken Sie auf **Markieren des Geräts als konform erforderlich**.

   3. Klicken Sie auf **Genehmigte Client-App erforderlich**.

   4. Klicken Sie unter **Für mehrere Steuerelemente** auf **Alle ausgewählten Kontrollen anfordern**. Durch diese Einstellung wird sichergestellt, dass beide Anforderungen, die Sie ausgewählt haben, erzwungen werden, wenn ein Gerät versucht, auf E-Mails zuzugreifen.

   5. Klicken Sie auf **Auswählen**.

   ![Auswählen von Steuerelementen](./media/tutorial-protect-email-on-enrolled-devices/ios-ca-policy-grant-access.png)

8. Klicken Sie unter **Richtlinie aktivieren** auf **Ein**.

   ![Aktivieren der Richtlinie](./media/tutorial-protect-email-on-enrolled-devices/ios-ca-policy-enable-policy.png)

9. Wählen Sie **Erstellen** aus.

## <a name="try-it-out"></a>Probieren Sie es aus

Mit den von Ihnen erstellten Richtlinien müssen iOS-Geräte, die sich beim Office 365-E-Mail-Dienst anmelden, bei Intune registrieren und die mobile Outlook-App für iOS/iPadOS verwenden. Um dieses Szenario auf iOS-Geräten zu testen, melden Sie sich bei Exchange Online mit den Anmeldeinformationen für einen Benutzer auf Ihrem Testmandanten an. Sie werden aufgefordert, das Gerät zu registrieren und die mobile Outlook-App zu installieren.

1. Um dies auf einem iPhone zu testen, navigieren Sie zu **Einstellungen** > **Kennwörter & Konten** > **Konto hinzufügen** > **Exchange**.

2. Geben Sie die E-Mail-Adresse für einen Benutzer auf Ihrem Testmandanten ein, und klicken Sie dann auf **Weiter**.

3. Klicken Sie auf **Anmelden**.

4. Geben Sie das Kennwort des Testbenutzers ein, und klicken Sie auf **Anmelden**.

5. Eine Meldung wird angezeigt, die besagt, dass Ihr Gerät für den Zugriff auf die Ressource zusammen mit einer Option zur Registrierung verwaltet werden muss.

## <a name="clean-up-resources"></a>Bereinigen der Ressourcen

Wenn die Testrichtlinien nicht mehr benötigt werden, können Sie diese entfernen.
1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) als globaler Administrator oder Intune-Dienstadministrator an.

2. Wählen Sie **Geräte** > **Konformitätsrichtlinien** aus.

3. Rufen Sie in der Liste **Richtlinienname** das Kontextmenü ( **...** ) für Ihre Testrichtlinie auf, und klicken Sie dann auf **Löschen**. Wählen Sie zum Bestätigen **OK** aus.

4. Klicken Sie auf **Endpunktsicherheit** > **Bedingter Zugriff**.

5. Rufen Sie in der Liste **Richtlinienname** das Kontextmenü ( **...** ) für Ihre Testrichtlinie auf, und klicken Sie dann auf **Löschen**. Klicken Sie zum Bestätigen auf **Ja**.

## <a name="next-steps"></a>Nächste Schritte

In diesem Tutorial haben Sie Richtlinien erstellt, die für den Zugriff auf den Exchange Online-E-Mail-Dienst von iOS-Geräten verlangen, sich bei Intune zu registrieren und die Outlook-App zu verwenden. Weitere Informationen zur Verwendung von Intune mit bedingtem Zugriff zum Schutz anderer Apps und Dienste (z.B. Exchange ActiveSync-Clients für Office 365 Exchange Online) finden Sie unter [Was ist bedingter Zugriff?](conditional-access.md).
