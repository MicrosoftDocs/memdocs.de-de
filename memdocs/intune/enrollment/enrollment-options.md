---
title: Registrierungsoptionen für von Microsoft Intune verwaltete Geräte
titleSuffix: ''
description: Eine Liste der Registrierungsoptionen, die Administratoren für von Microsoft Intune verwaltete Geräte festlegen können.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 10/31/2017
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: cf4ad6d4-423f-4826-ab8d-6eb7a7cfb559
search.appverid: MET150
ms.custom: get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 11dba32ea6b8cc9e7851ebb789776d1121e1d7ce
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990543"
---
# <a name="enrollment-options-for-devices-managed-by-intune"></a>Registrierungsoptionen für von Intune verwaltete Geräte

Als Intune-Administrator können Sie die Geräteregistrierung konfigurieren, um Benutzer zu unterstützen und Intune-Funktionen zu aktivieren.  Intune umfasst folgende Registrierungsoptionen:

## <a name="terms-and-conditions"></a>Geschäftsbedingungen

Sie können festlegen, dass für Benutzer die Annahme der Geschäftsbedingungen Ihres Unternehmens erforderlich ist, bevor diese das Unternehmensportal verwenden können, um ihre Geräte zu registrieren und auf Ressourcen wie Unternehmens-Apps und -E-Mails zuzugreifen. Die Konfiguration der Geschäftsbedingungen ist optional. Weitere Informationen zu den [Nutzungsbedingungen](terms-and-conditions-create.md).

## <a name="enrollment-restrictions"></a>Registrierungseinschränkungen

Sie können auswählen, ob die Geräteregistrierung beschränkt werden soll, und zwar durch:
- Geräteplattform
- Anzahl von Geräten pro Benutzer
- Blockieren persönlicher Geräte

Weitere Informationen zu [Registrierungseinschränkungen](enrollment-restrictions-set.md).

## <a name="enable-apple-device-enrollment"></a>Aktivieren der Apple-Geräteregistrierung

Für die iOS-/iPadOS- und macOS-Geräteregistrierung ist ein MDM-Pushzertifikat erforderlich. Weitere Informationen zu [MDM-Push-Zertifikaten](apple-mdm-push-certificate-get.md).

## <a name="corporate-identifiers"></a>Unternehmensbezeichner

Sie können IMEI-Nummern (IMEI = International Mobile Equipment Identifier) und Seriennummern auflisten, um unternehmenseigene Geräte zu identifizieren. Weitere Informationen zu [Unternehmensbezeichnern](corporate-identifiers-add.md).
## <a name="multi-factor-authentication"></a>Mehrstufige Authentifizierung

Sie können Benutzer dazu auffordern, eine zusätzliche Überprüfungsmethode wie eine Telefonnummer, eine PIN oder biometrische Daten zu verwenden, wenn sie ein Gerät registrieren. Erfahren Sie mehr über die [mehrstufige Authentifizierung](multi-factor-authentication.md).

## <a name="device-enrollment-manager"></a>Geräteregistrierungsmanager
Sie können Benutzer zu Geräteregistrierungs-Managern machen.  DEM-Benutzer (DEM = Device Enrollment Manager, Geräteregistrierungs-Manager) können eine große Anzahl mobiler Geräte mit einem einzelnen Benutzerkonto registrieren. Das DEM-Konto kann bis zu 1.000 Geräte registrieren. Weitere Informationen zu [Geräteregistrierungs-Managern](device-enrollment-manager-enroll.md).

## <a name="device-categories"></a>Gerätekategorien

Sie können mithilfe von Gerätekategorien basierend auf definierten Kategorien automatisch Geräte zu Gruppen hinzufügen. Durch die Organisation von Geräten in Gruppen wird die Verwaltung dieser Geräte vereinfacht. Weitere Informationen zu [Gerätekategorien](device-group-mapping.md).
