---
title: 'Hinzufügen benutzerdefinierter Einstellungen zu Android Enterprise-Geräten in Microsoft Intune: Azure | Microsoft-Dokumentation'
description: Hinzufügen oder Erstellen eines benutzerdefinierten Profils für Android Enterprise-Geräte zum Erstellen in Microsoft Intune
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/18/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 4724d6e5-05e5-496c-9af3-b74f083141f8
ms.reviewer: chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 827b5eb8b65aa59212b9ef990def3c5f191baf7c
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79334430"
---
# <a name="use-custom-settings-for-android-enterprise-devices-in-microsoft-intune"></a>Verwenden benutzerdefinierter Einstellungen für Android Enterprise-Geräte in Microsoft Intune

Mit Microsoft Intune können Sie mit einem „benutzerdefinierten Profil“ benutzerdefinierte Einstellungen für Ihre Android Enterprise-Geräte mit Arbeitsprofilen hinzufügen oder erstellen. Benutzerdefinierte Profile sind ein Feature in Intune. Sie sind dafür da, Geräteeinstellungen und -features hinzuzufügen, die nicht in Intune integriert sind.

Benutzerdefinierte Android Enterprise-Profile verwenden die OMA-URI-Einstellungen (Open Mobile Alliance Uniform Resource Identifier) zum Festlegen verschiedener Features auf Android Enterprise-Geräten. Diese Einstellungen werden in der Regel von den Herstellern der Geräte verwendet, um die Features festzulegen.

Intune unterstützt die folgende begrenzte Anzahl von benutzerdefinierten Android Enterprise-Profilen:

- ./Vendor/MSFT/WiFi/Profile/SSID/Settings: Unter [Verwenden eines Geräteprofils zum Erstellen eines WLAN-Profils mit einem vorinstallierten Schlüssel in Intune](wi-fi-profile-shared-key.md) finden Sie einige Beispiele.
- ./Vendor/MSFT/VPN/Profile/Name/PackageList: Unter [Verwenden eines benutzerdefinierten Microsoft Intune-Profils zum Erstellen eines VPN-Profils pro App für Android-Geräte](android-pulse-secure-per-app-vpn.md) finden Sie einige Beispiele.
- ./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste: Ein Beispiel finden Sie unter [Verwenden von benutzerdefinierten Einstellungen für Android Enterprise-Geräte in Microsoft Intune](#example). Die Einstellung ist ebenfalls in der Benutzeroberfläche verfügbar. Weitere Informationen finden Sie unter [Android Enterprise-Geräteeinstellungen zum Zulassen oder Einschränken von Features mit Intune](device-restrictions-android-for-work.md).

Wenn Sie weitere Einstellungen benötigen, lesen Sie den Artikel [Verwenden und Verwalten von Android Enterprise-Geräten mit OEMConfig in Microsoft Intune](android-oem-configuration-overview.md).

In diesem Artikel erfahren Sie, wie Sie ein benutzerdefiniertes Profil für Android Enterprise-Geräte erstellen. Außerdem wird im Artikel ein Beispiel für ein benutzerdefiniertes Profil aufgezeigt, das Kopier- und Einfügevorgänge blockiert.

## <a name="create-the-profile"></a>Erstellen des Profils

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
3. Legen Sie folgende Einstellungen fest:

    - **Name:** Geben Sie einen aussagekräftigen Namen für das Profil ein. Benennen Sie Ihre Profile, damit Sie diese später leicht wiedererkennen. Ein guter Profilname ist beispielsweise **Benutzerdefiniertes Android Enterprise-Profil**.
    - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.
    - **Plattform**: Wählen Sie **Android Enterprise** aus.
    - **Profiltyp**: Klicken Sie auf **Benutzerdefiniert**.

4. Klicken Sie unter **Benutzerdefinierte OMA-URI-Einstellungen** auf **Hinzufügen**. Legen Sie folgende Einstellungen fest:

    - **Name:** Geben Sie einen eindeutigen Namen für die OMA-URI-Einstellung ein, damit Sie diese leicht finden können.
    - **Beschreibung:** Geben Sie eine Beschreibung ein, die einen Überblick über die Einstellung und andere wichtige Details bietet.
    - **OMA-URI**: Geben Sie den OMA-URI ein, für den Sie eine Einstellung bereitstellen möchten.
    - **Datentyp:** Wählen Sie den Datentyp aus, den Sie für diese OMA-URI-Einstellung verwenden möchten. Folgende Optionen sind verfügbar:

      - Zeichenfolge
      - Zeichenfolge (XML-Datei)
      - Datum und Uhrzeit
      - Ganze Zahl
      - Gleitkomma
      - Boolesch
      - Base64 (Datei)

    - **Wert**: Geben Sie den gewünschten Datenwert an, der dem von Ihnen eingegebenen OMA-URI zugeordnet werden soll. Der Wert hängt vom ausgewählten Datentyp ab. Beim Datentyp **Datum und Uhrzeit** wählen Sie den Wert beispielsweise aus einer Datumsauswahl aus.

    Wenn Sie einige Einstellungen hinzugefügt haben, können Sie auf **Exportieren** klicken. Wenn Sie auf **Exportieren** klicken, wird eine Liste aller hinzugefügten Werte in einer Datei mit durch Trennzeichen getrennten Werten (CSV) erstellt.

5. Klicken Sie auf **OK**, um die Änderungen zu speichern. Fügen Sie nach Bedarf weitere Einstellungen hinzu.
6. Klicken Sie anschließend auf **OK** > **Erstellen**, um das Intune-Profil zu erstellen. Das Profil wird erstellt und in der Liste **Gerätekonfiguration > Konfigurationsprofile** angezeigt.

## <a name="example"></a>Beispiel

In diesem Beispiel erstellen Sie ein benutzerdefiniertes Profil, das Kopier- und Einfügevorgänge zwischen geschäftlichen und persönlichen Apps auf Android Enterprise-Geräten einschränkt.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
3. Legen Sie folgende Einstellungen fest:

    - **Name:** Geben Sie einen aussagekräftigen Namen für das Profil ein. Benennen Sie Ihre Profile, damit Sie diese später leicht wiedererkennen. Geben Sie beispielsweise **android ent block copy paste custom profile** (Android Enterprise, Kopieren und Einfügen blockieren, benutzerdefiniertes Profil) ein.
    - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.
    - **Plattform**: Wählen Sie **Android Enterprise** aus.
    - **Profiltyp**: Klicken Sie auf **Benutzerdefiniert**.

4. Klicken Sie unter **Benutzerdefinierte OMA-URI-Einstellungen** auf **Hinzufügen**. Legen Sie folgende Einstellungen fest:

    - **Name:** Geben Sie zum Beispiel `Block copy and paste` ein.
    - **Beschreibung:** Geben Sie zum Beispiel `Blocks copy/paste between work and personal apps` ein.
    - **OMA-URI**: Geben Sie `./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste` ein.
    - **Datentyp:** Wählen Sie **Boolean** (Boolescher Wert) aus, damit der Wert für den OMA-URI **TRUE** oder **FALSE** ist.
    - **Wert:** Wählen Sie **True** aus.

5. Nachdem Sie die Einstellungen festgelegt haben, sollte Ihre Umgebung in etwa wie folgt aussehen:

    ![Kopieren und Einfügen für das Android Enterprise-Profil blockieren](./media/custom-settings-android-for-work/custom-policy-afw-copy-paste.png)

Wenn Sie dieses Profil einem von Ihnen verwalteten Android Enterprise-Gerät zuweisen, werden Kopier- und Einfügevorgänge zwischen Apps im Arbeitsprofil und im persönlichen Profil blockiert.

## <a name="next-steps"></a>Nächste Schritte

Das Profil ist nun erstellt, führt aber noch keine Aktionen durch. Die nächsten Schritte sind das [Zuweisen von Benutzer- und Geräteprofilen in Microsoft Intune](device-profile-assign.md) und das [Überwachen von Geräteprofilen in Microsoft Intune](device-profile-monitor.md).

Erstellen Sie ein [benutzerdefiniertes Profil auf Android-Geräten](custom-settings-android.md).
