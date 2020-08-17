---
title: Hinzufügen und Zuweisen verwalteter Google Play-Apps zu Android Enterprise-Geräten
titleSuffix: Microsoft Intune
description: Erfahren Sie, wie Sie über den verwalteten Google Play Store Apps zu Android Enterprise-Geräten zuweisen und synchronisieren.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 2f6c06bf-e29a-4715-937b-1d2c7cf663d4
ms.reviewer: chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: b8ce02a86236e390983b4e1ecca8d48d4767e49e
ms.sourcegitcommit: 9eebe77af18045fceb3d41b43d76b370fe92b30e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/05/2020
ms.locfileid: "87821630"
---
# <a name="add-managed-google-play-apps-to-android-enterprise-devices-with-intune"></a>Hinzufügen verwalteter Google Play-Apps zu Android Enterprise-Geräten mit Intune

Verwaltetes Google Play ist der Enterprise App Store von Google und die einzige Quelle von Anwendungen für Android Enterprise. Mit Intune können Sie die App-Bereitstellung über verwaltetes Google Play für jedes Android Enterprise-Szenario (einschließlich Arbeitsprofil, dedizierte, vollständig verwaltete und unternehmenseigene Registrierungen von Arbeitsprofilen) orchestrieren. Das Hinzufügen von verwalteten Google Play-Apps zu Intune unterscheidet sich vom Hinzufügen von Android-Apps zu Nicht-Android Enterprise-Geräten. Store-, branchenspezifische und Web-Apps werden in verwaltetem Google Play genehmigt oder hinzugefügt und dann so mit Intune synchronisiert, dass sie in der Liste „Client-Apps“ angezeigt werden. Sobald sie in der Liste „Client-Apps“ aufgeführt sind, können Sie die Zuweisung einer verwalteten Google Play-App wie bei jeder anderen App verwalten.

Intune fügt bei der Verbindung Ihres Intune-Mandanten mit verwaltetem Google Play automatisch vier gängige auf Android Enterprise bezogene Apps zur Intune-Verwaltungskonsole hinzu, um Ihnen die Konfiguration und Nutzung der Android Enterprise-Verwaltung zu erleichtern. Es handelt sich um diese vier Apps:

- **[Microsoft Intune](https://play.google.com/store/apps/details?id=com.microsoft.intune)** : für vollständig verwaltete Android Enterprise-Szenarien. Diese App wird während des Geräteregistrierungsprozesses automatisch auf vollständig verwalteten Geräten installiert.
- **[Microsoft Authenticator](https://play.google.com/store/apps/details?id=com.azure.authenticator)** : hilft bei der Anmeldung bei Ihren Konten, wenn Sie die zweistufige Überprüfung verwenden. Diese App wird während des Geräteregistrierungsprozesses automatisch auf vollständig verwalteten Geräten installiert.
- **[Intune-Unternehmensportal](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal)** : wird für App Protection Policies (APP) und Szenarien mit Android Enterprise-Arbeitsprofilen genutzt. Diese App wird während des Geräteregistrierungsprozesses automatisch auf vollständig verwalteten Geräten installiert.
- **[Managed Home Screen](https://play.google.com/store/apps/details?id=com.microsoft.launcher.enterprise)** : wird für dedizierte/Kioskszenarien mit Android Enterprise verwendet. IT-Administratoren sollten eine Zuweisung erstellen, um diese App auf dedizierten Geräten zu installieren, die in Kioskszenarien mit mehreren Apps verwendet werden sollen.

>[!NOTE]
>Wenn ein Endbenutzer sein von Android Enterprise vollständig verwaltetes Gerät registriert, wird die App „Intune-Unternehmensportal“ automatisch installiert, woraufhin das Anwendungssymbol dem Endbenutzer möglicherweise angezeigt wird. Wenn der Endbenutzer versucht, die App „Intune-Unternehmensportal“ zu starten, wird der Endbenutzer zur App „Microsoft Intune“ umgeleitet, woraufhin das Symbol der Unternehmensportal-App ausgeblendet wird.

## <a name="before-you-start"></a>Vorbereitung
- Vergewissern Sie sich, dass Sie Ihren Intune-Mandanten mit verwaltetem Google Play verbunden haben.  Weitere Informationen finden Sie unter [Herstellen einer Verbindung zwischen Ihrem Intune-Konto und Ihrem verwalteten Google Play-Konto](../enrollment/connect-intune-android-enterprise.md).
- Wenn Sie vorhaben, Arbeitsprofilgeräte zu registrieren, stellen Sie sicher, dass Sie Intune und Android-Arbeitsprofile im Azure-Portal für die Workload **Geräteregistrierung** so konfiguriert haben, dass beide zusammenarbeiten. Weitere Informationen finden Sie unter [Registrieren von Android-Geräten](../enrollment/android-work-profile-enroll.md).

>[!NOTE]
>Für die Arbeit mit Microsoft Intune wird als Browser Microsoft Edge oder Google Chrome empfohlen.

## <a name="managed-google-play-app-types"></a>Typen verwalteter Google Play-Apps
Es gibt drei Arten von Apps, die mit verwaltetem Google Play verfügbar sind:

- **Verwaltete Google Play Store-Apps**: öffentliche Apps, die im Play Store allgemein verfügbar sind. Verwalten Sie diese Apps in Intune, indem Sie nach den Apps suchen, die Sie verwalten möchten, sie genehmigen und sie dann mit Intune synchronisieren.
- **Verwaltete private Google Play-Apps**: Hierbei handelt es sich um branchenspezifische Apps, die von Intune-Administratoren in verwaltetem Google Play veröffentlicht werden.  Diese Apps sind privat und nur für Ihren Intune-Mandanten verfügbar. Auf diese Weise werden branchenspezifische Apps mit verwaltetem Google Play und Android Enterprise verwaltet und bereitgestellt.
- **Weblinks zu verwaltetem Google Play**: Weblinks mit von IT-Administratoren definierten Symbolen, die auf Android Enterprise-Geräten bereitgestellt werden können. Diese werden auf einem Gerät wie normale Apps in dessen App-Liste angezeigt.

## <a name="managed-google-play-store-apps"></a>Apps im verwalteten Google Play Store
Es gibt zwei Möglichkeiten zum Suchen und Genehmigen verwalteter Google Play Store-Apps mit Intune:

1. Direkt in der Intune-Konsole: Suchen und genehmigen Sie Store-Apps in einer in Intune gehosteten Ansicht. Dieser Vorgang wird direkt in der Intune-Konsole geöffnet, sodass Sie sich nicht mit einem anderen Konto erneut authentifizieren müssen.
1. In der Konsole von verwaltetem Google Play: Sie können optional die Konsole von verwaltetem Google Play direkt öffnen und Apps dort genehmigen. Weitere Informationen finden Sie unter [Synchronisieren einer App aus dem verwalteten Google Play Store mit Intune](apps-add-android-for-work.md#sync-a-managed-google-play-app-with-intune).  Dazu ist eine separate Anmeldung über das Konto erforderlich, mit dem Sie Ihren Intune-Mandanten mit verwaltetem Google Play verbunden haben.

### <a name="add-a-managed-google-play-store-app-directly-in-the-intune-console"></a>Hinzufügen einer verwalteten Google Play Store-App direkt in der Intune-Konsole

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Apps** > **Alle Apps** > **Hinzufügen** aus.
3. Wählen Sie im Bereich **App-Typ auswählen** unter den verfügbaren **Store-App**-Typen **Verwaltete Google Play-App** aus.
4. Klicken Sie auf **Auswählen**. Der neue App-Store **Verwaltetes Google Play** wird angezeigt.

    > [!NOTE]
    > Ihr Intune-Mandantenkonto muss mit Ihrem Android Enterprise-Konto verbunden sein, um verwaltete Google Play-Store-Apps durchsuchen zu können. Weitere Informationen finden Sie unter [Herstellen einer Verbindung zwischen Ihrem Intune-Konto und Ihrem verwalteten Google Play-Konto](../enrollment/connect-intune-android-enterprise.md).

5. Wählen Sie eine App aus, um die App-Details anzuzeigen.
6. Klicken Sie auf der Seite, die die App anzeigt, auf **Genehmigen**. Ein Fenster für die App wird geöffnet, und Sie werden gebeten, der App Berechtigungen zum Durchführen verschiedener Vorgänge zu erteilen.
7. Klicken Sie auf **Genehmigen**, um die App-Berechtigungen zu akzeptieren und fortzufahren.
8. Wählen Sie **Genehmigt lassen, wenn Apps neue Berechtigungen anfordern** auf der Registerkarte **Genehmigungseinstellungen** aus, und klicken Sie dann auf **Fertig**. 

    > [!IMPORTANT]
    > Wenn Sie diese Option nicht auswählen, müssen Sie alle neuen Berechtigungen manuell genehmigen, wenn der App-Entwickler ein Update veröffentlicht. Dadurch werden Installationen und Updates für die App unterbrochen, bis die Berechtigungen genehmigt wurden. Aus diesem Grund wird empfohlen, die Option zum automatischen Genehmigen neuer Berechtigungen auszuwählen. 

9. Klicken Sie auf **Auswählen**, um die App auszuwählen.
10. Klicken Sie oben im Blatt auf **Synchronisieren**, um die App mit dem verwalteten Google Play-Dienst zu synchronisieren.
11. Klicken Sie auf **Aktualisieren**, um die App-Liste zu aktualisieren und die neu hinzugefügte App anzuzeigen.

### <a name="add-a-managed-google-play-store-app-in-the-managed-google-play-console-alternative"></a>Hinzufügen einer verwalteten Google Play Store-App in der Konsole von verwaltetem Google Play (Alternative)
Wenn Sie es vorziehen, eine verwaltete Google Play-App mit Intune zu synchronisieren, anstatt sie direkt mit Intune hinzuzufügen, gehen Sie wie folgt vor.

> [!IMPORTANT]
> Die folgenden Informationen sind eine alternative Methode, um eine verwaltete Google Play-App mit Intune wie oben beschrieben hinzuzufügen.

1. Besuchen Sie den [Managed Google Play Store](https://play.google.com/work). Melden Sie sich mit dem Konto an, das Sie zum Konfigurieren der Verbindung zwischen Intune und Android Enterprise verwendet haben.
2. Suchen Sie im Store nach der App, die Sie mithilfe von Intune zuweisen möchten, und wählen Sie die App aus.
3. Klicken Sie auf der Seite, die die App anzeigt, auf **Genehmigen**.  
    Im folgenden Beispiel wurde die Microsoft Excel-App ausgewählt.

    ![Die Schaltfläche „Genehmigen“ im Managed Google Play-Store](./media/apps-add-android-for-work/approve.png)

   Ein Fenster für die App wird geöffnet, und Sie werden gebeten, der App Berechtigungen zum Durchführen verschiedener Vorgänge zu erteilen.

4. Klicken Sie auf **Genehmigen**, um die App-Berechtigungen zu akzeptieren und fortzufahren.

    ![Die Schaltfläche „Genehmigen“ für App-Berechtigungen](./media/apps-add-android-for-work/approve-app-permissions.png)

5. Wählen Sie eine Option für die Behandlung neuer App-Berechtigungsanforderungen und dann **Speichern** aus.

    ![Optionen für die Behandlung neuer App-Berechtigungsanforderungen](./media/apps-add-android-for-work/approve-app-settings.png)

    Die App wird genehmigt und in Ihrer IT-Verwaltungskonsole angezeigt. Als Nächstes können Sie [die Android-Arbeitsprofil-App mit Intune synchronisieren](apps-add-android-for-work.md#sync-a-managed-google-play-app-with-intune).

## <a name="managed-google-play-private-lob-apps"></a>Private (branchenspezifische) verwaltete Google Play-Apps

Es gibt zwei Möglichkeiten, verwaltetem Google Play branchenspezifische Apps hinzuzufügen:

1. Direkt in der Intune-Konsole: Direkt in der Intune-Konsole: Dies ermöglicht Ihnen das Hinzufügen branchenspezifischer Apps direkt in Intune, indem Sie nur das APK der App und einen Titel übermitteln. Diese Methode erfordert weder ein Google-Entwicklerkonto noch die Zahlung der Gebühr zur Registrierung bei Google als Entwickler.  Diese Methode ist einfacher, weist deutlich weniger Schritte auf und macht branchenspezifische Apps in nur zehn Minuten für die Verwaltung verfügbar.
1. In der Google Play Developer Console: Wenn Sie ein Google-Entwicklerkonto haben oder erweiterte Verteilungsfunktionen konfigurieren möchten, die nur in der Google Play Developer Console verfügbar sind (z. B. das Hinzufügen zusätzlicher App-Screenshots), können Sie die [Google Play Developer Console](https://play.google.com/apps/publish) verwenden. 

### <a name="managed-google-play-private-lob-app-publishing-directly-in-the-intune-console"></a>Veröffentlichen privater branchenspezifischer verwalteter Google Play-Apps direkt in der Intune-Konsole

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Apps** > **Alle Apps** > **Hinzufügen** aus.
3. Wählen Sie im Bereich **App-Typ auswählen** unter den verfügbaren **Store-App**-Typen **Verwaltete Google Play-App** aus.
4. Klicken Sie auf **Auswählen**. Der neue App-Store **Verwaltetes Google Play** wird in Intune angezeigt.
5. Wählen Sie im Google Play-Fenster **Private Apps** (neben dem *Sperrsymbol*) aus. 
6. Klicken Sie in der unteren rechten Ecke auf die Schaltfläche **+** , um eine neue App hinzuzufügen.
7. Fügen Sie den **Titel** der App hinzu, und klicken Sie auf **APK hochladen**, um das APK-App-Paket hinzuzufügen.
   > [!NOTE]
   > Der Paketname Ihrer App muss in Google Play (nicht nur innerhalb Ihres Unternehmenskontos oder Google Play Developer-Kontos) global eindeutig sein. Andernfalls wird die Fehlermeldung **Neue APK-Datei mit anderem Paketnamen hochladen** angezeigt.
8. Klicken Sie auf **Erstellen**.
9. Schließen Sie den Bereich „Verwaltetes Google Play“, wenn das Hinzufügen von Apps abgeschlossen ist.
10. Klicken Sie im Bereich **App** auf **Synchronisieren**, um eine Synchronisierung mit dem verwalteten Google Play-Dienst durchzuführen. 

    > [!NOTE]
    > Es kann mehrere Minuten dauern, bis private Apps zur Synchronisierung verfügbar sind. Wenn die App bei der ersten Synchronisierung nicht angezeigt wird, warten Sie ein paar Minuten und starten dann eine neue Synchronisierung.

Weitere Informationen zu privaten verwalteten Google Play-Apps sowie häufig gestellte Fragen finden Sie im Google-Supportartikel: https://support.google.com/googleplay/work/answer/9146439

>[!IMPORTANT]
>Mit dieser Methode hinzugefügte private Apps können nicht öffentlich gemacht werden. Wählen Sie diese Veröffentlichungsoption nur, wenn Sie sicher sind, dass diese App für Ihre Organisation stets privat bleiben wird.

### <a name="managed-google-play-private-lob-app-publishing-using-the-google-developer-console"></a>Veröffentlichen privater branchenspezifischer verwalteter Google Play-Apps mithilfe der Google Developer Console

1. Melden Sie sich bei der [Google Play Developer Console](https://play.google.com/apps/publish) mit dem Konto an, das Sie zum Konfigurieren der Verbindung zwischen Intune und Android Enterprise verwendet haben.  
    Wenn Sie sich zum ersten Mal anmelden, müssen Sie sich registrieren und eine Gebühr bezahlen, um Mitglied im Google Developer-Programm zu werden.
2. Wählen Sie in der Konsole **Neue Anwendung hinzufügen** aus.
3. Informationen über Ihre App laden Sie auf dieselbe Weise hoch wie Sie Apps im Google Play Store veröffentlichen. Sie müssen jedoch **Only make this application available to my organization (<*organization name*>)** (Diese Anwendung nur für meine Organisation [<Name der Organisation>] verfügbar machen) auswählen.

    Durch diese Aktion wir die App nur für Ihre Organisation verfügbar gemacht. Sie wird nicht im öffentlichen Google Play Store verfügbar gemacht.

    Weitere Informationen zum Hochladen und Veröffentlichen von Android-Apps finden Sie in der [Google Developer Console-Hilfe](https://support.google.com/googleplay/android-developer/answer/113469).
4. Nachdem Sie Ihre App veröffentlicht haben, melden Sie sich beim [verwalteten Google Play Store](https://play.google.com/work) mit dem Konto an, das Sie zum Konfigurieren der Verbindung zwischen Intune und Android Enterprise verwendet haben.
5. Prüfen Sie im Knoten **Apps** im Store, ob die veröffentlichte App angezeigt wird.  
    Die App ist automatisch für die Synchronisierung mit Intune genehmigt.

## <a name="managed-google-play-web-links"></a>Weblinks „Verwaltetes Google Play“

Weblinks für verwaltetes Google Play können wie andere Android-Apps installiert und verwaltet werden. Bei Installation auf einem Gerät werden sie in der App-Liste des Benutzers neben den anderen installierten Apps angezeigt. Wenn darauf getippt wird, werden sie im Browser des Geräts gestartet.

Weblinks werden in Microsoft Edge oder einer anderen Browser-App geöffnet, die Sie bereitstellen möchten. Stellen Sie sicher, dass Sie mindestens eine Browser-App auf Geräten bereitstellen, damit Weblinks ordnungsgemäß geöffnet werden können. Alle für Weblinks verfügbaren Optionen für die **Anzeige** (Vollbildschirm, eigenständige und minimale Benutzeroberfläche) funktionieren jedoch nur im Browser Chrome. 

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Apps** > **Alle Apps** > **Hinzufügen** aus.
3. Wählen Sie im Bereich **App-Typ auswählen** unter den verfügbaren **Store-App**-Typen **Verwaltete Google Play-App** aus.
4. Klicken Sie auf **Auswählen**. Der neue App-Store **Verwaltetes Google Play** wird in Intune angezeigt.
5. Wählen Sie im Google Play-Fenster **Web-Apps** (neben dem *Globussymbol*) aus.
6. Klicken Sie in der unteren rechten Ecke auf die Schaltfläche **+** , um eine neue App hinzuzufügen.
7. Fügen Sie einen App-**Titel** und die **URL** der Web-App hinzu, wählen Sie, wie die App angezeigt werden soll, und dann ein App-Symbol aus.
8. Klicken Sie auf **Erstellen**.
9. Schließen Sie den Bereich „Verwaltetes Google Play“, wenn das Hinzufügen von Apps abgeschlossen ist.
10. Klicken Sie im Bereich **App** auf **Synchronisieren**, um eine Synchronisierung mit dem verwalteten Google Play-Dienst durchzuführen. 

    > [!NOTE]
    > Es kann mehrere Minuten dauern, bis Web-Apps zur Synchronisierung verfügbar sind. Wenn die App bei der ersten Synchronisierung nicht angezeigt wird, warten Sie ein paar Minuten und starten dann eine neue Synchronisierung.

## <a name="sync-a-managed-google-play-app-with-intune"></a>Synchronisieren einer App aus dem Managed Google Play Store mit Intune

Wenn Sie eine App aus dem Store genehmigt haben und diese nicht in der Workload **Apps** angezeigt wird, erzwingen Sie wie folgt eine sofortige Synchronisierung:

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
3. Klicken Sie auf **Mandantenverwaltung** > **Connectors und Token** > **Verwaltetes Google Play**.
5. Klicken Sie im Bereich **Verwaltetes Google Play** auf **Synchronisierung**.  
    Auf der Seite werden Uhrzeit und Status der letzten Synchronisierung aktualisiert.
6. Wählen Sie im Microsoft Endpoint Manager Admin Center die Option **Apps** > **Alle Apps** aus.  
    Die neu verfügbare Managed Google Play-App wird angezeigt.

## <a name="assigning-a-managed-google-play-app-to-android-enterprise-work-profile-and-corporate-owned-work-profile-devices"></a>Zuweisen einer verwalteten Google Play-App zu Android Enterprise-Arbeitsprofilen und unternehmenseigenen Arbeitsprofilgeräten

Wenn die App im Knoten **App-Lizenzen** des Workloadbereichs **Apps** angezeigt wird, können Sie sie [wie jede andere App zuweisen](/mem/intune/apps/apps-deploy), indem Sie die App Benutzergruppen zuweisen.

Nachdem Sie die App zugewiesen haben, wird sie auf den Geräten der von Ihnen ausgewählten Benutzern installiert (oder zur Installation verfügbar). Der Benutzer des Geräts wird nicht zur Genehmigung der Installation aufgefordert. Weitere Informationen zu dedizierten Android Enterprise-Arbeitsprofilgeräten finden Sie unter [Einrichten der Registrierung von Android Enterprise-Arbeitsprofilgeräten](../enrollment/android-work-profile-enroll.md). 

> [!NOTE] 
> Nur Apps, die zugewiesen wurden, werden einem Endbenutzer im verwalteten Google Play Store angezeigt. Dies ist daher ein wichtiger Schritt für den Administrator bei der Einrichtung von Apps mit verwaltetem Google Play.

## <a name="assigning-a-managed-google-play-app-to-android-enterprise-fully-managed-devices"></a>Zuweisen einer verwalteten Google Play-App zu vollständig verwalteten Android Enterprise-Geräten

[Vollständig verwaltete Android Enterprise-Geräte](../enrollment/android-fully-managed-enroll.md) sind unternehmenseigene Geräte, die einem einzelnen Benutzer zugeordnet sind und ausschließlich für Arbeits- und nicht für persönliche Zwecke genutzt werden. Benutzer vollständig verwalteter Geräte können ihre verfügbaren Unternehmens-Apps von der verwalteten Google Play-App auf ihrem Gerät beziehen.

Standardmäßig erlaubt ein vollständig verwaltetes Android Enterprise-Gerät Mitarbeitern nicht, Apps zu installieren, die nicht von der Organisation genehmigt sind. Außerdem können Mitarbeiter keine installierten Apps gegen geltende Richtlinien entfernen. Wenn Sie Benutzern den Zugriff auf den vollständigen Google Play-Store ermöglichen möchten, um Apps zu installieren, anstatt ihnen nur Zugriff auf die genehmigten Apps im verwalteten Google Play-Store einzuräumen, können Sie die Einstellung **Zugriff auf alle Apps im Google Play Store zulassen** auf **Zulassen** festlegen. Bei dieser Einstellung kann der Benutzer über sein Unternehmenskonto auf alle Apps im Google Play Store zugreifen, wobei Käufe jedoch eingeschränkt sein können. Sie können die Kaufbeschränkung aufheben, indem Sie Benutzern erlauben, neue Konten zum Gerät hinzuzufügen. Auf diese Weise können Endbenutzer Apps im Google Play Store über persönliche Konten erwerben und auch In-App-Käufe durchführen. Weitere Informationen finden Sie unter [Android Enterprise-Geräteeinstellungen zum Zulassen oder Einschränken von Features mit Intune](../configuration/device-restrictions-android-for-work.md). 

> [!NOTE]
> Die Microsoft Intune-App, die Microsoft Authenticator-App und die Unternehmensportal-App werden beim Onboarding als erforderliche Apps auf allen vollständig verwalteten Geräten installiert. Die automatische Installation dieser Apps bietet Unterstützung für bedingten Zugriff. Benutzer der App Microsoft Intune können Konformitätsprobleme erkennen und beheben. 

## <a name="manage-android-enterprise-app-permissions"></a>Verwalten von Berechtigungen für Android Enterprise-Apps
Android Enterprise erfordert, dass Sie Apps in der Webkonsole von verwaltetem Google Play genehmigen, bevor Sie sie mit Intune synchronisieren und Ihren Benutzern zuweisen. Da Sie diese Apps mit Android Enterprise im Hintergrund und automatisch auf die Geräte der Benutzer übertragen können, müssen Sie die App-Berechtigungen im Interesse aller Ihrer Benutzer akzeptieren. Benutzern werden bei der Installation der Apps keine App-Berechtigungen angezeigt. Daher ist es wichtig, dass Sie diese Berechtigungen verstehen.

Wenn ein App-Entwickler eine neue Version der App mit aktualisierten Berechtigungen veröffentlicht, werden diese Berechtigungen auch dann nicht automatisch akzeptiert, wenn Sie die vorherigen Berechtigungen genehmigt haben. Geräte, auf denen die vorherige Version der App ausgeführt wird, können diese weiterhin verwenden. Die App wird jedoch erst dann aktualisiert, wenn die neuen Berechtigungen genehmigt wurden. Geräte, auf denen die App nicht installiert ist, können die App nicht installieren, solange Sie die neuen Berechtigungen der App nicht genehmigt haben. 

### <a name="update-app-permissions"></a>Aktualisieren von App-Berechtigungen

Besuchen Sie regelmäßig die verwaltete Google Play-Konsole, um zu prüfen, ob neue Berechtigungen vorliegen. Sie können Google Play so konfigurieren, dass eine E-Mail an Sie oder andere Personen gesendet wird, wenn neue Berechtigungen für eine genehmigte App erforderlich sind. Wenn Sie eine App zuweisen und feststellen, dass sie nicht auf Geräten installiert ist, überprüfen Sie folgendermaßen, ob neue Berechtigungen vorliegen:

1. Wechseln Sie zu [Google Play](https://play.google.com/work).
2. Melden Sie sich mit dem Google-Konto an, das Sie zum Veröffentlichen und Genehmigen der Apps verwendet haben.
3. Wählen Sie die Registerkarte **Updates** aus, und überprüfen Sie, ob andere Apps ein Update erfordern.  
    Alle aufgelisteten Apps erfordern neue Berechtigungen und werden erst zugewiesen, wenn diese Berechtigungen angewendet wurden.

Alternativ können Sie Google Play so konfigurieren, dass App-Berechtigungen auf App-Basis automatisch erneut genehmigt werden.

## <a name="additional-managed-google-play-app-reporting-for-android-enterprise-work-profile-devices"></a>Zusätzliche Berichterstellung für verwaltete Google Play-Apps für Android Enterprise-Arbeitsprofilgeräte

Für auf Android Enterprise-Arbeitsprofilgeräten bereitgestellte verwaltete Google Play-Apps können Sie den Status und die Versionsnummer der auf einem Gerät installierten App abrufen, das Intune verwendet. 

## <a name="working-with-managed-google-play-closed-testing-tracks"></a>Arbeiten mit Managed Google Play-Tracks für geschlossene Tests

Sie können eine Nicht-Produktionsversion einer Managed Google Play-App auf Geräte verteilen, die in einem Android Enterprise-Szenario registriert sind (**Android Enterprise-Arbeitsprofil**, **Vollständig verwaltet**, **Dediziert** und **unternehmenseigenes Arbeitsprofil**), um Tests durchzuführen. In Intune wird außerdem angezeigt, ob eine App über einen veröffentlichten Präproduktionsbuild in einem Testtrack verfügt. Sie können diesen Track auch AAD-Benutzergruppen oder Gerätegruppen zuweisen. Der Workflow zum Zuweisen einer Produktionsversion zu einer Gruppe, die derzeit existiert, ist derselbe wie beim Zuweisen eines Nicht-Produktionskanals. Nach der Bereitstellung entspricht der Installationsstatus jedes Tracks der Versionsnummer des Tracks in Managed Google Play. Weitere Informationen finden Sie unter [Tracks für geschlossene Tests von Google Play für Pre-Release-Tests von Apps](https://support.google.com/googleplay/android-developer/answer/3131213).

## <a name="delete-managed-google-play-apps"></a>Löschen von verwalteten Google Play-Apps
Sie können verwaltete Google Play-Apps bei Bedarf aus Microsoft Intune löschen. Um eine verwaltete Google Play-App zu löschen, öffnen Sie Microsoft Intune im Azure-Portal und wählen **Apps** > **Alle Apps** aus. Klicken Sie in der App-Liste auf die Auslassungspunkte (...) rechts neben der verwalteten Google Play-App, und wählen Sie dann in der angezeigten Liste die Option **Löschen** aus. Wenn Sie eine verwaltete Google Play-App aus der App-Liste löschen, wird die Genehmigung für die Google Play-App automatisch aufgehoben.

> [!NOTE]
> Wenn eine App nicht genehmigt ist oder im verwalteten Google Play Store gelöscht wurde, wird sie nicht aus der Liste der Client-Apps in Intune entfernt. Dies ermöglicht es Ihnen, eine Deinstallationsrichtlinie für die App für Benutzer zu erstellen, selbst wenn die App nicht genehmigt ist.
> 
> Informationen zum Deaktivieren von Android Enterprise-Registrierung und -Verwaltung finden Sie unter [Trennen der Verbindung Ihres Android Enterprise-Verwaltungskontos](../enrollment/connect-intune-android-enterprise.md#disconnect-your-android-enterprise-administrative-account).

## <a name="android-enterprise-system-apps"></a>Android Enterprise-System-Apps

Sie können für [dedizierte Android Enterprise-Geräte](../enrollment/android-kiosk-enroll.md) oder [ vollständig verwaltete Geräte](../enrollment/android-fully-managed-enroll.md) eine Android Enterprise-System-App aktivieren. Weitere Informationen zum Hinzufügen einer Android Enterprise-System-App finden Sie unter [Hinzufügen von Android Enterprise-System-Apps zu Microsoft Intune](apps-ae-system.md).

## <a name="next-steps"></a>Nächste Schritte

- [Das Zuweisen von Apps zu Gruppen](apps-deploy.md)
