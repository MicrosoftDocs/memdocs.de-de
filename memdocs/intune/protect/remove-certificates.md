---
title: Entfernen von SCEP- und PKCS-Zertifikaten in Microsoft Intune – Azure | Microsoft-Dokumentation
titleSuffix: ''
description: Administratoren können mithilfe der Aktionen „Zurücksetzen“ oder „Außer Betrieb nehmen“ Zertifikate aus Microsoft Intune entfernen. In einigen Szenarios werden Zertifikate automatisch entfernt, wenn z.B. die Registrierung eines Geräts aufgehoben oder eine Konformitätsrichtlinie entfernt wird. In einigen Zertifikaten bleiben Zertifikate automatisch auf dem Gerät erhalten, wenn z.B. die Intune-Lizenz verloren geht oder entfernt wird. Informieren Sie sich über die verschiedenen Möglichkeiten für Android-, Android Enterprise-, iOS-/iPadOS-, macOS- und Windows-Geräte.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: lacranda
ms.openlocfilehash: 90f75420eeb19bf78f41190fa45ae5133e7746d9
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990050"
---
# <a name="remove-scep-and-pkcs-certificates-in-microsoft-intune"></a>Entfernen von SCEP- und PKCS-Zertifikaten in Microsoft Intune

In Microsoft Intune können Sie mithilfe von Zertifikatprofilen des Typs Simple Certificate Enrollment Protocol (SCEP) und Public Key Cryptography Standards (PKCS) Zertifikate zu Geräten hinzufügen.

Diese Zertifikate können anschließend wieder entfernt werden, wenn Sie das Gerät [zurücksetzen](../remote-actions/devices-wipe.md#wipe) oder [außer Betrieb nehmen](../remote-actions/devices-wipe.md#retire). In anderen Szenarien werden Zertifikate automatisch entfernt bzw. verbleiben auf dem Gerät. In diesem Artikel werden einige häufig auftretende Szenarios aufgelistet, und es wird beschrieben, welche Auswirkungen diese auf PKCS- und SCEP-Zertifikate haben.

> [!NOTE]
> Führen Sie die nachfolgenden Schritte in der richtigen Reihenfolge aus, um sicherzustellen, dass Zertifikate für einen Benutzer entfernt bzw. widerrufen werden, der aus einer lokalen Active Directory-Instanz bzw. Azure Active Directory (Azure AD) entfernt wird:
>
> 1. Setzen Sie das Gerät des Benutzers zurück, oder nehmen Sie es außer Betrieb.
> 2. Entfernen Sie den Benutzer aus der lokalen Active Directory-Instanz bzw. aus Azure AD.

## <a name="manually-deleted-certificates"></a>Manuell gelöschte Zertifikate

Das manuelle Löschen eines Zertifikats ist ein plattformübergreifendes Szenario und gilt für Zertifikate, die von SCEP- oder PKCS-Zertifikatsprofilen bereitgestellt werden. So kann beispielsweise ein Benutzer ein Zertifikat von einem Gerät löschen, wenn das Gerät weiterhin einer Zertifikatsrichtlinie unterliegt.

Wenn sich das Gerät in diesem Szenario nach dem Löschen des Zertifikats das nächste Mal bei Intune eincheckt, wird festgestellt, dass es nicht mehr konform ist, da ihm das erwartete Zertifikat fehlt. Intune stellt dann ein neues Zertifikat aus, damit das Gerät wieder den Anforderungen entspricht. Es ist keine weitere Aktion erforderlich, um das Zertifikat wiederherzustellen.

## <a name="windows-devices"></a>Windows-Geräte

### <a name="scep-certificates"></a>SCEP-Zertifikate

SCEP-Zertifikate werden widerrufen *und* entfernt, wenn:

- die Registrierung eines Benutzers aufgehoben wird.
- ein Administrator die Aktion [Zurücksetzen](../remote-actions/devices-wipe.md#wipe) ausführt.
- ein Administrator die Aktion [Außer Betrieb nehmen](../remote-actions/devices-wipe.md#retire) ausführt.
- das Gerät aus einer Azure AD-Gruppe entfernt wird.
- ein Zertifikatprofil aus der Gruppenzuweisung entfernt wird.

SCEP-Zertifikate werden widerrufen, wenn:

- ein Administrator das SCEP-Profil ändert oder aktualisiert.

Das Stammzertifikat wird entfernt, wenn:

- die Registrierung eines Benutzers aufgehoben wird.
- ein Administrator die Aktion [Zurücksetzen](../remote-actions/devices-wipe.md#wipe) ausführt.
- ein Administrator die Aktion [Außer Betrieb nehmen](../remote-actions/devices-wipe.md#retire) ausführt.

SCEP-Zertifikate *verbleiben* auf dem Gerät (d.h., sie werden weder widerrufen noch entfernt), wenn:

- ein Benutzer seine Intune-Lizenz verliert.
- ein Administrator die Intune-Lizenz widerruft.
- ein Administrator den Benutzer oder die Gruppe aus Azure AD entfernt.

### <a name="pkcs-certificates"></a>PKCS-Zertifikate

PKCS-Zertifikate werden widerrufen *und* entfernt, wenn:

- die Registrierung eines Benutzers aufgehoben wird.
- ein Administrator die Aktion [Zurücksetzen](../remote-actions/devices-wipe.md#wipe) ausführt.
- ein Administrator die Aktion [Außer Betrieb nehmen](../remote-actions/devices-wipe.md#retire) ausführt.

Das Stammzertifikat wird entfernt, wenn:

- die Registrierung eines Benutzers aufgehoben wird.
- ein Administrator die Aktion [Zurücksetzen](../remote-actions/devices-wipe.md#wipe) ausführt.
- ein Administrator die Aktion [Außer Betrieb nehmen](../remote-actions/devices-wipe.md#retire) ausführt.

PKCS-Zertifikate *verbleiben* auf dem Gerät (d.h., sie werden weder widerrufen noch entfernt), wenn:

- ein Benutzer seine Intune-Lizenz verliert.
- ein Administrator die Intune-Lizenz widerruft.
- ein Administrator den Benutzer oder die Gruppe aus Azure AD entfernt.
- ein Administrator das PKCS-Profil ändert oder aktualisiert
- ein Zertifikatprofil aus der Gruppenzuweisung entfernt wird.

## <a name="ios-devices"></a>iOS-Geräte

### <a name="scep-certificates"></a>SCEP-Zertifikate

SCEP-Zertifikate werden widerrufen *und* entfernt, wenn:

- die Registrierung eines Benutzers aufgehoben wird.
- ein Administrator die Aktion [Zurücksetzen](../remote-actions/devices-wipe.md#wipe) ausführt.
- ein Administrator die Aktion [Außer Betrieb nehmen](../remote-actions/devices-wipe.md#retire) ausführt.
- das Gerät aus der Azure AD-Gruppe entfernt wird.
- ein Zertifikatprofil aus der Gruppenzuweisung entfernt wird.

SCEP-Zertifikate werden widerrufen, wenn:

- ein Administrator das SCEP-Profil ändert oder aktualisiert.

Das Stammzertifikat wird entfernt, wenn:

- die Registrierung eines Benutzers aufgehoben wird.
- ein Administrator die Aktion [Zurücksetzen](../remote-actions/devices-wipe.md#wipe) ausführt.
- ein Administrator die Aktion [Außer Betrieb nehmen](../remote-actions/devices-wipe.md#retire) ausführt.

SCEP-Zertifikate *verbleiben* auf dem Gerät (d.h., sie werden weder widerrufen noch entfernt), wenn:

- ein Benutzer seine Intune-Lizenz verliert.
- ein Administrator die Intune-Lizenz widerruft.
- ein Administrator den Benutzer oder die Gruppe aus Azure AD entfernt.

### <a name="pkcs-certificates"></a>PKCS-Zertifikate

PKCS-Zertifikate werden widerrufen *und* entfernt, wenn:

- die Registrierung eines Benutzers aufgehoben wird.
- ein Administrator die Aktion [Zurücksetzen](../remote-actions/devices-wipe.md#wipe) ausführt.
- ein Administrator die Aktion [Außer Betrieb nehmen](../remote-actions/devices-wipe.md#retire) ausführt.

Das PKCS-Zertifikat wird entfernt, wenn:

- ein Zertifikatprofil aus der Gruppenzuweisung entfernt wird.

Das Stammzertifikat wird entfernt, wenn:

- die Registrierung eines Benutzers aufgehoben wird.
- ein Administrator die Aktion [Zurücksetzen](../remote-actions/devices-wipe.md#wipe) ausführt.
- ein Administrator die Aktion [Außer Betrieb nehmen](../remote-actions/devices-wipe.md#retire) ausführt.

PKCS-Zertifikate *verbleiben* auf dem Gerät (d.h., sie werden weder widerrufen noch entfernt), wenn:

- ein Benutzer seine Intune-Lizenz verliert.
- ein Administrator die Intune-Lizenz widerruft.
- ein Administrator den Benutzer oder die Gruppe aus Azure AD entfernt.
- ein Administrator das PKCS-Profil ändert oder aktualisiert

## <a name="android-knox-devices"></a>Android KNOX-Geräte

### <a name="scep-certificates"></a>SCEP-Zertifikate

SCEP-Zertifikate werden widerrufen *und* entfernt, wenn:

- die Registrierung eines Benutzers aufgehoben wird.
- ein Administrator die Aktion [Zurücksetzen](../remote-actions/devices-wipe.md#wipe) ausführt.

SCEP-Zertifikate werden widerrufen, wenn:

- ein Administrator die Aktion [Außer Betrieb nehmen](../remote-actions/devices-wipe.md#retire) ausführt.
- das Gerät aus einer Azure AD-Gruppe entfernt wird.
- ein Zertifikatprofil aus der Gruppenzuweisung entfernt wird.
- ein Administrator den Benutzer oder die Gruppe aus Azure AD entfernt.
- ein Administrator das SCEP-Profil ändert oder aktualisiert.

Das Stammzertifikat wird entfernt, wenn:

- die Registrierung eines Benutzers aufgehoben wird.
- ein Administrator die Aktion [Zurücksetzen](../remote-actions/devices-wipe.md#wipe) ausführt.
- ein Administrator die Aktion [Außer Betrieb nehmen](../remote-actions/devices-wipe.md#retire) ausführt.

SCEP-Zertifikate *verbleiben* auf dem Gerät (d.h., sie werden weder widerrufen noch entfernt), wenn:

- ein Benutzer seine Intune-Lizenz verliert.
- ein Administrator die Intune-Lizenz widerruft.
- ein Administrator den Benutzer oder die Gruppe aus Azure AD entfernt.

### <a name="pkcs-certificates"></a>PKCS-Zertifikate

PKCS-Zertifikate werden widerrufen *und* entfernt, wenn:

- die Registrierung eines Benutzers aufgehoben wird.
- ein Administrator die Aktion [Zurücksetzen](../remote-actions/devices-wipe.md#wipe) ausführt.
- ein Administrator die Aktion [Außer Betrieb nehmen](../remote-actions/devices-wipe.md#retire) ausführt.

Das Stammzertifikat wird entfernt, wenn:

- die Registrierung eines Benutzers aufgehoben wird.
- ein Administrator die Aktion [Zurücksetzen](../remote-actions/devices-wipe.md#wipe) ausführt.
- ein Administrator die Aktion [Außer Betrieb nehmen](../remote-actions/devices-wipe.md#retire) ausführt.

PKCS-Zertifikate *verbleiben* auf dem Gerät (d.h., sie werden weder widerrufen noch entfernt), wenn:

- ein Benutzer seine Intune-Lizenz verliert.
- ein Administrator die Intune-Lizenz widerruft.
- ein Administrator den Benutzer oder die Gruppe aus Azure AD entfernt.
- ein Administrator das PKCS-Profil ändert oder aktualisiert
- ein Zertifikatprofil aus der Gruppenzuweisung entfernt wird.


> [!NOTE]
> Android for Work-Geräte sind für die zuvor genannten Szenarios nicht freigegeben.
> Android-Legacygeräte (jedes Profilgerät, das kein Samsung- oder Work-Gerät ist) sind nicht für die Entfernung von Zertifikaten freigegeben.

## <a name="macos-certificates"></a>macOS-Zertifikate

### <a name="scep-certificates"></a>SCEP-Zertifikate

SCEP-Zertifikate werden widerrufen *und* entfernt, wenn:

- die Registrierung eines Benutzers aufgehoben wird.
- ein Administrator die Aktion [Außer Betrieb nehmen](../remote-actions/devices-wipe.md#retire) ausführt.
- das Gerät aus einer Azure AD-Gruppe entfernt wird.
- ein Zertifikatprofil aus der Gruppenzuweisung entfernt wird.

SCEP-Zertifikate werden widerrufen, wenn:

- ein Administrator das SCEP-Profil ändert oder aktualisiert.

SCEP-Zertifikate *verbleiben* auf dem Gerät (d.h., sie werden weder widerrufen noch entfernt), wenn:

- ein Benutzer seine Intune-Lizenz verliert.
- ein Administrator die Intune-Lizenz widerruft.
- ein Administrator den Benutzer oder die Gruppe aus Azure AD entfernt.

> [!NOTE]
> Die Aktion [Zurücksetzen](../remote-actions/devices-wipe.md#wipe) zum Zurücksetzen von macOS-Geräten auf die Werkseinstellungen wird nicht unterstützt.

### <a name="pkcs-certificates"></a>PKCS-Zertifikate

PKCS-Zertifikate werden widerrufen *und* entfernt, wenn:

- die Registrierung eines Benutzers aufgehoben wird.
- ein Administrator die Aktion [Außer Betrieb nehmen](../remote-actions/devices-wipe.md#retire) ausführt.

Das Stammzertifikat wird entfernt, wenn:

- die Registrierung eines Benutzers aufgehoben wird.
- ein Administrator die Aktion [Außer Betrieb nehmen](../remote-actions/devices-wipe.md#retire) ausführt.

PKCS-Zertifikate verbleiben auf dem Gerät (d. h., sie werden weder widerrufen noch entfernt), wenn:

- ein Benutzer seine Intune-Lizenz verliert.
- ein Administrator die Intune-Lizenz widerruft.
- ein Zertifikatprofil aus der Gruppenzuweisung entfernt wird. (Das Profil wird entfernt.)
- ein Administrator den Benutzer oder die Gruppe aus Azure AD entfernt.
- ein Administrator das PKCS-Profil ändert oder aktualisiert

## <a name="next-steps"></a>Nächste Schritte

[Verwenden von Zertifikaten für die Authentifizierung](certificates-configure.md)