---
title: Neustarten von Geräten mit Microsoft Intune – Azure | Microsoft-Dokumentation
description: Neustarten von Windows- und iOS-/iPadOS-Geräten mit Microsoft Intune im Azure-Portal mithilfe der Remoteaktion „Neu starten“.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: c707e0c4-391a-4bad-9dfd-9a7799c48dd5
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4e7bc7064fca5355f33aaa16306e452d8ecffb56
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79348899"
---
# <a name="remotely-restart-devices-with-intune"></a>Remoteneustart von Geräten mit Intune


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Die Geräteaktion **Neu starten** führt dazu, dass das von Ihnen gewählte Gerät (innerhalb von 5 Minuten) neu gestartet wird. Der Eigentümer des Geräts wird nicht automatisch über den Neustart benachrichtigt und kann Daten verlieren.

## <a name="supported-platforms"></a>Unterstützte Plattformen

- Windows – unter Windows 8.1 und höher unterstützt
- Windows Phone – Unterstützt auf Windows Phone 8.1 und später
- Android-Kioskgeräte – unterstützt unter Android 7.0 und höher
- iOS/iPadOS – Unterstützt

    > [!Note]  
    > Für diesen Befehl wird ein überwachtes Gerät und das Zugriffsrecht **Gerätesperre** benötigt. Das Gerät wird sofort neu gestartet. Kennungsgeschützte iOS-/iPadOS-Geräte stellen nach dem Neustart nicht wieder eine Verbindung mit einem WLAN-Netzwerk her. Nach dem Neustart kann das Gerät möglicherweise nicht mehr mit dem Server kommunizieren.
- macOS – Nicht unterstützt
- Android- und Android-Arbeitsprofilgeräte: Nicht unterstützt

## <a name="restart-a-device"></a>Neustarten eines Geräts

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
3. Klicken Sie auf **Geräte** > **Alle Geräte**.
4. Wählen Sie aus der Liste der von Ihnen verwalteten Geräten ein Gerät und dann **Neu starten** > **Ja** aus.

## <a name="next-steps"></a>Nächste Schritte

- Klicken Sie auf **Geräte** > **Geräteaktionen**, um den Status der Geräteaktion **Neu starten** anzuzeigen.
