---
title: Einrichten von BitLocker-Portalen
titleSuffix: Configuration Manager
description: Installieren der BitLocker-Verwaltungskomponenten für das Self-Service-Portal und die Verwaltungs- und Überwachungswebsite
ms.date: 09/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 1cd8ac9f-b7ba-4cf4-8cd2-d548b0d6b1df
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6834090cd2a58113fb26e298c0c451f846f5ce9
ms.sourcegitcommit: cba06c182646cb6dceef304b35230bf728d5133e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/15/2020
ms.locfileid: "90574591"
---
# <a name="set-up-bitlocker-portals"></a>Einrichten von BitLocker-Portalen

*Gilt für: Configuration Manager (Current Branch)*

<!--3601034-->

Um die folgenden BitLocker-Verwaltungskomponenten in Configuration Manager verwenden zu können, müssen Sie sie zunächst installieren:

- Self-Service-Portal für Benutzer
- Verwaltungs- und Überwachungswebsite (Helpdesk)

Sie können die Portale auf einem vorhandenen Standortserver oder Standortsystemserver mit installiertem IIS installieren oder einen eigenständigen Webserver als Host für die Portale verwenden.

> [!NOTE]
> Ab Version 2006 können Sie das BitLocker-Self-Service-Portal und die Verwaltungs- und Überwachungswebsite am zentralen Verwaltungsstandort installieren.<!-- 5925693 -->
>
> In Version 2002 und früheren Versionen können Sie nur das Self-Service-Portal und die Verwaltungs- und Überwachungswebsite mit einer Datenbank für den primären Standort installieren. Installieren Sie diese Websites in einer Hierarchie für jeden primären Standort.

Bevor Sie beginnen, überprüfen Sie die [Voraussetzungen](../../plan-design/bitlocker-management.md#prerequisites) für diese Komponenten.

## <a name="run-the-script"></a>Ausführen des Skripts

Führen Sie auf dem Zielwebserver die folgenden Aktionen aus:

> [!NOTE]
> Abhängig von Ihrem Siteentwurf müssen Sie das Skript möglicherweise mehrmals ausführen. Führen Sie beispielsweise das Skript auf dem Verwaltungspunkt aus, um die Verwaltungs- und Überwachungswebsite zu installieren. Führen Sie es dann erneut auf einem eigenständigen Webserver aus, um das Self-Service-Portal zu installieren.

1. Kopieren Sie die folgenden Dateien aus `SMSSETUP\BIN\X64` im Configuration Manager-Installationsordner auf dem Standortserver in einen lokalen Ordner auf dem Zielserver:

    - `MBAMWebSite.cab`
    - `MBAMWebSiteInstaller.ps1`

1. Führen Sie PowerShell als Administrator aus, und führen Sie dann das Skript so wie in der folgenden Befehlszeile angegeben aus:

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName <ServerName> -SqlInstanceName <InstanceName> -SqlDatabaseName <DatabaseName> -ReportWebServiceUrl <ReportWebServiceUrl> -HelpdeskUsersGroupName <DomainUserGroup> -HelpdeskAdminsGroupName <DomainUserGroup> -MbamReportUsersGroupName <DomainUserGroup> -SiteInstall Both
    ```

    Beispiel:

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName sql.contoso.com -SqlInstanceName instance1 -SqlDatabaseName CM_ABC -ReportWebServiceUrl https://rsp.contoso.com/ReportServer -HelpdeskUsersGroupName "contoso\BitLocker help desk users" -HelpdeskAdminsGroupName "contoso\BitLocker help desk admins" -MbamReportUsersGroupName "contoso\BitLocker report users" -SiteInstall Both
    ```

    > [!IMPORTANT]
    > Diese Beispielbefehlszeile verwendet alle möglichen Parameter, um ihre Verwendung anzuzeigen. Verwenden Sie sie Ihren Anforderungen gemäß in Ihrer Umgebung.

Greifen Sie nach der Installation über die folgenden URLs auf die Portale zu:

- Self-Service-Portal: `https://webserver.contoso.com/SelfService`
- Website „Administration and Monitoring“ (Verwaltung und Überwachung): `https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> Microsoft empfiehlt die Verwendung von HTTPS, dies ist jedoch nicht obligatorisch. Weitere Informationen finden Sie unter [Festlegen von SSL in IIS](/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="script-usage"></a>Verwendung eines Skripts

Dieser Prozess verwendet das PowerShell-Skript „MBAMWebSiteInstaller.ps1“, um diese Komponenten auf dem Webserver zu installieren. Es akzeptiert die folgenden Parameter:

- `-SqlServerName <ServerName>` (erforderlich): Der vollqualifizierte Domänenname des Datenbankservers am primären Standort.

- `-SqlInstanceName <InstanceName>`: Der Name der SQL Server-Instanz für die Datenbank am primären Standort. Wenn SQL die Standardinstanz verwendet, beziehen Sie diesen Parameter nicht ein.

- `-SqlDatabaseName <DatabaseName>` (erforderlich): Der Name der Datenbank am primären Standort, z. B. `CM_ABC`.

- `-ReportWebServiceUrl <ReportWebServiceUrl>`: Die Webdienst-URL des Reporting Services-Punkts des primären Standorts. Hierbei handelt es sich um den Wert der **Webdienst-URL** im **Konfigurations-Manager für Reporting Services**.

    > [!NOTE]
    > Mit diesem Parameter wird der **Bericht zur Wiederherstellungsüberwachung** installiert, der über die Verwaltungs- und Überwachungswebsite verknüpft ist. Standardmäßig enthält Configuration Manager die anderen BitLocker-Verwaltungsberichte.

- `-HelpdeskUsersGroupName <DomainUserGroup>`: Beispiel: `contoso\BitLocker help desk users`. Hierbei handelt es sich um die Domänenbenutzergruppe, deren Mitglieder Zugriff auf die Bereiche **Manage TPM** (TPM verwalten) und **Drive Recovery** (Laufwerkswiederherstellung) der Website „Administration and Monitoring“ (Verwaltung und Überwachung) haben. Bei Verwendung dieser Optionen müssen alle Felder für die Rolle ausgefüllt sein, einschließlich Domäne und Kontoname des Benutzers.

- `-HelpdeskAdminsGroupName <DomainUserGroup>`: Beispiel: `contoso\BitLocker help desk admins`. Eine Domänenbenutzergruppe, deren Mitglieder auf alle Wiederherstellungsbereiche der Website für Verwaltung und Überwachung zugreifen können. Bei der Unterstützung von Benutzern beim Wiederherstellen ihrer Laufwerke muss mit dieser Rolle nur der Wiederherstellungsschlüssel eingegeben werden.

- `-MbamReportUsersGroupName <DomainUserGroup>`: Beispiel: `contoso\BitLocker report users`. Eine Domänenbenutzergruppe, deren Mitglieder über schreibgeschützten Zugriff auf den Bereich **Berichte** der Website für Verwaltung und Überwachung verfügen.

    > [!NOTE]
    > Das Installerskript erstellt nicht die Domänenbenutzergruppen, die Sie in den Parametern **-HelpdeskUsersGroupName**, **-HelpdeskAdminsGroupName**und **-MbamReportUsersGroupName** angeben. Stellen Sie vor dem Ausführen des Skripts sicher, dass diese Gruppen erstellt werden.
    >
    > Wenn Sie die Parameter **-HelpdeskUsersGroupName**, **-HelpdeskAdminsGroupName** und **-MbamReportUsersGroupName** angeben, stellen Sie sicher, dass Sie den Domänennamen und den Gruppennamen angeben. Verwenden Sie das Format `"domain\user_group"`. Schließen Sie den Domänennamen nicht aus. Wenn der Domänen- oder Gruppenname Leerzeichen oder Sonderzeichen enthält, müssen Sie den Parameter in Anführungszeichen (`"`) einschließen.

- `-SiteInstall Both`: Gibt an, welche der Komponenten installiert werden soll. Gültige Optionen:
  - `Both`: Beide Komponenten installieren
  - `HelpDesk`: Nur die Website zur Verwaltung und Überwachung installieren
  - `SSP`: Nur das Self-Service-Portal installieren

- `-IISWebSite`: Die Website, auf der das Skript die MBAM-Webanwendungen installiert. Standardmäßig ist dies die IIS-Standardwebsite. Erstellen Sie die benutzerdefinierte Website, bevor Sie diesen Parameter verwenden.

- `-InstallDirectory`: Der Pfad, in dem das Skript die Webanwendungsdateien installiert. Dieser Pfad ist standardmäßig `C:\inetpub`. Erstellen Sie das benutzerdefinierte Verzeichnis, bevor Sie diesen Parameter verwenden.

- `-DomainName`  *gilt für Version 2002 und höher*: Legen Sie den NetBIOS-Domänennamen des Servers mit der Helpdesk- oder Self-Service-Webportal-Rolle fest. Nur erforderlich, wenn der NetBIOS-Domänenname nicht mit dem DNS-Domänennamen übereinstimmt. Diese Konfiguration wird auch als separater Domänennamespace bezeichnet. Zum Beispiel `-DomainName fabrikham`, wobei der DNS-Domänenname `contoso.com` lautet.<!-- MEMDocs #759 -->

- `-Uninstall`: Deinstalliert die Helpdesk- und Self-Service-Webportalsites für die BitLocker-Verwaltung auf einem Webserver, auf dem sie zuvor installiert waren.

## <a name="verify"></a>Überprüfen

Verwenden Sie zur Überwachung und Problembehandlung folgende Protokolle:

- Windows-Ereignisprotokolle unter **Microsoft-Windows-MBAM-Web**. Weitere Informationen finden Sie unter [BitLocker-Ereignisprotokolle](../../tech-ref/bitlocker/about-event-logs.md) und [Serverereignisprotokolle](../../tech-ref/bitlocker/server-event-logs.md).

- Ablaufverfolgungsprotokolle für jede Komponente befinden sich an den folgenden Standardspeicherorten:

  - Self-Service-Portal: `C:\inetpub\Microsoft BitLocker Management Solution\Logs\Self Service Website`

  - Website „Administration and Monitoring“ (Verwaltung und Überwachung): `C:\inetpub\Microsoft BitLocker Management Solution\Logs\Help Desk Website`

Weitere Informationen zur Problembehandlung finden Sie unter [Problembehandlung für BitLocker](../../tech-ref/bitlocker/troubleshoot.md).

## <a name="next-steps"></a>Nächste Schritte

[Anpassen des Self-Service-Portals](customize-self-service-portal.md)

Weitere Informationen zur Verwendung der installierten Komponenten finden Sie in den folgenden Artikeln:

- [Die Website „BitLocker Administration and Monitoring“ (Verwaltung und Überwachung von BitLocker)](helpdesk-portal.md)
- [BitLocker-Self-Service-Portal](self-service-portal.md)
