---
title: 'Schnellstart: Erstellen und Zuweisen von App-Schutzrichtlinien'
titleSuffix: Microsoft Intune
description: In diesem Schnellstart erfahren Sie, wie Sie Microsoft Intune zum Erstellen und Zuweisen von App-Schutzrichtlinien verwenden.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/26/2019
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 2586fce0-5dca-4686-b9c4-791778838401
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fb8b5eae3c88664caff76da597fc3ab9111f989c
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79343855"
---
# <a name="quickstart-create-and-assign-an-app-protection-policy"></a>Schnellstart: Erstellen und Zuweisen einer App-Schutzrichtlinie

In diesem Schnellstart erfahren Sie, wie Sie mithilfe von Intune eine App-Schutzrichtlinie erstellen und einer Client-App auf dem Gerät eines Endbenutzers zuweisen. Intune verwendet App-Schutzrichtlinien, um zu überprüfen, ob Ihre Apps die Datenschutzanforderungen Ihrer Organisation erfüllen.

Wenn Sie über kein Intune-Abonnement verfügen, [registrieren Sie sich für eine kostenlose Testversion](../fundamentals/free-trial-sign-up.md).

## <a name="prerequisites"></a>Voraussetzungen

- Sie müssen für diesen Schnellstart [einen Benutzer](../fundamentals/quickstart-create-user.md) und [eine Gruppe erstellen](../fundamentals/quickstart-create-group.md), [ein Gerät registrieren](../enrollment/quickstart-setup-auto-enrollment.md) und [eine App hinzufügen und zuweisen](quickstart-add-assign-app.md).

## <a name="sign-in-to-intune"></a>Anmelden bei Intune

Registrieren Sie sich bei [Intune](https://aka.ms/intuneportal) als [globaler Administrator oder Intune-Dienstadministrator](../fundamentals/users-add.md#types-of-administrators). Wenn Sie ein Testabonnement für Intune erstellt haben, besitzt das Konto, mit dem Sie das Abonnement erstellt haben, die Rolle des globalen Administrators.

## <a name="create-an-app-protection-policy"></a>Erstellen einer App-Schutzrichtlinie

Führen Sie die folgenden Schritte aus, um eine App-Schutzrichtlinie zu erstellen:

1. Wählen Sie in [Intune](https://aka.ms/intuneportal) die Option **Apps** > **App-Schutzrichtlinien** > **Richtlinie erstellen** aus. 
2. Geben Sie die folgenden Informationen an:

    - **Name:** *Inhaltsschutz für Windows 10*
    - **Beschreibung:** *Benutzer, denen die Richtlinie zugewiesen ist, können in zugewiesenen Apps und anderen nicht verwalteten Apps auf dem Gerät keine Inhalte ausschneiden, kopieren oder einfügen.*
    - **Plattform**: *Windows 10*
    - **Registrierungsstatus**: *Mit Registrierung*

3. Klicken Sie auf **Protected apps** (Geschützte Apps), um die Apps auszuwählen, für die diese Richtlinie gelten soll.
4. Klicken Sie auf **Apps hinzufügen**.
5. Klicken Sie unter **Empfohlene Apps** auf **Word Mobile**.
5. Klicken Sie auf **OK** > **OK**. 
6. Klicken Sie auf **Erforderliche Einstellungen**, um die App zu konfigurieren.
7. Klicken Sie auf **Außerkraftsetzungen zulassen**, um den Windows Information Protection-Modus festzulegen. Wenn Sie diese Option auswählen, wird verhindert, dass Unternehmensdaten die geschützte App verlassen.
8. Klicken Sie auf **OK** > **Erstellen**.

Dann wird die App-Schutzrichtlinie in Intune angezeigt.

### <a name="assign-the-app-protection-policy"></a>Zuweisen von App-Schutzrichtlinien

Wenn Sie eine App-Schutzrichtlinie in Intune erstellt haben, können Sie diese Gruppen zuweisen. 

Führen Sie die folgenden Schritte aus, um eine App-Schutzrichtlinie zu zuzuweisen:

1. Wählen Sie in [Intune](https://aka.ms/intuneportal) die Option **Intune** > **Apps** > **App-Schutzrichtlinien** aus. 
2. Wählen Sie die App-Schutzrichtlinie aus, die Sie zuvor erstellt haben. In diesem Schnellstart heißt die Richtlinie **Inhaltsschutz für Windows 10**.
3. Wählen Sie **Zuweisungen** aus.
4. Klicken Sie auf der Registerkarte **Einschließen** auf **Select groups to include** (Einzuschließende Gruppen auswählen).
5. Wählen Sie **Contoso Testers** als einzuschließende Gruppe aus.
6. Klicken Sie auf **Auswählen** > **Speichern**. 

Somit ist die App-Schutzrichtlinie zugewiesen.

> [!NOTE]
> App-Schutzrichtlinien können nur auf Gruppen angewendet werden, denen Benutzer angehören. Gruppen, denen Geräte angehören, sind davon ausgeschlossen.

## <a name="next-steps"></a>Nächste Schritte

In diesem Schnellstart wurde erläutert, wie Sie App-Schutzrichtlinien erstellen und zuweisen können. Benutzer, denen die Richtlinie zugewiesen ist, können in zugewiesenen Apps und anderen nicht verwalteten Apps auf dem Gerät keine Inhalte ausschneiden, kopieren oder einfügen. Dadurch werden die Daten Ihrer Organisation geschützt. Weitere Informationen zu App-Schutzrichtlinien in Intune finden Sie unter [Was sind App-Schutzrichtlinien?](app-protection-policy.md)

Weitere Informationen zu Intune erhalten Sie im nächsten Schnellstart.

> [!div class="nextstepaction"]
> [Schnellstart: Erstellen und Zuweisen einer benutzerdefinierten Rolle](../fundamentals/create-custom-role.md)
