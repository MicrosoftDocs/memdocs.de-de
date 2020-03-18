---
title: Verwenden einer Drittanbieter-Zertifizierungsstelle mit SCEP in Microsoft Intune – Azure | Microsoft-Dokumentation
description: In Microsoft Intune können Sie eine Zertifizierungsstelle eines Herstellers oder Drittanbieters hinzufügen, die über das SCEP-Protokoll Zertifikate für mobile Geräte ausstellen kann. In dieser Übersicht erhält Microsoft Intune durch eine Azure AD-Anwendung (Azure Active Directory) die Berechtigung zum Überprüfen von Zertifikaten. Mit der Anwendungs-ID, dem Authentifizierungsschlüssel und der Mandanten-ID der AAD-Anwendung stellen Sie anschließend während der Einrichtung des SCEP-Servers Zertifikate aus.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/03/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1dfac34615c208328cab06a3fd047d3a9b99c794
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79353891"
---
# <a name="add-partner-certification-authority-in-intune-using-scep"></a>Hinzufügen einer Partnerzertifizierungsstelle in Intune mithilfe von SCEP

Verwenden Sie Zertifizierungsstellen von Drittanbietern mit Intune. Zertifizierungsstellen von Drittanbietern stellen neue oder erneuerte Zertifikate für mobile Geräte über das Simple Certificate Enrollment-Protokoll (SCEP) aus und können Windows-, iOS-/iPadOS-, Android- und macOS-Geräte unterstützen.

Die Nutzung des Features umfasst zwei Aspekte: die Verwendung einer Open Source-API und die Durchführung von Intune-Administratoraufgaben.

**1. Verwenden einer Open Source-API**  
Microsoft hat eine API für die Integration in Intune erstellt. Über diese API können Sie Zertifikate überprüfen, Erfolgs- oder Fehlermeldungen senden und SSL – insbesondere SSLSocketFactory – zur Kommunikation mit Intune verwenden.

Sie können die API aus dem [öffentlichen GitHub-Repository für die Intune-SCEP-API](https://github.com/Microsoft/Intune-Resource-Access/tree/develop/src/CsrValidation) herunterladen und in Ihren Lösungen verwenden. Verwenden Sie diese API mit SCEP-Servern von Drittanbietern, um benutzerdefinierte Aufforderungsüberprüfungen bei Intune auszuführen, bevor SCEP ein Zertifikat für das Gerät bereitstellt.

Unter [Integrieren von Drittanbieter-Zertifizierungsstellen in eine Intune-SCEP-Verwaltungslösung](scep-libraries-apis.md) finden Sie weitere Informationen zur Nutzung der API, deren Methoden und dem Testen der Lösung.

**2. Erstellen der Anwendung und des Profils**  
Mit einer Azure AD-Anwendung können Sie Rechte an Intune delegieren, wodurch sich SCEP-Anforderungen von Geräten verarbeitet lassen. Die Azure AD-Anwendung enthält die Anwendungs-ID und die Authentifizierungsschlüsselwerte, die in der API-Lösung der Entwickler verwendet werden. Administratoren können dann über Intune SCEP-Zertifikatprofile erstellen und bereitstellen und Berichte zum Bereitstellungsstatus auf den Geräten anzeigen.

Dieser Artikel stellt eine Übersicht über dieses Feature aus der Perspektive von Administratoren bereit und geht auch auf die Erstellung einer Azure AD-Anwendung ein.

## <a name="overview"></a>Übersicht

Die folgenden Schritte bieten einen Überblick über die Verwendung von SCEP für Zertifikate in Intune:

1. Ein Administrator erstellt in Intune ein SCEP-Zertifikatprofil für bestimmte Benutzer oder Geräte.
2. Das Gerät verbindet sich mit Intune.
3. Intune erstellt eine eindeutige SCEP-Aufforderung und stellt zusätzliche Informationen zur Integritätsprüfung bereit. Dazu gehören beispielsweise der erwartete Antragstellername und der alternative Antragstellername.
4. Intune verschlüsselt und signiert sowohl die Aufforderung als auch die Informationen zur Integritätsprüfung und sendet diese Informationen dann an das Gerät, das die SCEP-Anforderung stellt.
5. Das Gerät generiert auf der Grundlage des SCEP-Zertifikatprofils, das per Push von Intune übertragen wird, eine Zertifikatsignierungsanforderung (CSR) und ein Schlüsselpaar aus einem öffentlichen und privaten Schlüssel.
6. Die CSR und die verschlüsselt/signierte Aufforderung werden an den SCEP-Server-Endpunkt des Drittanbieters gesendet.
7. Der SCEP-Server sendet die CSR und die Aufforderung an Intune. Intune überprüft anschließend die Signatur, entschlüsselt die Nutzlast und vergleicht die CSR mit den Informationen zur Integritätsprüfung.
8. Intune sendet eine Antwort an den SCEP-Server zurück und gibt an, ob die Überprüfung der Aufforderung erfolgreich war.  
9. Wenn die Überprüfung der Aufforderung erfolgreich war, stellt der SCEP-Server das Zertifikat aus und überträgt es an das Gerät.

Im folgenden Diagramm wird der Ablauf der Drittanbieter-SCEP-Integration in Intune ausführlich dargestellt:

> [!div class="mx-imgBorder"]
> ![Integration von Drittanbieter-Zertifizierungsstellen mittels SCEP in Microsoft Intune](./media/certificate-authority-add-scep-overview/scep-certificate-vendor-integration.png)

## <a name="set-up-third-party-ca-integration"></a>Vorbereitungsschritte zur Integration von Drittanbieter-Zertifizierungsstellen

### <a name="validate-third-party-certification-authority"></a>Überprüfen der Drittanbieter-Zertifizierungsstelle

Vor der Integration von Drittanbieter-Zertifizierungsstellen in Intune muss sichergestellt werden, dass die verwendete Zertifizierungsstelle Intune unterstützt. Im Abschnitt [Drittanbieter-Partnerzertifizierungsstellen](#third-party-certification-authority-partners) weiter unten finden Sie eine Liste mit unterstützten Partnern. Weitere Informationen finden Sie auch im Leitfaden Ihrer Zertifizierungsstelle. Möglicherweise stellt Ihre Zertifizierungsstelle implementierungsspezifische Einrichtungsanleitungen bereit.

### <a name="authorize-communication-between-ca-and-intune"></a>Autorisieren der Kommunikation zwischen Zertifizierungsstelle und Intune

Wen ein SCEP-Server eines Drittanbieters eine benutzerdefinierte Aufforderung für Intune überprüfen soll, ist es erforderlich, eine App in Azure AD zu erstellen. Diese App erteilt Intune delegierte Berechtigungen, mit denen SCEP-Anforderungen überprüft werden.

Achten Sie darauf, dass Sie über die erforderlichen Berechtigungen zum Registrieren einer Azure AD-App verfügen. Siehe [Erforderliche Berechtigungen](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#required-permissions) in der Azure AD-Dokumentation.

#### <a name="create-an-application-in-azure-active-directory"></a>Registrieren einer Anwendung in Azure Active Directory  

1. Navigieren Sie im [Azure-Portal](https://portal.azure.com) zu **Azure Active Directory** > **App-Registrierungen**, und wählen Sie dann **Neue Registrierung** aus.  

2. Geben Sie auf der Seite **Anwendung registrieren** folgende Details an:  
   - Geben Sie im Abschnitt **Name** einen aussagekräftigen Anwendungsnamen ein.  
   - Wählen Sie im Abschnitt **Unterstützte Kontotypen** die Option **Konten in einem Organisationsverzeichnis** aus.  
   - Für **Umleitungs-URI** übernehmen Sie den Standardwert „Web“, und geben Sie dann die Anmelde-URL für den SCEP-Server des Drittanbieters an.  

3. Wählen Sie **Registrieren** aus, um die Anwendung zu erstellen und die Seite „Übersicht“ für die neue App zu öffnen.  

4. Kopieren Sie auf der App-Seite **Übersicht** den Wert der **Anwendungs-ID (Client)** , und notieren Sie ihn zur späteren Verwendung. Sie benötigen diesen Wert später.  

5. Navigieren Sie im Navigationsbereich der App unter **Verwalten** zu **Zertifikate und Geheimnisse**. Wählen Sie die Schaltfläche **Neuer geheimer Clientschlüssel** aus. Geben Sie einen Wert in „Beschreibung“ ein, wählen Sie eine Option für **Gültig bis** aus, und wählen Sie **Hinzufügen** aus, um einen *Wert* für den geheimen Clientschlüssel zu generieren. 
   > [!IMPORTANT]  
   > Bevor Sie diese Seite verlassen, kopieren Sie den Wert für den geheimen Clientschlüssel, und notieren Sie ihn zur späteren Verwendung mit der Zertifizierungsstellenimplementierung Ihres Drittanbieters. Dieser Wert wird nicht erneut angezeigt. Beachten Sie unbedingt den Leitfaden für die Zertifizierungsstelle Ihres Drittanbieters hinsichtlich der Konfiguration der Anwendungs-ID, des Authentifizierungsschlüssels und der Mandanten-ID.  

6. Notieren Sie sich Ihre **Mandanten-ID**. Die Mandanten-ID ist der Domänentext, der auf das @-Zeichen in Ihrem Konto folgt. Wenn Ihr Konto beispielsweise *admin@name.onmicrosoft.com* lautet, ist Ihre Mandanten-ID **name.onmicrosoft.com**.  

7. Wechseln Sie im Navigationsbereich für die App unter **Verwalten** zu **API-Berechtigungen**, und wählen Sie dann **Berechtigung hinzufügen** aus.  

8. Wählen Sie auf der Seite **API-Berechtigungen anfordern** den Eintrag **Intune** aus, und wählen Sie dann **Anwendungsberechtigungen** aus. Aktivieren Sie das Kontrollkästchen für **scep_challenge_provider** (SCEP-Challenge-Validierung).  

   Wählen Sie **Berechtigungen hinzufügen** aus, um diese Konfiguration zu speichern.  

9. Bleiben Sie auf der Seite **API-Berechtigungen**, und wählen Sie den Eintrag **Administratoreinwilligung für Microsoft gewähren** aus, und wählen Sie dann **Ja** aus.  
   
   Der Prozess der App-Registrierung in Azure AD ist abgeschlossen.





### <a name="configure-and-deploy-a-scep-certificate-profile"></a>Konfigurieren und Bereitstellen eines SCEP-Zertifikatprofils
Erstellen Sie als Administrator ein SCEP-Zertifikatprofil für bestimmte Benutzer oder Geräte. Weisen Sie anschließend das Profil zu. Weitere Informationen finden Sie in den folgenden Artikeln:

- [Erstellen eines SCEP-Zertifikatprofils](certificates-profile-scep.md#create-a-scep-certificate-profile)

- [Zuweisen des Zertifikatprofils](certificates-profile-scep.md#assign-the-certificate-profile)

## <a name="removing-certificates"></a>Entfernen von Zertifikaten

Wenn Sie die Registrierung aufheben oder das Gerät zurücksetzen, werden die Zertifikate entfernt. Die Zertifikate werden nicht widerrufen.

## <a name="third-party-certification-authority-partners"></a>Drittanbieter-Partnerzertifizierungsstellen
Intune wird von den folgenden Drittanbieter-Zertifizierungsstellen unterstützt:

- [Entrust Datacard](https://go.entrustdatacard.com/pki/intune/)
- [EJBCA GitHub open-source version (Open Source-Version von EJBCA in GitHub)](https://github.com/agerbergt/intune-ejbca-connector)
- [EverTrust](https://evertrust.fr/en/products/)
- [GlobalSign](https://downloads.globalsign.com/acton/attachment/2674/f-6903f60b-9111-432d-b283-77823cc65500/1/-/-/-/-/globalsign-aeg-microsoft-intune-integration-guide.pdf)
- [IDnomic](https://www.idnomic.com/)
- [Sectigo](https://sectigo.com/products)
- [DigiCert](https://knowledge.digicert.com/tutorials/microsoft-intune.html)
- [Venafi](https://www.venafi.com/platform/enterprise-mobility)
- [SCEPman](https://azuremarketplace.microsoft.com/marketplace/apps/gluckkanja.scepman)

Wenn Sie als Drittanbieter-Zertifizierungsstelle daran interessiert sind, Ihr Produkt in Intune zu integrieren, müssen Sie sich mit dem API-Leitfaden vertraut machen:

- [GitHub-Repository für Intune-SCEP-API](https://github.com/Microsoft/Intune-Resource-Access/tree/develop/src/CsrValidation)
- [Intune-SCEP-API-Leitfaden für Drittanbieter-Zertifizierungsstellen](scep-libraries-apis.md)

## <a name="see-also"></a>Weitere Informationen:

- [Konfigurieren von Zertifikatprofilen](certificates-scep-configure.md)
- [GitHub-Repository für Intune-SCEP-API](https://github.com/Microsoft/Intune-Resource-Access/tree/develop/src/CsrValidation)
- [Intune-SCEP-API-Leitfaden für Drittanbieter-Zertifizierungsstellen](scep-libraries-apis.md)
