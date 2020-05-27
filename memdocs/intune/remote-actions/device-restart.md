---
title: Neustarten von Geräten mit Microsoft Intune – Azure | Microsoft-Dokumentation
description: Neustarten von Windows- und iOS-/iPadOS-Geräten mit Microsoft Intune im Azure-Portal mithilfe der Remoteaktion „Neu starten“.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: c707e0c4-391a-4bad-9dfd-9a7799c48dd5
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e95ceb3aabf4e97d020c52983deea683646fa85d
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83983136"
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
