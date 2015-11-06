Arbeiten mit dem Management Portal
==================================

Das Azure Management Portal ist die zentrale Anlaufstelle, um Cloud Ressourcen, wie Web Apps, Virtual Machines oder Storage Accounts, anzulegen und zu verwalten. Über das Portal können die Ressourcen sehr leicht und flexibel konfiguriert, überwacht und skaliert werden.

Dieses Lab umfasst folgende Übungen:

1. [Überblick über das Portal](#Task1)
1. [Anlegen neuer Ressourcen](#Task2)
1. [Verwaltung bestehender Ressourcen](#Task3)

In diesem Lab werden Sie folgendes lernen:

- Arbeiten mit dem Azure Management Portal
- Erstellen neuer Elemente und Dienste
- Verwaltung eingerichteter Ressourcen

<a name="Task1"></a>
## Überblick über das Portal

In dieser Übung erhalten Sie einen Überblick über die verschiedenen Bestandteile und Elemente des Azure Management Portals.

1. Öffnen Sie Ihren Browser und navigieren Sie zu [https://portal.azure.com/](https://portal.azure.com/). Um zu vermeiden, dass der Browser gespeicherte (ggf. ungeeignete) User-Credentials zur Anmeldung verwendet, empfiehlt sich die Ausführung des Browsers im InPrivate-Modus (Internet Explorer) bzw. Incognito-Fenster (Chrome) etc.

2. Geben Sie Ihre Anmeldeinformation für den Zugriff auf Ihre _Azure Subscription_ ein. 

    Dies bringt Sie zur Startseite des Portals. Standardmäßig zeigt diese Ansicht alle Ressourcen an, die in der betreffenden Subscription angelegt wurden.

	![Management Portal - Startseite](images/portal-landing-page.png?raw=true)

	_Management Portal - Startseite_

3. Auf der linken Seite befindet sich die Sidebar mit Verweisen auf alle verfügbaren Dienste und Werkzeuge. Auswahl eines dieser Elemente filtert die Ansicht nach den betreffenden Elementtypen.

	![Left Sidebar](images/portal-left-sidebar.png?raw=true)

	_Linke Sidebar_

4. Am unteren Rand des Portal befindet sich eine Leiste, die kontextabhängig Aktionsschaltflächen enthält. Auf Übersichtsseiten sind dies links die Schaltfläche **NEW** und rechts die Schaltfläche **Help**. Diese Schalftlächen werden in den Abschnitten unten näher betrachtet.

	![New Button](images/portal-new-button.png?raw=true)

	_Die Schaltflächen NEW und Help_

<a name="Task2"></a>
## Anlegen neuer Ressourcen
In dieser Übung legen Sie eine neue Ressource innerhalb Ihrer Subscription an. Konkret legen Sie eine Web App mit Hilfe des **Create Wizards** an.

1. Wählen Sie die Schaltfläche **NEW** am unteren Rand des Portals.

	![Die Schaltfläche NEW](images/new-button-clicked.png?raw=true)

	_Die Schaltfläche NEW_

	Dies ruft den _Create Wizard_ auf. In diesem können Sie den Typ der zu erstellenden Ressource wählen. Wählen Sie die Werte In this case you will create a _Website_.

2. Wählen Sie den Menüpunkt **COMPUTE**. Die Compute Services werden angezeigt.

3. Wählen Sie den Menüpunkt **WEB APP**.

	Folgende drei Optionen werden angezeigt.

	- **QUICK CREATE**: Diese Option erlaubt die schnellstmögliche Erstellung einer Web App.

	- **CUSTOM CREATE**: Hier kann zur Web App gleich eine SQL Database angelegt und verknüpft sowie eine Quelle für Continuous Deployment eingerichtet werden.

	- **FROM GALLERY**: Über diesen Menüpunkt kann eine Web App auf Basis einer von vielen Vorlagen erstellt werden.

	![Optionen für die Erstellung einer Web App](images/create-flow.png?raw=true)
	_Optionen für die Erstellung einer Web App_

4. Wählen Sie die Schaltfläche **QUICK CREATE**. 

	Das Formular zur Eingabe der erforderlichen Parameter wird angezeigt. Hier können Sie die URL für Ihre Web App und die Region auswählen, in der die Anwendung ausgeführt werden soll. Es empfiehlt sich, die Region zu wählen, die am nächsten zu den erwarteten Anwendern liegt.

5. Geben Sie den **URL** für Ihre Web App an und wählen Sie die Schaltfläche  **CREATE WEBSITE**.

	> **Hinweis:** Der URL für die Web App muss eindeutig sein, da dieser für den Zugriff über das öffentliche Internet verwendet wird.

	![Creating the Website](images/create-flow-quick-create-clicked.png?raw=true)

	_Erstellung der Web App_

6. Nach einer kurzen Wartezeit (ca. 20 Sekunden) ist die Web App erstellt. Dies wird über die Statusleiste mitgeteilt. Wählen Sie in der Sidebar den Menüpunkt **WEB APPS**. Daraufhin wird die neu erstellte Web App angezeigt.

	![Die erstellte Web App](images/website-listing.png?raw=true)

	_Die erstellte Web App_
	
7. Klicken Sie auf den Namen der neu erstellten Web App, um zur _Quick Start Management Seite_ der Web App zu gelangen.

8. Wählen Sie die Schaltfläche **BROWSE** am unteren Rand des Portals, um zur erstellen Web App zu navigieren.

	![Klick auf Browse, um die Web App aufzurufen](images/clicking-browse-to-view-the-site.png?raw=true)

	_Klick auf Browse, um die Web App aufzurufen_

	![Anzeige der Web App](images/browsing-the-website.png?raw=true)

	_Anzeige der Web App_

9. Schließen Sie die Web App und kehren Sie zur **Management Portal** zurück.
	
<a name="Task3"></a>
## Verwaltung bestehender Ressourcen

In dieser Übung gehen Sie durch die verschiedenen Optionen zur Verwaltung der zuvor erstellten Web App.

1. Sofern Sie nicht schon auf der _Quick Start Management_ Seite sind, wählen Sie den Namen der Web App, um sie anzuzeigen.
	
	Diese Seite ermöglicht schnellen Zugriff auf wichtige Funktionen zur Verwaltung des Deployments einer Web App in Microsoft Azure. Diese Seite ist darüber hinaus die Einstiegsseite für neu angelegte Web Apps.

    ![Quickstart Management Seite einer Web App](images/website-quickstart.png?raw=true)

    _Quickstart Management Seite einer Web App_

2. Beachten Sie die Aktionsschaltflächen am unteren Rand der Seite. Dies sind:

    - **BROWSE**: Zum Aufrufen der aktuell installierten Version der Web App
    - **STOP**: Zum Anhalten des Web App Deployments
    - **RESTART**: Zum Neustart des Web App Deployments
    - **DELETE**: Zum Löschen der Web App
    - **WEBMATRIX**: Ermöglicht die Installation von WebMatrix, Microsofts Authoring Werkzeug zum Erstellen, Editieren und Veröffentlichen von Web Apps

3. Beachten Sie die Top Bar mit den verfügbaren Konfigurationsbereichen. Diese Bereiche sind:

    - Dashboard
	- Monitor
	- Webjobs
    - Configure
    - Scale
    - Linked Resources
    - Backups

	Der Rest dieser Übung geht auf die wichtigsten dieser Bereiche ein.
  
	> **Hinweis**: Für Informationen zu all diesen Optionen, siehe [Configure Web Apps in Azure App Service](http://azure.microsoft.com/en-us/documentation/articles/web-sites-manage/).
    
4. Wählen Sie die Schaltfläche **DASHBOARD**. 

	Dies zeigt das Dashboard der Web App an. Diese Ansicht gibt Ihnen die wichtigsten Informationen der Web App in einer Übersicht an. Vom Health-Status bis hin zu Nutzungsstatistiken bietet die Seite Details zur Web App.

	![Dashboard Ansicht](images/website-dashboard-view.png?raw=true)

	_Dashboard Ansicht_
    
5. Wählen Sie die Schaltfläche **MONITOR**. 

	Diese Ansicht ermöglicht die Einrichtung von Tests, die die Verfügbarkeit von HTTP und HTTPS Endpunkten von drei global verteilten Lokationen prüfen. Ein Test schlägt fehl, wenn der HTTP Response Code einen Fehler beschreibt (4xx oder 5xx) oder die Antwort länger als 30 Sekunden benötigt. Ein Endpunkt wird als verfügbar betrachtet, wenn die Monitoring-Tests von allen angegebenen Lokationen erfolgreich sind.

	![Monitor Ansicht](images/website-monitor-view.png?raw=true)

	_Monitor Ansicht_
    
6. Wählen Sie die Schaltfläche **WEBJOBS**. 

	Die WebJobs Management-Seite ermöglicht die Einrichtung von Tasks der Web App, die auf Anforderung (on-demand), nach Zeitplan oder durchgängig laufen.

	> **Hinweis**: Für weitere Informationen zu WebJobs siehe [Run Background tasks with WebJobs](http://azure.microsoft.com/en-us/documentation/articles/web-sites-create-web-jobs/).
    
    ![WebJobs Ansicht](images/website-webjobs-view.png?raw=true)

	_WebJobs Ansicht_
    
7. Abschließend wählen Sie die Schaltfläche **SCALE**, um die Skalierungsmöglichkeiten anzuzeigen. 

	Um Performance und Durchsatz der Web App zu erhöhe können Sie die Leistungsstufe des App Service Hosting Plans auf die Einstellungen _Free_ , _Shared_ , _Basic_ und _Standard_ setzen. Die Skalierung eines Web App Hosting Plans umfasst zwei Schritte: Änderung des App Hosting Plan Modes zu einer anderen Leistungsstufe und Konfiguration entsprechender Einstellungen der Leistungsstufe (z.B. Änderung der Instanz-Anzahl). Diese Änderungen erfolgen innerhalb weniger Sekunden und wirken sich dann auf alle Web Apps des Web App Hosting Plans aus. Weder sind Änderungen an der Anwendung noch ein Redeployment der Anwendung erforderlich.

    ![Scale Ansicht](images/website-scale-view.png?raw=true)

	_Scale Ansicht_

	>**Hinweis:** Es hat sich (nicht zuletzt aus Kostengründen) bewährt, nicht mehr benötigte Ressourcen, zu löschen. Um die zuvor erstellte Web App zu löschen, führen Sie folgende Schritte durch:
	>
	>1. Wählen Sie die Schaltfläche **DASHBOARD** am oberen Seitenrand.
	>
	>1. Wählen Sie die Schaltfläche **DELETE** am unteren Seitenrand.
	>
	>   ![Löschen einer Web App](images/clicking-delete-website.png?raw=true)
	>
	>   _Löschen einer Web App_
	>
	>1. Im **Delete Confirmation** Dialog, wählen Sie die Schaltfläche **OK**.
	>
	>![Bestätigung der Löschung](images/delete-confirmation-dialog.png?raw=true)
	>
	>_Bestätigung der Löschung_
	>
	>Nach kurzer Zeit (wenige Sekunden) sollten Sie die Bestätigung erhalten, dass die Web App erfolgreich gelöscht wurde. Die Web App wird dann nicht länger unter den bestehenden Web Apps gelistet.



## Zusammenfassung
In diesem Lab haben Sie das **Azure Management Portal** kennengelernt. Sie haben die wichtigsten Elemente des Portals gesehen und anhand einer Web App die Schritte zum Erstellen und Management von Ressourcen betrachtet.
