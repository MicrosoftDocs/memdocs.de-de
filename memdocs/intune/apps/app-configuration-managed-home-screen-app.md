---
title: Konfigurieren der Managed Home Screen-App von Microsoft
titleSuffix: Microsoft Intune
description: Erfahren Sie, wie Sie die Managed Home Screen-App von Microsoft konfigurieren können.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/01/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 865c7f03-f525-4dfa-b3a8-d088a9106502
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0279a85d0eb3bac7d222c27ce15203f58fd4ede6
ms.sourcegitcommit: ded11a8b999450f4939dcfc3d1c1adbc35c42168
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/01/2020
ms.locfileid: "89281165"
---
# <a name="configure-the-microsoft-managed-home-screen-app-for-android-enterprise"></a>Konfigurieren der Managed Home Screen-App von Microsoft für Android Enterprise

Managed Home Screen ist die App, die für unternehmenseigene dedizierte Android Enterprise-Geräte verwendet wird, die über Intune registriert wurden und im Modus „Multi-App-Kiosk“ ausgeführt werden. Bei diesen Geräten fungiert die Managed Home Screen-App als Startprogramm für andere genehmigte Apps, die darauf ausgeführt werden. Die Managed Home Screen-App bietet IT-Administratoren die Möglichkeit, ihre Geräte anzupassen und die Funktionen einzuschränken, auf die der Endbenutzer zugreifen kann. 

## <a name="when-to-configure-the-microsoft-managed-home-screen-app"></a>Wann die Managed Home Screen-App von Microsoft konfiguriert werden sollte

Wenn Ihnen Einstellungen über „Gerätekonfiguration“ zur Verfügung stehen, konfigurieren Sie die Einstellungen normalerweise dort. Auf diese Weise können Sie Zeit sparen, Fehler minimieren und erhalten eine bessere Benutzeroberfläche für Intune-Support. Allerdings stehen einige der Einstellungen für Managed Home Screen derzeit nur im Bereich **App-Konfigurationsrichtlinien** in der Intune-Konsole zur Verfügung. Anhand dieses Dokuments lernen Sie, wie Sie die verschiedenen Einstellungen entweder mithilfe des Konfigurations-Designers oder eines JSON-Skripts konfigurieren. 

> [!NOTE]
> Es ist derzeit möglich und ratsam, Anwendungen für die Zulassungsliste und angeheftete Weblinks über **Apps** und **Gerätekonfiguration** festzulegen. Die vollständige Liste von Einstellungen, die in **Gerätekonfiguration** zur Verfügung stehen und sich auf Managed Home Screen auswirken, finden Sie unter [Einstellungen dedizierter Geräte](../configuration/device-restrictions-android-for-work.md#device-experience).  

Navigieren Sie zuerst zum [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431), und klicken Sie auf **Apps** > **App-Konfigurationsrichtlinien**. Fügen Sie eine Konfigurationsrichtlinie für **Verwaltete Geräte** unter **Android** hinzu, und wählen Sie **Managed Home Screen** als zugeordnete App aus. Klicken Sie auf **Konfigurationseinstellungen**, um die verschiedenen verfügbaren Einstellungen für Managed Home Screen zu konfigurieren. 

## <a name="choosing-a-configuration-settings-format"></a>Auswählen eines Formats für die Konfigurationseinstellungen

Es gibt zwei Methoden, mit denen Sie Konfigurationseinstellungen für Managed Home Screen definieren können:

- **Konfigurations-Designer** ermöglicht Ihnen das Konfigurieren von Einstellungen über eine benutzerfreundliche Oberfläche, auf der Sie Features aktivieren oder deaktivieren und Werte festlegen können. Bei dieser Methode gibt es einige deaktivierte Konfigurationsschlüssel mit dem Werttyp `BundleArray`. Diese Konfigurationsschlüssel können nur durch Eingabe von JSON-Daten konfiguriert werden. 
- **JSON-Daten** ermöglicht Ihnen das Definieren aller möglichen Konfigurationsschlüssel mithilfe eines JSON-Skripts. 

Wenn Sie Eigenschaften mit Konfigurations-Designer hinzufügen, können Sie diese Eigenschaften automatisch in JSON konvertieren, indem Sie in der Dropdownliste **Format der Konfigurationseinstellungen** den Eintrag **JSON-Daten eingeben** auswählen.

![Screenshot der Optionen für „Format der Konfigurationseinstellungen“](./media/app-configuration-managed-home-screen-app/app-configuration-managed-home-screen-app_01.png)

## <a name="using-configuration-designer"></a>Verwenden von Konfigurations-Designer

Mithilfe von Konfigurations-Designer können Sie vorgegebene Einstellungen und die ihnen zugeordneten Werte auswählen. 

![Screenshot von hinzugefügten Konfigurationseinstellungen](./media/app-configuration-managed-home-screen-app/app-configuration-managed-home-screen-app_02.png)

In der nachstehenden Tabelle sind die verfügbaren Konfigurationsschlüssel, Werttypen, Standardwerte und Beschreibungen für Managed Home Screen aufgeführt. Die Beschreibung enthält das erwartete Geräteverhalten basierend auf den ausgewählten Werten. Konfigurationsschlüssel, die im Konfigurations-Designer deaktiviert sind, werden in der Tabelle nicht aufgeführt.

| Konfigurationsschlüssel | Werttyp | Standardwert | Beschreibung |
|---------------------------------------------------------------------------------------------------------------------------|-------------|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Rastergröße einstellen | string | Automatisch | Ermöglicht es Ihnen, die Rastergröße für Apps festzulegen, die auf Managed Home Screen positioniert werden sollen. Sie können die Anzahl der App-Zeilen und -Spalten festlegen, um die Rastergröße im Format `columns;rows` zu definieren. Wenn Sie die Rastergröße definieren, wäre die maximale Anzahl der Apps, die in einer Zeile auf dem Startbildschirm angezeigt werden, die Anzahl der von Ihnen festgelegten Zeilen, und die maximale Anzahl der Apps, die in einer Spalte auf dem Startbildschirm angezeigt werden, wäre die Anzahl der festgelegten Spalten. |
| Infobadge aktivieren | bool | FALSE | Aktiviert den Infobadge für App-Symbole, der die Anzahl der neuen Benachrichtigungen auf der App anzeigt. Wenn Sie diese Einstellung aktivieren, sehen Endbenutzer die Infobadges auf Apps, in denen es ungelesene Benachrichtigungen gibt. Wenn Sie diesen Konfigurationsschlüssel deaktiviert lassen, kann der Endbenutzer keine Infobadges auf Apps sehen, die möglicherweise ungelesene Benachrichtigungen enthalten. |
| Startbildschirm sperren | bool | TRUE | Hindert den Endbenutzer daran, App-Symbole auf dem Startbildschirm zu verschieben. Wenn Sie diesen Konfigurationsschlüssel aktivieren, werden die App-Symbole auf dem Startbildschirm gesperrt, und der Endbenutzer kann sie nicht an verschiedene Rasterpositionen des Bildschirms ziehen und dort ablegen. Wenn `false` festgelegt wurde, können Endbenutzer Anwendungs- und Weblinksymbole auf Managed Home Screen verschieben.  |
| Hintergrundbild für Gerät festlegen | string | Standard | Ermöglicht es Ihnen, ein Hintergrundbild Ihrer Wahl festzulegen, indem Sie die URL des Bilds eingeben, das Ihr Hintergrundbild werden soll. |
| App-Symbolgröße festlegen | integer | 2 | Ermöglicht es Ihnen, die Symbolgröße für Apps festzulegen, die auf dem Startbildschirm angezeigt werden. Sie können folgende Werte in dieser Konfiguration für unterschiedliche Größen auswählen: „0“ (Kleinste), „1“ (Klein), „2“ (Normal), „3“ (Groß) und „4“ (Größte). |
| Symbol für App-Ordner festlegen | integer | 0 | Ermöglicht es Ihnen, die Darstellung von App-Ordnern auf dem Startbildschirm zu definieren. Sie können die Darstellung aus folgenden Werten auswählen: „Dunkel Quadrat(0)“; „Dunkel Kreis (1)“; „Hell Quadrat(2)“; „Hell Kreis (3)“. |
| Bildschirmausrichtung festlegen | integer | 1 | Ermöglicht es Ihnen, die Ausrichtung des Startbildschirms auf „Hochformat“, „Querformat“ oder „Automatisch drehen“ festzulegen. Sie können die Ausrichtung festlegen, indem Sie die Werte „1“ (für „Hochformat“), „2“ (für „Querformat“) oder „3“ (für „Automatisch drehen“) eingeben. |
| Festlegen von Anwendungen für die Zulassungsliste | bundleArray | FALSE | Ermöglicht es Ihnen, aus den auf dem Gerät installierten Apps diejenige Gruppe von Apps zu definieren, die auf dem Startbildschirm sichtbar sein soll. Sie können die Apps definieren, indem Sie den App-Paketnamen der Apps eingeben, die Sie sichtbar machen möchten. Mit „com.microsoft.emmx“ beispielsweise können Einstellungen auf dem Startbildschirm angezeigt werden. Die Apps, die Sie der Zulassungsliste in diesem Abschnitt hinzufügen, sollten bereits auf dem Gerät installiert sein, damit sie auf dem Startbildschirm sichtbar sind. |
| Angeheftete Weblinks festlegen | bundleArray | FALSE | Ermöglicht es Ihnen, Websites als Schnellstartsymbole auf dem Startbildschirm anzuheften. Bei dieser Konfiguration können Sie die URL definieren und auf dem Startbildschirm hinzufügen, damit sie der Endbenutzer mit einem einfachen Tippen im Browser starten kann. Anmerkung: Sie sollten [verwaltete Google Play-Weblinks](./apps-add-android-for-work.md#managed-google-play-web-links) für Ihre Geräte erstellen, zuweisen und genehmigen. Diese werden wie auf der Zulassungsliste aufgeführte Anwendungen behandelt. |
| Bildschirmschoner aktivieren | bool | FALSE | Dient dazu, den Bildschirmschonermodus zu aktivieren bzw. zu deaktivieren. Wenn „true“ festgelegt wird, können Sie **screen_saver_image**, **screen_saver_show_time**,**inactive_time_to_show_screen_saver** und **media_detect_screen_saver** konfigurieren. |
| Bild für Bildschirmschoner | string |   | Hiermit legen Sie die URL für das Bildschirmschonerbild fest. Wurde keine URL festgelegt, zeigen Geräte das Standardbild an, wenn der Bildschirmschoner aktiviert wird. Das Standardbild zeigt das Symbol der Managed Home Screen-App.  |
| Anzeigezeit für den Bildschirmschoner | integer | 0 | Bietet die Möglichkeit, die Zeitspanne in Sekunden festzulegen, während der das Gerät im Bildschirmschonermodus den Bildschirmschoner anzeigt. Wenn „0“ festgelegt wurde, wird der Bildschirmschoner so lange im Bildschirmschonermodus angezeigt, bis das Gerät inaktiv wird.  |
| Inaktive Zeit zum Aktivieren des Bildschirmschoners | integer | 30 | Die Anzahl von Sekunden, während der das Gerät inaktiv ist, bevor der Bildschirmschoner ausgelöst wird. Wenn „0“ festgelegt wurde, wechselt das Gerät niemals in den Bildschirmschonermodus. |
| Medienerkennung vor Anzeige des Bildschirmschoners | bool | TRUE | Wählen Sie aus, ob auf dem Gerätebildschirm der Bildschirmschoner angezeigt werden soll, wenn auf dem Gerät Audio- oder Videodaten wiedergegeben werden. Wenn „true“ festgelegt wurde, gibt das Gerät – unabhängig vom Wert in **inactive_time_to_show_scree_saver** – kein Audio/Video wieder. Bei „false“ zeigt der Gerätebildschirm den Bildschirmschoner entsprechend dem Wert an, der in **inactive_time_to_show_screen_saver** festgelegt wurde.   |
| Virtuelle Startschaltfläche aktivieren | bool | FALSE | Legen Sie diese Einstellung auf `True` fest, damit der Endbenutzer auf eine Startschaltfläche für Managed Home Screen zugreifen kann, über die er aus seiner aktuellen Aufgabe zu Managed Home Screen zurückkehren wird.  |
| Typ der virtuellen Startschaltfläche | string | swipe_up | Verwenden Sie **swipe_up** für den Zugriff auf die Startschaltfläche mit einem Wischen nach oben. Verwenden Sie **float** für den Zugriff auf eine angeheftete persistente Startschaltfläche, die der Endbenutzer auf dem Bildschirm verschieben kann. |
| Anzeigeleiste für Akku- und Signalstärke | bool | True  | Wenn Sie diese Einstellung auf `True` festlegen, wird die Anzeigeleiste für Akku- und Signalstärke eingeblendet. |
| Kennwort für Aufgabensperrmodus beenden | string |   | Geben Sie einen 4- bis 6-stelligen Code ein, der für die vorübergehende Aufhebung des Aufgabensperrmodus zur Problembehandlung verwendet werden soll. |
| Verwaltete Einstellung anzeigen | bool | TRUE | „Verwaltete Einstellung“ ist eine Managed Home Screen-App, die nur angezeigt wird, wenn Sie Einstellungen für den Schnellzugriff konfiguriert haben, darunter **WLAN-Einstellung anzeigen**, **Bluetooth-Einstellung anzeigen**, **Lautstärkeeinstellung anzeigen** und **Taschenlampeneinstellung anzeigen**. Auf diese Einstellungen kann auch zugegriffen werden, indem Sie auf dem Display mit dem Finger nach unten wischen. Legen Sie diesen Schlüssel auf `False` fest, um die App „Verwaltete Einstellung“ auszublenden und Endbenutzern den Zugriff auf die Einstellungen nur zu ermöglichen, indem sie eine Wischbewegung nach unten durchführen.    |
| Einfachen Zugriff auf das Menü „Debuggen“ aktivieren | bool | FALSE | Legen Sie diese Einstellung auf `True` fest, um das Menü „Debuggen“ aus der Anwendung „Verwaltete Einstellungen“ oder durch Wischen nach unten auf dem Managed Home Screen aufzurufen. Im Menü „Debuggen“ befindet sich derzeit die Möglichkeit, den Kioskmodus zu verlassen, und es wird durch etwa 15-maliges Klicken auf die Schaltfläche „Zurück“ aufgerufen. Lassen Sie diese Einstellung auf `False` festgelegt, damit der Einstiegspunkt zum Menü „Debuggen“ nur über die Schaltfläche „Zurück“ erreichbar bleibt.   |
| WLAN-Einstellung anzeigen | bool | FALSE | Wenn Sie diese Einstellung auf `True` festlegen, kann der Endbenutzer WLAN aktivieren oder deaktivieren oder aber eine Verbindung mit verschiedenen WLAN-Netzwerken herstellen.  |
| WLAN-Zulassungsliste aktivieren | bool | FALSE | Legen Sie diese Einstellung auf `True` fest, und füllen Sie die **WLAN-Zulassungsliste** aus, um einzuschränken, welche WLAN-Netzwerke auf dem Managed Home Screen angezeigt werden. Legen Sie diese Einstellung auf `False` fest, um alle möglichen verfügbaren WLAN-Netzwerke anzuzeigen, die das Gerät ermittelt hat. Beachten Sie, dass diese Einstellung nur dann relevant ist, wenn **WLAN-Einstellung anzeigen** auf `True` festgelegt wurde und die **WLAN-Zulassungsliste** ausgefüllt wurde.   |
| WLAN-Zulassungsliste| bundleArray | FALSE | Ermöglicht es Ihnen, alle SSIDs der WLAN-Netzwerke aufzulisten, die das Gerät auf dem Managed Home Screen anzeigen soll. Diese Liste ist nur relevant, wenn **WLAN-Einstellung anzeigen** und **WLAN-Zulassungsliste aktivieren** auf `True` festgelegt wurden. Wenn eine der beiden Optionen auf `False` festgelegt wurde, müssen Sie diese Konfiguration nicht ändern.    |
| Bluetooth-Einstellung anzeigen | bool | FALSE | Wenn Sie diese Einstellung auf `True` festlegen, kann der Endbenutzer Bluetooth aktivieren oder deaktivieren und eine Verbindung mit verschiedenen Bluetooth-fähigen Geräten herstellen.   |
| Lautstärkeeinstellung anzeigen | bool | FALSE | Wenn diese Einstellung auf `True` festgelegt wird, kann der Endbenutzer auf einen Schieberegler zur Einstellung der Medienlautstärke zugreifen.   |
| Taschenlampeneinstellung anzeigen | bool | FALSE | Wenn diese Einstellung auf `True` festgelegt wird, kann der Endbenutzer die Taschenlampe des Geräts ein- oder ausschalten. Wenn das Gerät keine Taschenlampe unterstützt, wird diese Einstellung auch dann nicht angezeigt, wenn sie auf `True` festgelegt ist.   |
| Einstellung für Geräteinformationen anzeigen | bool | FALSE | Wenn diese Einstellung auf `True` festgelegt wird, kann der Endbenutzer über die App „Verwaltete Einstellungen“ oder durch Wischen nach unten eine QuickInfo zum Gerät anzeigen. Zu den verfügbaren Informationen gehören Marke, Modell und Seriennummer des Geräts.   |
| Anwendungen im Ordner sind nach Namen sortiert | bool | TRUE | Wenn Sie diese Einstellung auf `False` festlegen, werden all Elemente in einem Ordner in der Reihenfolge angezeigt, in der sie angegeben wurden. Andernfalls werden sie alphabetisch angezeigt.   |
| Anwendungsreihenfolge aktiviert | bool | FALSE | Wenn Sie diese Einstellung auf `True` festlegen, kann die Reihenfolge von Anwendungen, Weblinks und Ordner auf dem Managed Home Screen festgelegt werden. Nachdem die Option aktiviert wurde, legen Sie die Reihenfolge mit **app_order** fest.   |
| Anwendungsreihenfolge | bundleArray | FALSE | Hiermit können Sie die Reihenfolge von Anwendungen, Weblinks und Ordnern auf dem Managed Home Screen festlegen. Um diese Einstellung zu verwenden, muss **Startbildschirm sperren** aktiviert, **Rastergröße festlegen** definiert und **Anwendungsreihenfolge aktiviert** auf `True` festgelegt sein.   |

## <a name="enter-json-data"></a>Eingeben von JSON-Daten

Geben Sie JSON-Daten ein, um alle verfügbaren Einstellungen für Managed Home Screen sowie die in **Konfigurations-Designer** deaktivierten Einstellungen zu konfigurieren.

![Screenshot der hinzugefügten JSON-Daten](./media/app-configuration-managed-home-screen-app/app-configuration-managed-home-screen-app_03.png)

Zusätzlich zur Liste von konfigurierbaren Einstellungen, die in der Tabelle **Konfigurations-Designer** (siehe oben) aufgeführt sind, enthält die nachstehende Tabelle die Konfigurationsschlüssel, die Sie nur über JSON-Daten konfigurieren können.

|    Konfigurationsschlüssel    |    Werttyp    |    Standardwert    |    Beschreibung    |
|-------------------------------------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    Festlegen von Anwendungen für die Zulassungsliste    |    bundleArray    | <img alt="JSON - Example 1" src="./media/app-configuration-managed-home-screen-app/defaultvaluejson01.png" width="300"> |    Ermöglicht es Ihnen, aus den auf dem Gerät installierten Apps diejenige Gruppe von Apps zu definieren, die auf dem Startbildschirm sichtbar sein soll. Sie können die Apps definieren, indem Sie den App-Paketnamen der Apps eingeben, die Sie sichtbar machen möchten. So würden Sie Einstellungen beispielsweise mit „com.android.settings“ auf dem Startbildschirm sichtbar machen. Die Apps, die Sie der Zulassungsliste in diesem Abschnitt hinzufügen, sollten bereits auf dem Gerät installiert sein, damit sie auf dem Startbildschirm sichtbar sind.    |
|    Angeheftete Weblinks festlegen    |    bundleArray    | <img alt="JSON - Example 2" src="./media/app-configuration-managed-home-screen-app/defaultvaluejson02.png" width="300"> |    Ermöglicht es Ihnen, Websites als Schnellstartsymbole auf dem Startbildschirm anzuheften. Bei dieser Konfiguration können Sie die URL definieren und auf dem Startbildschirm hinzufügen, damit sie der Endbenutzer mit einem einfachen Tippen im Browser starten kann. Anmerkung: Sie sollten [verwaltete Google Play-Weblinks](./apps-add-android-for-work.md#managed-google-play-web-links) für Ihre Geräte erstellen, zuweisen und genehmigen. Diese werden wie auf der Zulassungsliste aufgeführte Anwendungen behandelt.    |
|    Verwalteten Ordner zum Gruppieren von Apps erstellen    |    bundleArray    | <img alt="JSON - Example 3" src="./media/app-configuration-managed-home-screen-app/defaultvaluejson03.png" width="300"> |    Ermöglicht es Ihnen, Ordner zu erstellen und zu benennen sowie Apps in diesen Ordnern zu gruppieren. Endbenutzer können Ordner nicht verschieben, sie umbenennen oder die Apps innerhalb der Ordner verschieben.   Ordner werden in der Reihenfolge ihrer Erstellung und die Apps in den Ordnern in alphabetischer Reihenfolge angezeigt.         Hinweis: Alle Apps, die Sie in Ordnern gruppieren möchten, müssen dem Gerät nach Bedarf zugewiesen werden und vorher Managed Home Screen hinzugefügt worden sein.     |

Dies ist ein Beispiel für ein JSON-Skript, in dem alle verfügbaren Konfigurationsschlüssel enthalten sind:

```json
{
    "kind": "androidenterprise#managedConfiguration",
    "productId": "com.microsoft.launcher.enterprise",
    "managedProperty": [
        {
            "key": "lock_home_screen",
            "valueBool": true
        },
        {
            "key": "wallpaper",
            "valueString": "default"
        },
        {
            "key": "icon_size",
            "valueInteger": 2
        },
        {
            "key": "app_folder_icon",
            "valueInteger": 0
        },
        {
            "key": "screen_orientation",
            "valueInteger": 1
        },
        {
            "key": "applications",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "package",
                            "valueString": "app package name here"
                        }
                    ]
                }
            ]
        },
        {
            "key": "weblinks",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "link",
                            "valueString": "link here"
                        },
                        {
                            "key": "label",
                            "valueString": "weblink label here"
                        }
                    ]
                }
            ]
        },
        {
            "key": "show_virtual_home",
            "valueBool": false
        },
        {
            "key": "virtual_home_type",
            "valueString": "swipe_up"
        },
        {
            "key": "show_virtual_status_bar",
            "valueBool": true
        },
        {
            "key": "exit_lock_task_mode_code",
            "valueString": ""
        },
        {
            "key": "show_wifi_setting",
            "valueBool": false
        },
        {
            "key": "show_bluetooth_setting",
            "valueBool": false
        },
        {
            "key": "show_flashlight_setting",
            "valueBool": false
        },
        {
            "key": "show_volume_setting",
            "valueBool": false
        },
        {
            "key": "show_device_info_setting",
            "valueBool": false
        },
        {
            "key": "show_managed_setting",
            "valueBool": false
        },
        {
            "key": "enable_easy_access_debugmenu",
            "valueBool": false
        },
        {
            "key": "enable_wifi_allowlist",
            "valueBool": false
        },
        {
            "key": "wifi_allowlist",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "SSID",
                            "valueString": "name of Wi-Fi network 1 here"
                        }
                    ]
                },   
                {
                    "managedProperty": [
                        {
                            "key": "SSID",
                            "valueString": "name of Wi-Fi network 2 here"
                        }
                    ]
                }  
            ]
        },
        {
            "key": "grid_size",
            "valueString": "4;5"
        },
        {
            "key": "app_order_enabled",
            "valueBool": true
        },
        {
            "key": "apps_in_folder_ordered_by_name",
            "valueBool": true
        },
        {
            "key": "app_orders",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "package",
                            "valueString": "com.Microsoft.emmx"
                        },
                        {
                            "key": "type",
                            "valueString": "application"
                        },
                        {
                            "key": "container",
                            "valueInteger": 1
                        },
                        {
                            "key": "position",
                            "valueInteger": 1
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "folder_name",
                            "valueString": "Work"
                        },
                        {
                            "key": "type",
                            "valueString": "managed_folder"
                        },
                        {
                            "key": "container",
                            "valueInteger": 1
                        },
                        {
                            "key": "position",
                            "valueInteger": 2
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "package",
                            "valueString": "com.microsoft.launcher.enterprise"
                        },
                        {
                            "key": "type",
                            "valueString": "application"
                        },
                        {
                            "key": "class",
                            "valueString": "com.microsoft.launcher.launcher"
                        },
                        {
                            "key": "container",
                            "valueInteger": 1
                        },
                        {
                            "key": "position",
                            "valueInteger": 3
                        }
                    ]
                }
            ]
        },
        {
            "key": "managed_folders",
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "folder_name",
                            "valueString": "Folder name here"
                        },
                        {
                            "key": "applications",
                            "valueBundleArray": [
                                {
                                    "managedProperty": [
                                        {
                                            "key": "package",
                                            "valueString": "com.microsoft.emmx"
                                        }
                                    ]
                                },
                                {
                                    "managedProperty": [
                                        {
                                            "key": "package",
                                            "valueString": "com.microsoft.bing"
                                        }
                                    ]
                                },
                                {
                                    "managedProperty": [
                                        {
                                            "key": "link",
                                            "valueString": "https://microsoft.com/"
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "folder_name",
                            "valueString": "Example folder name 2"
                        },
                        {
                            "key": "applications",
                            "valueBundleArray": [
                                {
                                    "managedProperty": [
                                        {
                                            "key": "package",
                                            "valueString": "com.microsoft.office.word"
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                }
            ]
        }
    ]
}
```

## <a name="googles-android-device-policy-app"></a>Android Device Policy von Google
Mit der App „Managed Home Screen“ ist nun der Zugriff auf die Android Device Policy-App von Google möglich. Die App „Managed Home Screen“ ist ein benutzerdefiniertes Startprogramm, das für Geräte verwendet wird, die bei Intune als dedizierte Android Enterprise-Geräte (AE) registriert sind und den Kioskmodus mit mehreren Apps verwenden. Zu Unterstützungs- und Debugzwecken können Sie auf die Android Device Policy-App zugreifen oder Benutzer auf diese weiterleiten. Diese Startfunktion ist verfügbar, sobald das Gerät registriert wird und sich bei der App „Managed Home Screen“ einloggt. Für diese Funktion sind keine weiteren Installationen nötig.

## <a name="managed-home-screen-debug-screen"></a>Managed Home Screen-Debugbildschirm
Sie können auf den Managed Home Screen-Debugbildschirm zugreifen, indem Sie auf die Schaltfläche **Zurück** klicken, bis der Debugbildschirm angezeigt wird (klicken Sie mindestens 15 mal auf die Schaltfläche **Zurück**). Von diesem Debugbildschirm aus können Sie die Android Device Policy-Anwendung starten, Protokolle anzeigen und hochladen oder den Kioskmodus vorübergehend anhalten, um das Gerät zu aktualisieren. Weitere Informationen zum Anhalten des Kioskmodus finden Sie unter **Kioskmodus verlassen** in den [Einstellungen dedizierter Geräte](../configuration/device-restrictions-android-for-work.md#device-experience) in Android Enterprise. Wenn Sie einen einfacheren Zugriff auf den Debugbildschirm des Managed Home Screens wünschen, können Sie das Menü **Einfachen Zugriff auf das Menü „Debuggen“ aktivieren** mithilfe von Richtlinien zur Anwendungskonfiguration auf `True` festlegen. 

## <a name="next-steps"></a>Nächste Schritte

- Weitere Informationen zu dedizierten Android Enterprise-Geräten finden Sie unter [Einrichten der Intune-Registrierung für dedizierte Android Enterprise-Geräte](../enrollment/android-kiosk-enroll.md).
