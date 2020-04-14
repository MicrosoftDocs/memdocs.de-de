---
title: Vorbereiten von Apps für die Verwaltung von mobilen Anwendungen mit Microsoft Intune
description: Die Informationen in diesem Thema unterstützen Sie bei der Entscheidung, wann Sie das App Wrapping Tool und das App SDK verwenden sollten, um Ihrer benutzerdefinierten Reihe von Branchen-Apps die Verwendung der Verwaltungsrichtlinien für mobile Apps zu ermöglichen.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/02/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 29e22121-8268-48b5-a671-f940a6be1d24
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6a26e32d0a719df7c3982591042991ae760d9281
ms.sourcegitcommit: db511e03f14e6120968b60def8990485eb42529b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/02/2020
ms.locfileid: "80611701"
---
# <a name="prepare-line-of-business-apps-for-app-protection-policies"></a>Vorbereiten von branchenspezifischen Apps für App-Schutzrichtlinien

Sie können die Verwendung von App-Schutzrichtlinien bei Ihren Apps mit dem Intune App Wrapping Tool oder dem Intune App SDK aktivieren. Verwenden Sie diese Informationen, um diese beiden Methoden und den Zeitpunkt für ihre Verwendung kennenzulernen.

## <a name="intune-app-wrapping-tool"></a>Intune App Wrapping Tool

Das App Wrapping Tool wird in erster Linie für **interne** Line-of-Business-Apps (LOB) verwendet. Das Tool ist eine Befehlszeilenanwendung, die einen Wrapper für die App erstellt, der es der App anschließend ermöglicht, von einer Intune-App-Schutzrichtlinie verwaltet zu werden. Wenn Sie eine App schützen, die von einem unabhängigen Softwareanbieter (ISV, Independent Software Vendor) bereitgestellt wurde, sollten Sie unbedingt klären, ob der ISV die umschlossene App weiterhin unterstützt.

Der Quellcode ist für die Verwendung des Tools nicht erforderlich, aber Sie benötigen entsprechende Anmeldeinformationen. Weitere Informationen zu Anmeldeinformationen finden Sie im [Intune-Blog](https://blogs.technet.microsoft.com/enterprisemobility/2015/02/25/how-to-obtain-the-prerequisites-for-the-intune-app-wrapping-tool-for-ios/). Die Dokumentation zum App Wrapping Tool finden Sie unter [Android App Wrapping Tool](app-wrapper-prepare-android.md) und [iOS App Wrapping Tool](app-wrapper-prepare-ios.md).

Das App Wrapping Tool unterstützt **keine** Apps im Apple App Store oder Google Play Store. Es unterstützt auch keine bestimmten Features, die Entwicklerintegration erfordern (siehe die folgende Featurevergleichstabelle).

Weitere Informationen zum App Wrapping Tool für App-Schutzrichtlinien auf Geräten, die nicht bei Intune registriert sind, finden Sie unter [Schützen von branchenspezifischen Apps und Daten auf nicht in Microsoft Intune registrierten Geräten](../apps/apps-add.md).

### <a name="reasons-to-use-the-app-wrapping-tool"></a>Gründe für die Verwendung des App Wrapping Tools

* Ihre App verfügt nicht über integrierte Datenschutzfunktionen.
* Ihre App wird intern bereitgestellt.
* Sie haben keinen Zugriff auf den Quellcode der App.
* Sie haben die App nicht entwickelt.
* Die Benutzerauthentifizierung ist bei Ihrer App auf ein Minimum beschränkt.

### <a name="supported-app-development-platforms"></a>Unterstützte App-Entwicklungsplattformen

|**App Wrapping Tool** | **Xamarin** |**Cordova** |
|------|----|----|
|**iOS** |Ja|Ja|
|**Android**|Nein – [Intune App SDK-Xamarin-Bindungen](app-sdk-xamarin.md) verwenden|Ja|

## <a name="intune-app-sdk"></a>Intune App SDK

Das App SDK ist in erster Linie für Kunden konzipiert, die über Apps im Apple App Store oder Google Play Store verfügen und diese Apps mit Intune verwalten möchten. Das SDK kann jedoch in jede App integriert werden, auch in branchenspezifische Apps.

Weitere Informationen zum SDK finden Sie unter [Übersicht](app-sdk.md). Ein Einführung in das SDK finden Sie unter [Erste Schritte mit dem Microsoft Intune App SDK](app-sdk-get-started.md).

### <a name="reasons-to-use-the-sdk"></a>Gründe für die Verwendung des SDKs

* Ihre App verfügt nicht über integrierte Datenschutzfunktionen.
* Ihre App wird in einem öffentlichen App Store wie Google Play oder Apple App Store bereitgestellt.
* Sie sind ein App-Entwickler mit dem entsprechenden technischen Hintergrund zur Verwendung des SDKs.
* Ihre App verfügt über andere SDK-Integrationen.
* Ihre App wird regelmäßig aktualisiert.

### <a name="supported-app-development-platforms"></a>Unterstützte App-Entwicklungsplattformen

|**Intune App SDK** |**Xamarin** |**Cordova**
|------|----|----|
|**iOS**|Ja – [Intune App SDK-Xamarin-Bindungen](app-sdk-xamarin.md) verwenden|Nein|
|**Android**| Ja – [Intune App SDK-Xamarin-Bindungen](app-sdk-xamarin.md) verwenden|Nein|

## <a name="not-using-an-app-development-platform-listed-above"></a>Sie verwenden keine der oben aufgeführten Plattformen für die App-Entwicklung?

Das Intune SDK-Entwicklungsteam testet und unterstützt aktiv Apps, die mit den nativen Android-, iOS-Plattformen (Obj-C, Swift), Xamarin- und Xamarin.Forms-Plattformen erstellt wurden. Während einige Kunden das Intune SDK erfolgreich in andere Plattformen wie React Native und NativeScript integrieren konnten, bieten wir keine expliziten Anleitungen oder Plug-Ins für App-Entwickler, die andere als unsere unterstützten Plattformen verwenden. 

## <a name="feature-comparison"></a>Funktionsvergleich

In der folgenden Tabelle werden die Einstellungen aufgelistet, die aktiviert sind, wenn eine App das App SDK oder das App Wrapping Tool verwendet. Für einige Features ist es erforderlich, dass App-Entwickler Logik anwenden, die über die grundlegende Integration in das Intune SDK hinausgeht. Diese Features werden daher nicht aktiviert, wenn die App das App Wrapping Tool verwendet. 

|Komponente|App SDK|App Wrapping Tool|
|-----------|---------------------|-----------|
|Einschränken von anzuzeigenden Webinhalten in einem unternehmensverwalteten Browser|X|X|
|Verhindern von Android-, iTunes- oder iCloud-Sicherungen|X|X|
|App Übertragung von Daten an andere Apps erlauben|X|X|
|App Empfang von Daten aus anderen Apps erlauben|X|X|
|Ausschneiden, Kopieren und Einfügen mit anderen Apps einschränken|X|X|
|Geben Sie die Anzahl der Zeichen an, die aus einer verwalteten App ausgeschnitten oder kopiert werden können|X|X|
|Einfache PIN für Zugriff erforderlich|X|X|
|Angeben der Anzahl von Versuchen vor dem Zurücksetzen der PIN|X|X|
|Fingerabdruck anstelle von PIN zulassen|X|X|
|Gesichtserkennung anstelle von PIN zulassen (nur iOS)|X|X|
|Unternehmensanmeldeinformationen für Zugriff erforderlich|X|X|
|PIN-Ablauf festlegen|X|X|
|Blockieren der Ausführung von verwalteten Apps auf per Jailbreak oder Rooting manipulierten Geräten|X|X|
|App-Daten verschlüsseln|X|X|
|Erneutes Überprüfen der Zugriffsanforderungen nach einer angegebenen Anzahl von Minuten|X|X|
|Angeben der Offlinetoleranzperiode|X|X|
|Blockieren von Bildschirmaufnahmen (nur Android)|X|X|
|Unterstützung von MAM ohne Geräteregistrierung|X|X|
|Vollständiges Zurücksetzen von App-Daten|X|X|
|Selektives Zurücksetzen von Geschäfts-, Schul- oder Unikontodaten in Szenarios mit mehreren Identitäten <br><br>**Hinweis:** Für iOS/iPadOS wird beim Entfernen des Verwaltungsprofils auch die App entfernt.|X||
|Verhindern von „Speichern unter“|X||
|Gezielte Anwendungskonfiguration (oder App-Konfiguration über den MAM-Kanal)|X|X|
|Unterstützung von mehreren Identitäten|X||
|Anpassbarer Stil |X|||
|Bedarfsgesteuerte VPN-Verbindungen mit Anwendungen mit Citrix mVPN|X|X| 
|Kontaktsynchronisierung deaktivieren|X|X|
|Drucken deaktivieren|X|X|
|App-Mindestversion erfordern|X|X|
|iOS-Mindestbetriebssystem erfordern|X|X|
|Mindestversion für das Android-Sicherheitspatch erfordern (nur Android)|X|X|
|Mindestversion des Intune SDK für iOS erfordern (nur iOS)|X|X|
|SafetyNet-Gerätenachweis (nur Android)|X|X|
|Bedrohungsüberprüfung für Apps (nur Android)|X|X|
|Maximale Risikostufe für den Mobile Threat Defense-Anbieter verlangen|X||
|Konfigurieren von App-Benachrichtigungsinhalt für Organisationskonten|X|X|
|Verwendung von genehmigten Tastaturen verlangen (nur Android)|X|X|
|App-Schutzrichtlinie verlangen (bedingter Zugriff)|X||
|Genehmigte Client-App verlangen (bedingter Zugriff)|X||

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu App-Schutzrichtlinien und Intune finden Sie in den folgenden Themen:

- [Android App Wrapping Tool](app-wrapper-prepare-android.md)<br>
- [Vorbereiten von iOS-Apps für die Verwaltung mobiler Anwendungen mit dem Intune App Wrapping Tool](app-wrapper-prepare-ios.md)<br>
- [Verwenden des SDK zum Aktivieren von Apps für die Verwaltung von mobilen Anwendungen](app-sdk.md)
