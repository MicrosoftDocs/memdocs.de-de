---
title: Konfigurieren von E-Mail-Einstellungen in Microsoft Intune – Azure | Microsoft-Dokumentation
titleSuffix: ''
description: Erstellen Sie ein E-Mail-Profil in Microsoft Intune, und stellen Sie dieses Profil im Android-Geräteadministrator sowie auf Android Enterprise-, iOS-, iPadOS- und Windows-Geräten bereit. Verwenden Sie E-Mail-Profile, um allgemeine E-Mail-Einstellungen zu konfigurieren, einschließlich E-Mail-Server und Authentifizierungsmethoden für die Verbindungsherstellung mit Unternehmens-E-Mails auf von Ihnen verwalteten Geräten.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 99f3dcd944270acef98cc0f1f06138d75dba4453
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996417"
---
# <a name="add-email-settings-to-devices-using-intune"></a>Hinzufügen von E-Mail-Einstellungen für Geräte mit Intune

Microsoft Intune umfasst verschiedene E-Mail-Einstellungen, die Sie für Geräte in Ihrer Organisation bereitstellen können. Ein IT-Administrator kann E-Mail-Profile mit spezifischen Einstellungen für die Verbindungsherstellung mit einem E-Mail-Server – z.B. Microsoft 365 und Gmail – erstellen. Endbenutzer können anschließend über ihre mobilen Geräte eine Verbindung mit ihren Organisations-E-Mail-Konten herstellen, sich authentifizieren und eine Synchronisierung durchführen. Durch das Erstellen und Bereitstellen eines E-Mail-Profils können Sie sicherstellen, dass geräteübergreifend Standardeinstellungen verwendet werden. Außerdem kann dies die Anzahl von Anrufen beim Support durch Benutzer verringern, die nicht die richtigen E-Mail-Einstellungen kennen.

Sie können E-Mail-Profile verwenden, um die integrierten E-Mail-Einstellungen auf den folgenden Geräten zu konfigurieren:

- Android-Geräteadministrator auf Geräten mit Samsung Knox Standard 5.0 und höher
- Android Enterprise
- iOS 11.0 und neuer
- iOS 13.0 und höher
- Windows 10 (Desktop)

Dieser Artikel zeigt, wie Sie ein E-Mail-Profil in Microsoft Intune erstellen. Außerdem werden Links zu verschiedenen Plattformen mit Informationen zu spezifischeren Einstellungen bereitgestellt.

## <a name="create-the-profile"></a>Erstellen des Profils

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
3. Geben Sie die folgenden Eigenschaften ein:

    - **Plattform**: Wählen Sie die Plattform Ihrer Geräte aus. Folgende Optionen sind verfügbar:  

        - **Android-Geräteadministrator** (nur Samsung Android Knox Standard)
        - **Android Enterprise**
        - **iOS/iPadOS**
        - **Windows 10 und höher**

    - **Profil**: Wählen Sie **E-Mail** aus.

4. Wählen Sie **Erstellen** aus.
5. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:

    - **Name:** Geben Sie einen aussagekräftigen Namen für die Richtlinie ein. Benennen Sie Ihre Richtlinien so, dass Sie diese später leicht wiedererkennen. Ein guter Richtlinienname ist beispielsweise **Windows 10: E-Mail-Einstellungen für alle Windows 10-Geräte**.
    - **Beschreibung:** Geben Sie eine Beschreibung für die Richtlinie ein. Diese Einstellung ist optional, wird jedoch empfohlen.

6. Wählen Sie **Weiter** aus.

7. Die verfügbaren **Konfigurationseinstellungen** variieren je nach ausgewählter Plattform. Wählen Sie Ihre Plattform für detaillierte Einstellungen aus:

    - [Android-Geräteadministrator (Samsung Knox Standard)](email-settings-android.md)
    - [Android Enterprise](email-settings-android-enterprise.md)
    - [iOS/iPadOS](email-settings-ios.md)
    - [Windows 10](email-settings-windows-10.md)

8. Wählen Sie **Weiter** aus.
9. Weisen Sie in **Bereichstags** (optional) ein Tag zu, um das Profil nach bestimmten IT-Gruppen wie `US-NC IT Team` oder `JohnGlenn_ITDepartment` zu filtern. Weitere Informationen zu Bereichstags finden Sie unter [Verwenden der RBAC und von Bereichstags für verteilte IT](../fundamentals/scope-tags.md).

    Wählen Sie **Weiter** aus.

10. Wählen Sie unter **Zuweisungen** die Benutzer oder Gerätegruppen aus, denen das Profil zugewiesen werden soll. Weitere Informationen zum Zuweisen von Profilen finden Sie im Abschnitt [Was Sie wissen müssen](#what-you-need-to-know) (in diesem Artikel) oder unter [Zuweisen von Benutzer- und Geräteprofilen in Microsoft Intune](device-profile-assign.md).

    Wählen Sie **Weiter** aus.

11. Überprüfen Sie die Einstellungen unter **Überprüfen + erstellen**. Wenn Sie auf **Erstellen** klicken, werden die Änderungen gespeichert, und das Profil wird zugewiesen. Die Richtlinie wird auch in der Profilliste angezeigt.

## <a name="what-you-need-to-know"></a>Was Sie wissen müssen

- E-Mail-Profile werden für den Benutzer bereitgestellt, der das Gerät registriert hat. Für die Konfiguration des E-Mail-Profils werden in Intune die Azure AD-Eigenschaften (Azure Active Directory) des E-Mail-Benutzerprofils bei der Anmeldung verwendet.

- In Microsoft Outlook für iOS-/iPadOS- und Android-Geräte werden E-Mail-Profile nicht unterstützt. Stellen Sie stattdessen eine Konfigurationsrichtlinie für Apps bereit. Weitere Informationen finden Sie unter [Microsoft Outlook-Konfigurationseinstellungen](../apps/app-configuration-policies-outlook.md).

  Stellen Sie auf Android Enterprise-Geräten über den verwalteten Google Play Store Gmail oder Nine for Work bereit. Eine Anleitung hierzu finden Sie unter [Hinzufügen verwalteter Google Play-Apps](../apps/apps-add-android-for-work.md).

- E-Mail basiert auf Identitäts- und Benutzereinstellungen. E-Mail-Profile werden in der Regel Benutzergruppen zugewiesen und nicht Gerätegruppen. Daher sollten Sie Folgendes berücksichtigen:

  - Enthält das E-Mail-Profil Benutzerzertifikate, weisen Sie es Benutzergruppen zu. Möglicherweise verfügen Sie über mehrere zugewiesene Benutzerzertifikatprofile. Dies führt zu einer Kette von Profilbereitstellungen. Stellen Sie diese Profilkette für Benutzergruppen bereit.

    Wenn ein Profil in dieser Kette für eine Gerätegruppe bereitgestellt wird, werden Benutzer möglicherweise kontinuierlich dazu aufgefordert, ihr Kennwort einzugeben.

  - Gerätegruppen werden in der Regel verwendet, wenn kein primärer Benutzer vorhanden ist oder nicht bekannt ist, wer der Benutzer sein wird. E-Mail-Profile, deren Ziel Gerätegruppen (und nicht Benutzergruppen) sind, werden möglicherweise nicht an das Gerät übermittelt.

    Wenn Ihr E-Mail-Profil z. B. für eine Gerätegruppe nur aus iOS-/iPadOS-Geräten gedacht ist, stellen Sie sicher, dass alle diese Geräte über einen Benutzer verfügen. Verfügt ein Gerät über keinen Benutzer, so wird das E-Mail-Profil möglicherweise nicht bereitgestellt. Dann beschränken Sie das Profil und könnten einige Geräte übersehen. Verfügt das Gerät über einen primären Benutzer, sollte das Bereitstellen für Gerätegruppen funktionieren.

    Weitere Informationen zu möglichen Problemen bei der Verwendung von Gerätegruppen finden Sie unter [Häufig auftretende Probleme und Lösungen für E-Mail-Profile in Microsoft Intune](troubleshoot-email-profiles-in-microsoft-intune.md).

## <a name="remove-an-email-profile"></a>Entfernen eines E-Mail-Profils

Es gibt verschiedene Möglichkeiten, ein E-Mail-Profil von einem Gerät zu entfernen, auch wenn nur ein E-Mail-Profil vorhanden ist:

- **Option 1**: Öffnen Sie das E-Mail-Profil (**Geräte** > **Konfigurationsprofile** > wählen Sie Ihr Profil aus), und wählen Sie **Zuweisungen** aus. Auf der Registerkarte **Einschließen** werden die Gruppen angezeigt, denen das Profil zugewiesen ist. Klicken Sie mit der rechten Maustaste auf die Gruppe, und wählen Sie dann **Entfernen**. Klicken Sie auf **Speichern**, um die Änderungen zu speichern.

- **Option 2**: [Setzen Sie das Gerät zurück, oder nehmen Sie es außer Betrieb.](../remote-actions/devices-wipe.md) Mit diesen Optionen können Sie einige oder alle Daten und Einstellungen entfernen.

## <a name="secure-email-access"></a>Sicherer E-Mail-Zugriff

E-Mail-Profile können mit einer dieser Optionen geschützt werden:

- **Zertifikate:** Beim Erstellen des E-Mail-Profils wählen Sie ein Zertifikatprofil aus, das Sie zuvor in Intune erstellt haben. Dieses Zertifikat wird als Identitätszertifikat bezeichnet. Es dient zur Authentifizierung anhand eines vertrauenswürdigen Zertifikatprofils oder eines Stammzertifikats, um zu bestätigen, dass das Gerät des Benutzers eine Verbindung herstellen darf. Das vertrauenswürdige Zertifikat wird dem Computer zugewiesen, der die E-Mail-Verbindung authentifiziert. Dies ist in der Regel der native E-Mail-Server.

  Wenn Sie zertifikatbasierte Authentifizierung für Ihr E-Mail-Profil verwenden, stellen Sie das E-Mail-Profil, das Zertifikatprofil und das vertrauenswürdige Stammprofil für dieselben Gruppen bereit. Mit dieser Bereitstellung wird sichergestellt, dass jedes Gerät die Rechtmäßigkeit Ihrer Zertifizierungsstelle erkennen kann.

  Weitere Informationen zum Erstellen und Verwenden von Zertifikatprofilen in Intune finden Sie unter [Konfigurieren von Zertifikaten mit Intune](../protect/certificates-configure.md).

- **Benutzername und Kennwort**: Der Endbenutzer authentifiziert sich beim nativen Mailserver durch Eingabe eines Benutzernamens und Kennworts. Das Kennwort ist nicht im E-Mail-Profil enthalten. Deshalb muss der Endbenutzer das Kennwort eingeben, wenn eine Verbindung mit dem E-Mail-Postfach hergestellt wird.

## <a name="how-intune-handles-existing-email-accounts"></a>Behandlung vorhandener E-Mail-Konten in Intune

Wenn der Benutzer bereits ein E-Mail-Konto konfiguriert hat, wird das E-Mail-Profil je nach Plattform unterschiedlich zugewiesen.

- **iOS/iPadOS:** Basierend auf dem Hostnamen und der E-Mail-Adresse wird ein vorhandenes doppeltes E-Mail-Profil erkannt. Das doppelte E-Mail-Profil verhindert die Zuweisung eines Intune-Profils. In diesem Fall benachrichtigt das Unternehmensportal den Endbenutzer über die fehlende Konformität und fordert ihn auf, das konfigurierte E-Mail-Profil manuell zu entfernen. Weisen Sie Ihre Endbenutzer an, sich *vor* der Installation eines E-Mail-Profils zu registrieren und die Einrichtung des Profils durch Intune zuzulassen, um dieses Szenario zu vermeiden.

- **Windows:** Basierend auf dem Hostnamen und der E-Mail-Adresse wird ein vorhandenes doppeltes E-Mail-Profil erkannt. Intune überschreibt das vorhandene vom Endbenutzer erstellte E-Mail-Profil.

- **Android Samsung Knox Standard**: Basierend auf der E-Mail-Adresse wird ein vorhandenes doppeltes E-Mail-Profil erkannt und durch das Intune-Profil überschrieben. Android identifiziert das Profil nicht anhand des Hostnamens. Erstellen Sie nicht mehrere E-Mail-Profile mit derselben E-Mail-Adresse auf verschiedenen Hosts. Die Profile überschreiben sich gegenseitig.

- **Android-Arbeitsprofile**: Intune stellt zwei Android-E-Mail-Arbeitsprofile bereit: eines für die E-Mail-App Gmail und eines für die E-Mail-App Nine Work. Diese Apps sind im Google Play Store erhältlich und können mit dem Arbeitsprofil des Geräts installiert werden. Diese Apps erstellen keine doppelten Profile. Beide Apps unterstützen Verbindungen mit Exchange. Stellen Sie zur Verwendung der E-Mail-Konnektivität eine dieser E-Mail-Apps auf den Benutzergeräten bereit. Erstellen Sie anschließend das E-Mail-Profil, und stellen Sie es bereit. Sie können E-Mail-Konfigurationsprofile für Gmail und Nine verwenden, die für die Registrierungstypen „Arbeitsprofil“ sowie „Fully Managed, Dedicated, and Corporate-Owned Work Profile“ (Vollständig verwaltet, dediziert und unternehmenseigen mit einem Arbeitsprofil) verwendet werden können. Außerdem können Zertifikatprofile für beide E-Mail-Konfigurationstypen verwendet werden. Alle Gmail- oder Nine-Richtlinien, die Sie über die Gerätekonfiguration für Arbeitsprofile erstellen, werden weiterhin auf das Gerät angewendet. Es ist nicht notwendig, sie in die App-Konfigurationsrichtlinien zu verschieben. E-Mail-Apps wie Nine Work sind möglicherweise nicht kostenlos. Lesen Sie die Lizenzierungsdetails der App, oder kontaktieren Sie bei Fragen das Unternehmen, das die App bereitstellt.

## <a name="changes-to-assigned-email-profiles"></a>Änderungen an zugewiesenen E-Mail-Profilen

Wenn Sie ein zuvor zugewiesenes E-Mail-Profil ändern, werden Endbenutzer möglicherweise in einer Meldung aufgefordert, die Neukonfiguration ihrer E-Mail-Einstellungen zu genehmigen.

## <a name="next-steps"></a>Nächste Schritte

Das Profil ist nun erstellt, führt aber noch keine Aktionen durch. Die nächsten Schritte sind das [Zuweisen von Benutzer- und Geräteprofilen in Microsoft Intune](device-profile-assign.md) und das [Überwachen von Geräteprofilen in Microsoft Intune](device-profile-monitor.md).
