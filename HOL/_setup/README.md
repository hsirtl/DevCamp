Hinweise zum Einrichten der Entwicklungsumgebung für die Labs
=============================================================
Dieses Dokument enthält alle Informationen zum Einrichten aller benötigten Tools und Komponenten, die für den Workshop benötigt werden. Nach Durcharbeiten dieser Dokumentation haben Sie eine Umgebung, mit der Sie die einzelnen Hands-on-Labs des Workshops durchführen können.

Einrichten Ihres Computers
--------------------------

### Installation der Visual Studio 2015 Community Edition
Zur Durchführung der Labs benötigen Sie Visual Studio 2015 (z.B. in der Community Edition). Das Tool kann [hier](https://go.microsoft.com/fwlink/?LinkId=532606&clcid=0x409) heruntergeladen werden.

Alternativ können Sie Visual Studio 2013 verwenden, sofern Sie folgende Elemente installiert haben:

* Visual Studio 2013 Update 3 (oder höher) ([Download](http://www.visualstudio.com/en-us/downloads/download-visual-studio-vs)).

* Azure SDK for Visual Studio 2013 ([Download](http://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409)).

	> **Hinweis 1:** Abhängig davon, wie viele der vom SDK benötigten Komponenten bereits auf Ihrer Maschine installiert sind, kann die Installation des SDKs längere Zeit in Anspruch nehmen, von wenigen Minuten bis zu einer halben Stunde oder länger.

    > **Hinweis 2:** Wenngleich nicht für die vollständige Bearbeitung der Labs benötigt, verbessert die [Web Essentials](http://vswebessentials.com/download) Extension für Visual Studio die Möglichkeiten zum Editieren von HTML und JavaScript, indem sie Features wie Angular Attribute Detection und verbesserte JavaScript IntelliSense Unterstützung hinzufügt.

### Installation des Azure SDK für .Net ###
Das Microsoft Azure SDK für .Net kann mit Hilfe des [Microsoft Web Platform Installers](http://www.microsoft.com/web/downloads/platform.aspx) installiert werden. Hierfür benötigen Sie Version 2.3 oder höher.

Für die Installation führen Sie bitte folgende Schritte durch:

1. Öffnen Sie den Web Platform Installer.
1. Finden Sie die Zeile für das zu Ihrer Visual Studio Version passende **Microsoft Azure SDK for .Net**. Wählen Sie dort die zugehörige Schaltfläche **Add**. 
1. Wählen Sie die Schaltfläche **Install** zur Installation.

![Installation des Microsoft Azure SDK für .Net](images/install-microsoft-azure-sdk-for-net.png?raw=true)

_Installation des Microsoft Azure SDK für .Net entsprechend Ihrer Version von Visual Studio_

### Installation der Windows PowerShell ###
Windows 8, 8.1 und 10 werden bereits mit PowerShell 3.0 vorinstalliert. Dies ist möglicherweise in anderen (älteren) Windows Versionen nicht der Fall. Sie können prüfen, ob PowerShell auf Ihrem System installiert ist und für die Anforderungen der Labs geeignet ist, indem Sie folgende Schritte durchführen:

1. Rufen Sie den **Start** Bildschirm (Windows 8.x) bzw. das **Start-Menü** (Windows 10) auf und tippen Sie die Zeichenfolge **power**.

	Dieses listet alle Apps auf, die der Zeichenfolge entsprechen. Dies umfasst auch die **Windows PowerShell**. Sofern Windows PowerShell in den Suchergebnissen fehlt, können Sie die nächsten Schritte überspringen und über den unten angegebenen Link installieren.

1. Um die PowerShell Konsole zu öffnen, wählen Sie **Windows PowerShell**.

1. Führen Sie folgendes Kommando aus :

	```PowerShell
	$PSVersionTable.PSVersion
	```

	Dieses Kommando sollte die Versionsnummer 3.0 oder höher anzeigen. 

	![Überprüfung der Windows PowerShell Version](images/verifying-powershell-version.png?raw=true)

	_Überprüfung der Windows PowerShell Version_

Sofern die **Windows PowerShell** auf Ihrem System nicht installiert ist oder Sie eine ältere Version im Einsatz haben, laden und installieren Sie bitte eine neuere Version von der [Windows PowerShell Scripting](https://technet.microsoft.com/en-us/scriptcenter/dd742419.aspx) Seite.

### Installation der Microsoft Azure PowerShell Cmdlets

Die **Azure PowerShell** Module und deren benötigte Komponenten sind über den [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx) verfügbar. Zur Installation führen Si ebitte folgende Schritte durch:

1. Öffnen Sie den Microsoft Web Platform Installer.
1. Finden Sie die Zeile für die **Microsoft Azure PowerShell** und wählen Sie die Schaltfläche **Add**. 
1. Wählen Sie die Schaltfläce **Install**.

![Installation der Microsoft Azure Powershell im Microsoft Web Platform Installer](images/install-ms-azure-powershell.png?raw=true)

_Installation der Microsoft Azure PowerShell_

### Klonen oder Herunterladen des Inhalts dieses GitHub Repositorys (optional aber empfohlen)

Die bereitgestellten Labs enthalten eine Kombination aus Text-Dokumentation und Beispielcode. Um die komplette Dokumentation und alle benötigten Beispiel-Dateien lokal auf dem eigenen Computer zu haben, empfiehlt es sich, den Inhalt des Repositorys entweder (mit Hilfe von [Git](http://git-scm.com/)) zu klonen oder den kompletten Inhalt auf den lokalen Computer [herunterzuladen](https://github.com/Azure-Readiness/HOL-Intro-to-Azure/archive/master.zip). Sofern Sie das ZIP-Archiv herunterladen, kann es erforderlich sein, die Datei vor dem Entpacken zu [entsperren](http://blogs.msdn.com/b/delay/p/unblockingdownloadedfile.aspx).

Zusammenfassung
---------------

Sie haben folgende Werkzeuge auf Ihrem Computer installiert:

* Visual Studio 2015 oder Visual Studio 2013 mit Update 3 (oder höher)
* Azure SDK für .NET (für Visual Studio 2015 oder Visual Studio 2013)
* Windows Powershell Version 3.0 oder höher
* Microsoft Azure PowerShell Cmdlets
