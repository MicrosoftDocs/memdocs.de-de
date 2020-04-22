---
title: 'Schnellstart: Registrieren Ihres Windows 10-Desktopgeräts bei Microsoft Intune'
description: 'Schnellstart: So verwenden Sie das Unternehmensportals zum Registrieren Ihres Windows 10-Desktopgeräts bei Microsoft Intune.'
services: microsoft-intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/30/2019
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 658a7655-a6df-4dbe-b56c-22c7fc60e706
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4f70c8487d9cb30b2a7cced63e6e019541f73704
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80327056"
---
# <a name="quickstart-enroll-your-windows-10-device"></a>Schnellstart: Registrieren Ihres Windows 10-Geräts

In diesem Schnellstart registrieren Sie Ihr Windows 10-Gerät als Intune-Benutzer bei Microsoft Intune. Gehen Sie anschließend zu Intune zurück, und bestätigen Sie das registrierte Gerät.

Wenn Sie Ihre Geräte bei Microsoft Intune registrieren, können Ihre Windows 10-Geräte Zugriff auf die sicheren Daten Ihrer Organisation wie E-Mails, Dateien und andere Ressourcen erhalten. Dies gilt für Windows 10 Desktop- und Windows 10 Mobile-Geräte. Durch die Registrierung Ihrer Geräte können Sie diesen Zugriff sowohl für sich selbst als auch für Ihr Unternehmen sichern und Ihre Arbeitsdaten von Ihren persönlichen Daten getrennt halten.

> [!TIP]
> Erfahren Sie, was geschieht, wenn Sie [Ihr Gerät bei Intune registrieren](../user-help/what-happens-if-you-install-the-company-portal-app-and-enroll-your-device-in-intune-windows.md), und was das für die [Informationen auf Ihrem Gerät](../user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md) bedeutet.

Wenn Sie über kein Intune-Abonnement verfügen, [registrieren Sie sich für eine kostenlose Testversion](../fundamentals/free-trial-sign-up.md).

## <a name="prerequisites"></a>Voraussetzungen

- Ein Microsoft Intune-Abonnement: [Registrieren Sie sich für eine kostenlose Testversion](../fundamentals/free-trial-sign-up.md).
- Um diesen Schnellstart abzuschließen, müssen Sie die Schritte zum [Einrichten der automatischen Registrierung bei Intune](quickstart-setup-auto-enrollment.md) befolgen.

## <a name="confirm-your-windows-10-desktop-version"></a>Bestätigen der Windows 10-Version Ihres Desktopgeräts

Bevor Sie Ihr Windows 10-Desktopgerät registrieren, müssen Sie die installierte Version von Windows bestätigen.

1. Klicken Sie mit der rechten Maustaste auf das **Windows-Symbol**, und wählen Sie **Einstellungen** aus, um die Einstellungen für Windows anzuzeigen.

   ![Screenshot der Windows-Einstellungen – System](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-01.png)

2. Klicken Sie auf **System** > **Info**. 

   ![Screenshot der Systemeinstellungen](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-02.png)

    > [!TIP]
    > Sie können ebenfalls „PC-Infos“ in die **Suchleiste** eingeben und dann **PC-Infos** auswählen.

3. Im Fenster **Einstellungen** wird eine Liste der **Windows-Spezifikationen** für Ihren PC angezeigt. Suchen Sie in der Liste nach der **Version**.

4. Bestätigen Sie, dass Ihre **Version** von Windows 10 **1607 oder höher** ist.

    > [!IMPORTANT]
    > Die Schritte in diesem Schnellstart beziehen sich auf Version **1607 oder höher** von Windows 10. Wenn Sie Version **1511 oder niedriger** verwenden, fahren Sie mit [diesen Schritten](../user-help/enroll-windows-10-device.md) fort.  

## <a name="enroll-windows-10-desktop"></a>Registrieren von Windows 10-Desktopgeräten

1. Kehren Sie zu den Windows-Einstellungen zurück, und wählen Sie **Konten** aus.

   ![Screenshot der Systemeinstellungen – Konten](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-03.png)

2. Wählen Sie **Zugriff auf Geschäfts-, Schul- oder Unikonto** > **Verbinden** aus.

    ![Wählen Sie „Auf Geschäfts-,Schul- oder Unikonto zugreifen“ aus](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-04.png)

3. Melden Sie sich mit Ihrem Geschäfts-, Schul- oder Unikonto bei Intune an, und klicken Sie auf **Weiter**. Wenn Sie den Schnellstart [Erstellen eines Benutzers und Zuweisen einer Lizenz](../fundamentals/quickstart-create-user.md) abgeschlossen haben, können Sie sich mit dem dort erstellten Benutzerkonto anmelden.

    > [!NOTE]
    > Wenn Sie eine onmicrosoft.com-Domäne einrichten, ist **.onmicrosoft.com** Teil der Adresse des Benutzerkontos. 

   ![Geschäfts-, Schul- oder Unikonto eingeben](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-05.png)

    In einer Meldung wird angezeigt, dass Ihr Unternehmen oder Ihre Schule oder Uni Ihr Gerät registriert.

4. Wenn die Seite **Alles bereit!** sehen sehen, klicken Sie auf **Fertig**. Der Vorgang ist abgeschlossen.

5. Das hinzugefügte Konto wird nun als Teil der Einstellungen zum **Zugriff auf Geschäfts-, Schul- oder Unikonten** auf Ihrem Windows-Desktopgerät angezeigt.

   ![Screenshot des neu hinzugefügten Kontos](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-06.png)

    Wenn Sie die obigen Schritte ausgeführt haben und trotzdem nicht auf E-Mails und Dateien Ihres Geschäfts-, Schul- oder Unikontos zugreifen können, befolgen Sie die Schritte unter [Schritte zur Problembehandlung bei Anzeige von „Zugriff auf Geschäfts-, Schul- oder Unikonto“](../user-help/troubleshoot-your-windows-10-device-windows.md#troubleshooting-steps-to-follow-if-you-see-access-work-or-school).

## <a name="confirm-your-device-enrollment-in-intune"></a>Bestätigen der Geräteregistrierung bei Intune

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) als globaler Administrator oder Intune-Dienstadministrator an.
2. Wählen Sie **Geräte** > **Alle Geräte** aus, um die registrierten Geräte in Intune anzuzeigen.
3. Stellen Sie sicher, dass Sie zusätzliche Geräte bei Intune registriert haben.

   ![Screenshot der bei Intune registrierten Geräte](./media/quickstart-enroll-windows-device/quickstart-enroll-windows-device-07.png)

## <a name="clean-up-resources"></a>Bereinigen der Ressourcen

Weitere Informationen zur Aufhebung der Registrierung eines Geräts finden Sie unter [Entfernen Ihres Windows-Geräts aus der Verwaltung](../user-help/unenroll-your-device-from-intune-windows.md).

## <a name="next-steps"></a>Nächste Schritte

In dieser Schnellstartanleitung haben Sie gelernt, wie Sie ein Windows 10-Gerät bei Intune registrieren. Sie erhalten auf allen Plattformen Informationen zu weiteren Möglichkeiten, Geräte zu registrieren. Weitere Informationen zur Verwendung von Geräten mit Intune finden Sie unter [Verwenden verwalteter Geräte zum Erledigen von Aufgaben](../user-help/use-managed-devices-to-get-work-done.md).

Weitere Informationen zu Intune erhalten Sie im nächsten Schnellstart.

> [!div class="nextstepaction"]
> [Schnellstart: Festlegen einer erforderlichen Kennwortlänge für Android-Geräte](../protect/quickstart-set-password-length-android.md)
