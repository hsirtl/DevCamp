Infrastructure as a Service in Microsoft Azure
=======================================================================================

Die Möglichkeit eine virtuelle Maschine (VM) auf Abruf zu erstellen, gleichgültig ob von einem Standardimage oder einem Image Ihrer Wahl, kann sehr nützlich sein. 
Dieser Ansatz, allgemein bekannt als Infrastructure as a Service, wird von Azure Virtual Machines bereitgestellt. 

Um eine VM zu erstellen, müssen Sie eine VHD und die Größe der VM auswählen. Sie zahlen nur für die Zeit in der die VM eingeschaltet ist pro Minute, allerdings existiert eine minimale Speichergebühr um die VHD verfügbar zu halten.
Azure bietet eine Auswahl an geführten VHDs (Images), die ein bootfähiges Betriebssystem beeinhalten. Hierbei gibt es sowohl Microsoft als auch Partneroptionen, wie z.B. Windows Server, Linux, SQL Server, Oracle und viele mehr.
Sie können auch Ihre eigenen VHDs erstellen und diese anschließend hochladen. Außerdem können Sie sogar VHDs hochladen, die nur Daten beeinhalten um von Ihren VMs darauf zuzugreifen. 

Dieser generelle cloud-computing Ansatz kann für die Adressierung von zahlreichen Themen verwendet werden:
  
* **Dev/Test** - Sie können diese zur günstigen Entwicklung und als Testplattform einsetzen, die Sie nach Fertigstellung einfach herunterfahren können. 
Außerdem können Sie Applikationen erstellen und ausführen, unabhängig von Ihren präferierten Sprachen und Bibliotheken. Diese Applikationen können jede der von Azure angebotenen Datenmanagement Optionen verwenden, und Sie können auch einen SQL-Server oder ein anderes DBMS auf einer oder auf mehreren VM's ausführen.
* **Umzug von Applikationen auf Azure (Lift-and-shift)** - "Lift-and-shift" bezieht sich auf den Umzug Ihrer Applikation ähnlich zum Benutzen eines Gabelstaplers um ein großes Objekt zu bewegen. Sie heben ("lift") die VHD von Ihrem lokalen Datencenter, schieben ("shift") es zu Azure und führen es dort aus. Sie werden vermutlich ein wenig Arbeit mit dem Entfernen von Abhängigkeiten auf anderen Systemen haben. Falls es zu viele sind, können Sie Option 3 in Erwägung ziehen. 
* **Erweitern Ihres Datencenters** - Verwenden Sie Azure VMs als eine Erweiterung Ihres on-premises Datencenters, indem Sie SharePoint oder andere Applikationen ausführen. Um dies zu unterstützen ist es möglich Windows Domains in der Cloud zu erstellen, indem Active Directory in der Cloud aufgesetzt wird. Sie können Azure Virtual Networks verwenden, um Ihr lokales mit den Azure Netzwerken zu verbinden. 

In diesem Lab werden Sie lernen, wie man virtuelle Maschinen mit unterschiedlichen Optionen in Azure erstellt. Außerdem werden Sie Festplatten hinzufügen, auf diese zugreifen und VM Erweiterungen installieren. 

Dieses Lab enthält folgende Aufgabenstellungen:

* [**Erstellen einer Virtual Machine mit dem Azure-Vorschauportal**](#creating-a-vm-using-portal)

	In dieser Aufgabenstellung werden Sie eine Windows VM mit einem existierendem Image mit dem Azure-Vorschauportal erstellen.

* [**Erstellen einer Virtual Machine mit dem Cross-Platform Command-Line Interface**](#creating-a-vm-using-cli) 

	In dieser Aufgabenstellung werden Sie die Kommandozeilen cross-platform Tools verwenden um: [die Subscription in der Kommandozeile mit Hilfe einer publishsettings Datei zu konfigurieren](#connect-to-your-azure-subscription-xplatcli), [eine Linux VM mit einem existierendem Image zu erstellen](#create-vm-xplatcli), [eine leere Festplatte hinzuzufügen](#attach-disk-xplatcli), [eine Verbindung zur virtuellen Maschine mit PuTTY herzustellen](#connect-to-vm-xplatcli) und [die verbundene Festplatte zu konfigurieren](#configure-datadisk-xplatcli).

* [**Erstellen einer Virtual Machine mit PowerShell**](#creating-a-vm-using-powershell):

	In dieser Aufgabenstellung werden Sie PowerShell verwenden um: [die Azure Subscription mit Azure AD zu konfigurieren](#configure-subscription-powershell), [erstellen einer Windows VM](#create-vm-powershell), [Hinzufügen einer leeren Festplatte zur VM](#attach-disk-powershell), [Installieren einer VM Extension](#install-vm-extension-powershell), und [verbinden der VM durch eine generierte rdp Datei](#connect-to-vm-powershell) um [die verbundene Festplatte in der VM zu konfigurieren](#configure-datadisk-powershell).

* [**Erstellen einer Virtual Machine mit einem Runbook**](#creating-a-vm-using-Runbook)

	In dieser Aufgabenstellung werden Sie [sicherstellen, dass die nötigen Voraussetzungen existieren](#runbook-setup) wie [Erstellen eines Geschäftskontos (organizational account)](#creating-new-organizational-account), [Erstellen eines Automation Accounts](#create-automation-account), [Erstellen eines leeren Runbook](#create-empty-runbook), [editieren des Runbookst um eine VM zu erstellen und veröffentlichen](#edit-runbook), [Erstellen der nötigen Assets für die Ausführung des Runbooks](#create-assets), [Starten des Runbooks](#start-runbook) und nach der Erstellung [verifizieren Sie, dass die VM im Portal erstellt worden ist](#verify-vm-runbook).

* [Appendix - Cleanup](#cleanup)

Dieses Lab zeigt Ihnen, dass man ähnliche Aktionen mit unterschiedlichen Tools ausführen kann, sodass Sie den Task auswählen können, den Sie gehen möchten. Es wird empfohlen, dass Sie [Erstellen einer Virtual Machine mit dem Cross-Platform Command-Line Interface](#creating-a-vm-using-cli) und [Erstellen einer Virtual Machine mit PowerShell](#creating-a-vm-using-powershell), da diese eine hohe Abdeckung an Tasks auf virtuellen Maschinen abdecken.

<a name="creating-a-vm-using-portal"></a>
##Erstellen einer Virtual Machine mit dem Azure-Vorschauportal ##

In dieser Aufgabenstellung werden Sie eine Windows VM mit dem Azure-Vorschauportal erstellen.

1. Melden Sie sich an im [Azure-Vorschauportal](https://portal.azure.com/).

1. Klicken Sie auf **Neu**, dann auf **Compute** und anschließend auf **Windows Server 2012 R2 Datacenter**.

	![Creating VM - Click New and Everything](images/creating-vm---click-new-and-everything.png?raw=true)

	_Erstellen eines Windows Server 2012 R2 Datacenters_ 

1. In der **Windows Server 2012 R2 Datacenter** Spalte, die sich öffnet, klicken Sie **Erstellen**

	![Creating VM Confirm image](images/creating-vm-confirm-image.png?raw=true)

	_Erstellen eines Windows Server 2012 R2 Datacenters_ 

1. In der **Virtuellen Computer erstellen** Spalte, geben Sie folgende Informationen ein: 

	* **Host Name**: Name der VM (z.B. azureVM)
	* **User Name**: Administrator der VM (z.B. adminUser)
	* **Password**: Eindeutiges Passwort für den Administrator

	![Creating a VM - Enter VM Name, User Name and Password](images/creating-vm-enter-vm-name-user-name-and-passw.png?raw=true)

	_Erstellen einer VM - geben Sie Host Name, User Name und Password ein_

1. Klicken Sie auf **Erstellen**.

1. Die VM wird erstellt. Sie können den Fortschritt über den **Notifications** Button oder auf dem Dashboard überwachen.  

	![Creating a VM - Monitor progress on the Notifications Hub](images/creating-vm-monitor-progress-on-the-notifi.png?raw=true)

	_Erstellen einer VM - Überwachen des Fortschritts_

	>![Creating a VM - A pin in the startboard exists after creation](images/creating-vm-pin-in-startboard-after-creation.png?raw=true)
	>
	>_Erstellen einer VM - Eine Kachel wurde auf dem Dashboard angelegt_

	>Nach dem Erstellen der Virtuellen Maschine können Sie neue oder bereits vorhandene Festplatten zu der VM hinzufügen. Für mehr Informationen, lesen Sie: [Informationen zu virtuellen Computerdatenträgern in Azure](https://msdn.microsoft.com/library/azure/dn790303.aspx). 

<a name="creating-a-vm-using-cli"></a>
## Erstellen einer Virtual Machine mit dem Cross-Platform Command-Line Interface

In dieser Aufgabenstellung werden Sie **Azure Cross-Platform Command-Line Interface** (xplat-cli) verwenden um eine Linux VM zu erstellen und dieser eine leere Festplatte zuweisen. Anschließend werden Sie sich zur VM verbinden und die Festplatte konfigurieren. 

<a name="connect-to-your-azure-subscription-xplatcli"></a>
Sie beginnen mit der Konfiguration Ihrer Azure Subscription in dem xplat-cli.

Obwohl einige Kommandos, die von xplat-cli bereitgestellt werden auch ohne Azure Subscription funktionieren, benötigen viele Kommandos eine Subscription. 
Um xplat-cli mit Ihrer Subscription zu konfigurieren, können Sie entweder eine publish settings Datei herunterladen und benutzen, oder sich in Azure mit einem Firmenkonto anmelden. Wenn Sie sich anmelden wird Azure Active Directory zur Authentifizierung Ihrer Nutzerdaten verwendet. 

Um Ihnen bei der Auswahl der Authentifizierungsmethode zu helfen, bedenken Sie das Folgende: 

*  Die Login Methode kann den Umgang mit Subscriptions einfacher machen, aber kann die Automatisierung durch time-outs Ihrer Nutzerdaten unterbrechen und Sie auffordern sich erneut anzumelden.

*  Die publish settings Datei installiert ein Zertifikat, das Ihnen die Durchführung von Managementaufgaben so lange erlaubt wie Subscription und Zertifikat valide sind. Diese Methode macht es einfacher Automatisierungsprozesse für lang andauernde Aufgaben anzuwenden. Nach dem Herunterladen und dem Import der Informationen, müssen Sie es nicht erneut bereitstellen. Dennoch wird das Verwalten der Zugänge zu Subscriptions erschwert, da jeder mit Zugriff auf das Zertifikat auf die Subscription zugreifen kann. 

Für mehr Informationen zur Authentifizierung und dem Management von Subscriptions, lesen Sie ["Was ist der Unterschied zwischen kontobasierter Authentifizierung und zertifikatbasierter Authentifizierung, und kann ich die zertifikatbasierte Authentifizierung weiterhin nutzen?"](http://msdn.microsoft.com/de/library/windowsazure/hh531793.aspx#BKMK_AccountVCert).

Um die Methode mit der publish settings Datei zu verwenden, befolgen Sie folgende Schritte:

1. Öffnen Sie eine **Kommandozeile** und führen Sie das folgende Kommando zum Herunterladen der publish settings Datei aus:

	```
	azure account download
	```

	Dieser Befehl leitet Sie zu Ihrem Standardbrowser und wird Sie auffordern sich im Azure Management Portal anzumelden. Danach wird eine `.publishsettings` Datei heruntergeladen. Merken Sie sich bitte, wo die Datei gespeichert wurde. 
    
    Falls Sie Azure xplat-cli noch nicht installiert haben, folgen Sie den Instruktionen unter ["Install the Azure CLI"](https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-install/)

1. Importieren Sie die `.publishsettings` Datei, indem Sie folgendes Kommando ausführen und `[Pfad zur .publishsettings Datei]` durch Ihren Pfad zu der `.publishsettings` Datei ersetzen :

	```
	azure account import [path to .publishsettings file]
	```

	> **Note:** Wenn Sie die publish settings importieren werden die Zugangsinformationen zur Azure Subscription in einem `.azure` Verzeichnis in Ihrem `user` Verzeichnis gespeichert. Ihr `user` Verzeichnis wird durch Ihr Betriebssystem geschützt; dennoch wird es empfohlen zusätzliche Schritte zum Verschlüsseln Ihres `user` Verzeichnises durchzuführen. Sie können auf folgende Arten erreichen:

	>
	> * Auf Windows können Sie die Verzeichniseinstellungen modifizieren oder Bitlocker verwenden.
	> * Auf Mac können Sie FileVault für Ihr Verzeichnis aktivieren.
	> * Auf Ubuntu können Sie die verschlüsselte Home Verzeichnis Funktionalität aktivieren. Andere Linux Distributionen bieten ähnliche Funktionalitäten an. 

1. Nachdem Sie die publish settings importiert haben, sollten Sie die `.publishsettings` Datei löschen, da es ein Sicherheitsrisiko darstellt, da man durch die Datei Zugriff auf Ihre Subscription erhalten kann.

	> **Note:** Falls Sie die Login Methode präferieren, führen Sie folgendes Kommando aus:
	>
	> ```
	> azure login -u username -p password
	> ```
	> 

	<a name="create-vm-xplatcli"></a>

	Sie haben Ihre Azure Subscription mit der Kommandozeile konfiguriert und werden nun eine VM erstellen.

1. Führen Sie in der **Kommandozeile** folgendes Kommando aus um alle verfügbaren Region aufzulisten, von denen Sie eine VM erstellen können. Merken Sie sich eine (z.B.: _West Europe_); Sie werden es im nächsten Schritt benötigen.


	```
	azure vm location list
	```

1. Um eine neue VM basierend auf dem  _b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04-LTS-amd64-server-20140724-en-us-30GB_ Image zu erstellen, 
führen Sie folgendes Kommando aus. Ersetzen Sie _[LINUX-VM-NAME]_ und _[ADMIN-USERNAME]_ mit Ihrem Namen der VM und Ihrem Administrator Benutzernamen.
Sie können auch  _West US_ durch die Lokation Ihrer Wahl im vorherigen Schritt ersetzen.  


	```
	azure vm create [LINUX-VM-NAME] b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04-LTS-amd64-server-20140724-en-us-30GB [ADMIN-USERNAME] --location "West US" --ssh

	```
	> **Note 1:** Der _--ssh_ Parameter erlaubt Ihre aufgesetzte Linux VM mit SSH zu verwalten.

	> **Note 2:** Um alle verfügbaren Images aufzulisten, verwenden Sie folgendes Kommando: azure vm image list

	> **Note 3:** Sie können die blob storage URL durch Angabe des _--blob-url_ Parameters im _vm create_ Kommando. 
    Um einen Storage Account zu erstellen, befolgen Sie die Schritte:

	> 1. Ersetzen Sie den _[ACCOUNT-NAME]_ Platzhalter und führen das folgende Kommande zur Erstellung eines neuen Storage Accounts aus. 
    >    Sie werden aufgefordert die Lokation auszuwählen, in der Sie den Storage Account erstellen wollen. Versichern Sie sich, 
    >    dass Sie diesselbe Lokation wie zur Erstellung der VM verwenden.
    >
	>    ```
	> 	azure storage account create [ACCOUNT-NAME]
	> 	```
    >   Sie werden nach dem Account Typ gefragt werden. 
    >   Zur Auswahl stehen: LRS (Locally Redundant), ZRS (Zone Redundant), GRS (Geo Redundant), RAGRS (Read Access Geo Redundant).
	> 
    > 2. Ersetzen Sie _[ACCOUNT-NAME]_ durch Ihren im vorherigen Schritt verwendeten:
    >   ```
    >   azure storage account keys list [ACCOUNT-NAME]
    > 	```

	> 3. Nun erstellen Sie einen neuen Container im blob Storage Account, indem Sie folgendes Kommando ausführen:
    >
    > azure storage container create [CONTAINER-NAME] --account-name [ACCOUNT-NAME] --account-key [STORAGE-ACCOUNT-KEY]
    > 
    > 4. Abschließend führen Sie das `azure vm create` Kommando mit dem _--blob-url_ Parameter aus (`https://<accountname>.blob.core.windows.net/<containerName>/<the-blob-name.vhd>`).
	>   
    >  azure vm create [LINUX-VM-NAME] b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04-LTS-amd64-server-20140724-en-us-30GB [ADMIN-USERNAME] --location "West US" --ssh --blob-url https://[ACCOUNT-NAME].blob.core.windows.net/<containerName>/<the-blob-name.vhd>

	Wenn die virtuelle Maschine erstellt wurde, können Sie dieser eine leere Festplatte zuweisen.

	<a name="attach-disk-xplatcli"></a>
1. Um eine 30GB Festplatte zu Ihrer VM hinzuzufügen, führen Sie folgendes Kommando aus. Ersetzen Sie _your-linux-vm_ mit dem Namen Ihrer VM.
 

	```
	azure vm disk attach-new [LINUX-VM-NAME] 30
	```

	Sie sollten folgende Nachricht erhalten:

	```
	info:    Executing command vm disk attach-new
	+Getting virtual machines
	+Adding Data-Disk
	info:    vm disk attach-new command OK
	```

1. Um Details über die virtuelle Maschine anzuzeigen, führen Sie folgendes Kommando aus. Ersetzen Sie _[LINUX-VM-NAME]_ mit dem Namen Ihrer VM. Merken Sie sich _DNSName_ und versichern Sie sich, dass der SSH Endpunkt existiert. 

	```
	azure vm show [LINUX-VM-NAME]
	```

	Sie sollten folgende Nachricht erhalten:

	```
	info:    Executing command vm show
	+Getting virtual machines
	data:    DNSName "your-linux-vm.cloudapp.net"
	data:    Location "West US"
	data:    VMName "your-linux-vm"
	data:    IPAddress "100.78.86.88"
	data:    InstanceStatus "ReadyRole"
	data:    InstanceSize "Small"
	data:    Image "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_1-LTS-amd64-server-20141125-en-us-30GB"
	data:    OSDisk hostCaching "ReadWrite"
	data:    OSDisk name "your-linux-vm-your-linux-vm-0-201501202057370849"
	data:    OSDisk mediaLink "https://portalvhdsqmqsgyc6l4zl4.blob.core.windows.net/vhds/your-linux-vm-your-linux-vm-2015-01-20.vhd"
	data:    OSDisk sourceImageName "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_1-LTS-amd64-server-20141125-en-us-30GB"
	data:    OSDisk operatingSystem "Linux"
	data:    OSDisk iOType "Standard"
	data:    DataDisks 0 hostCaching "None"
	data:    DataDisks 0 label "your-linux-vm-your-linux-vm-your-linux-vm42-0"
	data:    DataDisks 0 name "your-linux-vm-your-linux-vm-0-201501202103240353"
	data:    DataDisks 0 logicalDiskSizeInGB 30
	data:    DataDisks 0 mediaLink "https://portalvhdsqmqsgyc6l4zl4.blob.core.windows.net/vhds/your-linux-vm-f539b3ed4be4e5ab.vhd"
	data:    DataDisks 0 iOType "Standard"
	data:    ReservedIPName ""
	data:    VirtualIPAddresses 0 address "104.42.11.83"
	data:    VirtualIPAddresses 0 name "your-linux-vmContractContract"
	data:    VirtualIPAddresses 0 isDnsProgrammed true
	data:    Network Endpoints 0 localPort 22
	data:    Network Endpoints 0 name "SSH"
	data:    Network Endpoints 0 port 22
	data:    Network Endpoints 0 protocol "tcp"
	data:    Network Endpoints 0 virtualIPAddress "104.42.11.83"
	data:    Network Endpoints 0 enableDirectServerReturn false
	info:    vm show command OK
	```

	<a name="connect-to-vm-xplatcli"></a>
	Um die Einstellungen und die Applikationen auf der VM zu verwalten, können Sie einen SSH client verwenden. Hier werden Sie PuTTY verwenden, um Zugriff auf die VM zu erhalten.

	> **Note:** Hierzu müssen Sie den SSH client auf Ihrem Computer installieren. Sie können zwischen verschiedenen SSH clients wählen: 
	> 
	> - Falls Sie einen Windows Computer verwenden, können Sie einen SSH client wie PuTTY verwenden: [PuTTY Download](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).
	> - Falls Sie einen Linux Computer verwenden, können Sie einen SSH client wie OpenSSH verwenden: [OpenSSH](http://www.openssh.org/).

1. Öffnen Sie PuTTY.

	> **Note:** Falls Sie einen Konsolen SSH client verwenden, tippen Sie: `ssh`

1. Geben Sie **DNSName**, den Sie von der Ausführung des `azure vm show` Kommandos erhalten haben, in das **Host Name** Feld ein und klicken auf **Open**.

	![Opening the connection to the virtual machine in PuTTY](images/openning-the-connection-to-the-vm.png?raw=true)

	_Öffnen der Verbindung zur VM in PuTTY_

1. Klicken Sie **Yes** in der _PuTTY Security Alert_ Dialogbox um den Serverkey zum Cache hinzuzufügen.

	![Clicking yes to save the key in the cache](images/clicking-yes-to-save-the-key.png?raw=true)


1. Loggen Sie sich in der VM ein, indem Sie Administrator Usernamen verwenden den Sie bei der Erstellung der VM gewählt haben (z.B.: _yourVMUsername_).

	![Log on to the virtual machine](images/log-on-to-the-vm.png?raw=true)

	_Einloggen in die VM_

	Sie können nun mit der Maschine arbeiten, wie Sie es mit jedem anderem Server tun würden. 

	<a name="configure-datadisk-xplatcli"></a>
	Ihre Applikation muss vielleicht Daten speichern. Um dies zu ermöglichen, haben Sie eine leere Festplatte hinzugefügt.

	Auf Linux ist die Resource Disk normalerweise von einem Azure Linux Agent verwaltet und wird automatisch bereitgestellt (mount) als **/mnt/resource** (oder **/mnt** für Ubuntu images). Die Festplatte kann auch nach dem Kernel bennant sein, wie z.B. `/dev/sdc`, und Benutzer müssen die Ressource partitionieren, formatieren und bereitstellen (mount). Sie werden nun lernen, wie Sie dies tun. Bitte lesen Sie für mehr Informationen den: [Azure Linux Agent User Guide](http://www.windowsazure.com/en-us/manage/linux/how-to-guides/linux-agent-guide/).

	> **Note:** Don’t store data on the resource disk. This disk provides temporary storage for applications and processes and is used to store unnecessary data such as swap files. Data disks reside in Azure Storage as .vhd files in page blobs and provide storage redundancy to protect your data. For more detail, see [About Disks and Images in Azure](http://msdn.microsoft.com/en-us/library/jj672979.aspx).

1. Im SSH Fenster, führen Sie folgendes Kommando aus:

	```
	sudo grep SCSI /var/log/syslog
	```

	Sie können die ID der leeren Festplatte, die zuletzt hinzugefügt wurde in den angezeigten Nachrichten in Klammern erkennen: (z.B. [sdc]).

1. Im SSH Fenster, führen Sie folgendes Kommando aus um ein neues Device zu erstellen:

	```
	sudo fdisk /dev/sdc
	```

	![Executing fdisk in the virtual machine](images/executing-fdisk-in-the-vm.png?raw=true)

	_Ausführen von fdisk in der VM_

	> **Note:** In diesem Beispiel müssen Sie evtl `sudo -i` auf manchen Distributionen verwenden, falls /sbin oder /usr/sbin nicht in Ihrem `$PATH` vorhanden sind.

1. Tippen Sie **n** um eine neue Partition zu erstellen.

1. Tippen Sie **p** um die Partition als primär zu markieren, Tippen Sie **1** um es als die erste Partition zu markieren, und tippen Enter um die default Werte zu akzeptieren.

6. Tippen Sie **p** um Details zur Festplatte zu sehen, die partitioniert wurde.

	![Displaying disk details](images/seeing-the-details-about-the-disk.png?raw=true)

	_Anzeigen von Festplattendetails_
	
7. Tippen Sie  **w** um Einstellungen für die Platte festzulegen.

8. Sie müssen das Dateisystem auf der neuen Partition erstellen. Als Beispiel, führen Sie folgendes Kommando aus to create the file system:

	```
	sudo mkfs -t ext4 /dev/sdc1
	```

	> **Note:** Machen Sie sich bewusst, dass SUSE Linux Enterprise 11 Systeme nur read-only Zugriff auf ext4 Dateisysteme bereitstellen.
                Für diese Systeme empfehlen wir das neue Dateisystem als ext3 zu formatieren.

9. Erstellen Sie einen Pfad um das neue Dateisystem bereitzustellen (mount). Führen Sie als Beispiel folgendes Kommando aus:

	```
	sudo mkdir /datadrive
	```

10. Führen Sie folgendes Kommando zum bereitstellen (mount) aus:

	```
	sudo mount /dev/sdc1 /datadrive
	```

	Die neue Festplatte ist nun bereit zur Verwendung als **/datadrive**.

11. Um sich zu vergewissern, dass die Festplatte nach einem Neustart erneut bereitgestellt (re-mounted) wird, muss Sie zu der /etc/fstab Datei hinzugefügt werden. Zusätzlich wird es stark empfohlen, dass die UUID (Universally Unique IDentifier) in /etc/fstab benutzt wird um auf das Laufwerk als nur auf seinen Namen (i.e. /dev/sdc1) zu verweisen. Um die UUID des neuen Laufwerks herauszufinden, können Sie die **blkid** Uility verwenden:

	```
	sudo -i blkid
	```

	Sie sollten folgende Nachricht erhalten:

	```
	/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
	/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
	/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
	```

	> **Achtung:** Unsachgemäßes editieren der /etc/fstab Datei, kann in einem unbootable System enden. 
    >             Es wird empfohlen eine Kopie der /etc/fstab Datei anzulegen. Bei Unsicherheiten können Sie einen Blick in die Dokumentation werfen.

1. Benutzen Sie einen Texteditor um die Informationen über das neue Dateisystem an das Ende der /etc/fstab Datei zu schreiben. In diesem Beispiel werden wir die UUID für das neue **/dev/sdc1** Gerät verwenden, das in den vorherigen Schritten erstellt wurde, und den mountpoint **/datadrive** verwenden.

	```
	UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2
	```

	> **Note 1:** Bei Systemen, die auf SUSE Linux basieren müssen Sie ein andere Format verwenden:
	> 
	> ```
	> /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /   ext3   defaults   1   2
	> ```

	> **Note 2:** Sie können den vim Texteditor verwenden um diese Schritte durchzuführen:

	> 1. Führen Sie folgendes Kommando aus um vim zu starten:
	>
	> ```
	> sudo vim /etc/fstab
	> ```
	> 1. Tippen Sie **i** um in den _INSERT_ Modus zu kommen und verwenden Sie die Pfeiltasten um zum Ende der Datei zu gelangen.
	> 1. Tippen Sie Enter und fügen Sie die Informatione hinzu. 
	> 1. Tippen Sie **Esc** um den _INSERT_ Modus zu verlassen.
	> 1. Tippen Sie **:wq** um in die Datei zu schreiben und vim zu beenden.

	> **Note 3:** Falls zusätzliche Dateisysteme oder Partitionen erstellt werden, müssen diese in /etc/fstab separat eingegeben werden.

1. Sie können die Bereitstellung des Dateisystems testen, indem Sie es einfach auswerfen und erneut bereitstellen: 
	```
	sudo umount /datadrive
	sudo mount /datadrive
	```

	Falls das zweite Kommando einen Fehler produziert, werfen Sie einen Blicn in die /etc/fstab Datei und versichern Sie sich, dass die Syntax korrekt ist. 

	> **Note:** Entfernen der Festplatte ohne fstab zu editieren, kann dazu führen, dass die VM nicht mehr hochfährt. 
                Die meisten Distributionen bieten `nofail` und/oder `nobootwait` fstab Optionen, die es einem System erlauben auch ohne vorhandene Festplatte
                hochzufahren. Verwenden Sie die Dokumentation Ihrere Distribution um mehr Informationen zu erhalten.


<a name="creating-a-vm-using-powershell"></a>
##Erstellen einer Virtual Machine mit PowerShell

In dieser Aufgabenstellung werden Sie eine Windows VM mit PowerShell cmdlets erstellen. 

In den folgenden Schritten werden Sie Ihre Azure Subscription in PowerShell konfigurieren, überprüfen ob Ihre Subscription mit einem Storage Account verbunden ist und ihn verbindet, falls er nicht vorhanden ist. Sie werden dann Einstellungen in der VM vornehmen.
    Sie werden lernen, wie man eine neue Festplatte zur VM hinzufügt und wie man eine VM Extension zur VM hinzufügt. Abschließend werden sie eine Remote Desktop Protokoll Datei erstellen um auf Ihre VM zuzugreifen und um die neue Festplatte zu initialisieren.

<a name="configure-subscription-powershell"></a>
Sie werden mit der Konfiguration Ihrer Azure subscription in Powershell beginnen.

Wie bei xplat-cli, benötigen viele cmdlets und eine Azure Subscription. Es gibt zwei Arten die Subscription Information an Windows PowerShell zu übermitteln: Sie können ein Management Zertifikat, das die Informationen erhält, verwenden oder Sie können sich in Azure mit Ihrem Microsoft Account oder einem Geschäftskonto anmelden. Wenn Sie sich einloggen authentifiziert Azure Active Directory die Nutzerdaten und gibt ein Zugriffstoken zurück, das PowerShell erlaubt Ihren Account zu verwalten.

Azure AD ist die empfohlene Authentifizierungsmethode, da es das Verwalten des Subscription Zugriffs erleichtert. Mit dem Update in Version 0.8.6, ist ein Automatisierungsszenario mit Azure AD Authentifizierung über ein Arbeits- oder Schulkonto möglich. Dies funktioniert auch mit der Azure Resource Manager API.

Für mehr Informationen über Authentifizierung und Subscription management, lesen Sie ["What's the difference between account-based authentication and certificate-based authentication"](http://msdn.microsoft.com/en-us/library/windowsazure/hh531793.aspx#BKMK_AccountVCert).

Folgen Sie den Instruktionen um sich mit Ihrem Azure AD Account anzumelden:

1. Öffnen Sie **Microsoft Azure PowerShell**.

1. Tippen Sie das folgende Kommando und drücken Enter:

	```PowerShell
	Add-AzureAccount
	```

1. Eine Dialogbox **Sign in to Windows Azure** erscheint. Folgen Sie den Instruktionen, geben Sie Email-Addresse und Passwort ein.

	Azure authentifiziert und speichert die Anmeldeinformation und schließt das Fenster. Danach werden Sie folgenden Output sehen können:

	![Running Add-AzureAccount](images/running-add-azureaccount.png?raw=true)

	_Ausführen des Add-AzureAccount Kommandos_

	>Ab Version 0.8.6 können Sie mit einem Geschäftskonto das pop-up Anmeldefenster umgehen:  
	>
	>```PowerShell
	>$cred = Get-Credential
	>Add-AzureAccount -Credential $cred
	>```
	>
	>Dies wird das Standard Windows PowerShell Anmeldefenster öffnen und Sie auffordern Ihre Nutzerdaten einzugeben.
	>
	>Falls Sie ein Automatisierungsskript verwenden und Popup Fenster unterbinden wollen, verwenden Sie Folgendes:
	>
	>```PowerShell
	>$userName = "<your work or school account user name>"
	>$securePassword = ConvertTo-SecureString -String "<your work or school account password>" -AsPlainText -Force
	>$cred = New-Object System.Management.Automation.PSCredential($userName, $securePassword)
	>Add-AzureAccount -Credential $cred 
	>```

	>**Note:** Die nicht-interaktive Login Methode funktioniert nur mit einem Geschäftskonto. Falls Sie kein Geschäftskonto besitzen, können Sie folgende Schritte durchführen um eines zu erstellen: [Erstellen eines Geschäftskontos](#creating-new-organizational-account).


1. Um zu verifizieren ob Ihre Subscription mit einem Storage Account verbunden ist, führen Sie folgendes Kommando aus:

	```PowerShell
	Get-AzureSubscription
	```

	Folgenden Output sollten Sie sehen:

	![Get-AzureSubscription Output ohne Storage Account](images/getazuresubscription-output-no-storage-accoun.png?raw=true)

	_Get-AzureSubscription Output wenn kein Storage Account gesetzt ist_

	Notieren Sie den **SubscriptionName** im Output (_Free Trial_ in this case). Sie werden in später zum ersetzen von: [SUBSCRIPTION-NAME] verwenden.

1. Führen Sie folgendes Kommando aus um Informationen zum Storage Account zu erhalten:

	```PowerShell
	Get-AzureStorageAccount
	```

	Folgenden Output sollten Sie sehen:
	
	![Get-AzureStorageAccount output](images/get-azurestorageaccount-output.png?raw=true)

	_Get-AzureStorageAccount output_

	Notieren Sie: **Label** und **Location** ies.  Sie werden in später zum ersetzen von: [STORAGE-ACCOUNT-LABEL] und [STORAGE-ACCOUNT-LOCATION] verwenden.

1. Falls das Kommando **Get-AzureSubscription** keinen Wert **CurrentStorageAccountName** angezeigt hat, führen Sie folgendes Kommando aus um diesen Wert zu setzen. Erstzen Sie [SUBSCRIPTION-NAME] und [STORAGE-ACCOUNT-LABEL] mit den Werten die Sie vorher erhalten haben:

	```PowerShell
	Set-AzureSubscription -SubscriptionName "[SUBSCRIPTION-NAME]" -CurrentStorageAccountName [STORAGE-ACCOUNT-LABEL]
	```

	Dieser Befehl setzt den Storage Account. Nun sollte der Wert nach Ausführen des **Get-AzureSubscription** Kommandos gelistet werden. 

	<a name="create-vm-powershell"></a>

1. Führen Sie folgenden Code aus, ersetzen Sie [ADMIN-USER-NAME] und [ADMIN-PASSWORD] durch Ihre präferierten Werte und benutzen Sie den Wert, den Sie vorher erhalten haben für: [STORAGE-ACCOUNT-LOCATION].

	```PowerShell
	$dclocation = '[STORAGE-ACCOUNT-LOCATION]'
	$adminUserName = '[ADMIN-USER-NAME]'
	$adminPassword = '[ADMIN-PASSWORD]'
	$vmname = 'azureVM'
	```

1. Wählen Sie einen eindeutigen Namen für Cloud Service. Ob der von Ihnen gewählte Name bereits existiert, können Sie mit dem **Test-AzureName** Kommando herausfinden - falls  es "false" zurückgibt, ist der Name verfügbar.

	```PowerShell
	Test-AzureName -Service '[CLOUD-SERVICE-NAME]'

	$cloudSvcName = '[CLOUD-SERVICE-NAME]'
	```

1. Setzen Sie den Namen des Images Ihrer VM auf: _a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201412.01-en.us-127GB.vhd_. Dies stimmt mit einem Image vom Windows Server R2 DataCenter überein.

	```PowerShell
	$image = 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201412.01-en.us-127GB.vhd'
	```

	>Note: führen Sie folgendes Kommando aus um die komplette Liste an verfügbaren Images anzuzeigen:
	>
	>```PowerShell
	>Get-AzureVMImage | select ImageName
	>```
	>Sie können die VM auch basierend auf einem anderen Image erstellen. 

1. Führen Sie folgendes Kommando aus um die VM zu erstellen:

	```PowerShell
	New-AzureQuickVM -AdminUserName $adminUserName -Windows -ServiceName $cloudSvcName -Name $vmname -ImageName $image -Password $adminPassword -Location $dclocation

	```

	>**Note:** führen Sie folgendes Kommando aus, falls Sie ein Linux Image erstellen wollen:

	>```PowerShell
	>New-AzureQuickVM -Linux -ServiceName $cloudSvcName -Name $vmname -ImageName $image -LinuxUser $adminUserName -Password $adminPassword -Location $dclocation
	>
	>```
	>
	>Die Unterschiede sind im **-Linux** OS switch und im **-LinuxUser** switch, der den **-AdminUserName** switch in Windows ersetzt.
	>
	>**Note 2:** Spezifizieren des **-Location** Parameters beim Aufruf von **New-AzureQuickVM** oder **New-AzureVM** führt dazu, dass der Cloud Service als Container für VMs erstellt wird. Benutzen Sie diese Option nur wenn Sie die erste VM erstellen oder wenn Sie Ihre VM einem neuem Cloud Service zuordnen möchten. 
	>
	>**Note 3:** Für mehr Informationen, klicken Sie: [New-AzureQuickVM reference](https://msdn.microsoft.com/en-us/library/azure/dn495183.aspx) page.

1. Die VM wurde erstellt. 

	![Creating Virtual Machine with Powershell output](images/creating-vm-with-powershell-output.png?raw=true)

	_VM wurde erstellt_

1. Sie können alle VMs im Cloud Service auflisten, indem Sie das Kommando ausführen:

	```PowerShell
	Get-AzureVM -ServiceName $cloudSvcName
	```

	![Get-AzureVM output - list all vms](images/get-azurevm-output---list-all-vms.png?raw=true)

	_Get-AzureVM output, wenn alle VMs aufgelistet werden_

	Falls Sie nur die Details enumieren möchten, benutzen Sie den **-Name** switch:

	```PowerShell
	Get-AzureVM -ServiceName $cloudSvcName -Name $vmname
	```

	<a name="attach-disk-powershell"></a>

	Nun werden Sie eine leere Festplatte zur VM hinzufügen. Da die Maschine bereits erstellt wurde, muss Sie modifiziert werden. Dies erfordert das Einholen der aktuellen Einstellungen durch das **Get-AzureVM** Kommando, die Modifikation der Einstellungen, und abschließend den Aufruf des **Update-AzureVM** Cmdlets um die Änderungen zu speichern.

	>**Note:** Es ist best practice eine oder mehrere separate Festplatten für das Speichern der VM Daten zu verwenden. Nach dem Erstellen einer Azure VM, ist eine Festplatte für das Betriebssystem mit dem Laufwerksbuchstaben C vorhanden und eine temporäre Festplatte D. Benutzen Sie NICHT die D Festplatte um Daten zu speichern. Diese Festplatte ist nur für temporäre Daten vorgesehen. Es bietet keine Redundanz und kein Backup, da es sich nicht im Azure Storage befinden.


1. Führen Sie folgende cmdlets aus:

	```PowerShell
	Get-AzureVM -Name $vmname -ServiceName $cloudSvcName |
		 Add-AzureDataDisk -CreateNew -DiskSizeInGB 50 -DiskLabel 'datadisk1' -LUN 2 |
		 Update-AzureVM 
	```

	Das **Get-AzureVM** Cmdlet erhält das VM Object und leitet es an die PowerShell Pipeline.

	Das **Add-AzureDataDisk** Cmdlet mit dem **-CreateNew** Parameter erlaubt Ihnen dynamisch Speicher zur VM hinzuzufügen. In diesem Fall fügen Sie eine unformatierte, leere VHD mit 50GB hinzu. Der **-LUN** Parameter ist für die Reihenfolge, in der das Gerät hinzugefügt wird und der **-MediaLocation** Parameter spezifiziert die Lokation im Storage für die neuen VHDs.

	**Add-AzureDataDisk** unterstützt den **-Import** Parameter um eine Festplatte der Festplattenbibliothek hinzuzufügen und **-ImportFrom** um eine bereits existierende Festplatte dem Storage hinzuzufügen.

1. Sobald **Update-AzureVM** ausgeführt wurde, kann Ihre VM benutzt werden. 

	![Update-AzureVM output after adding a datadisk](images/update-azurevm-output-after-adding-a-datadisk.png?raw=true)

	_Update-AzureVM Output nach dem Hinzufügen einer neuen Festplatte_


	<a name="install-vm-extension-powershell"></a>
	Nun werden Sie lernen wie man Extensions zu Ihrer erstellten VM hinzufügt.

	Microsoft Azure stellt VM Extensions von Microsoft und vertrauenswürdigen third-party Anbietern bereit um Sicherheit, Laufzeit, Debugging, Management, und andere Funktionen zur Steigerung der Produktivität Ihrer Azure VMs zur Verfügung zu stellen. 
	Für mehr Details, besuchen Sie: [Azure VM Extensions and Features](https://msdn.microsoft.com/en-us/library/azure/dn606311.aspx).

	Der **Azure Virtual Machine Agent** (VM Agent) ist zur Installation, Konfiguration, Mangament und zur Ausführung von **Azure Virtual Machine Extensions** (VM Extensions). Der VM Agent ist ein sicherer, leichtgewichtiger Prozess zur Installation, Konfiguration und zum Entfernen von VM Extensions auf Azure VM Instanzen von der Image Gallery und auf eignen VM Instanzen auf denen der VM Agent installiert ist.  

	Es gibt zwei Azure VM Agents, einen für Windows VMs und einen für Linux VMs. Per default wird der VM Agent automatisch installiert wenn eine VM von der Image Gallery erstellt wird, aber der VM Agent kann auch nach der Erstellung einer Instanz oder auf einem eigenem VM Image installiert werden. 

	Sie werden nun verifizieren, dass der VM Agent in Ihrer erstellten VM aktiviert ist und anschließend die Symantec Protection Extension installieren. Zum Schluss werden Sie die erfolgreiche Installation der Extension verifizieren. 

1. Überprüfen Sie, ob der VM Agent auf Ihrer VM erlaubt ist; führen Sie folgendes Kommando aus: 

	```PowerShell
	$vm = Get-AzureVM -ServiceName $cloudSvcName
	$vm.VM.ProvisionGuestAgent
	```

	Das erste Kommando sollte keine Fehler zurückgeben und das zweite Kommando sollte "True" zurückgeben. 

	Das Ausführen dieser Kommandos setzt die $vm.VM Variable, welche in den nachfolgenden Schritten verwendet wird um die Extension hinzuzufügen.

	>**Note:** Falls der Wert **$vm.VM.ProvisionGuestAgent** "False" ist, verbinden Sie sich zu Ihrer VM und installieren Sie den VM Agent. Sie können diesen [hier](<http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409>) herunterladen. Führen Sie folgende Schritte aus:
	>
	>```PowerShell
	>$vm = Get-AzureVM -serviceName $cloudSvcName -Name $vmname
	>$vm.VM.ProvisionGuestAgent = $TRUE
	>Update-AzureVM -Name $name -VM $vm.VM -ServiceName $cloudSvcName
	>```
	
	Nun werden Sie die Symantec endpoint protection extension installieren.

1. Führen Sie folgendes Kommando aus um die Erweiterung hinzuzufügen:

	```PowerShell
	Set-AzureVMExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection -VM $vm.VM -Version 12.*
	Update-AzureVM -ServiceName $cloudSvcName -Name $vmname -VM $vm.VM
	```

	**Set-AzureVMExtension** setzt die Einstellungen für die Extension. **Update-AzureVM** installiert die Extension.

	Der Output sollte wie folgt aussehen:

	![Set-AzureVMExtension output](images/set-azurevmextension-output.png?raw=true)

	_Output vom Hinzufügen einer VM Extension_

1. Überprüfen Sie, ob die Extension auf Ihrer VM installiert wurde; führen Sie folgendes Kommando aus:

	```PowerShell
	Get-AzureVMExtension -VM $vm.VM
	```
	Der Output sollte wie folgt aussehen:

	![Get-AzureVMExtension output](images/get-azurevmextension-output.png?raw=true)

	_Get-AzureVMExtension output_

	<a name="connect-to-vm-powershell"></a>
	Nachdem Sie eine Festplatte zur VM hinzufügt haben, muss Sie initialisiert werden. Dazu müssen Sie sich auf der VM anmelden. 

1. Führen Sie folgendes Kommando aus um eine remote desktop protocol Datei (rdp) zu erstellen und führen Sie diese aus. Verwenden Sie Ihre Anmeldedaten von dem Administrator den Sie erstellt haben.

	>**Note:** Der Pfad der rdp muss existieren, sonst werden Sie einen Fehler erhalten.

	```PowerShell
	Get-AzureRemoteDesktopFile -ServiceName $cloudSvcName -Name $vmname -LocalPath 'C:\myvmconnection.rdp' -Launch
	```

	Dies wird die rdp Datei ausführen. 

	![Get-AzureRemoteDesktopFile output](images/get-azureremotedesktopfile-output.png?raw=true)

	_Get-AzureRemoteDesktopFile output_

1. In der Remote Desktop Connection Dialogbox, klicken Sie **Connect**.

1. Geben Sie den Usernamen und das Passwort des Administratorbenutzer ein und klicken **OK**.

	![Enter admin User credentials](images/enter-admin-user-credentials.png?raw=true) 

	_Eingabe der Administrator Anmeldedaten_

1. In der Remote Desktop Connection Dialogbox, klicken Sie **Yes** um die Identität des Remotecomputers zu verifizieren. Sie können die "Don't ask me again for connections to this computer" Checkbox aktivieren, wenn Sie diesen Dialog nicht erneut sehen möchten.

	![Verify virtual machine identity](images/verify-virtual-machine-identity.png?raw=true)
	
	_Verifizieren der VM Identität_

1. Nach ein paar Sekunden öffnet sich das Remotedesktopverbindung Fenster für den Administrator. Nach der Fertigstellung sehen Sie das **Server Manager Dashboard**, welches Sie nun in den folgenden Schritten zur Konfiguration der Festplatte verwenden werden. 


	![Using the remote virtual machine](images/using-the-remote-virtual-machine.png?raw=true)

	_Benutzen der VM_

	<a name="configure-datadisk-powershell"></a>
	Nun werden Sie die Festplatte konfigurieren, die Sie zur Ihrer VM hinzugefügt haben.

1. In dem **Server Manager Dashboard**, das in der VM geöffnet ist, klicken Sie **File and Storage Services**.

	![Clicking File and Storage Services](images/click-file-and-storage-services.png?raw=true)

	_Klicken Sie auf File and Storage Services_

1. Im **Servers** pane, klicken Sie **Disks**.

	![Clicking Disks in File and Storage Services](images/clicking-disks-in-file-and-storage-services.png?raw=true)

	_Anzeigen der Festplatten im File und Storage Service_

	Alle verfügbaren Festplatten werden angezeigt. Eine Festplatte ist als Microsoft Virtual Disk mit der Partition _Unknown_ und der Kapazität Ihrer Wahl gesetzt. 

1. Rechtsklicken Sie auf die Festplatte und wählen **Initialize**.

	![Initialize the disk](images/initialize-the-disk.png?raw=true)

	_Initialisieren der disk_

1. Klicken Sie **Yes** in der Messagebox und bestätigen Sie, dass Sie alle Daten auf der Festplatte löschen möchten.

	![Confirm initialization of disk](images/confirm-initialization-of-disk.png?raw=true)

	_Bestätigen der Initalisierung der Festplatte_

1. Rechtsklicken Sie auf die Festplatte und wählen  **New Volume**.

	![Creating new volume](images/creating-new-volume.png?raw=true)

	_Klicken Sie New Volume im Kontextmenü_

1. Klicken Sie **Next** in der **New Volume Wizard** Dialogbox, die sich öffnet.

1. Im **Server and Disk** Schritt des **New Volume Wizard**, klicken Sie **Next**.


1. Im **Size**  Schritt des **New Volume Wizard**, verändern Sie die Größe - falls gewünscht - und klicken Sie **Next**.

	![New Volume Wizard - Size step](images/newvolumewizard-size-step.png?raw=true)

	_New Volume Wizard - Size step_

1. Im **Drive Letter or Folder** Schritt des **New Volume Wizard**, verändern Sie die Informationen - falls gewünscht - und klicken Sie **Next**.

1. Im **File System Settings** Schritt des **New Volume Wizard**, verändern Sie die Informationen - falls gewünscht - und klicken Sie **Next**.

	![New Volume Wizard - File System Settings step](images/newvolumewizard-file-system-settings-step.png?raw=true)

	_New Volume Wizard - File System Settings step_

1. Im **Confirmation** Schritt des **New Volume Wizard**, überprüfen Sie die Informationen und  klicken Sie **Create**.


1. Nachdem das Volume erstellt wurde, klicken Sie **Close**.

1. Sie können nun einen neuen **Explorer** öffnen und bestätigen, dass die Disk für die Benutzung bereit ist.

	![Attached disk ready to be used](images/attached-disk-ready-to-be-used.png?raw=true)

	_Anzeigen der hinzugefügten Festplatte im Explorer_


<a name="creating-a-vm-using-Runbook"></a>
##Erstellen einer VM mit einem Runbook

Azure Automation erlaubt die Automatisierung der Erstellung, Deployment, Überwachung und Wartung von Ressourcen in Ihrer Azure Umgebung mithilfe hoch-skalierbarer und verlässlicher Arbeitsabläufe.

Ein Azure Automation Account enthält:

* **Runbooks**: ein Runbook ist ein PowerShell Workflow, der Azure Cmdlets benutzt um unbeaufsichtigte Aktionen durchzuführen.
* **Assets**: ein asset ist ein Stück Information, das von allen Skripten im automation Account verwendet wird. Hierbei kann es sich um eine Verbindung, Anmeldedaten, Variable oder um einen Zeitplan handeln.
* **Jobs**: ein Job ist die Ausführung eines Runbooks. 

In dieser Aufgabenstellung werden Sie ein Runbook erstellen und starten um eine VM zu erstellen. Außerdem werden Sie nötige Assets für das Runbook  erstellen und diese starten. Davor werden Sie sich versichern, dass ein paar Vorbereitungen getroffen werden.

<a name="runbook-setup"></a>
Um das Runbook zu erstellen und erfolgreich zu starten, müssen Sie sich vergewissern, dass die Subscription einen Storage Account und ein Geschäftskontenaccount als Co-Administrator enthält.

Um festzustellen ob Sie bereits einen Storage Account besitzen, oder um einen Neuen zu erstellen, befolgen Sie folgende Schritte:
 
1. Melden Sie sich an im [Azure-Vorschauportal](https://portal.azure.com/).

1. Klicken Sie auf **Durchsuchen** und wählen Sie **Speicherkonto (klassisch)**. 

	![Checking storage accounts](images/checking-storage-accounts.png?raw=true)

	_Überprüfen ob ein Speicherkonto existiert_

	Falls in der Liste mindestens ein Speicherkonto erscheint, dass Sie verwenden können, überspringen Sie den nächsten Schritt.

1. Klicken Sie **Neu** > **Daten und Speicher** > **Storage** > **Erstellen**.

	![Creating a new storage account](images/creating-a-new-storage-account.png?raw=true)

	_Erstellen eines neuen Speicherkontos_

<a name="creating-new-organizational-account"></a>
Manche nicht-interaktive Loginmethoden funktionieren nur mit einem Geschäftskonto. Ein Geschäftskonto ist ein Benutzer, der durch seine Firma verwaltet wird und ist in der Azure Active Directory Instanz für die Organisation definiert. 
    Dies ist beim Runbook der Fall. 

Falls sie aktuell kein Geschäftskonto besitzen und einen Microsoft Account zum Login für Ihre Azure Subscription verwenden, können Sie nun einen erstellen indem Sie folgende Schritte befolgen:

>**Note:** Um einen Account im default AD der Subscription zu erstellen, benötigen Sie einen globalen Administrator für Ihre Subscription. Falls Sie dies nicht sind, müssen Sie entweder die Berechtigungen bei diesem anfragen oder der globale Admin muss diese Schritte für Sie durchführen. 


1. Im [Azure-Portal](https://manage.azure.com/)., klicken Sie **Active Directory**.

	![Viewing Active Directories](images/viewing-active-directories.png?raw=true)

1. Klicken Sie auf das **Standardverzeichnis (Default Directory)** und dann auf **Benutzer (Users)**. 

	![Clicking the Users tab for the directory](images/clicking-the-users-tab-for-the-directory.png?raw=true)

1. Klicken Sie **Benutzer hinzufügen (Add User)** in der unteren Leiste. 

	![Clicking Add User](images/clicking-add-user.png?raw=true)


1. Der **Benutzer hinzufügen (Add User)** Assistent erscheint und wird Sie bitten Nutzerinformationen einzugeben. Während der Erstellung des Users müssen Sie eine Email-Adresse und ein temporäres Passwort eingeben. Bitte merken Sie sich diese Daten. 

	![Organizational account created](images/organizational-account-created.png?raw=true)

	_Erstellung eines Geschäftskontos_
	

1. Im management portal, klicken Sie **Einstellungen (Settings)** > **Administrators**. 

	![Clicking administrators in Settings](images/clicking-administrators-in-settings.png?raw=true)

	_Wählen der Administratoren in Einstellungen_

1. Klicken Sie **Hinzufügen (Add)** in der unteren Leiste und fügen einen neuen User als Co-Administrator hinzu. Dies erlaubt dem Arbeits- oder Schulkonto die Verwaltung der Azure subscription.

	![Clicking Add User to Administrators](images/clicking-add-user-to-administrators.png?raw=true)

	_User hinzufügen_

	![User added as co-administrator](images/user-added-as-co-administrator.png?raw=true)

	_User wurde als Co-Administrator hinzugefügt_

1. Abschließend melden Sie sich vom Azure portal ab und melden sich mit Ihrem Arbeits- oder Schulkonto an. Da dies die erste Anmledung mit diesem Account darstellt, werden Sie aufgefordert Ihr Passwort zu ändern.

	>Für mehr Informationen zur Anmeldung in Microsoft Azure mit einem Arbeits- oder Schulkonto, lesen Sie: [Als Unternehmen für Azure registrieren](https://azure.microsoft.com/de-de/documentation/articles/sign-up-organization/).

1. Melden Sie sich vom Azure portal ab und melden Sie sich mit Ihrem eigenen Account an. 

	<a name="create-empty-runbook"></a>
1. Klicken Sie **Neu (Neu)** und wählen **App-Dienste (App Serives)** > **AUTOMATION** > **RUNBOOK** > **Schnellerfassung (Quick Create)**.

	![Creating a new Runbook](images/creating-a-new-runbook.png?raw=true)

	_Erstellen eines Runbooks_

1. In der **Schnellerfassung (Quick Create)**, geben Sie einen Namen für das Runbook (z.B.: _New-AzureVM_) ein, und wählen **Create a new automation account** im **Automation Account** Auswahlfeld; geben Sie einen Accountnamen ein. Klicken Sie auf **Erstellen (Create)**.

	![Creating a new Runbook and Automation account](images/creating-a-new-runbook-and-account.png?raw=true)

	_Erstellen eines neuen Runbooks und Automation Accounts_

	<a name="edit-runbook"></a>
1. Wenn sowohl der Automation account als auch das Runbook fertig erstellt wurden, klicken Sie **EDIT RUNBOOK**.

	![Selecting to edit the new Runbook](images/navigating-to-edit-runbook.png?raw=true)

	_Wählen Sie "Editieren" des neuen Runbook_

	Dies leitet Sie zur Workflow Edition Seite. In den nächsten Schritten werden Sie ein Runbook Skript erstellen.

	```PowerShell
	workflow New-AzureVM
	{ 
	}
	```

	Stellen Sie sicher, dass jeglicher Code, den Sie dem Workflow hinzufügen innerhalb der geschweiften Klammer steht. Außerdem sollte der Name des Workflows dem Namen des Runbook's entsprechen.


1. In der **DRAFT** Ansicht des Runbooks, fügen Sie den folgenden Code zur Workflow Definition hinzu um Parameter hinzuzufügen. Diese Parameter werden später in der Dialogbox erscheinen, wenn Sie das Runbook ausführen.

	```PowerShell
    param
	( 
		[Parameter(Mandatory=$true)] [String] $ServiceName,

		[Parameter(Mandatory=$true)] [String] $StorageAccountName,

		[Parameter(Mandatory=$true)] [PSCredential] $AzureCredential,

		[Parameter(Mandatory=$false)] [String] $VMName = "VM-Instance",
		[Parameter(Mandatory=$false)] [String] $VMInstanceSize = "ExtraSmall"
	)  
	```
	Die Parameter, die durch den Workflow definiert sind sind:

	* **$ServiceName**: Cloud Service Name, in welchem die VM erstellt wird. 
	* **$StorageAccountName**: Name des Storage Accounts, den die VM benutzen wird. 
	* **$AzureCredential**: ID des Azure Credential Assets (das später erstellt werden muss). Das PSCredential Object wird automatisch erstellt wenn das  Runbook vom Credential asset erstellt wird, dass diesem Identifier entspricht.
	* **$VMName**: name der virtuellen Maschine, die erstellt werden soll. Der default Name ist _VM-Instance_.
	* **$VMInstanceSize**: Größe der virtuellen Maschine. Der default Wert ist _ExtraSmall_.


1. Fügen Sie nun den folgenden Code unterhalb der Parameterdefinition ein um die Azure Credentials von der Automation Asset list zu erhalten und konfigurieren.

	```PowerShell
	# Get the Azure credentials and connect to Azure #######################################################

	# Get the credential to use for Authentication to Azure and Azure Subscription Name
	$AzureSubscriptionName = Get-AutomationVariable -Name 'Subscription name'
		 
	if($AzureSubscriptionName -eq $null)
	{
		throw "No variable asset was found by name 'Subscription name'. Please create it."
	} 

	# Connect to Azure
	$AzureAccount = Add-AzureAccount -Credential $AzureCredential 
	```
1. Fügen Sie nun den folgenden Code unterhalb des Codes ein, den Sie gerade hinzugefügt haben um die Anmeldedaten zu erhalten, die für den Zugriff auf die VM benutzt werden.

	```PowerShell
	# Get the VM credentials ###############################################################################

	$VMCred = Get-AutomationPSCredential -Name 'VM credentials'
	if($VMCred -eq $null)
	{
		throw "No Credential asset was found by name 'VM credentials'. Please create it."
	}

	$VMUserName = $VMCred.UserName
	$VMPassword = $VMCred.GetNetworkCredential().Password
 
	```

	The **Get-AutomationPSCredential** CmdLet retrieves an object of type PSCredential with the name _VM Credentials_. As with the $AzureCredentials parameter, you will create an Automation Asset named _VM credentials_, of type "credentials", in an upcoming step. 
   
1. Als Nächstes fügen Sie den folgenden Code unterhalb des Codes ein, den Sie gerade hinzugefügt haben. Dieser Code definiert einen _InlineScript_ Absatz, der einige Variablendefinitionen enthält, wie das Image das zur Erstellung der VM benutzt wird. 

	```PowerShell
	InlineScript
	{
		$VMUserName = $using:VMUserName
		$VMPassword = $using:VMPassword
		$VMName = $using:VMName
		$VMInstanceSize = $using:VMInstanceSize

		$VMImage = 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201412.01-en.us-127GB.vhd'

		$AzureAccount = $using:AzureAccount
		$AzureSubscriptionName = $using:AzureSubscriptionName
		$ServiceName = $using:ServiceName
		$StorageAccountName = $using:StorageAccountName

	} 
	```

1. Fügen Sie den folgenden Code innerhalb des _InlineScript_ Absatzes ein, direkt unter der Variablendefinition. Dieser Code setzt die Azure Subscription und den Storage Account als verwendet. Zusätzlich wird die Existenz des Storage Account validiert. 

	```PowerShell
    InlineScript
	{
	    # Set Azure subscription and storage ################################################################

	    Set-AzureSubscription -SubscriptionName $AzureSubscriptionName -CurrentStorageAccountName $StorageAccountName

	    $storageAccount = Get-AzureStorageAccount | Where-Object { ($_.StorageAccountName -eq $StorageAccountName) }
	    if ($storageAccount -eq $null)
	    {
		    throw "Could not retrieve storage account '{0}'. You need to create it first." -f $StorageAccountName
	    }

	    $Location = $storageAccount.Location 
    } 
	```

1. Abschließend fügen Sie den folgenden Code im _InlineScript_ Absatz direkt unter dem Code, den Sie gerade hinzugefügt haben, ein. Dieser Code wird eine VM auf die gleiche Art erstellen, wie Sie in der _Erstellen einer VM mit PowerShell_ Aufgabenstellung erstellt wurde.

	```PowerShell
	# Main script ########################################################################################

	# Check whether a VM by name $VMName already exists, if it does not exist create VM
	Write-Output ("Checking whether VM '{0}' already exists.." -f $VMName)

	$AzureVM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
	if ($AzureVM -eq $null)
	{
		Write-Output ("Creating VM with service name  {0}, VM name {1}, image name {2}, Location {3}" -f $ServiceName, $VMName, $VMImage, $Location)

		# Create VM
		$CloudServiceInfo = Get-AzureService | Where-Object { ($_.ServiceName -eq $ServiceName) }

		if( $CloudServiceInfo -eq $null)
		{
			$AzureVMConfig = New-AzureQuickVM -Windows -ServiceName $ServiceName -Name $VMName -ImageName $VMImage -Password $VMPassword -AdminUserName $VMUserName -Location $Location -InstanceSize $VMInstanceSize -WaitForBoot
		}
		else
		{
			if ($CloudServiceInfo.Location -eq $Location)
			{
				$AzureVMConfig = New-AzureQuickVM -Windows -ServiceName $ServiceName -Name $VMName -ImageName $VMImage -Password $VMPassword -AdminUserName $VMUserName -InstanceSize $VMInstanceSize 
			}
			else
			{
				throw "Cloud service location does not match the storage account location."
			}
		} 

		$AzureVM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
		if ($AzureVM -ne $null)
		{
			Write-Output ("VM '{0}' was created successfully" -f $VMName)
		}
		else
		{
			throw "Could not retrieve info for VM '{0}'. VM was not created" -f $VMName
		}
	}
	else
	{
		Write-Output ("VM '{0}' already exists." -f $VMName)
	}
	```

1. Da das Skript nun komplett ist, veröffentlichen Sie das Runbook indem Sie den **Veröffentlichen (Publish)** Button in der unteren Leiste anklicken.

	![Publishing the Runbook](images/publishing-the-runbook.png?raw=true)

	_Veröffentlichen des Runbooks_

1. Klicken Sie **Ja (Yes)** in dem Bestätigungsdialog, der nun erscheint.

	![Clicking yes to save and publish the Runbook](images/saving-and-publishing-the-runbook.png?raw=true)

	_Klicken Sie Ja um zu speicher und um das Runbook zu veröffentlichen_

	<a name="create-assets"></a>
	Dies veröffentlicht das Runbook. Nun werden Sie Assets hinzufügen, die vom Runbook verbraucht werden und später werden Sie das Runbook starten.

1. Navigieren Sie zum Automation Account indem Sie auf den "Zurück"-Pfeil über dem Namen des Runbooks klicken. 

	![Navigating to the Automation account](images/navigating-to-the-automation-account.png?raw=true)

	_Navigation zum Automation Account_

1. Klicken Sie auf den **ASSETS* tab.

	![Navigating to the Automation Assets tab](images/navigating-to-assets.png?raw=true)

	_Navigieren Sie zum Automation Assets tab_

1. Klicken Sie auf den **ADD SETTING** Button um ein neues Asset hinzuzufügen.

	![Adding a new asset](images/adding-a-new-asset.png?raw=true)

	_Hinzufügen eines neuen Assets_

1. In der **ADD SETTING** Dialogbox, wählen Sie die **ADD CREDENTIAL** Option.

	![Adding a credential](images/adding-a-credential.png?raw=true)

	_Hinzufügen der Anmeldedaten_

1. In der **ADD CREDENTIAL** Dialogbox, wählen Sie _Windows PowerShell Credential_ als Credential Type und tippen _VM credentials_ als Name, klicken Sie auf Weiter (Next).

	![Creating the virtual machine credential asset](images/creating-the-vm-credentials.png?raw=true)

	_Creating the virtual machine credential asset_

1. Setzen Sie den User name und das Password für den Benutzer der virtuellen Maschine und klicken Sie den check button.

	![Setting the user name and the password for the virtual machine](images/setting-the-user-and-password-for-the-vm.png?raw=true)

	_Setzen des User names und des Passworts für die virtuelle Maschine_

1. Wiederholen Sie die vorherigen Schritte um ein neues Credential mit dem Namen _Azure Credentials_ hinzuzufügen. Dies definiert ein Asset für die Credentials die beim Ausführen des Runbooks benutzt werden. In diesem Fall nutzen Sie die Credentials Ihres Geschäftskontos, die Sie am Anfang der Aufgabenstellung erstellt haben. 

1. Erstellen Sie nun eine neue Variable indem Sie den **ADD SETTING** Button anklicken. Wählen Sie diesmal **ADD VARIABLE**.

	![Adding a variable](images/adding-a-variable.png?raw=true)

	_Hinzufügen einer Variable_

1. Wählen Sie **String** als **VARIABLE TYPE**, geben Sie _Subscription name_ in das Name Feld ein und betätigen Sie den Check Button.

	![Creating a variable asset for the subscription name](images/creating-a-variable-for-the-subscription-name.png?raw=true)

	_Erstellen einer Asset Variable für den Subscription Namen_

1. Geben Sie den Namen Ihrer Subscription (i.e.: _Free Trial_) ein und klicken den Check Button.

	![Setting the value of the variable with the subscription name](images/setting-the-value-for-the-subscription-name.png?raw=true)

	_Setzen des Wertes der Variable mit dem Subscription Namen_

	<a name="start-runbook"></a>
1. Nun werden Sie das Runbook starten. Dazu navigieren Sie zum **RUNBOOKS** Tab, wählen Ihr eben kreiertes Runbook und drücken den **START** Button.

	![Starting the Runbook](images/starting-the-runbook.png?raw=true)

	_Starten des Runbooks_

1. Vervollständigen Sie alle Daten in der **START RUNBOOK** Dialogbox und klicken Sie auf "Weiter".

	> **Note:** Jede Dialogbox Eingabe trifft einen der Workflow Parameter und beeinhaltet eine Typvalidierung. 
	>
	> * **AzureCredential**: ID des Azure Credential Assets, das vorhin erstellt wurde (z.B. _Azure Credentials_).
	> * **ServiceName**: Cloud Service Name in dem die VM erstellt wird. Geben Sie einen neuen Namen ein.
	> * **StorageAccountName**: Name des Storage Account, der am Anfang der Aufgabenstellung erstellt wurde.
	> * **VMInstanceSize**: Größe der VM. Lassen Sie den default Wert stehen (_ExtraSmall_).
	> * **VMName**: Name der VM, die erstellt werden soll. Wählen Sie einen Namen oder behalten Sie den default Wert bei (_VM-Instance_).

	![Completing the form in the START RUNBOOK dialog box](images/completing-the-form-in-the-start-runbook.png?raw=true)

	_Vervollständigen der START RUNBOOK Dialogbox_


1. Klicken Sie den **VIEW JOB** Button.

	![Clicking the VIEW JOB button](images/clicking-the-view-job-button.png?raw=true)

1. Warten Sie bis der Job fertig gestellt wurde. Sie werden eine Nachricht über die erfolgreiche Erstellung erhalten und der Status wird sich auf _Completed_ setzen. 

	> **Note:** You can switch to the **HISTORY** tab to see more detailed output.

	![Waiting for the job to complete](images/waiting-for-the-job-to-complete.png?raw=true)

	_Waiting for the job to complete_

	<a name="verify-vm-runbook"></a>
1. Finally, navigate to the **Virtual Machines** section of the portal and validate that your new VM is ready.

	>**Note:** you may have to refresh the page by pressing **Ctrl+F5** for the Virtual Machine to show up.

	![Validating that the virtual machine was created](images/validating-that-the-vm-was-created.png?raw=true)

	_Überprüfen, dass die VM erstellt wurde_


<a name="cleanup"></a>
##Appendix - Cleanup

In dieser Aufgabenstellung wird gezeigt, wie man die virtuellen Maschinen und die zugehörigen Daten, die in den vorherigen Abschnitten erstellt wurden, löscht:

### Löschen der VM mit dem Vorschauportal

1. Klicken Sie auf **Virtuelle Computer** (oder unter **Durchsuchen** und dann **Virtuelle Computer**) 

	![Clicking Browse in the Hub Menu](images/clicking-browse-in-the-hub-menu.png?raw=true)


1. Eine Liste all Ihrer virtuellen Maschinen wird angezeigt. Klicken Sie auf Ihre in diesem Lab erstellte virtuelle Maschine.

1. Klicken Sie auf **Löschen**.

	![Deleting a virtual machine](images/deleting-a-virtual-machine.png?raw=true)

	_Löschen einer VM_

1. Geben Sie in der **Möchten Sie die VM wirklich löschen?** Dialogbox den Namen der VM ein und klicken Sie auf **Löschen**.

	![Confirming the deletion of virtual machine](images/confirming-the-deletion-of-virtual-machine.png?raw=true)

	_Bestätigen Sie das Löschen der VM_

Die virtuelle Maschine wird gelöscht. Sie können den Fortschritt im **Notifications** Hub oder auf dem Dashboard überwachen.
Nach dem erfolgreichen Löschen wird die VM nicht mehr in der Liste der VMs aufgeführt. 
Verfahren Sie analog für alle anderen virtuellen Maschinen, die Sie in diesem Lab erstellt haben. 

##Summary

Durch die Fertigstellung dieses Labs haben Sie gelernt, wie man Virtuelle Maschinen mit unterschiedlichen Methoden erstellen kann: mit dem Vorschauportal, mit Cross-Platform Command Line Tools, mit PowerShell und Automation Runbook. Außerdem haben Sie gesehen, wie man eine leere Festplatte zu einer VM hinzufügt, wie man eine Remote Desktop Protocol Datei zum Verbinden auf die Maschine erstellt und wie man Extension installiert. 
