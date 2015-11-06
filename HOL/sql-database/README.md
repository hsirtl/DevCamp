Schnellstart in die Nutzung Azure SQL Database Elastic Scale
=======================================================================================

Wachsenden und schrumpfende Kapazitäten, welche sich am tatsächlichen Bedarf orientieren, sind eines der Kernversprechen von Cloud Computing. Diesem Versprechen gerecht zu werden war in der Vergangheit für die Datenbankschicht von Cloud Anwendugnen jedoch oft mühsam und komplex. Über die letzten Jahre hat sich in der Industrie hierfür ein Entwurfsmuster etabliert, welches als "Sharding* bekannt ist. Obwohl das allgemeine Sharding-Entwurfsmuster viele der Herausforderungen löst, sind für die Entwicklung und den Betrieb von Anwendungen die dieses nutzen, unabhängig von der Business Logic immer noch nennenswerte Investitionen in die Infrastruktur nötig.

Azure SQL Database Elastic Scale ermöglicht es der Datenschicht einer Anwendung, auf Basis von in der Industrie etablierten Vorgehensweisen für das Sharding, zu skalieren und zugleich die Entwicklung und das Management von Cloud-Anwendungen zu optimieren. Elastic Scale bietet Funktionalitäten für Entwicklung und Management über .Net Bibliotheken sowie Vorlagen für Azure Dienste, die Sie in Ihrer eigenen Azure Subscription betreiben können, um Ihre hochskalierbaren Anwendungen zu verwalten. Azure Database Elastic Scale setzt die Infrastrukturaspekte von Sharding um und erlaubt es Ihnen somit, sich auf die Geschäftslogik Ihrer Anwendung zu konzentrieren.  

In diesem Lab werden Sie die Entwicklerseite von Azure SQL Database Elastic Scale näher kennenlernen.

Dieses Lab enthält die folgende Aufgaben:

* [Erstellen eines Microsoft Azure SQL Database Servers](#Task1)
* [Durchlaufen des Beispiels](#Task2)
* [Anhang - Aufräumen](#cleanup)

<a name="Task1"></a>
## Erstellen eines Microsoft Azure SQL Database Servers ##

In dieser Aufgabe werden Sie einen neuen Microsoft Azure SQL Database Server erstellen und die Firewall so konfigurieren, dass Verbindungen von auf dem lokalen Computer ausgeführten Anwendungen Zugriff auf die Datenbanken in Ihrem SQL Database Server haben.

1. Melden Sie sich am [Management Portal](http://manage.windowsazure.com) an.

1. Klicken Sie im seitlichen Menü auf **SQL DATABASES**. Klicken Sie dann auf die Registerkarte **SERVERS**. 

	![Navigating to the SQL Database Servers tab](./images/navigating-to-the-sql-servers-tab.png)

	_Navigation zur Registerkarte SQL Database Server_

1. Klicken Sie auf **ADD** in der unteren Leiste, um einen neuen SQL Database Server anzulegen.

	![Adding a new SQL Database Server](./images/adding-a-new-sql-server.png)

	_Hinzufügen eines neuen SQL Database Servers_

1. Setzen Sie im **CREATE SERVER** Dialogfenster die Servereinstellungen wie folgt:

	* **Login Name**: Geben Sie den Adminstratornamen als ein Wort ohne Leerzeichen an. SQL Database verwendet SQL Authentifizierung über eine verschlüsselte Verbindung, um den Benutzer zu validieren. Ein neuer SQL Server Authentifizierungs-Login mit Administratorrechten wird mit dem von Ihnen definierten Namen erstellt. Der Administratorname kann kein Windows Benutzer oder Live ID / Microsoft Account sein. Windows Authetifizierung wird von SQL Database nicht unterstützt.
	
	* **Login Password**: Verwenden Sie ein Passwort mit mindestens 8 Zeichen, mit einer Kombination aus Groß- und Kleinbuchstaben und einer Zahl bzw. Sonderzeichen. Verwenden Sie die Hilfe-Schaltfäche **?** für mehr Informationen zu Passwortkomplexität.

	* **Region**: Wählen Sie eine Region. Die Region bestimmt die geographische Position Ihres Servers. Regionen können im laufenden Betrieb nicht einfach gewechselt werden, stellen Sie daher sicher die Region zu wählen, welche für Ihre Zwecke am besten geeignet ist. Der Betrieb der eigenen Azure Anwendung und der Datenbank in der gleiche Region hilft dabei die Latenz zu verringern und Kosten für ausgehenden Datentransfer zu reduzieren.
	
	* Stellen Sie sicher, dass **Allow Azure Services to access this server** ausgewählt ist, damit Dienste wie Azure SQL Reporting auf die Datenbank zugreifen können.

	Klicken Sie letztenendes auf den Haken im unteren Teil des Dialogs, um den Server zu erstellen.

	Beachten Sie, dass Sie keinen Servernamen definiert haben. Da der Server weltweit zugreifbar sein soll, konfiguriert SQL Database den entsprechenden DNS-Eintrag, wenn der Server erstellt wird. Der generierte Name stellt sicher, dass es keine Namenskonflikte mit anderen DNS-Einträgen gibt. Sie können den Namen Ihres SQL Database Servers nicht ändern.
	
	![Creating a new SQL Database Server](./images/creating-a-sql-database-server.png)

	_Erstellen eines neuen SQL Database Server_

1. Warten Sie bis der Server erstellt wurde. Sie werden dann einen Hinweis sehen und es wird eine Eintrag auf der **SQL databases** Seite hinzugefügt.

	![SQL Database Server created](images/sql-database-server-created.png?raw=true)

	_SQL Database Server erstellt_

	Nun werden Sie die Firewall so konfigurieren, dass Sie Verbindungen von Anwendungen auf dem lokalen Computer einen Zugriff auf die Datenbanken auf Ihrem SQL Database Server erlaubt.
	
	Um die Firewall so zu konfigurieren, dass Verbindungen erlaubt werden, werden Sie Informationen auf der Server Seite eingeben.
	
	> **Hinweis:** Der SQL Database Dienst ist nur über TCP port 1433 verfügbar, welcher vom TDS Protokoll verwendet wird. Stellen Sie daher sicher, dass die Firewall Ihres Netzwerks sowie der lokale Computer ausgehende Verbindungen auf Port 1433 erlaubt. Für mehre Details schauen Sie in die Informationen zur [SQL Database Firewall](http://social.technet.microsoft.com/wiki/contents/articles/2677.sql-azure-firewall-en-us.aspx).

1. Klicken Sie auf den Server den Sie gerade erstellt haben, um die Serverseite zu öffnen.

	![Navigating to the new server page](./images/navigating-to-the-new-server-page.png)

	_Navigation zum neuen Server_

1. Klicken Sie auf der Serverseite nun auf **Configure** um die **Allowed IP Addresses**-Einstellungen anzuzeigen. Klicken Sie dann auf den **Add to the allowed IP Addresses** Link. 

	Dies wird eine neue Firewall-Regel erzeugen, die Verbindungen erlaubt, die vom Router oder Proxy Server kommen, über den Sie verbunden sind.

	![Adding a firewall rule to the server](./images/adding-a-firewall-rule.png)

	_Hinzufügen einer Firewall-Regel für den Server_

	> **Hinweis:** Sie können zusätzliche Firewall-Regeln erzeugen, indem Sie einen Namen sowie einen IP-Bereich definieren.

1. Um die Änderungen zu speichern, klicken Sie auf **SAVE** am unteren Rand der Seite.

	![Saving the allowed ip changes](./images/saving-the-allowed-ip-changes.png)

	_Speichern der Änderungen an die erlaubten IP-Adressen_

1. Merken oder Notieren Sie sich den Namen des SQL Database Servers (z.B.: _z754axd2q8_), da Sie diesen im folgenden Schritt benötigen.

Sie haben nun einen SQL Database Server auf Azure, eine Firewall-Regel die den Zugriff auf den Server erlaubt und einen Administrator-Login.

<a name="Task2"></a>
## Durchlaufen des Beispiels ##

Die **Elastic Scale with Azure SQL Database - Getting Started** Beispielanwendung zeigt die wichtigstens Aspekte der Entwicklung von Anwendungen welche Sharding und Azure SQL DB Elastic Scale nutzen. Es konzentriert sich auf die Haupteinsatzzwecke von [Shard Map Management](http://go.microsoft.com/?linkid=9862595), [Data Dependent Routing](http://go.microsoft.com/?linkid=9862596) und [Multi-Shard Querying](http://go.microsoft.com/?linkid=9862597). 

Die werden nun das Beispiel herunterlagen, konfigurieren und ausführen. 

1. Öffnen Sie Visual Studio und wählen Sie **File -> New -> Project**.

	![Creating a new project](./images/creating-a-new-project.png)

	_Anlegen eines neuen Projektes_

1. Klicken Sie im _New Project_ Dialog auf **Online**.

	![Clicking Online](./images/clicking-online.png)

	_Wählen von Online_

1. Nun klicken Sie auf **Visual C#** unter **Samples**.

	![Navigating to online C# samples](./images/navigating-to-online-csharp-samples.png)

	_Wechseln zu Online C# Samples_

1. Tippen Sie **Elastic Scale** in die Suchmaske, um das Beispiel zu suchen. **Elastic DB Tools for Azure SQL - Getting Started** erscheint.
 
1. Wählen Sie das Beispiel aus, legen Sie einen Namen und einen Speicherort für das Projekt fest und klicken Sie auf **OK**, um das Projekt zu erstellen.

	![Creating the sample project](./images/creating-the-sample-project.png)

	_Erstellen des Beispielprojekts_

1. Falls der **Download and Install** Dialog erscheint, klicken Sie auf **Install**.

	![Download and Install Sample dialog](images/download-and-install-sample-dialog.png?raw=true)

	_Klicke auf Install im Download and Install Dialog_

1. Öffnen Sie die **App.config** Datei in der Solution und ersetzen Sie _MyServerName_ mit dem Namen Ihres Azure SQL Database Servers und _MyUserName_ sowie _MyPassword_ mit Ihren Anmeldeinformationen (Benutzername und Passwort).

	![Configuring the sample project](./images/configuring-the-sample.png)

	_Konfigurieren des Beispielprojekts_

1. Erstellen und Starten Sie die Anwendung. Wenn Sie gefragt werden, bestätigen Sie das wiederherstellen von NuGet Packeten in der Solution. Dies wird die neueste Version der Elastic Scale Client-Bibliotheken von NuGet herunterladen.

	![Running the sample](./images/running-the-sample.png)

	_Ausführen des Beispiels_

1. Tippen Sie **1** in der Anwendung und drücken Sie **_Enter_**, um den Shard Map Manager und mehrere Shards zu erzeugen.

	> **Hinweis:** Der Code in Datei **ShardMapManagerSample.cs** zeigt, wie Sie mit Shards, Ranges, Mappings arbeiten. Mehr zu diesem Thema finden Sie hier: [Shard Map Management](http://go.microsoft.com/?linkid=9862595).

	Die Ausgabe wird so aussehen:

	![Creating the shard map manager and adding a couple of shards](./images/creating-the-shard-map-manager.png)

	_Erzeugen des Shard Map Managers und hinzufügen mehrerer Shards_

1. Switch to the [Management Portal](http://manage.windowsazure.com), navigate to the SQL Database server page and click the **DATABASES** tab.

	Notice that you have three new databases: the shard manager and one for each shard.

	![Navigating to the SQL Database server page ](./images/navigating-to-the-server-in-the-portal.png)

	_Navigating to the SQL Database server page_

1. Switch back to the application, type **3** and then press **_enter_**. This will insert a sample row using Data-Dependent routing.

	> **Note:** Routing of transactions to the right shard is shown in **DataDependentRoutingSample.cs**. For more details, see [Data Dependent Routing](http://go.microsoft.com/?linkid=9862596). 


	![Inserting sample row](./images/inserting-sample-data.png)

	_Inserting sample row_

1. Repeat the last step at least three more times so that you have at least four rows.

1. Now, type **4** and press **_enter_** in the application to execute a sample Multi-Shard Query.

	Notice the _$ShardName_ column. It should show that the rows with a _CustomerId_ from 0 to 99 are located in the _ElasticScaleStarterKit_Shard0_ shard and those with a _CustomerId_ from 100 to 199 are located in the _ElasticScaleStarterKit_Shard1_ shard.

	> **Note:** Querying across shards is illustrated in the file **MultiShardQuerySample.cs**. For more information, see [Multi-Shard Querying](http://go.microsoft.com/?linkid=9862597).


	![Executing a Multi-Shard Query](./images/executing-a-multi-shard-query.png)

	_Executing a Multi-Shard Query_

1. Type **2** and press **_enter_** in the application to add another shard. When prompted for the higher key of the new range, press **_enter_** to use the default value of _300_.

	> **Note:** The iterative adition of new empty shards is performed by the code in
file **AddNewShardsSample.cs**. For more information see [Shard Map Management](http://go.microsoft.com/?linkid=9862595).


	![Adding a new shard](./images/adding-a-new-shard.png)

	_Adding a new shard_

1. Switch back to the **Management Portal**. You should see a new database for the new shard named _ElasticScaleStarterKit_Shard2_.

	![Viewing the new database in the portal ](./images/seeing-the-new-database-in-the-portal.png)

	_Viewing the new database in the portal_

1. Switch back to the application, type **5** and press **_enter_**. This will drop all the shards and the map manager database.

	![Removing the shards and the map manager](./images/removing-the-shards.png)

	_Removing the shards and the map manager_

1. Stop debugging.

You have successfully built and run your first Elastic Scale application on Azure SQL DB. You can find information on other Elastic Scale operations in the following links:

* **Splitting an existing shard**: The capability to split shards is provided through the **Split/Merge service**. You can find more information about this service here: [Split/Merge Service](http://go.microsoft.com/?linkid=9862795).

* **Merging existing shards**: Shard merges are also performed using the **Split/Merge service**. For more information, see [Split/Merge Service](http://go.microsoft.com/?linkid=9862795). 

<a name="cleanup"></a>
##Appendix - Cleanup

In this task you will learn how to delete the SQL Database Server created in the first task.

1. Sign in to the [Management Portal](http://manage.windowsazure.com).

1. On the sidebar, click **SQL DATABASES**. Then click the **SERVERS** tab. 

1. Click the row for the server you created to select it and then click **DELETE** from the bottom bar.

1. In the confirmation dialog that appears, type the server name and the click the check mark button.

![Delete server confirmation dialog](images/delete-server-confirmation-dialog.png?raw=true)

_Delete server confirmation dialog_

The server will be deleted. Once it is done you should see a notification in the bottom bar.

##Summary

By completing this lab you have learned the basic concepts of Azure SQL Database Elastic Scale: Shard Map Management, Data Dependent Routing and Multi-Shard Querying.
