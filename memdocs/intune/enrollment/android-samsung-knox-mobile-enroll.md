---
title: Automatisches Registrieren von Android-Geräten mit Samsung Knox Mobile Enrollment (KME)
titleSuffix: Microsoft Intune
description: Informationen zum Registrieren von Android-Geräten mit Samsung KME
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: ''
ms.date: 03/03/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 30df0f9e-6e9e-4d75-a722-3819e33d480d
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2d7ec41361571647cc417dc34ad29522d50477eb
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79339565"
---
# <a name="automatically-enroll-android-devices-by-using-samsungs-knox-mobile-enrollment"></a>Automatisches Registrieren von Android-Geräten mit Samsung Knox Mobile Enrollment

Dieses Thema bietet Ihnen Hilfe beim Einrichten von Intune für die Registrierung unterstützter Android-Geräte mit Samsung Knox Mobile Enrollment (KME). Wenn Sie Intune mit Samsung KME verwenden, können Sie eine große Anzahl unternehmenseigener Android-Geräte registrieren, wenn Endbenutzer ihre Geräte zum ersten Mal einschalten und eine Verbindung mit einem WLAN oder Mobilfunknetz herstellen. Darüber hinaus können Geräte bei Verwendung der Knox Deployment App auch über Bluetooth oder NFC registriert werden.

Um die Intune-Registrierung mit Samsung KME zu aktivieren, müssen Sie sowohl das Intune- als auch das Samsung Knox-Portal in der folgenden Reihenfolge verwenden:

1. Im Knox-Portal:
    1. [Erstellen eines MDM-Profils](#create-mdm-profile)
    2. [Hinzufügen von Geräten](#add-devices)
    3. [Zuweisen eines MDM-Profils für die Geräte](#assign-an-mdm-profile-to-devices)
2. Im Knox-Portal: [Konfigurieren Sie die Endbenutzeranmeldung](#configure-how-end-users-sign-in).
3. [Verteilen Sie die Geräte](#distribute-devices).


Beim Erwerb von Geräten von autorisierten Fachhändlern, die am Knox Deployment Program teilnehmen, wird dem Knox-Portal automatisch eine Liste der Geräte-IDs (Seriennummern und IMEIs) hinzugefügt.


## <a name="prerequisites"></a>Voraussetzungen

Damit Sie sich bei Intune mit KME registrieren können, müssen Sie zuerst Ihr Unternehmen im Samsung Knox-Portal registrieren, indem Sie die folgenden Schritte ausführen:
1. [Stellen Sie sicher, dass KME in Ihrem Land/Ihrer Region verfügbar ist](https://www.samsungknox.com/en/solutions/it-solutions/knox-configure/available-countries): KME steht in mehr als 55 Ländern/Regionen zur Verfügung. Überprüfen Sie, ob Ihr Land/Ihre Region für die Bereitstellung unterstützt wird.

2. [Unterstützte Geräte](https://www.samsungknox.com/en/knox-platform/supported-devices/2.4+): KME ist auf allen Samsung-Geräten ab Knox 2.4 für die Android-Registrierung und ab Knox 2.8 für die Android Enterprise-Registrierung verfügbar.

3. [Netzwerkanforderungen](https://docs.samsungknox.com/KME-Getting-Started/Content/firewall_exceptions.htm): Stellen Sie sicher, dass die erforderlichen Firewall- und Netzwerkzugriffsregeln in Ihrem Netzwerk zugelassen sind.

4. [Registrieren Sie sich für ein Samsung-Konto](https://www2.samsungknox.com/en/user/register): Ein Samsung-Konto ist erforderlich, um KME zu registrieren und zu aktivieren und alle Knox Enterprise-Berechtigungen an einem zentralen Ort zu verwalten.

5. Registrierungsüberprüfung: Nachdem Ihr Profil vervollständigt und übermittelt wurde, überprüft Samsung Ihre Anfrage und genehmigt diese entweder sofort oder versetzt die Anfrage zur weiteren Nachverfolgung in den Überprüfungsstatus „Ausstehend“. Nachdem Ihr Konto genehmigt wurde, können Sie mit weiteren Schritten fortfahren.

## <a name="create-mdm-profile"></a>Erstellen eines MDM-Profils

Wenn Ihr Unternehmen erfolgreich registriert wurde, können Sie Ihr MDM-Profil für Microsoft Intune im Knox-Portal anhand der nachstehenden Informationen erstellen. Sie können MDM-Profile für Android und Android Enterprise im Knox-Portal erstellen.
- Wählen Sie **Geräteadministrator** im Knox-Portal als Profiltyp aus, um ein Android-MDM-Profil zu erstellen. 
- Wählen Sie **Gerätebesitzer** im Knox-Portal als Profiltyp aus, um ein Android Enterprise-MDM-Profil zu erstellen.  

### <a name="for-android"></a>Für Android

| MDM-Profilfelder| Erforderlich? | Werte | 
|-------------------|-----------|-------| 
|Profilname       | Ja       |Geben Sie einen Profilnamen Ihrer Wahl ein. |
|Beschreibung        | Nein        |Geben Sie Text ein, der das Profil beschreibt. |
|MDM Information (MDM-Informationen)     | Ja        |Wählen Sie die Option **Server URI not required for my MDM** (Server-URI nicht für MDM verlangen) aus.| 
|MDM Agent APK      | Ja       |https://aka.ms/intune_kme_deviceowner| 
|Custom JSON        | Ja*        |{"com.google.android.apps.work.clouddpc.EXTRA_ENROLLMENT_TOKEN": "Geben Sie die Zeichenfolge des Intune-Registrierungstokens ein"}. Erfahren Sie, wie Sie Registrierungstoken für [dedizierte Geräte](android-kiosk-enroll.md) und [vollständig verwaltete Geräte](android-fully-managed-enroll.md) erstellen. |
|Skip Setup wizard  | Nein        |Wählen Sie diese Option aus, um die Eingabeaufforderungen für die Standardgeräteeinrichtung für den Endbenutzer zu überspringen.|
|Allow End User to Cancel Enrollment | Nein | Wählen Sie diese Option aus, um Benutzern zu erlauben, KME abzubrechen.|
| Privacy Policy, EULAs and Terms of Service (Datenschutzrichtlinie, EULAs und Nutzungsbedingungen) | Nein | Lassen Sie dieses Feld leer. |
| Support contact details (Supportkontaktinformationen) | Ja | Klicken Sie auf „Bearbeiten“, um die Kontaktinformationen anzupassen. |
|Associate a Knox license with this profile | Nein | Lassen Sie diese Option deaktiviert. Für die Registrierung bei Intune über KME ist keine Knox-Lizenz erforderlich.|

\* Dieses Feld ist nicht erforderlich, um die Profilerstellung im Knox-Portal abzuschließen. Allerdings erfordert Intune, dass dieses Feld ausgefüllt wird, damit das Profil erfolgreich das Gerät in Intune registrieren kann.

### <a name="for-android-enterprise"></a>Für Android Enterprise

Schritt-für-Schritt-Anleitungen finden Sie in den [Samsung-Anweisungen zum Erstellen eines Profils](https://docs.samsungknox.com/KME-Getting-Started/Content/create-profiles.htm).

| MDM-Profilfelder| Erforderlich? | Werte |
|-------------------|-----------|-------|
|Profilname       | Ja       |Geben Sie einen Profilnamen Ihrer Wahl ein.|
|Beschreibung        | Nein        |Geben Sie Text ein, der das Profil beschreibt.|
|Pick your MDM (MDM auswählen) | Ja | Wählen Sie Microsoft Intune aus. |
|MDM Agent APK      | Ja       |https://aka.ms/intune_kme|
|MDM Server URI     | Nein        |Lassen Sie dieses Feld leer.|
|Custom JSON Data (Benutzerdefinierte JSON-Daten)        | Nein        |Lassen Sie dieses Feld leer.|
|Dual DAR | Nein | Lassen Sie dieses Feld leer.|
|QR code for enrollment (QR-Code für die Registrierung) | Nein | Hier können Sie einen QR-Code hinzufügen, um die Registrierung zu beschleunigen.|
|System applications (Systemanwendungen) | Ja | Wählen Sie die Option **Leave all system apps enabled** (Alle System-Apps aktiviert lassen), um sicherzustellen, dass alle Apps für das Profil aktiviert und verfügbar sind. Wenn diese Option nicht aktiviert ist, wird nur eine eingeschränkte Anzahl von System-Apps in der App-Liste des Geräts angezeigt. Apps wie die E-Mail-App werden ausgeblendet. |
|Privacy Policy, EULAs and Terms of Service (Datenschutzrichtlinie, EULAs und Nutzungsbedingungen) | Nein | Lassen Sie dieses Feld leer.|
|Firmenname | Ja | Dieser Name wird bei der Geräteregistrierung angezeigt. |

## <a name="add-devices"></a>Hinzufügen von Geräten

Damit Sie Geräten MDM-Profile zuweisen können, müssen dem Knox-Portal mithilfe einer der folgenden Methoden unterstützte Samsung Knox-Geräte hinzugefügt werden:
- **Verwenden von autorisierten Samsung-Fachhändlern**: Verwenden Sie diese Methode, wenn Sie Geräte von einem der von Samsung zugelassenen Fachhändler erwerben. Bei entsprechender Genehmigung können Fachhändler Geräte für Sie automatisch hochladen. [Rufen Sie den Samsung Knox Enrollment User Guide auf, um Informationen zum Hinzufügen von Fachhändlern zu erhalten](https://docs.samsungknox.com/KME-Getting-Started/Content/Register_resellers.htm).

- **Verwenden der Knox Deployment App (KDA)** : Verwenden Sie diese Methode, wenn Sie über vorhandene Geräte verfügen, die mit KME registriert werden müssen. Bei dieser Methode können Sie Bluetooth oder NFC verwenden, um Geräte zum Knox-Portal hinzuzufügen. [Rufen Sie den Samsung Knox Enrollment User Guide auf, um Informationen zum Verwenden der KDA zu erhalten](https://docs.samsungknox.com/KME-Getting-Started/Content/add-device-info.htm).

## <a name="assign-an-mdm-profile-to-devices"></a>Zuweisen eines MDM-Profils für Geräte
Sie müssen hinzugefügten Geräten im Knox-Portal ein MDM-Profil zuweisen, bevor sie registriert werden können. [Rufen Sie den Samsung Knox Enrollment User Guide auf, um Informationen zur Gerätekonfiguration zu erhalten](https://docs.samsungknox.com/KME-Getting-Started/Content/configure-devices.htm).

## <a name="configure-how-end-users-sign-in"></a>Konfigurieren der Endbenutzeranmeldung

Für bei Intune mit KME für Android registrierte Geräte können Sie wie folgt konfigurieren, wie sich ein Endbenutzer anmelden kann:

- **Ohne Benutzernamenzuordnung**: Lassen Sie im Knox-Portal unter **Gerätedetails** die Felder **Benutzer-ID** und **Kennwort** für die hinzugefügten Geräte leer. Diese Option erfordert, dass der Endbenutzer für die Registrierung bei Intune sowohl einen Benutzernamen als auch ein Kennwort eingeben muss.

- **Mit Benutzernamenzuordnung**: Geben Sie im Knox-Portal unter **Gerätedetails** eine **Benutzer-ID** (z.B. einen Benutzernamen für den zugewiesenen Benutzer oder ein [Geräteregistrierungs-Manager](device-enrollment-manager-enroll.md)-Konto) für die hinzugefügten Geräte an. Diese Option bewirkt, dass der Benutzername vorab ausgefüllt wird und der Endbenutzer für die Registrierung bei Intune ein Kennwort eingeben muss.

> [!NOTE]
>
>Die Benutzerzuordnung gilt nur für die Registrierung mithilfe eines Android-Geräteadministrators. Wenn eine Benutzerzuordnung definiert ist, kann nur der zugeordnete Benutzer das Gerät mit KME registrieren. Dies gilt auch nach einer Zurücksetzung des Geräts auf die Werkseinstellungen. Wenn im Knox-Portal keine Benutzerzuordnung definiert ist, kann jeder Benutzer mit einer gültigen Intune-Lizenz das Gerät mit KME registrieren.
>Selbst wenn bei vollständig verwalteten Android Enterprise-Geräten eine Benutzerzuordnung definiert ist, wird diese nicht an das Gerät weitergegeben und das Gerät nicht an den Benutzer gebunden.
>

## <a name="distribute-devices"></a>Verteilen von Geräten

Nachdem Sie ein MDM-Profil erstellt und zugewiesen, einen Benutzernamen zugeordnet und in Intune die Geräte als unternehmenseigen identifiziert haben, können Sie die Geräte an Benutzer verteilen.

Benötigen Sie weitere Unterstützung? Lesen Sie das vollständige Handbuch [Knox Mobile Enrollment Admin Guide](https://docs.samsungknox.com/KME-Getting-Started/Content/get-started.htm).

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

- **Gerätebesitzerunterstützung** **:**  -  Intune unterstützt das Registrieren von dedizierten und vollständig verwalteten Geräten über das KME-Portal. Weitere Modi für Android Enterprise-Gerätebesitzer werden unterstützt, wenn sie in Intune zur Verfügung stehen.

- **Keine Unterstützung für Arbeitsprofile**: KME ist eine Registrierungsmethode für Unternehmensgeräte, und in einem Android-Arbeitsprofil registrierte Geräte stellen sicher, dass geschäftliche und persönliche Daten auf privaten Geräten voneinander getrennt werden. Deshalb ist die Geräteregistrierung in einem Arbeitsprofil mit KME kein unterstütztes Szenario in Intune.

- **Zurücksetzung auf Werkseinstellungen zum Registrieren bei Android Enterprise**: Wenn Geräte, die bereits eingerichtet wurden, für einen anderen Zweck genutzt werden sollen, müssen sie für die Registrierung bei Android Enterprise auf die Werkseinstellungen zurückgesetzt werden.

- **Google Play-Konto**: Für die Registrierung des Geräts bei Microsoft Intune ist kein Google Play-Konto erforderlich. Bei Registrierungen durch den Android-Geräteadministrator ist für künftige Updates der Intune-Unternehmensportal-App jedoch möglicherweise ein Google Play-Konto auf dem Gerät erforderlich. Ein Google Play-Konto ist nicht erforderlich, wenn die Registrierung bei einem Google-Gerätebesitzer erfolgt.

- **Das Feld „Kennwort“ wird ignoriert**: Wird im Knox-Portal unter **Gerätedetails** das Feld **Kennwort** aufgefüllt, wird es während der Android-Registrierung von der Intune-Unternehmensportal-App ignoriert. Der Endbenutzer muss auf dem Gerät ein Kennwort eingeben, um die Geräteregistrierung abzuschließen.


## <a name="getting-support"></a>Unterstützung erhalten
Erfahren Sie mehr darüber, wie Sie [Support für Samsung KME erhalten](https://docs.samsungknox.com/KME-Getting-Started/Content/to-get-kme-support.htm).


