---
title: Windows Autopilot-Kunden Zustimmung
description: Erfahren Sie, wie ein clouddienstanbieter-Partner (CSP) oder ein OEM die Kunden Autorisierung zum Registrieren von Windows Autopilot-Geräten im Auftrag des Kunden erhalten kann.
keywords: MDM, Setup, Windows, Windows 10, OOBE, Manage, Bereitstellung, Autopilot, ZTD, Zero-Touchscreen, Partner, msfb, InTune
ms.reviewer: mniehaus
manager: laurawi
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: db2dc86b4f7cb514f3ceca4d37bf387db31c13f4
ms.sourcegitcommit: e533cdf8722156a66b1cc46f710def96587345d0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/15/2020
ms.locfileid: "90568554"
---
# <a name="windows-autopilot-customer-consent"></a>Windows Autopilot-Kunden Zustimmung

**Gilt für: Windows 10**

In diesem Artikel wird beschrieben, wie ein clouddienstanbieter-Partner (Direct Bill, indirekter Anbieter oder indirekter Händler) oder ein OEM die Kunden Autorisierung zum Registrieren von Windows Autopilot-Geräten im Auftrag des Kunden erhalten kann.

## <a name="csp-authorization"></a>CSP-Autorisierung

CSP-Partner können die Kunden Autorisierung zum Registrieren von Windows Autopilot-Geräten im Auftrag des Kunden gemäß den folgenden Einschränkungen erhalten:

<table>
<tr><td>Direkter CSP<td>Ruft die direkte Autorisierung vom Kunden zum Registrieren von Geräten ab.
<tr><td>Indirekter CSP-Anbieter<td>Ruft die implizite Berechtigung zum Registrieren von Geräten über die Beziehung ab, die ihr CSP-Reseller-Partner mit dem Kunden hat. Indirekte CSP-Anbieter registrieren Geräte über das Microsoft Partner Center.
<tr><td>Indirekter CSP-Reseller<td>Ruft die direkte Autorisierung vom Kunden zum Registrieren von Geräten ab. Gleichzeitig erhält der indirekte CSP-Anbieter Partner auch die Autorisierung, was bedeutet, dass entweder der indirekte Anbieter oder der indirekte Reseller Geräte für den Kunden registrieren kann. Allerdings muss der indirekte CSP-Reseller Geräte über die MPC-Benutzeroberfläche registrieren (Manuelles Hochladen der CSV-Datei). Der indirekte CSP-Anbieter kann Geräte mithilfe der MPC-APIs registrieren.
</table>

### <a name="steps"></a>Schritte

Damit ein CSP Windows Autopilot-Geräte für einen Kunden registrieren kann, muss der Kunde diese CSP-Partner Berechtigung zunächst mithilfe des folgenden Prozesses erteilen:

1. CSP sendet einen Link zum Kunden, der Autorisierung/Zustimmung zum Registrieren/Verwalten von Geräten in Ihrem Auftrag anfordert. Gehen Sie folgendermaßen vor:
    1. CSP meldet sich bei Microsoft Partner Center an.
    2. Klicken Sie im oberen Menü auf **Dashboard** .
    3. Klicken Sie im Menü auf **Customer (Kunde** ).
    4. Klicken Sie auf den Link zum **Anfordern einer Reseller-Beziehung** :

        ![Eine Reseller-Beziehung anfordern](images/csp1.png)
 
    5. Aktivieren Sie das Kontrollkästchen, das anzeigt, ob Sie Delegierte Administratorrechte wünschen:
 
        ![Delegierte Rechte](images/csp2.png)

        > [!NOTE]
        > Abhängig von Ihrem Partner können Sie delegierte Administrator Berechtigungen (DAP) anfordern, wenn Sie diese Zustimmung anfordern. Wenn möglich, ist es besser, den neueren DAP-freien Prozess (in diesem Dokument gezeigt) zu verwenden. Wenn dies nicht der Wert ist, können Sie Ihren DAP-Status auf einfache Weise über das Microsoft Admin Center oder das Microsoft 365 Admin-Portal entfernen: https://docs.microsoft.com/partner-center/customers_revoke_admin_privileges
    6. Senden Sie die Vorlage oben per e-Mail an den Kunden.

2. Kunden mit globalen Administrator Berechtigungen von Microsoft Admin Center klicken auf den Link per e-Mail. Über den Link gelangen Sie zur folgenden Microsoft 365 Admin Center-Seite:

    ![ScreenCap der Seite "Vereinbarung akzeptieren" und "Partner genehmigen"-Delegierte Administratorrechte](images/csp3a.png)

    In der obigen Abbildung wird der Kunde sehen, wenn er Delegierte Administratorrechte (DAP) angefordert hat. Die Seite gibt an, welche Administrator Rollen angefordert werden. Wenn der Kunde keine delegierten Administratorrechte angefordert hat, wird die folgende Seite angezeigt:

    ![ScreenCap der Seite "Vereinbarung akzeptieren und Partner autorisieren"](images/csp3b.png) 

    > [!NOTE]
    > Benutzern ohne globale Administratorrechte, die auf den Link klicken, wird eine Meldung ähnlich der folgenden angezeigt:

    ![ScreenCap der Berechtigungs Seite](images/csp4.png)

3. Customer wählt das Kontrollkästchen **Ja** , gefolgt von der Schaltfläche **annehmen** aus. Die Autorisierung erfolgt sofort.
4. Um zu überprüfen, ob die Autorisierungs Anforderung fertiggestellt ist, kann der CSP die **Kunden** Liste in seinem MPC-Konto überprüfen. Wenn der Kunde in der Liste enthalten ist, ist die Anforderung fertiggestellt. Zum Beispiel:

    ![Kunden](images/csp5.png)

## <a name="oem-authorization"></a>OEM-Autorisierung

Jeder OEM verfügt über einen eindeutigen Link, der für die Kunden bereitgestellt werden kann, die der OEM von Microsoft anfordern kann msoemops@microsoft.com .

1. OEM-e-Mails sind mit dem Kunden verknüpft.
2. Kunden mit den globalen Administratorrechten von Microsoft Store for Business (msfb) klicken auf den Link in der e-Mail, der Sie direkt zur folgenden msfb-Seite führt:

    ![ScreenCap der Einladungs Seite für Partner akzeptieren](images/csp6.png)

    > [!NOTE]
    > Benutzern ohne globale Administratorrechte, die auf den Link klicken, wird eine Meldung ähnlich der folgenden angezeigt:

    ![Bildschirm Abbildung der Seite "erforderliche msfb-Berechtigung"](images/csp7.png)

3. Customer wählt das Kontrollkästchen **Ja** , gefolgt von der Schaltfläche **annehmen** , und Sie sind fertig. Die Autorisierung erfolgt sofort.

    > [!NOTE]
    > Nachdem dieser Vorgang abgeschlossen ist, ist es für einen Administrator derzeit nicht möglich, einen OEM zu entfernen. Wenn Sie einen OEM entfernen oder seine Berechtigungen widerrufen möchten, senden Sie eine Anforderung an. msoemops@microsoft.com

4. Der OEM kann mithilfe der API zum Überprüfen von Datenübertragungs Daten überprüfen, ob die Zustimmung abgeschlossen wurde. Diese API wird in der neuesten Version des API-Whitepaper "p" erläutert. 14 FF [https://devicepartner.microsoft.com/assets/detail/windows-autopilot-integration-with-oem-api-design-whitepaper-docx](https://devicepartner.microsoft.com/assets/detail/windows-autopilot-integration-with-oem-api-design-whitepaper-docx) . **Hinweis**: dieser Link ist nur für Microsoft-Geräte Partner zugänglich. Wie in diesem Artikel erläutert, ist es eine bewährte Vorgehensweise für OEM-Partner, die API-Prüfung auszuführen, um zu bestätigen, dass Sie die Zustimmung des Kunden erhalten haben, bevor Sie versuchen, Geräte zu registrieren. Diese Überprüfung kann helfen, Fehler im Registrierungsprozess zu vermeiden.

    > [!NOTE]
    > Während der OEM-Autorisierungs Registrierung werden dem OEM keine delegierten Administrator Berechtigungen erteilt.

## <a name="summary"></a>Zusammenfassung

In dieser Phase des Prozesses ist Microsoft nicht mehr beteiligt. der Zustimmungs Austausch erfolgt direkt zwischen OEM und Kunde. Und das alles geschieht sofort, sobald auf die Schaltflächen geklickt wird.
