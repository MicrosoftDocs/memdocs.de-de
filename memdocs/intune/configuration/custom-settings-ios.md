---
title: Hinzufügen von benutzerdefinierten Einstellungen für iOS-/iPadOS-Geräte in Microsoft Intune – Azure | Microsoft-Dokumentation
titleSuffix: ''
description: Exportieren Sie iOS- und iPadOS-Einstellungen aus Apple Configurator oder dem Apple-Profil-Manager, und importieren Sie diese Einstellungen in Microsoft Intune. Über diese Einstellungen können benutzerdefinierte Einstellungen und Funktionen auf iOS-/iPadOS-Geräten erstellt, verwendet und verwaltet werden. Das benutzerdefinierte Profil kann dann iOS-/iPadOS-Geräten in Ihrer Organisation zugewiesen oder an diese verteilt werden, um eine Baseline oder einen Standard zu erstellen.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/25/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8ac931bf20140865e1185c4f401de0141273cdb3
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80359403"
---
# <a name="use-custom-settings-for-ios-and-ipados-devices-in-microsoft-intune"></a>Verwenden benutzerdefinierter Einstellungen für iOS- und iPadOS-Geräte in Microsoft Intune

Mit Microsoft Intune können Sie benutzerdefinierte Einstellungen für iOS-/iPadOS-Geräte mit einem benutzerdefinierten Profil hinzufügen oder erstellen. Benutzerdefinierte Profile sind ein Feature in Intune. Sie sind dafür da, Geräteeinstellungen und -features hinzuzufügen, die nicht in Intune integriert sind.

Wenn Sie iOS-/iPadOS-Geräte verwenden, gibt es zwei Möglichkeiten, benutzerdefinierte Einstellungen in Intune zu importieren:

- [Apple Configurator](https://itunes.apple.com/app/apple-configurator-2/id1037126344?mt=12)
- [Apple-Profil-Manager](https://support.apple.com/profile-manager)

Mit diesen beiden Tools können Sie Einstellungen in ein Konfigurationsprofil exportieren. Diese Datei importieren Sie dann in Intune und weisen das Profil Ihren iOS-/iPadOS-Benutzern und -Geräten zu. Nach der Zuweisung werden die Einstellungen verteilt. Zudem wird über diese Einstellungen in Ihrer Organisation eine Baseline oder ein Standard für iOS/iPadOS erstellt.

Dieser Artikel enthält eine Anleitung zur Verwendung von Apple Configurator und des Apple-Profil-Managers sowie eine Beschreibung der Eigenschaften, die Sie konfigurieren können.

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie das Profil.](custom-settings-configure.md)

## <a name="what-you-need-to-know"></a>Was Sie wissen müssen

- Wenn Sie das Konfigurationsprofil mit **Apple Configurator** erstellen, vergewissern Sie sich, dass die exportierten Einstellungen mit der iOS-/iPadOS-Version auf den Geräten kompatibel sind. In der **Referenz zu Konfigurationsprofilen** und der **Referenz zum Protokoll für die Verwaltung mobiler Geräte** auf der [Apple Developer-Website](https://developer.apple.com/) finden Sie Informationen zum Beheben von Kompatibilitätsproblemen.

- Beachten Sie bei der Verwendung des **Apple-Profil-Managers** Folgendes:

  - Aktivieren Sie die [Verwaltung mobiler Geräte](https://help.apple.com/serverapp/mac/5.7/#/apd05B9B761-D390-4A75-9251-E9AD29A61D0C) im Profil-Manager.
  - Fügen Sie im Profil-Manager [iOS-/iPadOS-Geräte](https://help.apple.com/profilemanager/mac/5.7/#/pm9onzap1984) hinzu.
  - Nachdem Sie ein Gerät im Profil-Manager hinzugefügt haben, navigieren Sie zu **Bibliothek** > **Geräte**, wählen Sie Ihr Gerät aus, und klicken Sie auf **Einstellungen**. Legen Sie die allgemeinen Einstellungen für das Gerät fest.

    Laden Sie diese Datei herunter, und speichern Sie sie. Diese Datei fügen Sie in das Intune-Profil ein.

  - Vergewissern Sie sich, dass die Einstellungen, die Sie aus dem Apple-Profil-Manager exportieren, mit der iOS-/iPadOS-Version auf den Geräten kompatibel sind. In der **Referenz zu Konfigurationsprofilen** und der **Referenz zum Protokoll für die Verwaltung mobiler Geräte** auf der [Apple Developer-Website](https://developer.apple.com/) finden Sie Informationen zum Beheben von Kompatibilitätsproblemen.

## <a name="custom-configuration-profile-settings"></a>Einstellungen für das benutzerdefinierte Konfigurationsprofil

- **Name des benutzerdefinierten Konfigurationsprofils:** Geben Sie einen Namen für die Richtlinie ein. Dieser Name wird auf dem Gerät und im Intune-Status angezeigt.
- **Konfigurationsprofildatei:** Navigieren Sie zum mit Apple Configurator oder dem Apple-Profil-Manager erstellten Konfigurationsprofil. Die maximale Dateigröße beträgt `1000000` Bytes (annähernd 1 MB). Die importierte Datei wird im Bereich **Dateiinhalt** angezeigt.

  Sie können Ihren benutzerdefinierten Konfigurationsdateien auch Gerätetoken hinzufügen. Gerätetoken werden verwendet, um gerätespezifische Informationen hinzuzufügen. Geben Sie zum Beispiel zur Anzeige der Seriennummer `{{serialnumber}}` ein. Auf dem Gerät wird ein Text angezeigt, der für jedes Gerät eindeutig ist und der etwa folgendermaßen aussieht: `123456789ABC`. Achten Sie darauf, bei der Eingabe von Variablen geschweifte Klammern `{{ }}` zu verwenden. [App-Konfigurationstoken](../apps/app-configuration-policies-use-ios.md#tokens-used-in-the-property-list) umfassen eine Reihe von Variablen, die Sie nutzen können. Zudem können Sie `deviceid` oder einen anderen gerätespezifischen Wert verwenden.

  > [!NOTE]
  > Variablen werden in der Benutzeroberfläche nicht überprüft, und die Groß-/Kleinschreibung muss beachtet werden. Daher gibt es möglicherweise Profile, die mit fehlerhaften Eingaben gespeichert wurden. Wenn Sie beispielsweise `{{DeviceID}}` anstelle von `{{deviceid}}` eingeben, wird die Zeichenfolge anstelle der eindeutigen Geräte-ID angezeigt. Vergewissern Sie sich, dass die eingegebenen Informationen korrekt sind.

## <a name="next-steps"></a>Nächste Schritte

Das Profil ist nun erstellt, führt aber noch keine Aktionen durch. [Weisen Sie anschließend das Profil zu](device-profile-assign.md).

Weitere Informationen finden Sie im [Artikel zum Erstellen eines Profils auf einem macOS-Gerät](custom-settings-macos.md). 
