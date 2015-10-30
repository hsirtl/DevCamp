Arbeiten mit dem Azur Preview Portal
====================================

Das neue Azure Preview Portal is ein gegenüber dem Management Portal vollständig überarbeitetes Portal. Mit diesem können nahezu alle Arten von Azure Services angelegt, konfiguriert und überwacht werden.

Das Portal vereinfacht das Anlegen, Deployen und Verwalten Ihrer Cloud Ressourcen maßgeblich. Dabei umfasst es sowohl Funktionalitäten für Entwickler als auch Funktionalitäten für den Anwendungsbetrieb, um hierüber den gesamten Lebenszyklus einer Cloud-basierten Anwendung abzudecken.

Die Startseite (auch _Stardboard_ genannt) kann individuell angepasst werden. Die wichtigsten Inhalte könne auf die Startseite gepinnt werden. Durch Anpassung der Kachelgröße können mehr oder weniger Informationen zu den betreffenden Ressourcen angezeigt werden. Durch Klick auf eine Kachel können Detailinformationen angezeigt werden. Darüber hinaus gibt es eine Reihe weiterer Funktionen:

* **Vereinfachtes Resourcenmanagement**. Anstelle Ressourcen wie Web Apps, Visual Studio Projekte oder Datenbanken einzeln zu verwalten, können gesamte Anwendungen in Form von Ressourcengruppen administriert werden. Das Portal greift hierzu auf die Funktionen des Azure Resource Managers (ARM) zu.

* **Integrierte Abrechnungsinformationen**. Über die neue, integrierte Abrechnungsfunktion erhalten Entwickler und IT Pros einen Überblick über die jeweils aufgelaufenen Kosten ihrer laufenden Cloud Ressourcen.

* **Marketplace**. Der Azure Marketplace enthält Anwendungen und Dienste von Microsoft und der Open Source Community. Dieser integrierte Marktplatz freier und kostenpflichtiger Angebote ermöglicht eine schnelle Bereitstellung Cloud-basierter Anwendungen und Dienste.

* **Visual Studio Online**. Mit dem Azure Preview Portal hat Microsoft weitere Neuerungen in Azure veröffentlich. Dazu gehören Team Projekte, mit denen der gesamte Lebenszyklus über ein leichtgewichtiges Web-basiertes Werkzeug (Codename "Monaco") verwaltet werden kann und Code-Änderungen in Web-basierten Lösungen durchgeführt werden können, ohne das Portal verlassen zu müssen. Dazu kommt noch Application Insights, einer Analytics Lösung, mit denen Telemetriedaten wie Verfügbarkeit, Performance und Nutzung von Anwendungen mitverfolgt werden können und damit einen Überblick über den Status laufender Anwendungen geben.

## Erstellung einer Web App mit zugehöriger SQL Database ##

Bislang erfolgte die Verwaltung von Azure Ressourcen (z.B. einer Datenbank, Web App) zu einem Zeitpunkt immer nur für eine einzelne Ressource. Cloud-Anwendungen enthalten in der Regel aber mehrere Azure Ressourcen. Bislang lag es in der Verantwortung des Entwicklers bzw. IT Pros diese Ressourcen zusammen zu verwalten und auf einem konsistenten Stand zu halten. Mit dem Azure Preview Portal können die Funktionen des Azure Resource Managers genutzt werden, der eine Administration auf Ebene einer Ressourcengruppe ermöglicht. Damit kann für alle Ressourcen einer Ressourcengruppe ein gemeinsamer Lifecycle umgesetzt werden.

In dieser Übung erhalten Sie einen Überblick über das Preview Portal und lernen, darüber eine Web App mit zugehöriger SQL Database anzulegen.

1. Öffnen Sie ein Browser-Fenster, navigieren Sie zu http://portal.azure.com und melden Sie sich mit Ihren Credentials an.

2. Das erste, was sie sehen werden, ist das **Startboard**. Dieses ist die Homepage des Portals, auf der Sie einen Überblick über Ihre wichtigsten Ressourcen. Die einzelnen Kacheln lassen sich konfigurieren, neue hinzufügen, in der Größe ändern etc.

	> **Hinweis:** Sie können mit der rechten Maustaste auf die Kacheln klicken, um sie zu konfigurieren (entfernen, Größe ändern, etc.).

	![Startboard](Images/startboard.png?raw=true)

	_Ihre Startseite: Das Startboard_

3. Auf der linken Seite sehen Sie das **Hub Menü**. Dieses ist das Navigationsmenü, über das Sie Zugriff auf alle Ihre Ressourcen und Optionen haben. Wählen Sie die Schaltfläche **New** oben im **Hub Menü**.

	![Creating a new resource](Images/creating-a-new-resource.png?raw=true)

	_Erstellung einer neuen Ressource_

4. Es wird ein Auswahlpanel mit verschiedenen Optionen angezeigt. Aus diesen können Sie zum Anlegen einer neuen Ressource auswählen. Wählen Sie den Menüpunkt **Web + Mobile**, um die in dieser Ressourcen Kategorie enthaltenen Optionen anzuzeigen.

	![Displaying every resource type](Images/displaying-resource-types.png?raw=true)

	_Anzeige aller Ressourcentypen_

	Auf dem nächsten Panel werden Ihnen alle verfügbaren Optionen für Web, Mobile Apps und andere Azure App Service Apps angezeigt. Wählen Sie den Menüpunkt **Azure Marketplace**. Dort finden sie Vorlagen für Apps, die Sie direkt verwenden können.

	![Azure Marketplace](Images/web-mobile-apps-options.png?raw=true)

	_Azure Marketplace_

5. Scrollen Sie soweit nach unten, bis Sie die Option **Web App + SQL** sehen. Wählen Sie diese Option aus.

	![Selecting Web App](Images/selecting-website-sql.png?raw=true)

	_Auswahl Web App + SQL_

	Wählen Sie die Schaltfläche **Create**.

	![Creating Web app](Images/create-web-app-sql.png?raw=true)

	_Erstellung einer Web App + SQL Database_

	Ein weiteres _Blade_ öffnet sich. Über Blades können Sie Informationen zu bestehenden Ressourcen einsehen, Konfigurationen vornehmen und Aktionen anstoßen. Dieses spezielle _Blade_ ermöglicht die Eingabe der zentralen Konfigurationsparameter der anzulegenden **Web App**.

	> **Hinweis:** Für weitere Informationen zu _Blades_ können Sie auf dem **Startboard** die Kachel **Tour** klicken. Dies öffnet eine Dokumentationsseite des Preview Portals über die Informationen zu verschiedenen Aspekten des Portals wie Blades, Commands, Lenses etc. abrufbar sind.

	> ![Tour](Images/tour.png?raw=true)

6. Wenn Sie eine Anwendung anlegen, die aus mehreren Ressourcen besteht (wie hier eine Web App und eine SQL Database), wird für diese Anwendung immer innerhalb einer Ressourcengruppe angelegt, so dass alle beteiligten Ressourcen gemeinsam verwaltet werden können. Wählen Sie einen Namen für die Ressourcengruppe, z.B. _MyResourceGroup_ , und wählen Sie den Optionsbereich **Web App**.

	> **Hinweis:** Namen von Ressourcengruppen müssen innerhalb einer Subscription eindeutig sein. Sie können nur Buchstaben, Ziffern, Punkte, Unter- und Bindestriche erlaubt.

	![New Web App](Images/new-resource-group.png?raw=true)

	_Neue Ressourcengruppe_

7. Ein weiteres Blade öffnet sich. In diesem können Sie einige Einstellungen für die neue **Web app** vornehmen. Wählen Sie eine URL für Ihre Web App. Beachten Sie, dass dieser Name global eindeutig sein muss. Wählen Sie auch einen Namen für einen neu anzulegenden App Service Plan aus bzw. wählen Sie einen bestehenden Sevice Plan.

	![Creating the App Service Plan](Images/changing-the-web-hosting-plan.png?raw=true)

	_Erstellung eines App Service Plans_

8. Sofern Sie die Leistungsstufe (und damit die Preisstufe) ändern wollen, wählen Sie den Menüpunkt **Pricing Tier**. Im Blade _Choose your pricing tier_ können Sie die für Sie geeignete Leistungsstufe wählen.

	App Service Pläne stellen einen Container für mehrere App Service Apps dar und stellen für diese gemeinsame Funktionen und Kapazitäten bereit. App Service Pläne unterstützen mehrere Leistungsstufen (z.B. Free, Shared, Basic, Standard und Premium), jede mit ihren eigenen Leistungen. Es gibt einige wichtige unterschiede zwischen dieses Stufen. Pläne in der Stufe Free und Shared führen ihre Apps in einer Multi-Mandanten-Infrastrukutur aus, d.h. Ihre Apps teilen sich dort die Infrastruktur mit Apps anderer Kunden. App Service Pläne in den Stufen Basic, Standard und Premium bieten für ihre Apps eine dedizierte Infrastruktur, d.h. alle Apps in diesen Plänen laufen in dieser Infrastruktur. Darüber hinaus können in dieses Stufen eine oder mehrere Instanzen virtueller Maschinen konfiguriert werden. Für diese Übung belassen Sie einfach die Voreinstellung und schließen Sie das Blade.

	> **Hinweis:** Für alle Leistungsstufen (mit Ausnahme von 'Shared') fallen Kosten in Abhängigkeit von der Größe des App Service Plans an. Für die einzelnen Apps innerhalb des Service Plans fallen keine weiteren Kosten an. Shared App Service Pläne sind anders: aufgrund der Tatsache, dass die Apps in einer Multi-Mandanten-Infrastruktur ausgeführt werden, werden die Kosten in Abhängigkeit von der Zahl einzelner Apps bestimmt.

	![_Auswahl einer Leistungsstufe_](Images/selecting-a-web-hosting-plan.png?raw=true)

	_Auswahl einer Leistungsstufe_

9. Wählen Sie die Schaltfläche **OK**, um auf das **Web app** Blade zurückzukehren. Sie können zuvor noch den Standort des App Service Plans ändern, wenn Sie wünschen. Wählen Sie die Schaltfläche **OK**, um zum letzten Blade zurückzukehren.

10. Wählen Sie **Database**, um die Einstellungen der neuen Datenbank zu ändern.

	>**Hinweis:** Wenn bereits Datenbanken eingerichtet wurden, wird das **Database** Blade angezeigt. Wählen Sie dann den Menüpunkt **Create a new database**.

	![Changing your database settings](Images/changing-your-database-settings.png?raw=true)

	_Änderungen der Einstellungen für die Datenbank_

11. Wählen Sie einen Namen für die Datenbank, z.B _mywebsite-db_ , und wählen Sie die Schaltfläche **Server**.

	> **Hinweis:** Auch hier können Sie die Leistungsstufe (**Pricing Tier**) wählen.

	![Database Settings](Images/database-settings.png?raw=true)

	_Database Settings_

12. Geben Sie Werte für **Server Name**, **Server Admin Login** und **Passwort** ein. Bestätigen Sie mit **OK**, um zum **New Database** Blade zurückzukehren und wählen Sie **OK**, um dieses zu schließen.

	![Konfiguration des Datenbank Servers](Images/configuring-the-database-server.png?raw=true)

	_Konfiguration des Datenbank Servers_

13. Damit sind alle Voraussetzungen zum Anlegen der Ressourcengruppe erfüllt. Wählen Sie die Schaltfläche **Create**.

14. Sie können sich den Status des Deployments über das **Notifications** Tool ansehen. Am oberen Bildschirmrand klicken Sie hierzu auf das Notifications Symbol.

	![Notifications](Images/notifications.png?raw=true)

	_Notifications_

15. Sobald das Deployment abgeschlossen ist, können Sie auf die Notification klicken, um die Ressourcengruppe anzuzeigen.

	![Notification zur Erstellung der Ressourcengruppe](Images/created-resource-group-notification.png?raw=true)

	_Notification zur Erstellung der Ressourcengruppe_

16. Sie haben nun eine neue Ressourcengruppe angelegt. Diese enthält einen App Service Plan die Web App, einen SQL Database Server, eine SQL Database und eine Application Insights Ressource.

	![Das Blade für die neue Ressourcengruppe](Images/new-resource-group-blade.png?raw=true)

	_Das Blade für die neue Ressourcengruppe_

	> **Hinweis:** Beachten Sie, dass auf dem Startboard eine Kachel für die neue Ressourcengruppe angelegt wurde.
	![Resource Group added to Startboard](Images/resource-group-added-to-startboard.png?raw=true)

	>**Hinwes 2:** Es hat sich bewährt, nicht mehr benötigte Ressourcen wieder zu Löschen. Um die gerade angelegte Demo Ressourcen wieder zu löschen, gehen Sie wie folgt vor:
	>
	>1. Im Blade der Ressourcengruppe, wählen Sie die Schaltfläche **Delete** am oberen Seitenrand.
	>
	>![Auswahl der Schaltfläche Delete](Images/clicking-delete-resource-group.png?raw=true)
	>
	>_Auswahl der Schaltfläche Delete_
	>
	>2. Ein Blade zur Bestätigung öffnet sich. Tippen Sie dort nochmals den Namen der Ressourcengruppe und wählen Sie die Schaltfläche **Delete**.
	>
	>![Bestätigung der Löschung](Images/deleting-resource-group-confirmation.png?raw=true)
	>
	>_Bestätigung der Löschung_
	>
	>Nach einem kurzen Moment sollte eine entsprechende Lösch-Benachrichtigung angezeigt werden.
	>
	>![Benachrichtigung der Löschung](Images/notification-after-resource-group-was-deleted.png?raw=true)
	>
	>3. Wählen Sie die Schaltfläche **Home**, um zum StartBoard zurückzukehren. Sofern dies nicht automatisch geschehen ist, finden Sie dort noch immer die Kachel, die zur Ressourcengruppe gehört. Klicken Sie dort mit der rechten Maustaste und wählen Sie im Kontextmenü den Punkt **Unpin from Startboard**.
	>
	>![Lösen der Ressourcengruppe vom Startboard](Images/unpin-resource-group-from-startboard.png?raw=true)
	>
	>_Lösen der Ressourcengruppe vom Startboard_
	>Damit ist auch die Kachel gelöscht.


<a name="Summary"></a>
## Zusammenfassung ##

Das neue Azure Preview Portal führt Funktionen für Entwickler und IT Pros in einer gemeinsamen Oberfläche zusammen. Sehr einfach lassen sich Services, die zu einer Cloud-basierten App gehören, in Form einer Ressourcengruppe gemeinsam anlegen und administrieren.

In dieser Übung haben Sie über diese Möglichkeit eine Web App mit zugehöriger SQL Database (inkl. SQL Database Server) angelegt, konfiguriert und wieder gelöscht.
