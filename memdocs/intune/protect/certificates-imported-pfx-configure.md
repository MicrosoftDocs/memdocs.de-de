---
title: Verwenden importierter PFX-Zertifikate in Microsoft Intune – Azure | Microsoft-Dokumentation
description: So verwenden Sie importierte Public Key Cryptography Standards-Zertifikate (PKCS) mit Microsoft Intune. Importieren Sie Zertifikate, konfigurieren Sie Zertifikatvorlagen, installieren Sie den importierten Intune-PFX-Zertifikatconnector, und erstellen Sie ein importiertes PKCS-Zertifikatprofil.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/29/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda; rimarram
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 630d270202f1064c9e80e7cb87df3929138ee54a
ms.sourcegitcommit: 56a894edd291034510c144c31770cf09e20b2d6c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/10/2020
ms.locfileid: "88048105"
---
# <a name="configure-and-use-imported-pkcs-certificates-with-intune"></a>Konfigurieren und Verwenden importierter PKCS-Zertifikate mit Intune

Microsoft Intune unterstützt die Verwendung importierter PKCS-Zertifikate mit Paaren öffentlicher Schlüssel, die häufig für die S/MIME-Verschlüsselung mit E-Mail-Profilen verwendet werden. Bestimmte E-Mail-Profile in Intune unterstützen eine Option zum Aktivieren von S/MIME, mit der Sie ein S/MIME-Signaturzertifikat und ein S/MIME-Verschlüsselungszertifikat definieren können.

Die S/MIME-Verschlüsselung gestaltet sich schwierig, weil E-Mails mit einem bestimmten Zertifikat verschlüsselt werden:

- Zum Entschlüsseln der E-Mail müssen Sie auf dem Gerät, auf dem Sie die E-Mail lesen, über den privaten Schlüssel des Zertifikats verfügen, mit dem die E-Mail verschlüsselt wurde.
- Vor Ablauf eines Zertifikats auf einem Gerät müssen Sie ein neues Zertifikat importieren, damit Geräte weiterhin neue E-Mails entschlüsseln können. Die Erneuerung dieser Zertifikate wird nicht unterstützt.
- Verschlüsselungszertifikate werden regelmäßig erneuert. Das bedeutet, dass Sie das vorherige Zertifikat auf Ihren Geräten aufbewahren sollten, um sicherzustellen, dass ältere E-Mails weiterhin entschlüsselt werden können.  

Da auf allen Geräten das gleiche Zertifikat verwendet werden muss, können zu diesem Zweck keine [SCEP](certificates-scep-configure.md)- oder [PKCS](certficates-pfx-configure.md)-Zertifikatprofile verwendet werden, da diese Zertifikatübermittlungsmechanismen pro Gerät eindeutige Zertifikate übermitteln.

Weitere Informationen zur Verwendung von S/MIME mit Intune finden Sie unter [Verwenden von S/MIME zum Verschlüsseln von E-Mails](certificates-s-mime-encryption-sign.md).

## <a name="supported-platforms"></a>Unterstützte Plattformen

Intune unterstützt den Import von PFX-Zertifikaten für die folgenden Plattformen:

- Android: Geräteadministrator
- Android Enterprise: vollständig verwaltet
- Android Enterprise: Arbeitsprofil
- Android Enterprise: unternehmenseigen mit Arbeitsprofil
- iOS/iPadOS
- macOS
- Windows 10

## <a name="requirements"></a>Anforderungen

Wenn Sie importierte PKCS-Zertifikate mit Intune verwenden möchten, müssen Sie über folgende Infrastruktur verfügen:

- **PFX-Zertifikatconnector für Microsoft Intune:**

  Jeder Intune-Mandant unterstützt mehrere Instanzen dieses Connectors. Stellen Sie sicher, dass jeder Connector Zugriff auf den privaten Schlüssel hat, mit dem die Kennwörter der hochgeladenen PFX-Dateien verschlüsselt werden.
  Sie können diesen Connector auf demselben Server wie eine Instanz des Microsoft Intune Certificate Connectors installieren.

  Der Connector verarbeitet Anforderungen für PFX-Dateien, die in Intune importiert werden, um E-Mails eines bestimmten Benutzers mit S/MIME zu verschlüsseln.

  Dieser Connector kann sich automatisch selbst installieren, sobald neue Versionen zur Verfügung stehen. Zum Verwenden der Updatefunktion müssen Sie sich vergewissern, dass die Firewalls geöffnet sind, über die der Connector **autoupdate.msappproxy.net** an Port **443** kontaktieren kann.

  Weitere Informationen finden Sie unter [Netzwerkendpunkte für Microsoft Intune](../fundamentals/intune-endpoints.md) und [Anforderungen an die Intune-Netzwerkkonfiguration und Bandbreite](../fundamentals/network-bandwidth-use.md).

- **Windows Server:**

  Sie verwenden einen Windows-Server zum Hosten des PFX-Zertifikatconnectors für Microsoft Intune.  Der Connector wird zum Verarbeiten von Anforderungen für Zertifikate verwendet, die in Intune importiert werden.
  
  Der Connector erfordert Zugriff auf die gleichen Ports wie für verwaltete Geräte. Informationen hierzu finden Sie unter [Netzwerkendpunkte für Microsoft Intune](https://docs.microsoft.com/intune/fundamentals/intune-endpoints#access-for-managed-devices).

  Intune unterstützt die Installation des *Microsoft Intune-Zertifikatconnectors* auf demselben Server, auf dem auch der *PFX-Zertifikatconnector für Microsoft Intune* installiert ist.

  Zur Unterstützung des Connectors muss auf dem Server .NET Framework 4.6 oder höher ausgeführt werden. Wenn .NET Framework 4.6 beim Start der Connectorinstallation nicht installiert ist, wird die Installation automatisch während der Connectorinstallation durchgeführt.

- **Visual Studio 2015 oder höher** (optional):

  Mithilfe von Visual Studio erstellen Sie das PowerShell-Hilfsmodul mit Cmdlets zum Importieren von PFX-Zertifikaten in Microsoft Intune. Die PowerShell-Hilfs-Cmdlets finden Sie unter [PFXImport PowerShell Project in GitHub](https://github.com/microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell).

## <a name="how-it-works"></a>Funktionsweise

Wenn Sie Intune verwenden, um ein **importiertes PFX-Zertifikat** für einen Benutzer bereitzustellen, sind zusätzlich zum Gerät zwei Komponenten relevant:

- **Intune-Dienst**: Speichert die PFX-Zertifikate in einem verschlüsselten Zustand und übernimmt die Bereitstellung des Zertifikats für das Benutzergerät.  Die Kennwörter zum Schutz der privaten Schlüssel der Zertifikate werden vor dem Upload mit einem Hardwaresicherheitsmodul (HSM) oder mit Windows-Kryptografie verschlüsselt. So wird sichergestellt, dass Intune zu keinem Zeitpunkt auf den privaten Schlüssel zugreifen kann.

- **PFX-Zertifikatconnector für Microsoft Intune:** Wenn ein Gerät ein in Intune importiertes PFX-Zertifikat anfordert, werden das verschlüsselte Kennwort, das Zertifikat und der öffentliche Schlüssel des Geräts an den Connector gesendet.  Der Connector entschlüsselt das Kennwort mithilfe des lokalen privaten Schlüssels und verschlüsselt das Kennwort (und bei Verwendung von iOS eventuelle plist-Profile) mit dem Geräteschlüssel erneut, bevor das Zertifikat an Intune zurückgesendet wird.  Intune übergibt dann das Zertifikat an das Gerät, und das Gerät kann es mit dem privaten Schlüssel des Geräts entschlüsseln und das Zertifikat installieren.

## <a name="download-install-and-configure-the-pfx-certificate-connector-for-microsoft-intune"></a>Herunterladen, Installieren und Konfigurieren des PFX-Zertifikatconnectors für Microsoft Intune

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Mandantenverwaltung** > **Connectors und Token** > **Zertifikatconnectors** > **Hinzufügen** aus.

   ![Download des PFX-Zertifikatconnectors für Microsoft Intune](./media/certificates-imported-pfx-configure/download-imported-pfxconnector.png)

3. Befolgen Sie die Anweisungen zum Herunterladen des *PFX-Zertifikatconnectors für Microsoft Intune* an einen Speicherort, der für den Server zugänglich ist, auf dem Sie den Connector installieren möchten.

4. Melden Sie sich nach Abschluss des Downloads beim Server an, und führen Sie das Installationsprogramm aus (PfxCertificateConnectorBootstrapper.exe).  
   - Wenn Sie den Standardspeicherort für die Installation übernehmen, wird der Connector in `Program Files\Microsoft Intune\PFXCertificateConnector` installiert.
   - Der Connectordienst wird auf dem lokalen Systemkonto ausgeführt. Wenn für den Internetzugriff ein Proxy erforderlich ist, müssen Sie sicherstellen, dass das lokale Dienstkonto auf die Proxyeinstellungen auf dem Server zugreifen kann.

5. Nach der Installation wird die Registerkarte **Registrierung** vom PFX Certificate Connector für Microsoft Intune geöffnet. Klicken Sie auf **Anmelden**, und geben Sie anschließend ein Konto mit Berechtigungen eines globalen Administrators oder Intune-Administrators an, um die Verbindung mit Intune zu aktivieren.

   > [!WARNING]
   > Standardmäßig ist **Verstärkte Sicherheitskonfiguration für IE** in Windows Server auf **Ein** festgelegt. Dies kann zu Problemen bei der Office 365-Anmeldung führen.

6. Schließen Sie das Fenster.

7. Wechseln Sie im Microsoft Endpoint Manager Admin Center zurück zu **Mandantenverwaltung** > **Connectors und Token** > **Zertifikatconnectors**. Nach wenigen Augenblicken wird ein grünes Häkchen angezeigt, und der Verbindungsstatus wird aktualisiert. Der Connectorserver kann jetzt mit Intune kommunizieren.

## <a name="import-pfx-certificates-to-intune"></a>Importieren von PFX-Zertifikaten in Intune

Sie verwenden [Microsoft Graph](https://docs.microsoft.com/graph) zum Importieren Ihrer PFX-Benutzerzertifikate in Intune. Das Hilfsprogramm [PFXImport PowerShell Project in GitHub](https://github.com/microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell) bietet Ihnen Cmdlets, mit denen Sie die Vorgänge problemlos ausführen können.

Wenn Sie Ihre eigene benutzerdefinierte Lösung mit Graph einsetzen möchten, verwenden Sie den [userPFXCertificate-Ressourcentyp](https://docs.microsoft.com/graph/api/resources/intune-raimportcerts-userpfxcertificate?view=graph-rest-beta).

### <a name="build-pfximport-powershell-project-cmdlets"></a>Erstellen von PFXImport PowerShell Project-Cmdlets

Um die PowerShell-Cmdlets verwenden zu können, erstellen Sie das Projekt selbst mithilfe von Visual Studio. Der Prozess ist unkompliziert. Auch wenn er auf dem Server ausgeführt werden kann, empfehlen wir die Ausführung auf Ihrer Arbeitsstation.  

1. Wechseln Sie zum Stamm des GitHub-Repositorys [Intune-Resource-Access](https://github.com/microsoft/Intune-Resource-Access), und laden Sie dann das Repository mit Git auf Ihren Computer herunter, oder klonen Sie es.

   ![GitHub-Downloadschaltfläche](./media/certificates-imported-pfx-configure/github-download.png)

2. Wechseln Sie zu `.\Intune-Resource-Access-develop\src\PFXImportPowershell\`, und öffnen Sie das Projekt in Visual Studio über die Datei **PFXImportPS.sln**.

3. Wechseln Sie im oberen Bereich von **Debuggen** zu **Release**.

4. Wechseln Sie zu **Build**, und wählen Sie **PFXImportPS erstellen** aus. Nach wenigen Augenblicken wird die Bestätigung **Buildvorgang erfolgreich** im unteren linken Bereich von Visual Studio angezeigt.

   ![Visual Studio-Buildoption](./media/certificates-imported-pfx-configure/vs-build-release.png)

5. Beim Buildprozess wird unter `.\Intune-Resource-Access-develop\src\PFXImportPowershell\PFXImportPS\bin\Release` ein neuer Ordner mit dem PowerShell-Modul erstellt.

   Diesen Ordner **Release** verwenden Sie für die nächsten Schritte.

### <a name="create-the-encryption-public-key"></a>Erstellen des öffentlichen Verschlüsselungsschlüssels

Sie importieren PFX-Zertifikate und die zugehörigen privaten Schlüssel in Intune. Das Kennwort, das den privaten Schlüssel schützt, wird mit einem lokal gespeicherten öffentlichen Schlüssel verschlüsselt. Sie können entweder Windows-Kryptografie, ein Hardwaresicherheitsmodul oder einen anderen Kryptografietyp verwenden, um die Paare aus öffentlichem und privatem Schlüssel zu generieren und zu speichern.  Abhängig vom verwendeten Kryptografietyp kann das Paar aus öffentlichem und privatem Schlüssel zu Sicherungszwecken in ein Dateiformat exportiert werden.

Das PowerShell-Modul stellt Methoden zum Erstellen eines Schlüssels mithilfe der Windows-Kryptografie bereit. Sie können zum Erstellen eines Schlüssels auch andere Tools verwenden.  

#### <a name="to-create-the-encryption-key-using-windows-cryptography"></a>So erstellen Sie den Verschlüsselungsschlüssel mithilfe der Windows-Kryptografie

1. Kopieren Sie den von Visual Studio erstellten Ordner *Release* auf den Server, auf dem Sie den **PFX-Zertifikatconnector für Microsoft Intune** installiert haben. Dieser Ordner enthält das PowerShell-Modul.

2. Auf dem Server öffnen Sie *PowerShell* als Administrator und navigieren dann zu dem Ordner *Release*, der das PowerShell-Modul enthält.

3. Um das Modul zu importieren, führen Sie `Import-Module .\IntunePfxImport.psd1` aus.

4. Führen Sie anschließend `Add-IntuneKspKey -ProviderName "Microsoft Software Key Storage Provider" -KeyName "PFXEncryptionKey"` aus.

   > [!TIP]
   > Der von Ihnen verwendete Anbieter muss erneut ausgewählt werden, wenn Sie PFX-Zertifikate importieren. Sie können den **Microsoft-Anbieter für Softwareschlüsselspeicher** verwenden, aber auch die Verwendung eines anderen Anbieters wird unterstützt. Der Schlüsselname wird auch als Beispiel angegeben, und Sie können einen anderen Schlüsselnamen Ihrer Wahl verwenden.

   Wenn Sie beabsichtigen, das Zertifikat von Ihrer Arbeitsstation zu importieren, können Sie diesen Schlüssel mit dem folgenden Befehl in eine Datei exportieren: `Export-IntunePublicKey -ProviderName "<ProviderName>" -KeyName "<KeyName>" -FilePath "<File path\Filename.PFX>"`

   Der private Schlüssel muss auf dem Server importiert werden, der den PFX-Zertifikatconnector für Microsoft Intune hostet, damit importierte PFX-Zertifikate erfolgreich verarbeitet werden können.

#### <a name="to-use-a-hardware-security-module-hsm"></a>So verwenden Sie ein Hardwaresicherheitsmodul (HSM)

Sie können ein Hardwaresicherheitsmodul (HSM) verwenden, um das Paar aus öffentlichem und privatem Schlüssel zu generieren und zu speichern. Weitere Informationen finden Sie in der Dokumentation des HSM-Anbieters.

### <a name="import-pfx-certificates"></a>Importieren von PFX-Zertifikaten

Im folgenden Verfahren werden die PowerShell-Cmdlets als Beispiel für den Import der PFX-Zertifikate verwendet. Je nach Ihren Anforderungen können Sie andere Optionen auswählen.

Zu den Optionen gehören:

- Beabsichtigter Zweck (gruppiert Zertifikate basierend auf einem Tag):
  - Nicht zugewiesen
  - smimeEncryption
  - smimeSigning

- Auffüllungsschema:
  - oaepSha256
  - oaepSha384
  - oaepSha512

Wählen Sie den Schlüsselspeicheranbieter aus, der dem Anbieter entspricht, den Sie zum Erstellen des Schlüssels verwendet haben.

#### <a name="to-import-the-pfx-certificate"></a>So importieren Sie das PFX-Zertifikat  

1. Exportieren Sie die Zertifikate aus einer beliebigen Zertifizierungsstelle, indem Sie die Dokumentation des Anbieters befolgen.  Für Microsoft Active Directory-Zertifikatdienste können Sie [dieses Beispielskript](https://gallery.technet.microsoft.com/Export-CMPfxCertificatesFro-d55f687b) verwenden.

2. Auf dem Server öffnen Sie *PowerShell* als Administrator und navigieren dann zu dem Ordner *Release*, der das PowerShell-Modul enthält.

3. Führen Sie zum Importieren des Moduls `Import-Module .\IntunePfxImport.psd1` aus.

4. Führen Sie zum Authentifizieren bei Intune Graph `Set-IntuneAuthenticationToken  -AdminUserName "<Admin-UPN>"` aus.

   > [!NOTE]
   > Weil die Authentifizierung anhand von Graph ausgeführt wird, müssen Sie für die AppID Berechtigungen bereitstellen. Wenn Sie dieses Hilfsprogramm zum ersten Mal verwenden, ist ein *globaler Administrator* erforderlich. Die PowerShell-Cmdlets verwenden die gleiche AppID, die auch für die [PowerShell-Intune-Beispiele](https://github.com/microsoftgraph/powershell-intune-samples) verwendet wird.

5. Konvertieren Sie das Kennwort für jede zu importierende PFX-Datei in eine sichere Zeichenfolge, indem Sie `$SecureFilePassword = ConvertTo-SecureString -String "<PFXPassword>" -AsPlainText -Force` ausführen.

6. Führen Sie zum Erstellen eines **UserPFXCertificate**-Objekts `$userPFXObject = New-IntuneUserPfxCertificate -PathToPfxFile "<FullPathPFXToCert>" $SecureFilePassword "<UserUPN>" "<ProviderName>" "<KeyName>" "<IntendedPurpose>"` aus.

   Beispiel: `$userPFXObject = New-IntuneUserPfxCertificate -PathToPfxFile "C:\temp\userA.pfx" $SecureFilePassword "userA@contoso.com" "Microsoft Software Key Storage Provider" "PFXEncryptionKey" "smimeEncryption"`

   > [!NOTE]
   > Wenn Sie das Zertifikat von einem anderen System als dem Server importieren, auf dem der Connector installiert ist, müssen Sie den folgenden Befehl mit dem Schlüsseldateipfad verwenden: `$userPFXObject = New-IntuneUserPfxCertificate -PathToPfxFile "<FullPathPFXToCert>" $SecureFilePassword "<UserUPN>" "<ProviderName>" "<KeyName>" "<IntendedPurpose>" "<PaddingScheme>" "<File path to public key file>"`
   >
   > *VPN* wird nicht als IntendedPurpose unterstützt. 


7. Importieren Sie das **UserPFXCertificate**-Objekt in Intune, indem Sie `Import-IntuneUserPfxCertificate -CertificateList $userPFXObject` ausführen.

8. Um zu überprüfen, ob das Zertifikat importiert wurde, führen Sie `Get-IntuneUserPfxCertificate -UserList "<UserUPN>"` aus.

9.  Führen Sie `Remove-IntuneAuthenticationToken` als bewährte Methode aus, um den AAD-Tokencache zu bereinigen, ohne darauf zu warten, dass das Token abläuft.

Weitere Informationen zu anderen verfügbaren Befehlen finden Sie in der Infodatei unter [PFXImport PowerShell Project in GitHub](https://github.com/microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell).

## <a name="create-a-pkcs-imported-certificate-profile"></a>Erstellen eines Profils für ein importiertes PKCS-Zertifikat

Nach dem Importieren der Zertifikate in Intune erstellen Sie ein Profil für ein **importiertes PKCS-Zertifikat** und weisen es Azure Active Directory-Gruppen zu:

> [!NOTE]
> Nachdem Sie ein aus PKCS importiertes Zertifikatprofil erstellt haben, sind die Werte **Beabsichtigter Zweck** und **Schlüsselspeicheranbieter** (Key Storage Provider, KSP) im Profil schreibgeschützt und können nicht bearbeitet werden. Wenn Sie für eine dieser Einstellungen einen anderen Wert benötigen, müssen Sie ein neues Profil erstellen und bereitstellen. 

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.

3. Geben Sie die folgenden Eigenschaften ein:
   - **Plattform**: Wählen Sie die Plattform Ihrer Geräte aus.
   - **Profil**: Wählen Sie das **importierte PKCS-Zertifikat** aus.

4. Wählen Sie **Erstellen** aus.

5. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:
   - **Name:** Geben Sie einen aussagekräftigen Namen für das Profil ein. Benennen Sie Ihre Profile, damit Sie diese später leicht wiedererkennen. Ein geeigneter Profilname ist beispielsweise *Profil für importiertes PKCS-Zertifikat für das gesamte Unternehmen*.
   - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.

6. Wählen Sie **Weiter** aus.

7. Geben Sie in den **Konfigurationseinstellungen** die folgenden Eigenschaften ein:

   - **Beabsichtigter Zweck**: Geben Sie den Zweck der Zertifikate an, die für dieses Profil importiert werden. Administratoren können Zertifikate zu unterschiedlichen Zwecken importieren, z. B. zum Signieren oder Verschlüsseln mit S/MIME. Der Zweck, der im Zertifikatprofil ausgewählt wird, entspricht demjenigen des Zertifikatprofils mit den korrekten importierten Zertifikaten. Der beabsichtigte Zweck ist ein Tag zum Gruppieren importierter Zertifikate. Diese Angabe garantiert nicht, dass die mit diesem Tag importierten Zertifikate den beabsichtigten Zweck erfüllen.  

   <!-- Not in new UI:
   - **Certificate validity period**: Unless the validity period was changed in the certificate template, this option defaults to one year.
   -->
   - **Schlüsselspeicheranbieter (KSP)** : Wählen Sie für Windows den Schlüsselspeicherort auf dem Gerät aus.

8. Wählen Sie **Weiter** aus.

9. Weisen Sie in **Bereichstags** (optional) ein Tag zu, um das Profil nach bestimmten IT-Gruppen wie `US-NC IT Team` oder `JohnGlenn_ITDepartment` zu filtern. Weitere Informationen zu Bereichstags finden Sie unter [Verwenden der RBAC und von Bereichstags für verteilte IT](../fundamentals/scope-tags.md).

   Wählen Sie **Weiter** aus.

10. Wählen Sie unter **Zuweisungen** die Benutzer oder Gruppen aus, denen das Profil zugewiesen werden soll. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](../configuration/device-profile-assign.md).

    Wählen Sie **Weiter** aus.

11. (*Gilt nur für Windows 10*) Geben Sie unter **Anwendbarkeitsregeln** einige Anwendbarkeitsregeln an, um die Zuweisung dieses Profils genauer zu spezifizieren. Sie können auswählen, dass das Profil basierend auf der Betriebssystemedition oder der Version eines Geräts zugewiesen oder nicht zugewiesen wird.

    Weitere Informationen finden Sie im Artikel *Erstellen eines Geräteprofils in Microsoft Intune* im Abschnitt [Anwendbarkeitsregeln](../configuration/device-profile-create.md#applicability-rules).

    Wählen Sie **Weiter** aus.

12. Überprüfen Sie die Einstellungen unter **Überprüfen + erstellen**. Wenn Sie auf „Erstellen“ klicken, werden die Änderungen gespeichert, und das Profil wird zugewiesen. Die Richtlinie wird auch in der Profilliste angezeigt.

## <a name="support-for-third-party-partners"></a>Unterstützung für Drittanbieterpartner

Die folgenden Partner stellen unterstützte Methoden oder Tools bereit, die Sie verwenden können, um PFX-Zertifikate in Intune zu importieren.

### <a name="digicert"></a>DigiCert

Wenn Sie PKI Platform von DigiCert nutzen, können Sie das **DigiCert-Importtool für Intune-S/MIME-Zertifikate** verwenden, um PFX-Zertifikate in Intune zu importieren. Wenn Sie dieses Tool verwenden, müssen Sie die Anweisungen im Abschnitt [Importieren von PFX-Zertifikaten in Intune](#import-pfx-certificates-to-intune) nicht mehr befolgen, die weiter oben in diesem Artikel erläutert werden.

Weitere Informationen zum DigiCert-Importtool, einschließlich zur Beschaffung des Tools, finden Sie unter https://knowledge.digicert.com/tutorials/microsoft-intune.html in der DigiCert-Wissensdatenbank.

### <a name="keytalk"></a>KeyTalk

Bei Verwendung des KeyTalk-Diensts können Sie diesen Dienst für den Import von PFX-Zertifikaten in Intune konfigurieren. Nach Abschluss der Integration müssen Sie die Anweisungen im Abschnitt [Importieren von PFX-Zertifikaten in Intune](#import-pfx-certificates-to-intune) nicht mehr befolgen, die weiter oben in diesem Artikel erläutert werden.

Weitere Informationen zur Integration von KeyTalk und Intune finden Sie in der KeyTalk-Wissensdatenbank unter https://keytalk.com/support.

## <a name="next-steps"></a>Nächste Schritte

Das Profil ist nun erstellt, führt aber noch keine Aktionen durch. [Weisen Sie](../configuration/device-profile-assign.md) das neue Geräteprofil zu.
