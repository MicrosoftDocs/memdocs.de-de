---
title: Abrufen von Daten aus der Data Warehouse-API mit einem REST-Client
titleSuffix: Microsoft Intune
description: In diesem Thema wird beschrieben, wie Sie Daten über eine RESTful-API aus dem Microsoft Intune-Data Warehouse abrufen.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/06/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: D6D15039-4036-446C-A58F-A5E18175720A
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4f00ba5049401c07f5112061172dc3e7cda4f46c
ms.sourcegitcommit: 16bc2ed5b64eab7f5ae74391bd9d7b66c39d8ca6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/17/2020
ms.locfileid: "86437360"
---
# <a name="get-data-from-the-intune-data-warehouse-api-with-a-rest-client"></a>Abrufen von Daten aus der Intune-Data Warehouse-API mit einem REST-Client

Sie können auf das Intune-Data Warehouse-Datenmodell über RESTful-Endpunkte zugreifen. Um auf Ihre Daten zuzugreifen, muss sich der Client mithilfe von OAuth 2.0 bei Microsoft Azure Active Directory (Azure AD) autorisieren. Richten Sie zum Aktivieren des Zugriffs zuerst eine native App in Azure ein, und erteilen Sie ihr Berechtigungen für die Microsoft Intune-API. Ihr lokaler Client ruft die Autorisierung ab, und dann kann der Client über die native App mit den Data Warehouse-Endpunkten kommunizieren.

Für die Einrichtung eines Clients zum Abrufen von Daten aus der Data Warehouse-API bestehen die folgenden Anforderungen:

1. Erstellen Sie eine Client-App als eine native App in Azure.
3. Erteilen Sie der Client-App Zugriff auf die Microsoft Intune-API.
3. Erstellen Sie einen lokalen REST-Client zum Abrufen der Daten.

Aus den folgenden Schritten können Sie ersehen, wie Autorisierung und Zugriff auf eine API mit einem REST-Client erfolgen. Sehen wir uns zunächst einen generischen REST-Client am Beispiel von Postman an. Bei Postman handelt es sich um ein häufig verwendetes Tool zur Problembehandlung und Entwicklung von REST-Clients für APIs. Weitere Informationen zu Postman finden Sie auf der [Postman](https://www.getpostman.com)-Website. Anschließend können Sie ein C#-Codebeispiel betrachten. Darin wird gezeigt, wie ein Client autorisiert und Daten aus der API abgerufen werden.

## <a name="create-a-client-app-as-a-native-app-in-azure"></a>Erstellen Sie eine Client-App als eine native App in Azure.

Erstellen Sie eine native App in Azure. Diese native App ist die Client-App. Der Client auf dem lokalen Computer verweist auf die Intune-Data Warehouse-API, wenn der lokale Client Anmeldeinformationen anfordert.

1. Melden Sie sich beim [Azure Active Directory Admin Center](https://aad.portal.azure.com/) an.
2. Klicken Sie auf **Azure Active Directory** > **App-Registrierungen**, um den Bereich **App-Registrierungen** zu öffnen.
3. Wählen Sie **New app registration** (Neue App-Registrierung) aus.
4. Geben Sie die App-Informationen ein.
    1. Geben Sie unter **Name** einen Anzeigenamen wie „Intune-Data Warehouse-Client“ ein.
    2. Wählen Sie für **Unterstützte Kontotypen** die Option **Nur Konten in diesem Organisationsverzeichnis (nur Microsoft – einzelner Mandant)** aus.
    3. Geben Sie eine URL als **Umleitungs-URI** ein. Der Umleitungs-URI hängt vom spezifischen Szenario ab, wenn Sie jedoch Postman verwenden möchten, geben Sie `https://www.getpostman.com/oauth2/callback` ein. Sie verwenden bei der Authentifizierung in Azure AD den Schritt zum Rückruf der Client-Authentifizierung.
5. Wählen Sie **Registrieren** aus.
6. Notieren Sie sich die **Anwendungs-ID (Client)** dieser App. Sie benötigen sie im nächsten Abschnitt.

## <a name="grant-the-client-app-access-to-the-microsoft-intune-api"></a>Erteilen Sie der Client-App Zugriff auf die Microsoft Intune-API.

Sie haben jetzt eine in Azure definierte App. Erteilen Sie Zugriff von der nativen App auf die Microsoft Intune-API.

1. Melden Sie sich beim [Azure Active Directory Admin Center](https://aad.portal.azure.com/) an.
2. Klicken Sie auf **Azure Active Directory** > **App-Registrierungen**, um den Bereich **App-Registrierungen** zu öffnen.
3. Wählen Sie die App aus, der Sie den Zugriff gewähren müssen. Sie haben der App einen Namen wie **Intune-Data Warehouse-Client** gegeben.
4. Klicken Sie auf **API-Berechtigungen** > **Berechtigung hinzufügen**.
5. Suchen Sie die Intune-API, und wählen Sie sie aus. Sie heißt **Microsoft Intune-API**.
6. Klicken Sie auf das Feld **Delegierte Berechtigungen**, und klicken Sie dann auf **Get data warehouse information from Microsoft Intune** (Data Warehouse-Informationen von Microsoft Intune abrufen).
7. Klicken Sie auf **Berechtigungen hinzufügen**.
8. Optional können Sie im Bereich „Konfigurierte Berechtigungen“ auf **Administratorzustimmung für Microsoft erteilen** klicken und dann **Ja** auswählen. Dadurch wird der Zugriff auf alle Konten im aktuellen Verzeichnis gewährt. Außerdem wird so verhindert, dass das Zustimmungsdialogfeld für jeden Benutzer im Mandanten angezeigt wird. Weitere Informationen finden Sie unter [Integrieren von Anwendungen in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications).
9. Klicken Sie auf **Certificates & secrets** >  **+ New client secret** (Zertifikate & Geheimnisse > + Neuer geheimer Clientschlüssel), und generieren Sie ein neues Geheimnis. Stellen Sie sicher, dass Sie dieses an einen sicheren Ort kopieren, da Sie später nicht mehr darauf zugreifen können.

## <a name="get-data-from-the-microsoft-intune-api-with-postman"></a>Abrufen von Daten aus der Microsoft Intune-API mit Postman

Sie können mit der Intune-Data Warehouse-API und einem generischen REST-Client wie Postman arbeiten. Postman kann einen Einblick in die Features der API und das zugrunde liegende OData-Datenmodell geben sowie eine Problembehandlung für die Verbindung mit den API-Ressourcen durchführen. In diesem Abschnitt finden Sie Informationen zum Generieren eines Auth2.0-Tokens für den lokalen Client. Der Client benötigt das Token zum Authentifizieren bei Azure AD und den Zugriff auf die API-Ressourcen.

### <a name="information-you-will-need-to-make-the-call"></a>Informationen, die Sie für den Aufruf benötigen

Sie benötigen die folgenden Informationen für einen REST-Aufruf mit Postman:

| Attribut        | BESCHREIBUNG                                                                                                                                                                          | Beispiel                                                                                       |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| Rückruf-URL     | Legen Sie dies auf der Seite „Einstellungen“ Ihrer App als die Rückruf-URL fest.                                                                                                                              | https://www.getpostman.com/oauth2/callback                                                    |
| Tokenname       | Eine Zeichenfolge, mit der die Anmeldeinformationen der Azure-App übergeben werden. Der Prozess generiert Ihr Token, sodass Sie die Data Warehouse-API aufrufen können.                          | Bearer                                                                                        |
| Authentifizierungs-URL         | Dies ist die URL, die zum Authentifizieren verwendet wird. | https://login.microsoftonline.com/common/oauth2/authorize?resource=https://api.manage.microsoft.com/ |
| Zugriffstoken-URL | Mit dieser URL wird das Token erteilt.                                                                                                                                              | https://login.microsoftonline.com/common/oauth2/token |
| Client-ID        | Diese haben Sie erstellt und sich bei der Erstellung der nativen App in Azure notiert.                                                                                               | 4184c61a-e324-4f51-83d7-022b6a81b991                                                          |
| Geheimer Clientschlüssel        | Diese haben Sie erstellt und sich bei der Erstellung der nativen App in Azure notiert.                                                                                               | Ksml3dhDJs+jfK1f8Mwc8                                                          |
| Bereich (Optional) | Leer                                                                                                                                                                               | Sie können das Feld leer lassen.                                                                     |
| Gewährungstyp       | Das Token ist ein Autorisierungscode.                                                                                                                                                  | Autorisierungscode                                                                            |

### <a name="odata-endpoint"></a>OData-Endpunkt

Sie benötigen außerdem den Endpunkt. Um Ihren Data Warehouse-Endpunkt abzurufen, benötigen Sie die URL des benutzerdefinierten Feeds. Sie können den OData-Endpunkt aus dem Data Warehouse-Bereich abrufen.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
3. Öffnen Sie den Bereich **Data Warehouse**, indem Sie auf **Berichte** > **Data Warehouse** klicken.
4. Kopieren Sie die URL des benutzerdefinierten Feeds unter **OData-Feed für Berichterstellungsdienst**. Sie sollte etwa wie folgt aussehen: `https://fef.tenant.manage.microsoft.com/ReportingService/DataWarehouseFEService?api-version=v1.0`

Der Endpunkt weist das folgende Format auf: `https://fef.{yourtenant}.manage.microsoft.com/ReportingService/DataWarehouseFEService/{entity}?api-version={verson-number}`.

Beispielsweise sieht die Entität **dates** wie folgt aus: `https://fef.tenant.manage.microsoft.com/ReportingService/DataWarehouseFEService/dates?api-version=v1.0`

Weitere Informationen finden Sie unter [Intune Data Warehouse-API-Endpunkt](reports-api-url.md).

### <a name="make-the-rest-call"></a>Ausführen des REST-Aufrufs

Um ein neues Zugriffstoken für Postman abzurufen, müssen Sie die URL der Azure AD-Autorisierung, Ihre Client-ID und den geheimen Clientschlüssel hinzufügen. Postman lädt die Autorisierungsseite, auf der Sie Ihre Anmeldeinformationen eingeben.

#### <a name="add-the-information-used-to-request-the-token"></a>Fügen Sie die Informationen zum Anfordern des Tokens hinzu.

1. Wenn Sie es nicht bereits installiert haben, laden Sie Postman herunter. Postman können Sie unter [www.getpostman](https://www.getpostman.com) herunterladen.
2. Öffnen Sie Postman. Wählen Sie den HTTP-Vorgang **GET** aus.
3. Fügen Sie die Endpunkt-URL in die Adresse ein. Sie sollte etwa wie folgt aussehen:  

    `https://fef.tenant.manage.microsoft.com/ReportingService/DataWarehouseFEService/dates?api-version=v1.0`
4. Klicken Sie auf die Registerkarte **Autorisierung**, und wählen Sie aus der Liste **Typ** die Option **OAuth 2.0** aus.
5. Wählen Sie **Get New Access Token** (Neues Zugriffstoken abrufen) aus.
6. Stellen Sie sicher, dass Sie die Rückruf-URL bereits zu Ihrer App in Azure hinzugefügt haben. Die Rückruf-URL lautet `https://www.getpostman.com/oauth2/callback`.
7. Geben Sie „Bearer“ als **Tokenname** ein.
8. Fügen Sie die **Authentifizierungs-URL** hinzu. Sie sollte etwa wie folgt aussehen:  

    `https://login.microsoftonline.com/common/oauth2/authorize?resource=https://api.manage.microsoft.com/`
9. Fügen Sie das **Zugriffstoken** hinzu. Sie sollte etwa wie folgt aussehen:  

     `https://login.microsoftonline.com/common/oauth2/token`

10. Fügen Sie die **Client-ID** aus der nativen Anwendung hinzu, die Sie in Azure erstellt und `Intune Data Warehouse Client` genannt haben. Sie sollte etwa wie folgt aussehen:  

     `88C8527B-59CB-4679-A9C8-324941748BB4`

11. Fügen Sie den **geheimen Clientschlüssel** hinzu, den Sie in der in Azure erstellten nativen App generiert haben. Sie sollte etwa wie folgt aussehen:  

     `Ksml3dhDJs+jfK1f8Mwc8 `

12. Wählen Sie als Gewährungstyp **Authorization Code** (Autorisierungscode) aus.

13. Wählen Sie **Request Token** (Token anfordern) aus.

    ![Informationen für das Zugriffstoken](./media/reports-proc-data-rest/reports-postman_getnewtoken.png)

14. Geben Sie Ihre Anmeldeinformationen auf der Azure AD-Autorisierungsseite ein. Die Liste der Token in Postman enthält jetzt das Token mit dem Namen `Bearer`.
15. Wählen Sie **Token verwenden** aus. Die Liste der Header enthält den neuen Schlüsselwert von „Authorization“ (Autorisierung) und den Wert `Bearer <your-authorization-token>`.

#### <a name="send-the-call-to-the-endpoint-using-postman"></a>Senden des Aufrufs an den Endpunkt mit Postman

1. Wählen Sie **Senden** aus.
2. Die Rückgabedaten werden im Antworttextfeld von Postman angezeigt.

    ![Postman-Clientstatus ist gleich 200 OK](./media/reports-proc-data-rest/reports-postman_200OK.png)

## <a name="create-a-rest-client-c-to-get-data-from-the-intune-data-warehouse"></a>Erstellen eines REST-Clients (C#), um Daten aus der Intune-Data Warehouse-API abzurufen

Das folgende Beispiel enthält einen einfachen REST-Client. Der Code verwendet die **httpClient**-Klasse aus der .NET-Bibliothek. Sobald der Client Anmeldeinformationen für Azure AD erhält, erstellt er einen GET REST-Aufruf, um die Datumsentität aus der Data Warehouse-API abzurufen.

> [!Note]  
> Sie können [auf GitHub](https://github.com/Microsoft/Intune-Data-Warehouse/blob/master/Samples/CSharp/Program.cs) auf das folgende Codebeispiel zugreifen. Im GitHub-Repository finden Sie auch die neuesten Änderungen und Updates des Beispiels.

1. Öffnen Sie **Microsoft Visual Studio**.
2. Klicken Sie auf **Datei** > **Neues Projekt**. Erweitern Sie **Visual C#** , und wählen Sie **Konsolen-App (.NET Framework)** aus.
3. Nennen Sie das Projekt `IntuneDataWarehouseSamples`, navigieren Sie dorthin, wo Sie das Projekt speichern möchten, und wählen Sie dann **OK** aus.
4. Klicken Sie mit der rechten Maustaste auf den Namen der Projektmappe im Projektmappen-Explorer, und wählen Sie dann **NuGet-Pakete für Projektmappe verwalten** aus. Wählen Sie **Durchsuchen** aus, und geben Sie dann `Microsoft.IdentityModel.Clients.ActiveDirectory` in das Suchfeld ein.
5. Wählen Sie das Paket aus, wählen Sie unter „Manage Packages for Your Solution“ (Pakete für Ihre Projektmappe verwalten) das Projekt **IntuneDataWarehouseSamples** aus, und wählen Sie dann **Installieren** aus.
6. Wählen Sie **I Accept** (Ich stimme zu) aus, um die NuGet-Paketlizenz zu akzeptieren.
7. Öffnen Sie `Program.cs` über den Projektmappen-Explorer.

    ![„Program.cs“ und Projektmappen-Explorer in Visual Studio](./media/reports-proc-data-rest/reports-get_rest_data_in.png)

8. Ersetzen Sie den Code in *Program.cs* durch den folgenden Code:  

   ```csharp
   namespace IntuneDataWarehouseSamples
   {
   using System;
   using System.Net.Http;
   using System.Net.Http.Headers;
   using Microsoft.IdentityModel.Clients.ActiveDirectory;

   class Program
   {
    static void Main(string[] args)
   {
   /**
   * TODO: Replace the below values with your own.
   * emailAddress - The email address of the user that you will authenticate as.
   *
   * password  - The password for the above email address.
   *    This is inline only for simplicity in this sample. We do not
   *    recommend storing passwords in plaintext.
   *
   * applicationId - The application ID of the native app that was created in AAD.
   *
   * warehouseUrl   - The data warehouse URL for your tenant. This can be found in
   *      the Azure portal.
   *
   * collectionName - The name of the warehouse entity collection you would like to
   *      access.
   */
   var emailAddress = "intuneadmin@yourcompany.com";
   var password = "password_of(intuneadmin@yourcompany.com)";
   var applicationId = "<Application ID>";
   var warehouseUrl = "https://fef.{yourinfo}.manage.microsoft.com/ReportingService/DataWarehouseFEService?api-version=v1.0";
   var collectionName = "dates";

   var adalContext = new AuthenticationContext("https://login.windows.net/common/oauth2/token");
   AuthenticationResult authResult = adalContext.AcquireTokenAsync(
   resource: "https://api.manage.microsoft.com/",
   clientId: applicationId,
   userCredential: new UserPasswordCredential(emailAddress, password)).Result;

   var httpClient = new HttpClient();
   httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);

   var uriBuilder = new UriBuilder(warehouseUrl);
   uriBuilder.Path += "/" + collectionName;

   HttpResponseMessage response = httpClient.GetAsync(uriBuilder.Uri).Result;

   Console.Write(response.Content.ReadAsStringAsync().Result);
   Console.ReadKey();
   }
   }
   }
   ```

9. Aktualisieren Sie die `TODO`s im Codebeispiel.
10. Drücken Sie **STRG + F5**, um den Intune.DataWarehouseAPIClient im Debugmodus zu erstellen und auszuführen.

    ![Im JSON-Format abgerufene Datumsentität](./media/reports-proc-data-rest/reports-get_rest_data_output.png)

11. Überprüfen Sie die Konsolenausgabe. Die Ausgabe enthält die Daten im JSON-Format, die aus der **Datumsentität** in Ihrem Intune-Mandanten abgerufen wurden.

## <a name="next-steps"></a>Nächste Schritte

Informationen zur Autorisierung, der API-URL-Struktur und den OData-Endpunkten finden Sie unter [Endpunkt der Intune Data Warehouse-API](reports-api-url.md).

Auch im Intune Data Warehouse-Datenmodell finden Sie die in der API enthaltenen Datenentitäten. Weitere Informationen finden Sie unter [Datenmodell von Data Warehouse](reports-ref-data-model.md).
