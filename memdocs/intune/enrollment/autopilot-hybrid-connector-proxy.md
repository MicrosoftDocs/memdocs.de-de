---
title: Konfigurieren von Proxyeinstellungen für den Intune-Connector für Active Directory
description: In diesem Artikel wird beschrieben, wie Sie den Intune-Connector für Active Directory für die Verwendung vorhandener lokaler Proxyserver konfigurieren.
keywords: ''
author: master11218
ms.author: erikje
manager: dougeby
ms.date: 4/16/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tanvira
ms.suite: ems
search.appverid: ''
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 227ed78b593ce10d47b9a1cdcc14dfbd58acdd93
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79339513"
---
# <a name="work-with-existing-on-premises-proxy-servers"></a>Verwenden vorhandener lokaler Proxyserver

In diesem Artikel wird erläutert, wie Sie den Intune-Connector für Active Directory für die Verwendung ausgehender Proxyserver konfigurieren. Er ist für Kunden gedacht, die über Netzwerkumgebungen mit vorhandenen Proxys verfügen.

Standardmäßig versucht der Intune-Connector für Active Directory, mit dem Web Proxy Auto-Discovery-Dienst (WPAD) automatisch einen Proxyserver im Netzwerk zu finden. Wenn dies in Ihrem Netzwerk konfiguriert wurde, ist möglicherweise keine zusätzliche Konfiguration erforderlich.  Sollten Änderungen erforderlich sein, ist in den folgenden Abschnitten beschrieben, wie Sie die Standardeinstellungen mithilfe der [Standardfunktionen des .NET Frameworks für das Konfigurieren von Proxyeinstellungen](https://docs.microsoft.com/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings) außer Kraft setzen.  Weitere Optionen sind in dieser Dokumentation beschrieben.

Weitere Informationen zur Funktionsweise von Connectors finden Sie unter [Grundlegendes zu Azure AD-Anwendungsproxyconnectors](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-connectors).

## <a name="completely-bypass-outbound-proxies"></a>Vollständiges Umgehen ausgehender Proxys

Sie können den Connector so konfigurieren, dass er Ihren lokalen Proxy umgeht, um sicherzustellen, dass er eine direkte Verbindung zu den Azure-Diensten verwendet. Dieser Ansatz wird empfohlen, solange Ihre Netzwerkrichtlinie dies zulässt, da Sie dadurch eine Konfiguration weniger verwalten müssen.

Bearbeiten Sie die Datei „:\Programme\Microsoft Intune\ODJConnector\ODJConnectorUI\ODJConnectorUI.exe.config“, um die Verwendung ausgehender Proxys für den Connector zu deaktivieren, und fügen Sie die Proxyadresse und den Proxyport in dem Abschnitt hinzu, der in diesem Codebeispiel gezeigt wird:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <defaultProxy enabled="False" /> 
        </defaultProxy>  
    </system.net>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="mscorlib" publicKeyToken="b77a5c561934e089" culture="neutral"/>
                <bindingRedirect oldVersion="0.0.0.0-2.0.0.0" newVersion="4.6.0.0" />
            </dependentAssembly>
        </assemblyBinding>
    </runtime>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="SignInURL" value="https://portal.manage.microsoft.com/Home/ClientLogon"/>
        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
    </appSettings>
</configuration>
```

Nehmen Sie eine ähnliche Änderung an „C:\Programme\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc.exe.config“ vor, um sicherzustellen, dass der Connector Updater-Dienst den Proxy ebenfalls umgeht.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>
            <defaultProxy enabled="False" /> 
        </defaultProxy>  
    </system.net>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="BaseServiceAddress" value="https://manage.microsoft.com/" />
    </appSettings>
</configuration>
```

Kopieren Sie davor unbedingt die Originaldateien, falls Sie die .config-Standarddateien wiederherstellen müssen.

Nach dem Ändern der Konfigurationsdateien müssen Sie den Intune-Connectordienst neu starten. 

1. Öffnen Sie **services.msc**.
2. Suchen Sie den **Intune ODJConnector-Dienst**, und wählen Sie diesen aus.
3. Klicken Sie auf **Neu starten**.

![Screenshot: Neustart des Diensts](./media/autopilot-hybrid-connector-proxy/service-restart.png)


## <a name="specifying-an-alternative-proxy-server"></a>Festlegen eines anderen Proxyservers

Wenn ein anderer Proxyserver (z. B einer, der die Authentifizierung umgeht) mit dem Intune-Connector für Active Directory verwendet werden muss, kann dies in ähnlicher Weise festgelegt werden. Bearbeiten Sie hierzu die Datei „:\Programme\Microsoft Intune\ODJConnector\ODJConnectorUI\ODJConnectorUI.exe.config“, und fügen Sie die Proxyadresse und den Proxyport in dem Abschnitt hinzu, der in diesem Codebeispiel gezeigt wird:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <proxy proxyaddress="<PROXY ADDRESS HERE>:<PORT HERE>" bypassonlocal="True" usesystemdefault="True"/>   
        </defaultProxy>  
    </system.net>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="mscorlib" publicKeyToken="b77a5c561934e089" culture="neutral"/>
                <bindingRedirect oldVersion="0.0.0.0-2.0.0.0" newVersion="4.6.0.0" />
            </dependentAssembly>
        </assemblyBinding>
    </runtime>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="SignInURL" value="https://portal.manage.microsoft.com/Home/ClientLogon"/>
        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
    </appSettings>
</configuration>
```

Nehmen Sie eine ähnliche Änderung an „C:\Programme\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc.exe.config“ vor, um sicherzustellen, dass der Connector Updater-Dienst den Proxy ebenfalls umgeht.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <proxy proxyaddress="<PROXY ADDRESS HERE>:<PORT HERE>" bypassonlocal="True" usesystemdefault="True"/>   
        </defaultProxy>  
    </system.net>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="BaseServiceAddress" value="https://manage.microsoft.com/" />
    </appSettings>
</configuration>
```

Kopieren Sie davor unbedingt die Originaldateien, falls Sie die .config-Standarddateien wiederherstellen müssen.

Nach dem Ändern der Konfigurationsdateien müssen Sie den Intune-Connectordienst neu starten. 

1. Öffnen Sie **services.msc**.
2. Suchen Sie den **Intune ODJConnector-Dienst**, und wählen Sie diesen aus.
3. Klicken Sie auf **Neu starten**.

![Screenshot: Neustart des Diensts](./media/autopilot-hybrid-connector-proxy/service-restart.png)


## <a name="next-steps"></a>Nächste Schritte

[Verwalten von Geräten](../remote-actions/device-management.md)
