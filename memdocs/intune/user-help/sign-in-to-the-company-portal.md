---
title: Anmelden bei der Unternehmensportal-App | Microsoft-Dokumentation
description: Vorgehensweise beim Anmelden bei der Unternehmensportal-App auf verschiedenen Plattformen.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/31/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: cfd214bc-f072-4808-af2e-a3cbf7af9bca
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 59555c8bb9a35d5b70b46836f2298bf3ed342b2d
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83881832"
---
# <a name="sign-in-to-company-portal"></a>Anmelden beim Unternehmensportal  

Es gibt drei Möglichkeiten, sich bei der Unternehmensportal-App anzumelden:

* Anmeldung mit Ihrer geschäftlichen E-Mail-Adresse und Ihrem Kennwort  
* Anmeldung über die zertifikatbasierte Authentifizierung  
* Anmeldung über ein anderes Gerät    


## <a name="sign-in-with-your-email-address-and-password"></a>Anmeldung mit Ihrer E-Mail-Adresse und Ihrem Kennwort
Die folgenden Schritte enthalten Screenshots aus der Unternehmensportal für iOS.  

1. Öffnen Sie die App auf Ihrem Gerät, und tippen Sie auf **Anmelden**.  

   ![Screenshot: Anmeldeseite des Unternehmensportals](./media/intune-ios-cp-signin-1908.png)


2. Geben Sie Ihr **Geschäfts-, Schul- oder Unikonto** ein, und klicken Sie auf **Weiter**.

   ![Der Benutzer wird nur zur Eingabe der E-Mail-Adresse aufgefordert, nicht zur Eingabe von E-Mail-Adresse und Kennwort im gleichen Bildschirm.](./media/cp_ios_aad_signin_after_1804_002.png)

3. Geben Sie Ihr Kennwort ein, und tippen Sie dann auf **Anmelden**.

   ![Der Benutzer wird erst zur Eingabe des Kennworts aufgefordert, wenn die E-Mail-Adresse akzeptiert wurde.](./media/cp_ios_aad_signin_after_1804_003.png)

4. Ihre Anmeldeinformationen werden von der App überprüft. Wenn dieser Vorgang abgeschlossen wurde, können Sie auf die Ressourcen Ihrer Organisation zugreifen und verfügbare Apps installieren.  

   ![Nach dem Durchlaufen des Authentifizierungsprozesses erfolgt die Anmeldung bei der Unternehmensportal-App, und es wird ein Balken zum Ladefortschritt angezeigt.](./media/cp_ios_aad_signin_after_1804_004.png)

## <a name="sign-in-with-certificate-based-authentication"></a>Anmeldung über die zertifikatbasierte Authentifizierung
Diese Anmeldeoption wird nur angezeigt, wenn Ihre Organisation eine zertifikatbasierte Authentifizierung zulässt und ein Zertifikat verfügbar ist, das Sie verwenden können.  

1. Öffnen Sie die Unternehmensportal-App auf Ihrem Gerät.  

2. Geben Sie den Namen Ihres **Geschäfts- oder Schulkontos** ein.  

3. Tippen Sie auf den Link **Sign in with a certificate (Anmelden über ein Zertifikat)** .  

4. Tippen Sie auf **Fortfahren**, um das Zertifikat zu verwenden.  

## <a name="sign-in-from-another-device"></a>Anmeldung über ein anderes Gerät

Wenn in Ihrem Unternehmen der Computerzugriff per Smartcards geregelt wird, müssen Sie sich wahrscheinlich authentifizieren, indem Sie sich über ein anderes Gerät anmelden.  

1. Öffnen Sie die Unternehmensportal-App auf Ihrem Gerät. Stellen Sie sicher, dass es sich um das Gerät handelt, das Sie für den Zugriff auf Ihre Arbeitsressourcen verwenden.       

1. Wählen Sie **Anmeldung über ein anderes Gerät** aus.  

   ![Auf der Anmeldeseite für das Unternehmensportal werden die Benutzer zur Eingabe ihrer E-Mail-Adresse aufgefordert.  Ferner werden die Schaltfläche „Weiter“ und der Link „Von anderem Gerät aus anmelden“ angezeigt. Außerdem wird der Link „Kein Zugriff auf Ihr Konto?“ angezeigt. Ein Link am unteren Seitenrand führt zu Informationen von Microsoft zu Datenschutz und Cookies.](./media/cp_ios_aad_signin_after_1804_005.png)

2. Sie erhalten einen eindeutigen, einmal gültigen Code für die Anmeldung im Unternehmensportal. Kopieren Sie den Code.

   ![Der Benutzer erhält die Anweisung, mit einer über den Arbeitscomputer bezogenen eindeutigen Kennung zur Seite https://microsoft.com/devicelogin zu wechseln und sich dort mit dieser Kennung anzumelden.](./media/cp_ios_aad_signin_after_1804_006.png)

3. Öffnen Sie auf dem anderen Gerät (das Sie für die Authentifizierung verwenden) den Browser, und navigieren Sie zu [https://microsoft.com/devicelogin](https://microsoft.com/devicelogin). Geben oder fügen Sie den Code ein.  

   ![Ein Bild des Browsers des Benutzers auf dem Arbeitscomputer statt in der Unternehmensportal-App. Die angezeigte Seite „Geräteanmeldung“ fordert den Benutzer auf, den über die Unternehmensportal-App empfangenen Code einzugeben.](../fundamentals/media/whats-new-app-ui/cp_ios_aad_signin_from_another_device_after_1704_004.png)

4. Klicken Sie auf __Fortsetzen__, damit die Anmeldung beim Unternehmensportal auf Ihrem Arbeitsgerät erfolgen kann.   

   ![Der Benutzer hat den eindeutigen Code in das Feld eingegeben und wurde auf der Seite „Geräteanmeldung“ aufgefordert, zu bestätigen, dass das Intune-Unternehmensportal die App ist, die zur Anmeldung autorisiert werden soll.](../fundamentals/media/whats-new-app-ui/cp_ios_aad_signin_from_another_device_after_1704_005.png) 

5. Sobald der Code überprüft wurde, können Sie das Fenster schließen.  

   ![Eine Bestätigungsseite informiert darüber, dass der Benutzer sich jetzt auf dem Gerät bei der Unternehmensportal-App angemeldet hat und dass diese Seite geschlossen werden kann.](../fundamentals/media/whats-new-app-ui/cp_ios_aad_signin_from_another_device_after_1704_006.png)

6. Die Unternehmensportal-App meldet Sie auf Ihrem Arbeitsgerät an.  

   ![Nach Abschluss des Authentifizierungsprozesses meldet sich die Unternehmensportal-App Sie an und zeigt einen entsprechenden Ladebalken an.](./media/cp_ios_aad_signin_after_1804_007.png)

Benötigen Sie weitere Unterstützung? Kontaktieren Sie den Support Ihres Unternehmens. Die entsprechenden Kontaktinformationen finden Sie auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980).  
