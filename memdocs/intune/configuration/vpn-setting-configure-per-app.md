---
title: Einrichten eines Pro-App-VPN für iOS-Geräte in Intune – Azure | Microsoft-Dokumentation
description: In diesem Artikel erfahren Sie mehr über die Voraussetzungen, das Erstellen einer Gruppe für VPN-Benutzer (virtuelles privates Netzwerk), das Hinzufügen eines SCEP-Zertifikatprofils, das Konfigurieren eines Pro-App-VPN-Profils sowie das Zuweisen von Apps zum VPN-Profil in Microsoft Intune auf iOS/iPadOS-Geräten. Außerdem werden die Schritte zur Überprüfung der VPN-Verbindung auf dem Gerät beschrieben.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: D9958CBF-34BF-41C2-A86C-28F832F87C94
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1d52e968b5e35490027c7887b597608e25476e24
ms.sourcegitcommit: 19f5838eb3eb8724d22382f36f9564ac9a978b97
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/29/2020
ms.locfileid: "87365456"
---
# <a name="set-up-per-app-virtual-private-network-vpn-for-iosipados-devices-in-intune"></a>Einrichten eines Pro-App-VPN für iOS-Geräte in Intune

Sie können in Microsoft Intune VPNs erstellen und verwenden, die nur bestimmten Apps zugewiesen sind. Dieses Feature heißt „Pro-App-VPN“. Sie wählen die verwalteten Apps aus, die das VPN auf Geräten verwenden können, die von Intune verwaltet werden. Wenn Sie ein Pro-App-VPN verwenden, stellen Benutzer automatisch eine Verbindung über das VPN her und erhalten Zugriff auf Unternehmensressourcen wie etwa Dokumente.

Diese Funktion gilt für:

- iOS 9 und höher
- iOS 13.0 und höher

Informieren Sie sich in der Dokumentation Ihres VPN-Anbieters, um zu erfahren, ob Ihr VPN Pro-App-VPNs unterstützt.

In diesem Artikel erfahren Sie, wie Sie ein Pro-App-VPN-Profil erstellen und dieses Profil Ihren Apps zuweisen. Anhand der folgenden Schritte können Sie Ihren Endbenutzern nahtlos Pro-App-VPNs zur Verfügung stellen. Bei den meisten VPNs, die ein Pro-App-VPN unterstützen, öffnen Benutzer eine App, und die Verbindung zum VPN wird automatisch hergestellt.

Bei einigen VPNs ist auch eine Authentifizierung mit Anmeldeinformationen für ein Pro-App-VPN möglich. Das bedeutet, dass Benutzer einen Benutzernamen und ein Kennwort eingeben müssen, um eine Verbindung mit dem VPN herzustellen.

> [!IMPORTANT]
> Es gibt ein bekanntes Problem in iOS 13, das Pro-App-VPN-Profile daran hindert, in Benutzerregistrierungsumgebungen eine Verbindung herzustellen, wenn die zertifikatbasierte Authentifizierung verwendet wird. Apple plant, dies in einem zukünftigen Release von iOS zu beheben.

> [!IMPORTANT]
> Pro-App-VPN wird für IKEv2 VPN-Profile für iOS/iPadOS nicht unterstützt.

## <a name="per-app-vpn-with-zscaler"></a>Pro-App-VPN mit Zscaler

Zscaler Private Access (ZPA) kann für die Authentifizierung mit Azure Active Directory integriert werden. Bei ZPA benötigen Sie weder ein Profil mit einem [vertrauenswürdigen Zertifikat](#create-a-trusted-certificate-profile) noch ein Profil mit einem [SCEP- oder PKCS-Zertifikat](#create-a-scep-or-pkcs-certificate-profile) (dies wird in diesem Artikel beschrieben). Wenn Sie ein Pro-App-VPN-Profil für Zscaler eingerichtet haben, wird beim Öffnen einer verknüpften App nicht automatisch eine Verbindung mit ZPA hergestellt. Stattdessen muss sich der Benutzer zunächst bei der Zscaler-App anmelden. Dann ist der Remotezugriff auf die verknüpften Apps beschränkt.

## <a name="prerequisites-for-per-app-vpn"></a>Voraussetzungen für das Pro-App-VPN

> [!IMPORTANT]
> Ihr VPN-Anbieter hat möglicherweise andere Anforderungen wie spezielle Hardware oder bestimmte Lizenzen für die Nutzung des Pro-App-VPN. Vor der Einrichtung des Pro-App-VPN ist es daher erforderlich, dass Sie sich mit der Anbieterdokumentation vertraut machen und die beschriebenen Anforderungen erfüllen.

Um ihre Identität nachzuweisen, zeigt der VPN-Server das Zertifikat an, das vom Gerät ohne Aufforderung akzeptiert werden muss. Erstellen Sie ein Profil mit einem vertrauenswürdigen Zertifikat, das das durch die Zertifizierungsstelle (CA) ausgegebene Stammzertifikat des VPN-Servers enthält, um die automatische Genehmigung des Zertifikats sicherzustellen.

### <a name="export-the-certificate-and-add-the-ca"></a>Exportieren Sie das Zertifikat, und fügen Sie die CA hinzu.

1. Öffnen Sie die Verwaltungskonsole auf Ihrem VPN-Server.
2. Stellen Sie sicher, dass Ihr VPN-Server die zertifikatbasierte Authentifizierung verwendet. 
3. Exportieren Sie das vertrauenswürdige Zertifikat der Stammzertifizierungsstelle. Es verfügt über eine CER-Erweiterung, und Sie fügen es hinzu, wenn Sie ein vertrauenswürdiges Zertifikatprofil erstellen.
4. Fügen Sie den Namen der Zertifizierungsstelle hinzu, die das Zertifikat für die Authentifizierung an den VPN-Server ausgestellt hat.

    Wenn die vom Gerät vorgelegte Zertifizierungsstelle mit einer CA in der Liste der vertrauenswürdigen Zertifizierungsstellen auf dem VPN-Server übereinstimmt, authentifiziert der VPN-Server das Gerät.

## <a name="create-a-group-for-your-vpn-users"></a>Erstellen einer Gruppe für Ihre VPN-Benutzer

Erstellen oder wählen Sie eine vorhandene Gruppe in Azure Active Directory aus, die die Benutzer oder Geräte enthält, die Zugriffsberechtigungen für das Pro-App-VPN haben. Unter [Hinzufügen von Gruppen zum Organisieren von Benutzern und Geräten](../fundamentals/groups-add.md) erfahren Sie, wie Sie eine neue Gruppe erstellen.

## <a name="create-a-trusted-certificate-profile"></a>Erstellen eines vertrauenswürdigen Zertifikatprofils

Importieren Sie das Stammzertifikat des VPN-Servers, das von der Zertifizierungsstelle ausgegeben wurde, in ein in Intune erstelltes Profil. Das Profil des vertrauenswürdigen Zertifikats weist das iOS/iPadOS-Gerät an, automatisch der CA zu vertrauen, die der VPN-Server präsentiert.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
3. Geben Sie die folgenden Eigenschaften ein:

    - **Plattform**: Wählen Sie **iOS/iPadOS** aus.
    - **Profil**: Wählen Sie **Vertrauenswürdiges Zertifikat**.

4. Wählen Sie **Erstellen** aus.
5. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:

    - **Name:** Geben Sie einen aussagekräftigen Namen für das Profil ein. Benennen Sie Ihre Profile, damit Sie diese später leicht wiedererkennen. Ein geeigneter Profilname ist beispielsweise **VPN-Profil für vertrauenswürdiges iOS/iPadOS-Zertifikat für das gesamte Unternehmen** .
    - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.

6. Wählen Sie **Weiter** aus.
7. Wählen Sie in **Konfigurationseinstellungen** das Ordnersymbol aus, und navigieren Sie zu Ihrem VPN-Zertifikat (CER-Datei), das Sie über Ihre VPN-Verwaltungskonsole exportiert haben.
8. Wählen Sie **Weiter** aus, und setzen Sie die Erstellung des Profils fort. Weitere Informationen finden Sie unter [Erstellen von VPN-Profilen](vpn-settings-configure.md#create-the-profile).

    > [!div class="mx-imgBorder"]
    > ![Erstellen eines Profils mit einem vertrauenswürdigen Zertifikat für iOS/iPadOS-Geräte in Microsoft Intune](./media/vpn-setting-configure-per-app/vpn-per-app-create-trusted-cert.png)

## <a name="create-a-scep-or-pkcs-certificate-profile"></a>Erstellen eines SCEP- oder PKCS-Zertifikatprofils

Durch das Profil des vertrauenswürdigen Stammzertifikats stuft das Gerät den VPN-Server automatisch als vertrauenswürdig ein. Das SCEP- oder PKCS-Zertifikat stellt Anmeldeinformationen aus dem iOS/iPadOS-VPN-Client an den VPN-Server bereit. Durch das Zertifikat kann das Gerät im Hintergrund eine Authentifizierung durchführen, ohne dass der Benutzer zur Eingabe eines Benutzernamens und Kennworts aufgefordert wird. 

In den folgenden Artikeln erfahren Sie mehr zum Konfigurieren und Zuweisen eines Clientauthentifizierungszertifikats:

- [Konfigurieren der Infrastruktur für die Unterstützung von SCEP mit Intune](../protect/certificates-scep-configure.md)
- [Konfigurieren Ihrer Microsoft Intune-Zertifikatsinfrastruktur für PKCS](../protect/certficates-pfx-configure.md)

Achten Sie darauf, dass die Clientauthentifizierung für das Zertifikat konfiguriert wurde. Sie können die Clientauthentifizierung direkt in den SCEP-Zertifikatprofilen festlegen (**Erweiterte Schlüsselverwendung** > **Clientauthentifizierung**). Legen Sie für PKCS die Clientauthentifizierung in der Zertifikatvorlage in der Zertifizierungsstelle fest.

> [!div class="mx-imgBorder"]
> ![Erstellen Sie ein SCEP-Zertifikatprofil in Microsoft Intune, das u. a. das Format des Antragstellernamens, die Schlüsselverwendung und die erweiterte Schlüsselverwendung enthält.](./media/vpn-setting-configure-per-app/vpn-per-app-create-scep-cert.png)

## <a name="create-a-per-app-vpn-profile"></a>Erstellen eines Pro-App-VPN-Profils

Das VPN-Profil enthält das SCEP- oder PKCS-Zertifikat, das die Anmeldeinformationen des Clients, die Verbindungsinformationen für das VPN und das Pro-App-VPN-Flag enthält, das das von der iOS/iPadOS-Anwendung verwendete Pro-App-VPN aktiviert.

1. Wählen Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) die Option **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
3. Geben Sie die folgenden Eigenschaften ein:

    - **Plattform**: Wählen Sie **iOS/iPadOS** aus.
    - **Profil**: Wählen Sie **VPN** aus.

4. Wählen Sie **Erstellen** aus.
5. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:

    - **Name:** Geben Sie einen aussagekräftigen Namen für das benutzerdefinierte Profil ein. Benennen Sie Ihre Profile, damit Sie diese später leicht wiedererkennen. Ein geeigneter Profilname ist beispielsweise **Pro-App-VPN-Profil für iOS/iPadOS für das gesamte Unternehmen**.
    - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.

6. Konfigurieren Sie in den **Konfigurationseinstellungen** die folgenden Einstellungen:

    - **Verbindungstyp:** Wählen Sie Ihre VPN-Client-App aus.
    - **Basis-VPN**: Konfigurieren Sie Ihre Einstellungen. Im Artikel [Hinzufügen von VPN-Einstellungen auf iOS- und iPadOS-Geräten in Microsoft Intune](vpn-settings-ios.md) werden alle Einstellungen aufgelistet und beschrieben. Achten Sie darauf, dass Sie die folgenden Einstellungen wie unten angegeben vornehmen, wenn Sie ein Pro-App-VPN verwenden:

      - **Authentifizierungsmethode**: Wählen Sie **Zertifikate**. 
      - **Authentifizierungszertifikat**: Wählen Sie ein vorhandenes SCEP- oder PKCS-Zertifikat, und klicken Sie anschließend auf **OK**.
      - **Getrenntes Tunneln:** Klicken Sie auf **Disable** (Deaktivieren), um zu erzwingen, dass der gesamte Datenverkehr den VPN-Tunnel durchläuft, wenn die VPN-Verbindung aktiv ist. 

      > [!div class="mx-imgBorder"]
      > ![Festlegen eines Verbindungstyps, einer IP-Adresse oder eines FQDN, einer Authentifizierungsmethode und Aktivieren/Deaktivieren des getrennten Tunnelns im Pro-App-VPN-Profil in Microsoft Intune](./media/vpn-setting-configure-per-app/vpn-per-app-create-vpn-profile.png)

    Informationen zu den anderen Einstellungen finden Sie unter [Hinzufügen von VPN-Einstellungen auf iOS- und iPadOS-Geräten in Microsoft Intune](vpn-settings-ios.md).

    - **Automatisches VPN** > **Typ des automatischen VPN** > **Pro-App-VPN**

      > [!div class="mx-imgBorder"]
      > ![Festlegen des Typs des automatischen VPN auf Pro-App-VPN für iOS/iPadOS-Geräte in Intune](./media/vpn-setting-configure-per-app/vpn-per-app-automatic.png)

7. Wählen Sie **Weiter** aus, und setzen Sie die Erstellung des Profils fort. Weitere Informationen finden Sie unter [Erstellen von VPN-Profilen](vpn-settings-configure.md#create-the-profile).

## <a name="associate-an-app-with-the-vpn-profile"></a>Ordnen Sie dem VPN-Profil eine App zu.

Nachdem Sie Ihr VPN-Profil hinzugefügt haben, ordnen Sie die App und Azure AD-Gruppe dem Profil zu.

1. Wählen Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) die Option **Apps** > **Alle Apps** aus.
2. Wählen Sie eine App aus der Liste und dann **Eigenschaften** > **Zuweisungen** > **Gruppe hinzufügen** aus.
3. Wählen Sie unter **Zuweisungstyp** **Erforderlich** oder **Für registrierte Geräte verfügbar** aus.
4. Wählen Sie **Eingeschlossene Gruppe** > **Wählen Sie die Gruppen aus, die eingeschlossen werden sollen**. Wählen Sie dann die [von Ihnen im Rahmen dieses Artikels erstellte Gruppe aus](#create-a-group-for-your-vpn-users), und klicken Sie auf **Auswählen**.
5. Wählen Sie unter **VPNs** das Pro-App-VPN-Profil aus, [das Sie im Rahmen dieses Artikels erstellt haben](#create-a-per-app-vpn-profile).

    > [!div class="mx-imgBorder"]
    > ![Zuweisen einer App zu einem Pro-App-VPN-Profil in Microsoft Intune](./media/vpn-setting-configure-per-app/vpn-per-app-app-to-vpn.png)

6. Klicken Sie auf **OK** > **Speichern**.

Eine Zuordnung zwischen einer App und einem Profil wird während des nächsten Geräte-Check-Ins entfernt, wenn die folgenden Bedingungen erfüllt sind:

- Die App wurde mit erforderlicher Installationsabsicht ausgerichtet.
- Sowohl das Profil als auch die App sind auf dieselbe Gruppe ausgerichtet.
- Sie entfernen die Pro-App-VPN-Konfiguration aus der App-Zuweisung.

Eine Zuordnung zwischen einer App und einem Profil besteht so lange, bis der Benutzer eine erneute Installation über das Intune-Unternehmensportal anfordert, wenn die folgenden Bedingungen erfüllt sind:

- Die App wurde mit verfügbarer Installationsabsicht ausgerichtet.
- Sowohl das Profil als auch die App sind auf dieselbe Gruppe ausgerichtet.
- Der Endbenutzer hat die App-Installation aus dem Intune-Unternehmensportal angefordert. Dies führt dazu, dass App und Profil auf dem Gerät installiert werden.
- Sie entfernen oder ändern die Pro-App-VPN-Konfiguration über die App-Zuweisung.

## <a name="verify-the-connection-on-the-iosipados-device"></a>Überprüfen der Verbindung auf dem iOS/iPadOS-Gerät

Sobald Ihr Pro-App-VPN eingerichtet und Ihrer App zugeordnet ist, überprüfen Sie, ob die Verbindung von einem Gerät aus funktioniert.

### <a name="before-you-attempt-to-connect"></a>Bevor Sie eine Verbindung herstellen

- Stellen Sie sicher, dass Sie alle der oben erwähnten Richtlinien derselben Gruppe bereitstellen. Ansonsten funktioniert das Pro-App-VPN nicht.
- Wenn Sie die VPN-App Pulse Secure oder eine benutzerdefinierte VPN-Client-App verwenden, können Sie das Tunneln auf App- oder auf Paketebene verwenden. Legen Sie für Tunneln auf App-Ebene den Wert **ProviderType** auf **app-proxy** oder für Tunneln auf Paketebene auf **packet-tunnel** fest. Informieren Sie sich in der Dokumentation Ihres VPN-Anbieters, um sicherzustellen, dass Sie den richtigen Wert verwenden.

### <a name="connect-using-the-per-app-vpn"></a>Herstellen einer Verbindung mithilfe des Pro-App-VPNs

Überprüfen Sie die Zero Touch-Funktion, indem Sie eine Verbindung herstellen, ohne dabei das VPN auswählen oder Ihre Anmeldeinformationen eingeben zu müssen. Die Zero Touch-Funktion bedeutet Folgendes:

- Das Gerät fordert den Benutzer nicht auf, dem VPN-Server zu vertrauen. Dem Benutzer wird also nicht das Dialogfeld **Dynamic Trust** (Dynamische Vertrauensstellung) angezeigt.
- Der Benutzer muss keine Anmeldeinformationen eingeben.
- Das Benutzergerät wird mit dem VPN verbunden, sobald der Benutzer eine der verknüpften Apps öffnet.

## <a name="next-steps"></a>Nächste Schritte

- Navigieren Sie zu [Hinzufügen von VPN-Einstellungen auf iOS- und iPadOS-Geräten in Microsoft Intune](vpn-settings-ios.md), um die iOS/iPadOS-Einstellungen zu überprüfen.
- Weitere Informationen zur VPN-Einstellung und Intune finden Sie unter [Erstellen von VPN-Profilen in Intune](vpn-settings-configure.md).
