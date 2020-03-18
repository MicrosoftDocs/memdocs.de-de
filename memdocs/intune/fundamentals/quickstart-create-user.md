---
title: 'Schnellstart: Erstellen eines Benutzers in Intune'
description: 'Schnellstart: Erstellen eines Benutzers in Intune'
services: microsoft-intune
author: ErikjeMS
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.topic: quickstart
ms.date: 01/17/2020
ms.author: erikje
ms.manager: dougeby
ms.assetid: 820fcb18-0927-4ebd-be79-dce92b51c261
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: cf5c76e276722fb9bab2b5d6fac511f0b22ae1f2
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79356712"
---
# <a name="quickstart-create-a-user-in-intune-and-assign-the-user-a-license"></a>Schnellstart: Erstellen eines Benutzers in Intune und Zuweisen einer Lizenz

In dieser Schnellstartanleitung erstellen Sie einen Benutzer und weisen ihm eine Intune-Lizenz zu. Wenn Sie Intune verwenden, muss jede Person, die Zugriff auf Unternehmensdaten haben soll, über ein eigenes Benutzerkonto verfügen. Intune-Administratoren können später festlegen, dass Benutzer die Zugriffssteuerung verwalten.

## <a name="prerequisites"></a>Voraussetzungen

- Ein Microsoft Intune-Abonnement. [Registrieren Sie sich für ein kostenloses Testversionskonto](../fundamentals/free-trial-sign-up.md).

## <a name="sign-in-to-intune-in-microsoft-endpoint-manager"></a>Anmelden bei Intune im Microsoft Endpoint Manager

Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) als [globaler Administrator oder Intune-Dienstadministrator](users-add.md#types-of-administrators) an. Wenn Sie ein Testabonnement für Intune erstellt haben, besitzt das Konto, mit dem Sie das Abonnement erstellt haben, die Rolle des globalen Administrators.

## <a name="create-a-user"></a>Erstellen eines Benutzers

Ein Benutzer benötigt ein Benutzerkonto, um sich für die Intune-Geräteverwaltung registrieren zu können. So erstellen Sie einen neuen Benutzer:

1. Wählen Sie im Microsoft Endpoint Manager **Benutzer** > **Alle Benutzer** > **Neuer Benutzer** aus:  ![Wählen Sie im Microsoft Endpoint Manager „Neuer Benutzer“ aus](./media/quickstart-create-user/create-user.png)
2. Geben Sie in das Feld **Name** z. B. *Dewey Kellum* ein:  ![Benutzerinformationen hinzufügen](./media/quickstart-create-user/create-user-02.png)
3. Geben Sie in das Feld **Benutzername** eine Benutzer-ID ein, z. B. Dewey@contoso.onmicrosoft.com.

    > [!NOTE]
    > Wenn Sie noch keinen Kundendomänennamen erstellt haben, verwenden Sie den überprüften Domänennamen, den Sie zum Erstellen des Intune-Abonnements (oder der [kostenlosen Testversion](free-trial-sign-up.md#sign-up-for-a-microsoft-intune-free-trial)) verwendet haben. 

4. Wählen Sie **Kennwort anzeigen** aus, und notieren Sie sich das automatisch generierte Kennwort, mit dem Sie sich bei einem Testgerät anmelden können.
5. Wählen Sie **Erstellen** aus.

## <a name="assign-a-license-to-the-user"></a>Zuweisen einer Benutzerlizenz

Nachdem Sie einen Benutzer erstellt haben, müssen Sie diesem über das [Microsoft 365 Admin Center](https://go.microsoft.com/fwlink/p/?LinkId=698854) eine Intune-Lizenz zuweisen. Wenn Sie dem Benutzer keine Lizenz zuweisen, kann er sein Gerät nicht bei Intune registrieren.

So weisen Sie einem Benutzer eine Intune-Lizenz zu:

1. Melden Sie sich im [Microsoft 365 Admin Center](https://go.microsoft.com/fwlink/p/?LinkId=698854) mit den gleichen Anmeldeinformationen an, die Sie auch zur Anmeldung in Intune verwendet haben.
2. Wählen Sie **Benutzer** > **Aktive Benutzer** und dann den Benutzer aus, den Sie erstellt haben.
3. Wählen Sie die Registerkarte **Lizenzen und Apps** aus.
4. Wählen Sie unter **Speicherort auswählen** einen Speicherort für den Benutzer aus, wenn er nicht bereits festgelegt ist.
2. Aktivieren Sie das Kontrollkästchen **Intune** im Abschnitt **Lizenzen**. Wenn Intune in einer anderen Lizenz enthalten ist, können Sie diese Lizenz auswählen. Der angezeigte [Produktname](https://docs.microsoft.com/azure/active-directory/users-groups-roles/licensing-service-plan-reference) wird in der Azure-Verwaltung als Dienstplan verwendet.

    ![Auswählen von Speicherort und Intune-Lizenz](./media/quickstart-create-user/create-user-03.png)

   > [!NOTE]
   > Diese Einstellung verwendet eine Ihrer Lizenzen für den Benutzer. Wenn Sie eine Testumgebung verwenden, sollten Sie diese Lizenz später einem echten Benutzer in einer Liveumgebung zuweisen.

6. Wählen Sie **Änderungen speichern** aus.

Dem neuen aktiven Intune-Benutzer wird jetzt angezeigt, dass er eine **Intune**-Lizenz verwendet.

## <a name="clean-up-resources"></a>Bereinigen der Ressourcen

Wenn Sie diesen Benutzer nicht mehr benötigen, können Sie ihn löschen, indem Sie zum [Microsoft 365 Admin Center](https://go.microsoft.com/fwlink/p/?LinkId=698854) wechseln und **Benutzer** > *den Benutzer* > *das Benutzerlöschsymbol* > **Benutzer löschen** > **Schließen** auswählen.

   ![Auswählen des Löschsymbols](./media/quickstart-create-user/create-user-04.png)

## <a name="next-steps"></a>Nächste Schritte

In diesem Schnellstart haben Sie einen Benutzer erstellt und ihm eine Intune-Lizenz zugewiesen. Weitere Informationen zum Hinzufügen von Benutzern zu Intune finden Sie unter [Hinzufügen von Benutzern und Gewähren von Administratorrechten für Intune](users-add.md).

Um diese Reihe von Intune-Schnellstarts fortzusetzen, gehen Sie zum nächsten:

> [!div class="nextstepaction"]
> [Schnellstart: Erstellen einer Gruppe zum Verwalten von Benutzern](quickstart-create-group.md)
