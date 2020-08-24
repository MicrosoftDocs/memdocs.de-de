---
title: Upgraden oder Verwenden des S Modus auf Windows 10-Geräten – Microsoft Intune – Azure | Microsoft-Dokumentation
description: Verwenden Sie Microsoft Intune zum Upgraden von Windows 10-Geräten auf eine andere Edition oder zum Aktivieren des S Modus. Administratoren können ein Gerätekonfigurationsprofil verwenden, um ein Upgrade von Windows 10 Professional auf Windows 10 Enterprise durchzuführen und den S Modus zu verlassen. Sie erhalten Informationen zu unterstützten Upgradepfaden für Windows 10 Pro, N Edition, Education, Cloud, Enterprise, Core, Holographic und Mobile.
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
ms.assetid: ae8b6528-7979-47d8-abe0-58cea1905270
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0e18395aae96adec3bf4bbf60bdcccdd205dc90d
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146336"
---
# <a name="upgrade-windows-10-editions-or-switch-out-of-s-mode-on-devices-using-microsoft-intune"></a>Upgraden von Windows 10-Editionen oder Verlassen des S Modus auf Geräten mit Microsoft Intune

Als Bestandteil Ihrer Lösung für die mobile Geräteverwaltung (Mobile Device Management, MDM) können Sie Ihre Windows 10-Geräte upgraden. Sie können z.B. ein Upgrade Ihrer Windows 10 Professional-Geräte auf Windows 10 Enterprise durchführen. Oder Sie möchten, dass das Gerät den S Modus verlässt.

Der [Windows 10 S Modus](https://support.microsoft.com/help/4456067/windows-10-switch-out-of-s-mode) (öffnet eine weitere Microsoft-Website) ist auf Sicherheit und Leistung ausgelegt. Sie können Intune verwenden, um den S Modus zu verlassen. Das Verlassen des S Modus ist eine Möglichkeit. Sobald Sie den S Modus verlassen haben, können Sie jedoch nicht in den Windows 10 S Modus zurückkehren.

Sehen Sie sich hierzu [Häufig gestellte Fragen](https://support.microsoft.com/help/4020089/windows-10-in-s-mode-faq) zum S Modus an.

Diese Funktion gilt für:

- Windows 10 und höher
- Windows 10 1809 oder höher für S Modus
- Windows Holographic for Business

Diese Features sind in Intune verfügbar und werden vom Administrator konfiguriert. Intune verwendet „Konfigurationsprofile“ zum Erstellen und Anpassen dieser Einstellungen für die Anforderungen Ihrer Organisation. Nachdem Sie diese Features in einem Profil hinzugefügt haben, können Sie das Profil auf Windows 10-Geräte in Ihrer Organisation übertragen oder für sie bereitstellen. Wenn Sie das Profil bereitstellen, aktualisiert Intune automatisch die Geräte oder verlässt den S Modus.

Dieser Artikel listet die unterstützten Upgradepfade auf und zeigt Ihnen, wie Sie das Profil für die Gerätekonfiguration erstellen. Sie können auch alle verfügbaren Upgrade- und S Modus-Einstellungen für [Windows 10](edition-upgrade-windows-settings.md) sehen.

> [!NOTE]
> Wenn Sie später die Richtlinienzuweisung entfernen, wird die Windows-Version auf dem Gerät nicht wiederhergestellt. Das Gerät wird weiterhin wie gewohnt ausgeführt.

## <a name="prerequisites"></a>Voraussetzungen

Bevor Sie Geräte upgraden, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

- Einen gültigen Product Key für die Installation der aktualisierten Version von Windows auf allen Geräten, die das Ziel dieser Richtlinie sind (für Windows 10-Desktopeditionen). Sie können entweder Mehrfachaktivierungsschlüssel (Multiple Activation Keys, MAK) oder KMS-Schlüssel (Key Management Server, Schlüsselverwaltungsserver) verwenden.
- Für Windows 10 Holographic-Editionen können Sie eine Lizenzdatei von Microsoft verwenden. Die Lizenzdatei enthält die Lizenzierungsinformationen zur Installation der aktualisierten Edition auf allen Geräten, die unter diese Richtlinie fallen.
- Die Windows 10-Geräte, denen Sie die Richtlinie zuweisen, müssen bei Microsoft Intune registriert sein. Die Editionsupgraderichtlinie kann nicht für PCs verwendet werden, auf denen die Intune-PC-Clientsoftware ausgeführt wird.

## <a name="supported-upgrade-paths"></a>Unterstützte Upgradepfade

Die folgenden Tabelle enthält die unterstützten Upgradepfade für das Windows 10-Editionsupgradeprofil.

| Upgrade von | Upgrade auf: |
|---|---|
| Windows 10 Pro | Windows 10 Education <br/>Windows 10 Enterprise <br/>Windows 10 Pro Education |
| Windows 10 Pro N-Edition | Windows 10 Education N-Edition <br/>Windows 10 Enterprise N-Edition <br/>Windows 10 Pro Education N-Edition | 
| Windows 10 Pro Education | Windows 10 Education | 
| Windows 10 Pro Education N-Edition | Windows 10 Education N-Edition |
| Windows 10 Cloud | Windows 10 Education <br/>Windows 10 Enterprise <br/>Windows 10 Pro <br/>Windows 10 Pro Education | 
| Windows 10 Cloud N-Edition | Windows 10 Education N-Edition <br/>Windows 10 Enterprise N-Edition <br/>Windows 10 Pro N-Edition <br/>Windows 10 Pro Education N-Edition | 
| Windows 10 Enterprise | Windows 10 Education | 
| Windows 10 Enterprise N-Edition | Windows 10 Education N-Edition | 
| Windows 10 Core | Windows 10 Education <br/>Windows 10 Enterprise <br/>Windows 10 Pro Education | 
| Windows 10 Core N-Edition | Windows 10 Education N-Edition <br/>Windows 10 Enterprise N-Edition <br/>Windows 10 Pro Education N-Edition | 
| Windows 10 Holographic | Windows 10 Holographic for Business |

<!--The following table provides information about the supported upgrade paths for Windows 10 editions in this policy:

![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)  (X) = not supported    
![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)    (green checkmark) = supported    

|Upgrade from edition\Upgrade to edition|Education|Education N|Pro Education|Pro Education N|Enterprise|Enterprise N|Professional|Professional N|Mobile Enterprise|Holographic for Business|
|--------|--------|--------|--------|--------|--------|--------|--------|--------|--------|--------|--------|
|Pro|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Pro N|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Pro Education|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Pro Education N|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Cloud|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Cloud N|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Enterprise|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Enterprise N|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Core|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Core N|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Mobile|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Holographic|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png) -->

## <a name="create-the-profile"></a>Erstellen des Profils

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
3. Geben Sie die folgenden Eigenschaften ein:

    - **Plattform**: Wählen Sie **Windows 10 und höher** aus.
    - **Profil**: Wählen Sie **Upgrade der Edition** aus.

4. Wählen Sie **Erstellen** aus.
5. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:

    - **Name:** Geben Sie einen aussagekräftigen Namen für das neue Profil ein. Geben Sie zum Beispiel `Windows 10 edition upgrade profile` oder `Windows 10 switch off S mode` ein.
    - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.

6. Wählen Sie **Weiter** aus.
7. Geben Sie unter **Konfigurationseinstellungen** die Einstellungen ein, die Sie konfigurieren möchten. Eine Liste aller Einstellungen und ihrer Funktionen finden Sie unter:

    - [Windows 10-Upgrade und S Modus](edition-upgrade-windows-settings.md)
    - [Windows Holographic for Business](holographic-upgrade.md)

8. Wählen Sie **Weiter** aus.

9. Weisen Sie in **Bereichstags** (optional) ein Tag zu, um das Profil nach bestimmten IT-Gruppen wie `US-NC IT Team` oder `JohnGlenn_ITDepartment` zu filtern. Weitere Informationen zu Bereichstags finden Sie unter [Verwenden der RBAC und von Bereichstags für verteilte IT](../fundamentals/scope-tags.md).

    Wählen Sie **Weiter** aus.

10. Wählen Sie unter **Zuweisungen** die Benutzer oder Benutzergruppen aus, denen Ihr Profil zugewiesen werden soll. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](device-profile-assign.md).

    Wählen Sie **Weiter** aus.

11. Überprüfen Sie die Einstellungen unter **Überprüfen + erstellen**. Wenn Sie auf **Erstellen** klicken, werden die Änderungen gespeichert, und das Profil wird zugewiesen. Die Richtlinie wird auch in der Profilliste angezeigt.

Wenn die Geräte das nächste Mal einchecken, wird die Richtlinie angewendet.

## <a name="next-steps"></a>Nächste Schritte

[Überwachen Sie den Profilstatus](device-profile-monitor.md), [nachdem das Profil zugewiesen wurde](device-profile-assign.md).

Sehen sie sich die Upgrade- und S-Modus-Einstellungen für [Windows 10](edition-upgrade-windows-settings.md)- sowie [Windows Holographic for Business](holographic-upgrade.md)-Geräte an.
