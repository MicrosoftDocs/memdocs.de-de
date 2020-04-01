---
title: Erstellen von iOS/iPadOS- oder macOS-Geräteprofilen in Microsoft Intune – Azure | Microsoft-Dokumentation
description: In diesem Artikel erfahren Sie, wie Sie in Microsoft Intune ein iOS-, iPadOS- oder macOS-Geräteprofil erstellen oder ein solches Profil hinzufügen. Außerdem erfahren Sie, wie Sie Einstellungen für AirPrint, das Layout des Startbildschirms, App-Benachrichtigungen, freigegebene Geräte, einmaliges Anmelden und Webinhaltsfilter konfigurieren.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 30bf5ba078029e35988d3531ee510d9db6c6cdb8
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359470"
---
# <a name="add-ios-ipados-or-macos-device-feature-settings-in-intune"></a>Hinzufügen von Einstellungen für iOS-, iPadOS- oder macOS-Gerätefeatures in Intune

Intune umfasst zahlreiche Features und Einstellungen, mit denen Administratoren iOS-, iPadOS- und macOS-Geräte steuern können. Administratoren können z.B.:

- Benutzern den Zugriff auf AirPrint-Drucker in Ihrem Netzwerk ermöglichen
- Apps und Ordner dem Startbildschirm hinzufügen, einschließlich Hinzufügen von neuen Seiten
- Wählen, ob und wie App-Benachrichtigungen angezeigt werden
- Den Sperrbildschirm so konfigurieren, dass eine Nachricht oder das Bestandskennzeichen angezeigt wird, insbesondere für gemeinsam genutzte Geräte
- Benutzern sicheres einmaliges Anmelden ermöglichen, um Anmeldeinformationen zwischen Apps freizugeben
- Websites herausfiltern, die nicht jugendfreie Sprache verwenden, und bestimmte Websites zulassen oder blockieren

Intune verwendet „Konfigurationsprofile“ zum Erstellen und Anpassen dieser Einstellungen für die Anforderungen Ihrer Organisation. Nachdem Sie diese Features in einem Profil hinzugefügt haben, übertragen Sie das Profil per Push auf iOS/iPadOS- und macOS-Geräte in Ihrer Organisation oder stellen es für diese Geräte bereit.

In diesem Artikel werden die verschiedenen Features beschrieben, die Sie konfigurieren können, und es wird erläutert, wie Sie ein Gerätekonfigurationsprofil erstellen. Sie können auch alle verfügbaren Einstellungen für [iOS/iPadOS](ios-device-features-settings.md)- und [macOS](macos-device-features-settings.md)-Geräte anzeigen.

## <a name="airprint"></a>AirPrint

AirPrint ist ein Apple-Feature, mit dem Geräte Dateien über ein Drahtlosnetzwerk drucken können. In Intune können Sie AirPrint-Informationen zu Geräten hinzufügen.

Eine Liste der Einstellungen, die Sie in Intune konfigurieren können, finden Sie unter [AirPrint](ios-device-features-settings.md#airprint) (iOS/iPadOS) und [AirPrint](macos-device-features-settings.md#airprint) (macOS).

Weitere Informationen zu AirPrint finden Sie auf der Website von Apple unter [Informationen zu AirPrint](https://support.apple.com/HT201311).

Gilt für:

- iOS 7.0 und höher
- iOS 13.0 und höher
- macOS 10.10 und höher

## <a name="app-notifications"></a>App-Benachrichtigungen

Legen Sie fest, wie Apps auf iOS- und iPadOS-Geräten Benachrichtigungen empfangen sollen. Sie können beispielsweise App-Benachrichtigungen aus Intune senden, sodass diese in der Mitteilungszentrale oder auf dem Sperrbildschirm angezeigt werden oder ein akustisches Signal ertönt.

Eine Liste der Einstellungen, die Sie in Intune konfigurieren können, finden Sie unter [App-Benachrichtigungen](ios-device-features-settings.md#app-notifications).

Weitere Informationen zu diesem Feature finden Sie auf der Website von Apple unter [Notifications](https://developer.apple.com/notifications/) (Benachrichtigungen).

Gilt für:

- iOS 9.3 und höher
- iOS 13.0 und höher

## <a name="associated-domains"></a>Zugeordnete Domänen

Zugeordnete Domänen ermöglichen es Ihnen, eine Beziehung zwischen Ihren Domänen – z. B. `contoso.com` – und Ihren Apps zu erstellen. Dieses Feature bietet folgende Möglichkeiten:

- Sie können Daten und Anmeldeinformationen für Apps und Websites in Ihrer Organisation freigeben.
- Sie können App-Features verwenden, die auf Ihrer Website basieren, z. B. die App-Erweiterung für einmaliges Anmelden, universelle Links und das automatische Ausfüllen von Kennwörtern.

  Sie können beispielsweise eine zugeordnete Domäne erstellen, um das automatische Ausfüllen von Kennwörtern zuzulassen, sodass Anmeldeinformationen wie z. B. ein Kennwort für Websites empfohlen werden, die Ihrer App zugeordnet sind.

Eine Liste der Einstellungen, die Sie in Intune konfigurieren können, finden Sie unter [Zugeordnete Domänen unter macOS](macos-device-features-settings.md#associated-domains).

Weitere Informationen zu diesem Feature finden Sie auf der Website von Apple unter [Setting Up an App’s Associated Domains](https://developer.apple.com/documentation/security/password_autofill/setting_up_an_app_s_associated_domains) (Einrichten von zugeordneten Domänen einer App).

Gilt für:

- macOS 10.15 und neuer

## <a name="home-screen-layout"></a>Layout des Startbildschirms

Mit diesen Einstellungen konfigurieren Sie das Layout von Apps und Ordnern im Dock und auf dem Startbildschirm von iOS- und iPadOS-Geräten. Sie können:

- Verwenden Sie die Einstellungen für das **Dock**, um Apps oder Ordner zum Bildschirm hinzuzufügen. Sie können beispielsweise Safari und die E-Mail-App im Gerätedock anzeigen.
- Fügen Sie **Seiten** hinzu, die auf dem Startbildschirm angezeigt werden sollen, und fügen Sie Apps hinzu, die auf jeder Seite angezeigt werden sollen. Sie können beispielsweise eine Seite namens **Contoso** hinzufügen und auf dieser Seite die Einstellungs-App hinzufügen.

Eine Liste der Einstellungen, die Sie in Intune konfigurieren können, finden Sie unter [Layout des Startbildschirms](ios-device-features-settings.md#home-screen-layout).

Gilt für:

- iOS 9.3 und höher
- iOS 13.0 und höher

## <a name="lock-screen-message"></a>Nachricht auf Sperrbildschirm

Verwenden Sie diese Einstellungen, um eine benutzerdefinierte Nachricht oder einen Text im Anmeldefenster und auf dem Sperrbildschirm anzuzeigen. Sie können z. B. eine „Wenn verloren, zurück an“-Nachricht eingeben und Informationen zum Bestandskennzeichen anzeigen.

Eine Liste der Einstellungen, die Sie in Intune konfigurieren können, finden Sie unter [Nachricht auf Sperrbildschirm](ios-device-features-settings.md#lock-screen-message).

Weitere Informationen zu Sperrbildschirmnachrichten finden Sie auf der Website von Apple unter [LockScreenMessage](https://developer.apple.com/documentation/devicemanagement/lockscreenmessage).

Gilt für:

- iOS 9.3 und höher
- iOS 13.0 und höher

## <a name="login-items"></a>Anmeldeelemente

Verwenden Sie dieses Feature, um die Apps, benutzerdefinierten Apps, Dateien und Ordner auszuwählen, die geöffnet werden, wenn Benutzer sich bei ihren Geräten anmelden.

Eine Liste der Einstellungen, die Sie in Intune konfigurieren können, finden Sie unter [Anmeldeelemente unter macOS](macos-device-features-settings.md#login-items).

Gilt für:

- macOS 10.13 und höher

## <a name="login-window"></a>Fenster „Anmeldung“

Steuern Sie das Aussehen des Anmeldebildschirms sowie die Funktionen, die Benutzern vor der Anmeldung zur Verfügung stehen. Fügen Sie z. B. ein Banner mit einer benutzerdefinierten Meldung hinzu, wählen Sie aus, ob die Schaltfläche für den Energiesparmodus angezeigt wird, und vieles mehr.

Eine Liste der Einstellungen, die Sie in Intune konfigurieren können, finden Sie unter [Anmeldefenster unter macOS](macos-device-features-settings.md#login-window).

Gilt für:

- macOS 10.7 und höher

## <a name="single-sign-on"></a>Einmaliges Anmelden

Die meisten branchenspezifischen Apps erfordern eine bestimmte Form von Benutzerauthentifizierung, um Sicherheitsfeatures unterstützen zu können. Häufig müssen Benutzer bei dieser Art von Authentifizierung die gleichen Anmeldeinformationen mehrfach eingeben. Um die Benutzerfreundlichkeit zu verbessern, können Entwickler Apps erstellen, die einmaliges Anmelden (SSO) verwenden. Dadurch wird die Anzahl der Male reduziert, die ein Benutzer Anmeldeinformationen eingeben muss.

Um einmaliges Anmelden zu verwenden, achten Sie darauf, dass Sie folgende Anforderungen erfüllen:

- Es muss eine App vorhanden sein, die dafür codiert ist, den Anmeldeinformationsspeicher des Benutzers zum einmaligen Anmelden auf dem Gerät zu durchsuchen.
- Intune muss für einmaliges Anmelden von iOS/iPadOS-Geräten konfiguriert sein.

![Bereich „Einmaliges Anmelden“](./media/device-features-configure/sso-blade.png)

Eine Liste der Einstellungen, die Sie in Intune konfigurieren können, finden Sie unter [Einmaliges Anmelden](ios-device-features-settings.md#single-sign-on).

Gilt für:

- iOS 7.0 und höher
- iOS 13.0 und höher

## <a name="single-sign-on-app-extension"></a>App-Erweiterung für einmaliges Anmelden

Diese Einstellungen konfigurieren eine App-Erweiterung, die das einmalige Anmelden (Single Sign-On, SSO) für Ihre iOS-, iPadOS- und macOS-Geräte ermöglicht. Die meisten branchenspezifischen Apps und Organisationswebsites erfordern eine bestimmte Form der sicheren Benutzerauthentifizierung. Häufig müssen Benutzer bei dieser Art von Authentifizierung die gleichen Anmeldeinformationen mehrfach eingeben. SSO ermöglicht Benutzern den Zugriff auf ihre Apps und Websites, nachdem sie ihre Anmeldeinformationen nur einmal eingegeben haben. SSO bietet auch bessere Authentifizierungsoptionen für Benutzer und reduziert die Anzahl von wiederholten Aufforderungen zur Eingabe von Anmeldeinformationen.

In Intune verwenden Sie diese Einstellungen, um eine von Microsoft, Apple, Ihrer Organisation oder Ihrem Identitätsanbieter erstellte App-Erweiterung für das einmalige Anmelden zu konfigurieren. Die App-Erweiterung für einmaliges Anmelden verarbeitet die Authentifizierung für Ihre Benutzer. Diese Einstellungen konfigurieren SSO-App-Erweiterungen für Umleitungen und Anmeldeinformationen.

- Die Erweiterung für Umleitungen ist für moderne Authentifizierungsprotokolle wie OAuth und SAML2 konzipiert. Microsoft stellt eine Azure AD-SSO-App-Erweiterung zur Weiterleitung für iOS/iPadOS bereit, die mit den Einstellungen für SSO-App-Erweiterungen aktiviert werden kann.
- Die Erweiterung für Anmeldeinformationen ist für Abfrage- und Antwort-Authentifizierungsabläufe konzipiert. Sie können zwischen einer von Apple bereitgestellten Kerberos-spezifischen und einer generischen Erweiterung für Anmeldeinformationen auswählen.

Eine Liste der Einstellungen, die Sie in Intune konfigurieren können, finden Sie unter [App-Erweiterung für einmaliges Anmelden](ios-device-features-settings.md#single-sign-on-app-extension) (iOS/iPadOS) und [App-Erweiterung für einmaliges Anmelden](macos-device-features-settings.md#single-sign-on-app-extension) (macOS).

Weitere Informationen zum Entwickeln einer App-Erweiterung für das einmalige Anmelden finden Sie auf der Website von Apple im Video [Extensible Enterprise SSO](https://developer.apple.com/videos/play/tech-talks/301) (Erweiterbares einmaliges Anmelden für Unternehmen). Lesen Sie die Beschreibung des Features von Apple unter [Einstellungen der Payload „Erweiterungen der Gesamtauthentifizierung“](https://support.apple.com/guide/mdm/single-sign-on-extensions-mdmfd9cdf845/web). 

> [!NOTE]
> Das Feature **App-Erweiterung für einmaliges Anmelden** unterscheidet sich vom Feature **Einmaliges Anmelden**:
>
> - Die Einstellungen für **App-Erweiterung für einmaliges Anmelden** gelten für iPadOS 13.0 (und höher), für iOS 13.0 (und höher) sowie für macOS 10.15 (und höher). Die Einstellungen für **Einmaliges Anmelden** gelten für iPadOS 13.0 (und höher) sowie für iOS 7.0 (und höher).
>
> - Mit der **App-Erweiterung für einmaliges Anmelden** werden Erweiterungen definiert, die von Identitätsanbietern oder Organisationen zur Bereitstellung einer nahtlosen Anmeldung im Geschäftsumfeld verwendet werden können. Mit den Einstellungen für **Einmaliges Anmelden** werden Kerberos-Kontoinformationen definiert, wenn Benutzer auf Server oder Apps zugreifen.
>
> - Die **App-Erweiterung für einmaliges Anmelden** verwendet das Apple-Betriebssystem zur Authentifizierung. Dies kann benutzerfreundlicher sein als das **Einmalige Anmelden**.
>
> - Aus Entwicklerperspektive kann mit der **App-Erweiterung für einmaliges Anmelden** jede Art von SSO-Weiterleitung und SSO-Authentifizierung mit Anmeldeinformationen verwendet werden. Beim Feature **Einmaliges Anmelden** können Sie nur die Kerberos-SSO-Authentifizierung verwenden.
>
> - Die **App-Erweiterung für einmaliges Anmelden** von Kerberos wurde von Apple entwickelt und ist in die Plattformen von iOS/iPadOS 13.0 und höher und macOS 10.15 und höher integriert. Die integrierte Kerberos-Erweiterung kann verwendet werden, um Benutzer in nativen Apps und Websites zu protokollieren, die die Kerberos-Authentifizierung unterstützen. **Einmaliges Anmelden** ist nicht eine Apple-Implementierung von Kerberos.
>
> - Die integrierte **App-Erweiterung für einmaliges Anmelden** von Kerberos bewältigt Herausforderungen von Kerberos für Webseiten und Apps genauso wie **Einmaliges Anmelden**. Die integrierte Kerberos-Erweiterung unterstützt jedoch Kennwortänderungen und verhält sich in Unternehmensnetzwerken besser. Bei der Entscheidung zwischen der **App-Erweiterung für einmaliges Anmelden** und **Einmaliges Anmelden** von Kerberos wird die Verwendung der Erweiterung aufgrund verbesserter Leistung und Funktionen empfohlen.

Gilt für:

- iOS 13.0 und neuer
- iOS 13.0 und höher
- macOS 10.15 und neuer

## <a name="wallpaper"></a>Hintergrundbild

Fügen Sie ein benutzerdefiniertes PNG-, JPG- oder JPEG-Bild auf Ihren überwachten iOS/iPadOS-Geräten hinzu. Sie können Intune z. B. dafür verwenden, ein Firmenlogo auf den Sperrbildschirm Ihrer Geräte hinzuzufügen.

Eine Liste der Einstellungen, die Sie in Intune konfigurieren können, finden Sie unter [Hintergrundbild](ios-device-features-settings.md#wallpaper).

Gilt für:

- iOS
- iOS 13.0 und höher

## <a name="web-content-filter"></a>Webinhaltsfilter

Diese Einstellungen verwenden den integrierten AutoFilter-Algorithmus von Apple, um Webseiten zu bewerten und nicht jugendfreie Inhalte zu blockieren. Sie können auch Listen mit zulässigen und eingeschränkten Weblinks erstellen. Sie können z. B. festlegen, dass nur `contoso`-Websites geöffnet werden dürfen.

Eine Liste der Einstellungen, die Sie in Intune konfigurieren können, finden Sie unter [Webinhaltsfilter](ios-device-features-settings.md#web-content-filter).

Gilt für:

- iOS 7.0 und höher
- iOS 13.0 und höher

## <a name="create-the-profile"></a>Erstellen des Profils

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
3. Geben Sie die folgenden Eigenschaften ein:

    - **Plattform**: Wählen Sie die Plattform Ihrer Geräte aus. Folgende Optionen sind verfügbar:  

        - **iOS/iPadOS**
        - **macOS**

    - **Profil**: Wählen Sie **Gerätefunktionen** aus.

4. Wählen Sie **Erstellen** aus.
5. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:

    - **Name:** Geben Sie einen aussagekräftigen Namen für die Richtlinie ein. Benennen Sie Ihre Richtlinien so, dass Sie diese später leicht wiedererkennen. Ein guter Richtlinienname ist beispielsweise **macOS: Anmeldebildschirm konfigurieren**.
    - **Beschreibung:** Geben Sie eine Beschreibung für die Richtlinie ein. Diese Einstellung ist optional, wird jedoch empfohlen.

6. Wählen Sie **Weiter** aus.

7. Die verfügbaren **Konfigurationseinstellungen** variieren je nach ausgewählter Plattform. Wählen Sie Ihre Plattform für detaillierte Einstellungen aus:

    - [iOS/iPadOS](ios-device-features-settings.md)
    - [macOS](macos-device-features-settings.md)

8. Wählen Sie **Weiter** aus.
9. Weisen Sie in **Bereichstags** (optional) ein Tag zu, um das Profil nach bestimmten IT-Gruppen wie `US-NC IT Team` oder `JohnGlenn_ITDepartment` zu filtern. Weitere Informationen zu Bereichstags finden Sie unter [Verwenden der RBAC und von Bereichstags für verteilte IT](../fundamentals/scope-tags.md).

    Wählen Sie **Weiter** aus.

10. Wählen Sie unter **Zuweisungen** die Benutzer oder Gruppen aus, denen Ihr Profil zugewiesen werden soll. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](device-profile-assign.md).

    Wählen Sie **Weiter** aus.

11. Überprüfen Sie die Einstellungen unter **Überprüfen + erstellen**. Wenn Sie auf **Erstellen** klicken, werden die Änderungen gespeichert, und das Profil wird zugewiesen. Die Richtlinie wird auch in der Profilliste angezeigt.

## <a name="next-steps"></a>Nächste Schritte

Das Profil ist nun erstellt, führt aber vielleicht noch keine Aktionen durch. Die nächsten Schritte sind das [Zuweisen von Benutzer- und Geräteprofilen in Microsoft Intune](device-profile-assign.md) und das [Überwachen von Geräteprofilen in Microsoft Intune](device-profile-monitor.md).

Sehen Sie sich alle Einstellungen für Gerätefeatures für [iOS/iPadOS](ios-device-features-settings.md)- und [macOS](macos-device-features-settings.md)-Geräte an.
