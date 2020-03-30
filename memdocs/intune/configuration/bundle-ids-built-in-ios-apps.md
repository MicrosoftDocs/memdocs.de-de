---
title: iOS-/iPadOS-Bündel-IDs für integrierte Apps in Microsoft Intune – Azure | Microsoft-Dokumentation
titleSuffix: ''
description: In diesem Artikel werden die Bündel-IDs für integrierte iOS- und iPadOS-Apps aufgelistet. Verwenden Sie diese Bündel-IDs, um Apps in Gerätekonfigurationsprofilen und Richtlinien in Microsoft Intune explizit zuzulassen.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c7de0b978c24f28988c62854a249505a0598db95
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2020
ms.locfileid: "80084077"
---
# <a name="bundle-ids-for-built-in-ios-and-ipados-apps-you-can-use-in-intune"></a>Bündel-IDs für integrierte iOS- und iPadOS-Apps, die Sie in Intune verwenden können

Beim Konfigurieren von Funktionen auf iOS-/iPadOS-Geräte können Sie auch die integrierten Apps auf iOS-/iPadOS-Geräten hinzufügen. Dieser Artikel enthält eine Liste der Bündel-IDs einiger gängiger integrierter iOS-/iPadOS-Apps. Um die Bündel-ID von anderen Apps zu finden, wenden Sie sich an den Softwarehersteller. Informationen hierzu finden Sie in der Apple-Liste der [iOS-/iPadOS-Bündel-IDs](https://support.apple.com/guide/mdm/ios-bundle-ids-mdm90f60c1ce/web) (öffnet die Website von Apple).

## <a name="bundle-ids"></a>Bündel-IDs

| Paket-ID                   | App-Name     | Herausgeber |
|-----------------------------|--------------|-----------|
| com.apple.AppStore          | App Store    | Apple     |
| com.apple.store.Jolly       | Apple Store  | Apple     |
| com.apple.calculator        | Calculator   | Apple     |
| com.apple.mobilecal         | Kalender     | Apple     |
| com.apple.camera            | Kamera       | Apple     |
| com.apple.mobiletimer       | Clock        | Apple     |
| com.apple.clips             | Clips        | Apple     |
| com.apple.compass           | Compass      | Apple     |
| com.apple.MobileAddressBook | Kontakte     | Apple     |
| com.apple.facetime          | FaceTime     | Apple     |
| com.apple.DocumentsApp      | Dateien        | Apple     |
| com.apple.mobileme.fmf1     | Find Friends | Apple     |
| com.apple.mobileme.fmip1    | Find iPhone  | Apple     |
| com.apple.gamecenter        | Gamecenter  | Apple     |
| com.apple.mobilegarageband  | GarageBand   | Apple     |
| com.apple.Health            | Integrität       | Apple     |
| com.apple.Home              | -Startseite         | Apple     |
| com.apple.iBooks            | iBooks       | Apple     |
| com.apple.iMovie            | iMovie       | Apple     |
| com.apple.itunesconnect.mobile | iTunes Connect | Apple |
| com.apple.MobileStore       | iTunes Store | Apple     |
| com.apple.itunesu           | iTunes U     | Apple     |
| com.apple.Keynote           | Keynote      | Apple     |
| com.apple.mobilemail        | Mail         | Apple     |
| com.apple.Maps              | Zuordnungen         | Apple     |
| com.apple.measure           | Maßeinheit      | Apple     |
| com.apple.MobileSMS         | Nachrichten     | Apple     |
| com.apple.Music             | Musik        | Apple     |
| com.apple.news              | News         | Apple     |
| com.apple.mobilenotes       | Hinweise        | Apple     |
| com.apple.Numbers           | Zahlen      | Apple     |
| com.apple.Pages             | Seiten        | Apple     |
| com.apple.mobilephone       | Telefon        | Apple     |
| com.apple.Photo-Booth       | Photo Booth  | Apple     |
| com.apple.mobileslideshow   | Fotos       | Apple     |
| com.apple.podcasts          | Podcasts     | Apple     |
| com.apple.reminders         | Reminders    | Apple     |
| com.apple.mobilesafari      | Safari       | Apple     |
| com.apple.Preferences       | Einstellung     | Apple     |
| com.apple.shortcuts         | Verknüpfungen    | Apple     |
| com.apple.SiriViewService   | Siri         | Apple     |
| com.apple.stocks            | Stocks       | Apple     |
| com.apple.tips              | Tipps         | Apple     |
| com.apple.tv                | TV           | Apple     |
| com.apple.videos            | Videos       | Apple     |
| com.apple.VoiceMemos        | VoiceMemos   | Apple     |
| com.apple.Passbook          | Wallet       | Apple     |
| com.apple.Bridge            | Überwachen        | Apple     |
| com.apple.weather           | Weather      | Apple     |

## <a name="next-steps"></a>Nächste Schritte

Verwenden Sie diese Bündel-IDs, um [Gerätefunktionen](ios-device-features-settings.md) zu konfigurieren und auf iOS-/iPadOS-Geräten [einige Einstellungen zuzulassen oder einzuschränken](device-restrictions-ios.md).
