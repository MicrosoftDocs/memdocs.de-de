---
title: Zuweisen von Geräteprofilen in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Verwenden Sie das Microsoft Endpoint Manager Admin Center, um Benutzern und Geräten Geräteprofile und Richtlinien zuzuweisen. Informationen zum Ausschließen von Gruppen von einer Profilzuweisung in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f6f5414d-0e41-42fc-b6cf-e7ad76e1e06d
ms.reviewer: altsou
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, contperfq1
ms.collection: M365-identity-device-management
ms.openlocfilehash: 000ee384ff289b9511b2dde3b1468525ffed63d4
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88819999"
---
# <a name="assign-user-and-device-profiles-in-microsoft-intune"></a>Zuweisen von Benutzer- und Geräteprofilen in Microsoft Intune

Wenn Sie ein Profil erstellen, enthält es alle Einstellungen, die Sie vorgenommen haben. Als Nächstes stellen Sie das Profil für eine Benutzer- oder Gerätegruppe bereit. Dieser Vorgang wird auch als „Zuweisen“ bezeichnet. Wenn Sie ein Profil zuweisen, erhalten Benutzer und Geräte das Profil, und die von Ihnen angegebenen Einstellungen werden angewendet.

In diesem Artikel wird erklärt, wie Sie ein Profil zuweisen können, und Sie erhalten Informationen zur Verwendung von Bereichsmarkierungen für Ihre Profile.

> [!NOTE]  
> Wenn ein Profil entfernt wird oder nicht mehr einem Gerät zugewiesen ist, kann dies je nach den Einstellungen im Profil verschiedene Folgen haben. Die Einstellungen basieren auf CSPs, und jeder CSP kann mit der Entfernung des Profils anders umgehen. Eine Einstellung könnte z. B. den vorhandenen Wert beibehalten und nicht auf einen Standardwert zurücksetzen. Das Verhalten wird von jedem CSP im Betriebssystem gesteuert. Eine Liste der Windows-CSPs finden Sie in der [Referenz des Konfigurationsdienstanbieters (Configuration Service Provider, CSP)](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference).
>
> Wenn Sie den Wert einer Einstellung ändern möchten, erstellen Sie ein neues Profil, konfigurieren Sie die Einstellung **Nicht konfiguriert**, und weisen Sie das Profil zu. Nach Anwendung auf das Gerät sollten Benutzer die Einstellung auf ihren bevorzugten Wert ändern können.
>
> Zum Konfigurieren dieser Einstellungen empfehlen wir die Bereitstellung für eine Pilotgruppe. Weitere Hinweise zum Intune-Rollout finden Sie unter [Entwickeln eines Rolloutplans](../fundamentals/planning-guide-rollout-plan.md).

## <a name="before-you-begin"></a>Vorbereitung

Stellen Sie sicher, dass Sie über die richtige Rolle zum Zuweisen von Profilen verfügen. Weitere Informationen finden Sie unter [Rollenbasierte Zugriffssteuerung (RBAC) mit Microsoft Intune](../fundamentals/role-based-access-control.md).

## <a name="assign-a-device-profile"></a>Zuweisen eines Geräteprofils

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **Konfigurationsprofile** aus. Dort sind alle Profile aufgelistet.
3. Wählen Sie das Profil aus, das Sie zuweisen möchten, und klicken Sie auf **Eigenschaften** > **Zuweisungen** > **Bearbeiten**:

    :::image type="content" source="./media/device-profile-assign/properties-select-assignments.png" alt-text="Auswählen von Zuweisungen zum Bereitstellen des Profils für Benutzer und Gruppen in Microsoft Intune und Endpoint Manager":::

4. Wählen Sie **Eingeschlossene Gruppen** oder **Ausgeschlossene Gruppen** aus, und klicken Sie dann auf **Einzuschließende Gruppen auswählen**. Wenn Sie Ihre Gruppen auswählen, wählen Sie eine Azure AD-Gruppe aus. Halten Sie die **STRG**-Taste gedrückt, um mehrere Gruppen auszuwählen, und wählen Sie Ihre Gruppen anschließend aus.

    :::image type="content" source="./media/device-profile-assign/select-included-excluded-groups-profile-assignment.png" alt-text="Ein- oder Ausschließen von Benutzern und Gruppen beim Zuweisen oder Bereitstellen eines Profils in Microsoft Intune und Endpoint Manager":::

5. Klicken Sie auf **Überprüfen und speichern**. Diese Schritt weist das Profil nicht zu.
6. Klicken Sie auf **Speichern**. Nach dem Speichern ist das Profil zugewiesen. Ihre Gruppen empfangen die Profileinstellungen, wenn die Geräte beim Intune-Dienst eingecheckt werden.

## <a name="use-scope-tags-or-applicability-rules"></a>Verwenden von Bereichstags oder Anwendbarkeitsregeln

Wenn Sie ein Profil erstellen oder aktualisieren, können Sie diesem auch Bereichstags und Anwendbarkeitsregeln hinzufügen.

**Bereichsmarkierungen** sind eine gute Möglichkeit, Profile für bestimmte Gruppen wie z. B. `US-NC IT Team` oder `JohnGlenn_ITDepartment` zu filtern. Unter [Use RBAC and scope tags for distributed IT (Verwenden der RBAC und von Bereichsmarkierungen für eine verteilte IT)](../fundamentals/scope-tags.md) finden Sie weitere Informationen.

Auf Windows 10-Geräten können Sie **Anwendbarkeitsregeln** hinzufügen, wodurch das Profil nur für eine bestimmte Betriebssystemversion oder eine bestimmte Windows-Version gilt. Unter [Anwendbarkeitsregeln](device-profile-create.md#applicability-rules) finden Sie weitere Informationen.

## <a name="user-groups-vs-device-groups"></a>Benutzer- und Gerätegruppen im Vergleich

Viele Benutzer fragen sich, ob sie besser Benutzergruppen oder Gerätegruppen verwenden sollen. Bei der Beantwortung dieser Frage spielt Ihr Ziel eine entscheidende Rolle. Nachfolgend finden Sie Informationen für den Einstieg.

### <a name="device-groups"></a>Gerätegruppen

Wenn Sie Einstellungen auf ein Gerät anwenden möchten und es für Sie keine Rolle spielt, wer auf dem Gerät angemeldet ist, weisen Sie Ihre Profile einer Benutzergruppe zu. Einstellungen, die auf Gerätegruppen angewendet werden, gelten immer für das jeweilige Gerät und nicht für den Benutzer.

Beispiel:

- Gerätegruppen sind nützlich für die Verwaltung von Geräten ohne dedizierten Benutzer. Geräte zum Drucken von Tickets oder zum Einscannen von Warenbeständen werden beispielsweise gemeinsam von Mitarbeitern in unterschiedlichen Schichten verwendet und sind einem bestimmten Lager zugewiesen. Ordnen Sie diese Geräte einer Gerätegruppe zu, und weisen Sie dieser Ihre Profile zu.

- Sie erstellen ein [Intune-Profil für die Schnittstelle zur Konfiguration der Gerätefirmware](device-firmware-configuration-interface-windows.md), das die Einstellungen im BIOS aktualisiert. Beispielsweise können Sie dieses Profil so konfigurieren, dass die Kamera des Geräts deaktiviert wird, oder die Startoptionen sperren, um zu verhindern, dass Benutzer ein anderes Betriebssystem starten. Es bietet sich hierbei an, dieses Profil einer Gerätegruppe zuzuweisen.

- Auf manchen Windows-Geräten sollten Sie immer einige Einstellungen für Microsoft Edge steuern – unabhängig davon, wer das Gerät verwendet. Möglicherweise möchten Sie alle Downloads blockieren, sämtliche Cookies auf die aktuelle Browsersitzung einschränken und den Browserverlauf löschen. Dafür bietet es sich an, diese Windows-Geräte einer Gerätegruppe zuzuordnen. Erstellen Sie anschließend [in Intune eine administrative Vorlage](administrative-templates-windows.md), fügen Sie diese Geräteeinstellungen hinzu, und weisen Sie dieses Profil anschließend der Gerätegruppe zu.

Fazit: Verwenden Sie Gerätegruppen immer dann, wenn es keine Rolle spielt, wer bei dem jeweiligen Gerät angemeldet ist oder ob überhaupt jemand sich anmeldet. Damit sind Ihre Einstellungen immer auf dem Gerät gespeichert.

### <a name="user-groups"></a>Benutzergruppen

Profileinstellungen, die auf Benutzergruppen angewendet werden, gelten immer für den jeweiligen Benutzer – auch wenn er mehrere Geräte verwendet. Es ist normal, dass Benutzer mehrere Geräte verwenden, z. B. ein Surface Pro für die Arbeit und ein iOS/iPadOS-Gerät für den Privatgebrauch. In der Regel greifen diese Benutzer dann auch über ihre verschiedenen Geräte auf ihre E-Mails und andere Unternehmensressourcen zu.

Befolgen Sie die folgende allgemeine Regel: Wenn ein Feature zu einem Benutzer gehört, z. B. E-Mail oder Benutzerzertifikate, weisen Sie dieses Benutzergruppen zu.

Beispiel:

- Sie möchten ein Helpdesksymbol für alle Benutzer auf all ihren Geräten einrichten. Fügen Sie dafür diese Benutzer einer Benutzergruppe hinzu, und weisen Sie dieser Benutzergruppe das Helpdesksymbol zu.
- Ein Benutzer erhält ein neues Gerät, das der Organisation gehört. Er meldet sich mit seinem Domänenkonto bei dem Gerät an. Das Gerät wird automatisch in Azure AD registriert und von Intune verwaltet. Es bietet sich hierbei an, dieses Profil einer Benutzergruppe zuzuweisen.
- Wenn ein Benutzer sich bei einem Gerät anmeldet, sollten Sie Features über Apps wie OneDrive oder Office steuern. Weisen Sie in diesem Fall die Profileinstellungen für OneDrive oder Office einer Benutzergruppe zu.

  Angenommen, Sie möchten nicht vertrauenswürdige ActiveX-Steuerelemente in Ihren Office-Apps blockieren. Dann können Sie [in Intune eine administrative Vorlage](administrative-templates-windows.md) erstellen, Einstellungen konfigurieren und anschließend dieses Profil einer Benutzergruppe zuweisen.

Fazit: Verwenden Sie Benutzergruppen immer dann, wenn Sie Ihre Einstellungen und Regeln mit dem Benutzer verknüpfen möchten – unabhängig davon, welches Gerät er verwendet.

## <a name="exclude-groups-from-a-profile-assignment"></a>Ausschließen von Gruppen aus einer Profilzuweisung

Mit Gerätekonfigurationsprofilen für Intune können Sie Gruppen in die Profilzuweisung einschließen und von dieser ausschließen.

Es hat sich bewährt, Profile speziell für Ihre Benutzergruppen zu erstellen und zuzuweisen. Erstellen Sie außerdem unterschiedliche Profile für einzelne Gerätegruppen. Weitere Informationen zu Gruppen finden Sie unter [Hinzufügen von Gruppen zum Organisieren von Benutzern und Geräten](../fundamentals/groups-add.md).

Wenn Sie Ihre Profile zuweisen, können Sie für da Ein- und Ausschließen von Gruppen die folgende Tabelle zurate ziehen. Ein Häkchen bedeutet, dass die Zuweisung unterstützt wird:

:::image type="content" source="./media/device-profile-assign/include-exclude-user-device-groups.png" alt-text="Unterstützte Optionen schließen Gruppen in eine Profilzuweisung ein oder daraus aus":::

### <a name="what-you-should-know"></a>Was Sie wissen sollten

- Der Ausschluss hat in folgenden Szenarien für denselben Gruppentyp Vorrang vor der Einbeziehung:

  - Einschließen von Benutzergruppen und Ausschließen von Benutzergruppen
  - Einschließen von Gerätegruppen und Ausschließen von Gerätegruppen

  Angenommen Sie weisen der Benutzergruppe **Alle Unternehmensbenutzer** ein Geräteprofil zu, schließen aber gleichzeitig Mitglieder der Benutzergruppe **Mitarbeiter der Führungsebene** aus. Da es sich bei beiden Gruppen um Benutzergruppen handelt, wird dieses Profil **allen Unternehmensbenutzern** außer den **Führungskräften** zugewiesen.

- Intune bewertet keine Beziehungen zwischen Benutzer- und Gerätegruppen. Wenn Sie Profile gemischten Gruppen zuweisen, entsprechen die Ergebnisse möglicherweise nicht Ihren Anforderungen oder Erwartungen.

  Beispielsweise weisen Sie der Benutzergruppe **Alle Benutzer** ein Geräteprofil zu, schließen jedoch eine Gerätegruppe **Alle persönlichen Geräte** aus. In dieser gemischten Gruppenprofilzuweisung wird **allen Benutzern** das Profil zugewiesen. Der Ausschluss wird nicht angewendet.

  Daher wird das Zuweisen von Profilen für gemischte Gruppen nicht empfohlen.

## <a name="next-steps"></a>Nächste Schritte

Unter [Überwachen von Geräteprofilen in Microsoft Intune](device-profile-monitor.md) finden Sie weitere Informationen zum Überwachen Ihrer Profile und der Geräte, auf denen Ihre Profile ausgeführt werden.
