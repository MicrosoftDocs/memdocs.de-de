---
title: Abrufen eines Apple-MDM-Push-Zertifikats für Intune
titleSuffix: ''
description: Rufen Sie ein Apple-MDM-Pushzertifikat zum Verwalten von iOS-/iPadOS-Geräten mit Intune ab.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/08/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6f67fcd2-5682-4f9c-8d74-d4ab69dc978c
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: dd1bea64bbde5c7da7579471f93f659b71dffa87
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80327210"
---
# <a name="get-an-apple-mdm-push-certificate"></a>Abrufen eines Apple-MDM-Push-Zertifikats

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Für die Verwaltung von iOS-/iPadOS- und macOS-Geräten durch Intune ist ein Apple-MDM-Pushzertifikat erforderlich. Wenn Sie das Zertifikat zu Intune hinzugefügt haben, können Ihre Benutzer ihre Geräte registrieren, indem sie folgende Hilfsmittel verwenden:

- die Unternehmensportal-App

- Methoden von Apple zur Massenregistrierung, z.B. das Programm zur Geräteregistrierung, Apple School Manager oder Apple Configurator.

Weitere Informationen zu Registrierungsoptionen finden Sie unter [Auswählen der Registrierungsmethode für iOS-/iPadOS-Geräte](ios-enroll.md).

Wenn ein Pushzertifikat abläuft, müssen Sie dieses erneuern. Vergewissern Sie sich dabei, dass Sie dieselbe Apple-ID wie bei der Erstellung des ersten Pushzertifikats verwenden.


## <a name="steps-to-get-your-certificate"></a>Erforderliche Schritte, um Ihr Zertifikat abzurufen
Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an, navigieren Sie zu **Geräte** > **Geräte registrieren** > **Apple-Registrierung** > **Apple-MDM-Push-Zertifikat**, und führen Sie dann die folgenden Schritte aus.

### <a name="step-1-grant-microsoft-permission-to-send-user-and-device-information-to-apple"></a>Schritt 1: Erteilen Sie Microsoft die Berechtigung, Benutzer- und Geräteinformationen an Apple zu senden.
Klicken Sie auf **Ich stimme zu.** , um Microsoft die Berechtigung zu erteilen, Daten an Apple zu senden.

![Der Bildschirm „MDM-Push-Zertifikat konfigurieren“, auf dem MDM Push nicht eingerichtet ist.](./media/apple-mdm-push-certificate-get/create-mdm-push-certificate.png)

### <a name="step-2-download-the-intune-certificate-signing-request-required-to-create-an-apple-mdm-push-certificate"></a>Schritt 2: Laden Sie die erforderliche Anforderung zur Signierung eines Intune-Zertifikats herunter, um ein Apple-MDM-Pushzertifikat erstellen zu können.
Klicken Sie auf **CSR herunterladen**, um die Anforderungsdatei herunterzuladen und lokal zu speichern. Die Datei wird verwendet, um ein Vertrauensstellungszertifikat vom Apple Push Certificates-Portal anzufordern.

### <a name="step-3-create-an-apple-mdm-push-certificate"></a>Schritt 3. Erstellen eines Apple-MDM-Pushzertifikats
Wählen Sie **Eigenes MDM-Push-Zertifikat erstellen** aus, um zum Apple Push Certificates Portal zu gelangen. Melden Sie sich mit der Apple-ID Ihres Unternehmens an, und klicken Sie dann auf **Zertifikat erstellen**. Klicken Sie auf **Datei auswählen**, und suchen Sie die Anforderungsdatei für die Signierung des Zertifikats. Klicken Sie dann auf **Hochladen**. Klicken Sie auf der Bestätigungsseite auf **Herunterladen**, um die Zertifikatdatei (.pem) herunterzuladen, und speichern Sie die Datei lokal.

> [!NOTE]
> Das Zertifikat ist mit der Apple-ID verknüpft, die verwendet wurde, um es zu erstellen. Eine bewährte Methode ist es, eine Apple-ID Ihres Unternehmens für Verwaltungsaufgaben zu verwenden und sicherzustellen, dass das Postfach von mehreren Personen – z.B. einer Verteilerliste – überwacht wird. Verwenden Sie niemals eine persönliche Apple-ID.

### <a name="step-4-enter-the-apple-id-used-to-create-your-apple-mdm-push-certificate"></a>Schritt 4: Geben Sie die zum Erstellen Ihres Apple-MDM-Pushzertifikats verwendete Apple-ID ein.
Notieren Sie sich diese ID, damit Sie sich daran erinnern, wenn Sie das Zertifikat erneuern müssen.

### <a name="step-5-browse-to-your-apple-mdm-push-certificate-to-upload"></a>Schritt 5: Navigieren Sie zu Ihrem hochzuladenden Apple-MDM-Pushzertifikat.
Wechseln Sie zur Zertifikatsdatei (.pem), wählen Sie **Öffnen** aus, und wählen Sie dann **Hochladen**aus. Mit dem Push-Zertifikat kann Intune Apple-Geräte registrieren und verwalten.

## <a name="renew-apple-mdm-push-certificate"></a>Erneuern eines Apple-MDM-Push-Zertifikats
Das Apple-MDM-Pushzertifikat ist für ein Jahr gültig und muss jährlich erneuert werden, um die Geräteverwaltung von iOS/iPadOS und macOS beizubehalten. Wenn Ihr Zertifikat abläuft können registrierte Apple-Geräte nicht kontaktiert werden.

Das Zertifikat ist mit der Apple-ID verknüpft, die verwendet wurde, um es zu erstellen. Erneuern Sie das MDM-Push-Zertifikat mit derselben Apple-ID, mit der es erstellt wurde.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an, und navigieren Sie zu **Geräte** > **Geräte registrieren** > **Apple-Registrierung** > **Apple-MDM-Push-Zertifikat**.
2. Wählen Sie **CSR herunterladen** aus, um die CSR-Datei herunterzuladen und lokal zu speichern. Die Datei wird verwendet, um ein Vertrauensstellungszertifikat vom Apple Push Certificates-Portal anzufordern.
3. Wählen Sie **Eigenes MDM-Push-Zertifikat erstellen** aus, um zum Apple Push Certificates Portal zu gelangen. Suchen Sie das Zertifikat, das Sie erneuern möchten, und wählen Sie **Erneuern** aus.
4. Schreiben Sie auf dem Bildschirm **Push-Zertifikat erneuern** Notizen, die Ihnen zukünftig bei der Identifizierung des Zertifikats helfen. Klicken Sie auf **Datei auswählen**, um die neue Anforderungsdatei zu durchsuchen, die Sie heruntergeladen haben und dann auf **Hochladen**.
   > [!TIP]
   > Ein Zertifikat kann durch die Benutzer-ID identifiziert werden. Überprüfen Sie die **Antragsteller-ID** in den Zertifikatdetails, um den GUID-Teil der Benutzer-ID zu finden. Wenn Sie ein registriertes iOS-/iPadOS-Gerät verwenden, klicken Sie auf **Einstellungen** > **Allgemein** > **Gerät** **Verwaltung** > **Verwaltungsprofil** > **Weitere Details** > **Verwaltungsprofil**. Das zweite Zeilenelement **Thema**, enthält die eindeutige GUID, die Sie mit dem Zertifikat im Apple Push Certificates-Portal vergleichen können.
 
6. Wählen Sie auf dem Bildschirm **Bestätigen** die Option **Herunterladen** aus, und speichern Sie die PEM-Datei lokal.
7. Wählen Sie in [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) das Symbol zum Durchsuchen des **Apple-MDM-Push-Zertifikats** aus, wählen Sie die PEM-Datei, die Sie von Apple heruntergeladen haben und anschließend **Hochladen** aus.

Ihr Apple MDM-Push-Zertifikat erscheint als **aktiv** und läuft in 365 Tagen ab.
