---
title: Massenregistrierung für Windows 10
titleSuffix: Microsoft Intune
description: Erstellen eines Pakets für die Massenregistrierung für Microsoft Intune
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 5/21/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1f39c02a-8d8a-4911-b4e1-e8d014dbce95
ms.reviewer: spshumwa
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: eabdae9fcc8bdc3b6c93d5b735a5b9fbf4dcf69a
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078922"
---
# <a name="bulk-enrollment-for-windows-devices"></a>Massenregistrierung für Windows-Geräte

Als Administrator können Sie eine große Anzahl von neuen Windows-Geräten in Azure Active Directory und Intune einbinden. Um Geräte per Massenvorgang bei Ihrem Azure AD-Mandanten zu registrieren, erstellen Sie mit der Windows Configuration Designer-App (WCD) ein Bereitstellungspaket. Durch Anwenden des Bereitstellungspakets auf unternehmenseigene Geräte werden die Geräte in Ihrem Azure AD-Mandanten eingebunden und für die Verwaltung über Intune registriert. Sobald das Paket angewendet wurde, können sich Ihre Azure AD-Benutzer auf dem betreffenden Gerät anmelden.

Azure AD-Benutzer sind auf diesen Geräten Standardbenutzer und erhalten zugewiesene Intune-Richtlinien sowie erforderliche Apps. Windows-Geräte, die mit der Windows-Massenregistrierung in Intune registriert werden, können die Unternehmensportal-App nutzen, um verfügbare Apps zu installieren. 

## <a name="prerequisites-for-windows-devices-bulk-enrollment"></a>Voraussetzungen für die Massenregistrierung von Windows-Geräten

- Geräte mit Windows 10 Creators Update (Build 1703) oder höher
- [Automatische Windows-Registrierung](windows-enroll.md#enable-windows-10-automatic-enrollment)

## <a name="create-a-provisioning-package"></a>Erstellen eines Bereitstellungspakets

1. Laden Sie [Windows Configuration Designer (WCD)](https://www.microsoft.com/store/apps/9nblggh4tx22) aus dem Microsoft Store herunter.
   ![Abbildung der Windows Configuration Designer-App im Store](./media/windows-bulk-enroll/bulk-enroll-store.png)

2. Öffnen Sie die **Windows Configuration Designer**-App, und wählen Sie **Desktopgeräte bereitstellen** aus.
   ![Screenshot: Auswählen der Option zum Bereitstellen von Desktopgeräten in der Windows Configuration Designer-App](./media/windows-bulk-enroll/bulk-enroll-select.png)

3. Das Fenster **Neues Projekt** wird geöffnet, in dem Sie folgende Informationen angeben:
   - **Name**: Der Name für das Projekt
   - **Projektordner**: Speicherort des Projekts
   - **Beschreibung**: Optionale Beschreibung des Projekts ![Screenshot: Angeben von Name, Projektordner und Beschreibung in der Windows Configuration Designer-App](./media/windows-bulk-enroll/bulk-enroll-name.png)

4. Geben Sie einen eindeutigen Namen für Ihre Geräte ein. Die Namen können eine Seriennummer (%SERIENNUMMER%) oder eine zufällige Folge von Zeichen umfassen. Optional können Sie auch einen Product Key eingeben, wenn Sie die Windows-Edition aktualisieren, das Gerät für die gemeinsame Nutzung konfigurieren und vorinstallierte Software entfernen.
   
   ![Abbildung vom Angeben des Namens und Produktschlüssels in der Windows Configuration Designer-App](./media/windows-bulk-enroll/bulk-enroll-device.png)

5. Optional können Sie das WLAN konfigurieren, bei dem sich Geräte beim ersten Start anmelden.  Wenn die Netzwerkgeräte nicht konfiguriert wurden, ist beim ersten Start des Geräts eine kabelgebundene Netzwerkverbindung erforderlich.
   ![Screenshot: Aktivierung eines WLANs, einschließlich Netzwerk-SSID und Netzwerktyp, in der Windows Configuration Designer-App](./media/windows-bulk-enroll/bulk-enroll-network.png)

6. Wählen Sie **Bei Azure AD registrieren**, geben Sie ein Datum für den **Ablauf des Massentokens** ein, und wählen Sie dann **Massentoken abrufen** aus.
   ![Abbildung von der Kontoverwaltung in der Windows Configuration Designer-App](./media/windows-bulk-enroll/bulk-enroll-account.png)

7. Geben Sie Ihre Azure AD-Anmeldeinformationen an, um ein Massentoken abzurufen.
   ![Abbildung vom Anmelden in der Windows Configuration Designer-App im Store](./media/windows-bulk-enroll/bulk-enroll-cred.png)

8. Wählen Sie auf der Seite **Use this account everywhere on this device** (Dieses Konto überall auf dem Gerät verwenden) die Option **This app only** (Nur diese App) aus.

9. Klicken Sie auf **Weiter**, wenn das **Massentoken** erfolgreich abgerufen wurde.

10. Optional können Sie **Anwendungen hinzufügen** und **Zertifikate hinzufügen**. Diese Anwendungen und Zertifikate werden auf dem Gerät bereitgestellt.

11. Optional können Sie Ihr Bereitstellungspaket mit einem Kennwort schützen.  Klicken Sie auf **Erstellen**.
    ![Abbildung vom Paketschutz in der Windows Configuration Designer-App im Store](./media/windows-bulk-enroll/bulk-enroll-create.png)

## <a name="provision-devices"></a>Bereitstellen von Geräten

1. Greifen Sie auf das Bereitstellungspaket zu, das sich an dem unter **Projektordner** in der App angegebenen Speicherort befindet.

2. Wählen Sie aus, wie Sie das Bereitstellungspaket auf das Gerät anwenden möchten.  Ein Bereitstellungspaket kann mit einer der folgenden Methoden auf ein Gerät angewendet werden:
   - Speichern Sie das Paket auf einem USB-Laufwerk, verbinden Sie dieses Laufwerk mit dem Gerät, das Sie per Massenvorgang registrieren möchten, und wenden Sie das Paket während des anfänglichen Setups an.
   - Speichern Sie das Paket in einem Netzwerkordner, und wenden Sie es nach der ersten Einrichtung an.

   Eine Schrittanleitung zum Anwenden eines Bereitstellungspakets finden Sie unter [Anwenden eines Bereitstellungspakets](https://technet.microsoft.com/itpro/windows/configure/provisioning-apply-package).

3. Nachdem das Paket angewendet wurde, wird das Gerät nach ca. 1 Minute automatisch neu gestartet.
   ![Screenshot: Angeben von Name, Projektordner und Beschreibung in der Windows Configuration Designer-App](./media/windows-bulk-enroll/bulk-enroll-add.png)

4. Wenn das Gerät neu gestartet wird, stellt es eine Verbindung mit Azure Active Directory her und registriert sich bei Microsoft Intune.

## <a name="troubleshooting-windows-bulk-enrollment"></a>Problembehandlung bei der Massenregistrierung unter Windows

### <a name="provisioning-issues"></a>Probleme beim Bereitstellen
Diese Bereitstellung ist für die Verwendung auf neuen Windows-Geräten gedacht. Bei Bereitstellungsfehlern ist möglicherweise eine Zurücksetzung des Geräts auf die Werkseinstellungen oder eine Wiederherstellung des Geräts von einem Startimage erforderlich. Folgende Beispiele beschreiben einige mögliche Gründe für Fehler bei der Bereitstellung:

- Wenn ein Bereitstellungspaket versucht, ein Gerät in eine Active Directory-Domäne oder einen Azure Active Directory-Mandanten einzubinden, die bzw. der kein lokales Konto erstellt, ist das Gerät möglicherweise nicht erreichbar, wenn der Einbindungsprozess aufgrund einer nicht vorhandenen Netzwerkverbindung nicht durchgeführt werden kann.
- Skripts, die vom Bereitstellungspaket ausgeführt werden, werden im Systemkontext ausgeführt. Die Skripts können beliebige Änderungen am Gerätedateisystem und an den Konfigurationen vornehmen. Ein schädliches oder fehlerhaftes Skript kann das Gerät in einen Zustand versetzen, aus dem eine Wiederherstellung nur durch erneutes Aufspielen eines Images oder durch Zurücksetzen des Geräts möglich ist.

Sie können überprüfen, ob die Einstellungen in Ihrem Paket im **Provisioning-Diagnostics-Provider**- Administratorprotokoll in der Ereignisanzeige erfolgreich bzw. fehlgeschlagen sind.

### <a name="bulk-enrollment-with-wi-fi"></a>Massenregistrierung über WLAN 

Wenn Sie kein offenes Netzwerk verwenden, müssen Sie [Zertifikate auf Geräteebene](../protect/certificates-configure.md) verwenden, um Verbindungen zu initiieren. Geräte, die per Massenvorgang registriert wurden, können keine benutzerspezifischen Zertifikate für den Netzwerkzugriff verwenden. 

### <a name="conditional-access"></a>Bedingter Zugriff
Der bedingte Zugriff ist für Windows-Geräte nicht verfügbar, die mit der Massenregistrierung registriert wurden.
