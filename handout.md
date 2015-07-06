# Betriebssysteme

## {{Vorstellung eines modernen PC Betriebssystems}}

## Prozess
Im ersten Moment besteht vorerst gar kein Unterschied zwischen einem Prozess und einem Thread,
denn letztendlich besteht ein Prozess mindestens aus einem Thread. Ferner endet ein Prozess, wenn sich
alle Threads beenden. Somit ist der eine Prozess verantwortlich für die gleichzeitige Ausführung mehrerer Threads –
da doch Threads auch nur innerhalb eines Prozesses ausgeführt werden. Der gravierende Unterschied zwischen den
Threads und den Prozessen besteht darin, dass Threads unabhängige Befehlsfolgen innerhalb eines Prozesses sind.

## Thread / Task
Ein Thread ist ein Ausführungsstrang in der Abarbeitung eines Computerprogramms.
Threads teilen sich innerhalb eines Prozesses Prozessoren, den Speicher und andere betriebssystemabhängige Ressourcen
wie Dateien und Netzwerkverbindungen. Deswegen ist der Verwaltungsaufwand für Threads üblicherweise geringer als der
für Prozesse. Ein wesentlicher Effizienzvorteil von Threads besteht darin, dass im Gegensatz zu Prozessen beim
Threadwechsel kein vollständiger Wechsel des Prozesskontextes notwendig ist, da alle Threads einen gemeinsamen
Teil des Prozesskontextes verwenden.

## Multitasking
Der Begriff Multitasking  bzw. Mehrprozessbetrieb bezeichnet die Fähigkeit eines Betriebssystems,
mehrere Aufgaben (Tasks) nebenläufig auszuführen. Die verschiedenen Prozesse werden in so kurzen Abständen immer abwechselnd
aktiviert, dass der Eindruck der Gleichzeitigkeit entsteht. Multitasking ist somit ein Synonym für
Zeit-Multiplexverfahren. Besitzt ein Computer mehrere CPU-Kerne, so dass er mehrere Aufgaben echt-gleichzeitig
ausführen kann, so spricht man von Multiprocessing. In modernen Computern werden beide Verfahren
kombiniert eingesetzt.

### Präemptives Multitasking
Basis der heutzutage standardmäßig angewendete Methode ist das präemptive Multitasking.
Die Abarbeitung der einzelnen Prozesse wird ebenfalls gesteuert durch den Scheduler, ein Bestandteil des
Betriebssystemkerns. Jeder Prozess wird nach einer bestimmten Abarbeitungszeit unterbrochen.
Dabei spricht man auch von so genannten Zeitschlitzen (bzw. Zeitscheiben, engl. time slices). Dann „schläft“
der Prozess (ist inaktiv) und andere Prozesse werden bearbeitet. Erhält er wieder eine Prozessorzuteilung,
so setzt er seine Arbeit fort (ist aktiv). Meist wird jedem Prozess eine „absolute“ Zeitscheibe zugewiesen
(alle Zeitscheiben haben die gleiche, feste Dauer); alternativ wird ihm pro definierter Zeiteinheit ein
bestimmter Prozentteil dieser Zeiteinheit zugewiesen (z. B. abhängig von seiner Priorität), den er höchstens
nutzen kann (die Länge der Zeitscheibe wird also jedes Mal neu bestimmt). Endet seine Zeitscheibe
(„seine Prozessorzuteilung ist zu Ende“), dann unterbricht ihn ein Hardware-Timer, er wird wieder „schlafen
gelegt“ und das Betriebssystem erlangt wieder Kontrolle. Sollte er bereits vor Ablauf seiner Zeitscheibe eine
Funktion des Betriebssystems benötigen, so wird er sogleich angehalten und als „nicht rechenbereit“ markiert,
bis das Betriebssystem den gewünschten Dienst erbracht hat. Nur als „rechenbereit“ markierte Prozesse erhalten
Prozessorzeit-Zuteilungen.

Eine beliebte Umsetzung des präemptiven Multitaskings ist die Verwendung einer Vorrangwarteschlange in
Verbindung mit der Round-Robin-Scheduling-Strategie. Es gibt auch die Prozessorzuteilung abhängig von
der Taskpriorität, vor allem bei Echtzeitsystemen z. B. MicroC/OS-II. Für das Multitasking spielt das
nur eine untergeordnete Rolle, da präemptives Multitasking die Kernel- bzw. Prozessorkontrolle über
die Prozesse beschreibt.

### kooperatives Multitasking
Beim „kooperativen Multitasking“ wird das Multitasking durch eine zentrale Prozessverwaltung im Systemkernel
realisiert: ein einfacher, sogenannter Scheduler. Der Scheduler sichert den Prozesskontext des gerade unterbrochenen
Tasks, wählt den nächsten Prozess aus, der Rechenzeit erhalten soll, stellt dessen Prozesskontext her und gibt den
Prozessor dann an diesen neuen Prozess ab. Der Scheduler kann Listen mit verschieden priorisierten Tasks führen,
und niedrig priorisierte entsprechend selten aufrufen. Dabei kann auch die bereits verbrauchte Rechenzeit eines
Tasks berücksichtigt werden. In der Regel werden Betriebssystem-interne Aufgaben zuerst erledigt, bevor ein neuer
Task den Prozessor erhält. Es ist jedem Prozess selbst überlassen, wann er die Kontrolle an den Kern zurückgibt;
in der Regel wird zumindest jede Dienst-Anforderung an das Betriebssystem mit einem Taskwechsel verbunden.

## Deadlock
Deadlock oder Verklemmung bezeichnet in der Informatik einen Zustand, bei dem eine zyklische Wartesituation
zwischen mehreren Prozessen auftritt, wobei jeder beteiligte Prozess auf die Freigabe von Betriebsmitteln wartet,
die ein anderer beteiligter Prozess bereits exklusiv belegt hat. Eine andere Form der Blockierung von Prozessen
ist der Livelock.

Der Zustand eines Deadlocks kann folgendermaßen definiert werden: Eine Menge von Prozessen befindet sich in einem
Deadlock, wenn jeder dieser Prozesse auf ein Ereignis wartet, das nur ein anderer Prozess aus dieser Menge
verursachen kann.

## Einteilung der Funktionalitäten in ein Schalen- bzw. Schichtenmodell.

### Schicht 5:
API (Application Program Interface) Über Softwareschnittstellen wie die Win32 API verwenden Programme
für sie freigegebene Betriebssystemfunktionen etwa den Kopieren oder Öffnen Dialog für Dateien. Diese werden über
einheitliche Anwendungsbefehle mit Parametern allen Programmen einheitlich zur Verfügung gestellt. Beispiel hierfür
sind auch DFÜ Dienste.
Bibliotheken Bibliotheken stellen dem Betriebssystem und Anwendungsprogrammen fertige Programmteile zur Verfügung,
die den Zugang für verschiedene Funktionen vereinfachen. Durch Bibliotheken (.dll, .OCX, ...) greifen Entwickler
vereinfacht auf häufig benötigte Funktionen zurück ohne diese selbst für die Anwendung neu erfinden zu müssen.

### Schicht 4:
Systemschnittstelle (Kernel) Die Systemschnittstelle kapselt den Betriebssystemkern von der API ab,
häufig dient sie auch als Trennmarke des CPU Modus vom privilegierten Ring 0 des Kernel.

### Schicht 3: 
Management Die Managementschicht sorgt für den reibungslosen Ablauf der Systemprozesse durch
kooperatives, präemptives oder echtzeit Multitasking. Je nach Priorität teilt das Betriebssystem dem Prozess
CPU-Zeit, Speicher und I/O-Zugriffe zu.

### Schicht 2: 
Dateisystem, Treiber Wichtige Aufgaben des Betriebssystem sind die Darstellung eines bis mehrerer
Dateisysteme, die über entsprechende Treiber virtuell realisierbar sind. Zusätzliche Funktionen wie Verschlüsselung
oder Komprimierung gehören auch dazu. Treiber für Standard Hardware wie Tastatur, LPT oder COM Schnittstellen
werden rudimentär direkt vom Betriebssystem unterstützt, Beispiel sind DOS Betriebssysteme. Moderne Betriebssysteme
bringen Standard Treiber für die meisten Hardwarekomponenten gleich mit. Für erweiterte Funktionen und optimale
Leistung stellen die Hersteller eigene Treiber für ihre Hardware bereit.

### Schicht 1:
HAL (Hardware Abstraction Layer) Die HAL ermöglicht den Einsatz auf einer Hardwareplattform die
speziell auf eine Prozessor Architektur ausgelegt ist. Dazu gehören etwa die x86, Alpha, PowerPC oder Sparc
Architektur. Steht die Portierbarkeit des Betriebssystems für andere Plattformen im Vordergrund, spielt die
HAL eine zentrale Rolle für die Portierbarkeit.

Aber nicht alle Betriebssyssteme sind so aufgebaut.
Es gibt auch Monolithische Kernel.
Der monolithische Kernel stellt eine einzige ausführbare Datei dar, in der alle systemnahen Komponenten vereint
wurden. Treiber, Prozess- Speicher- und Dateisystemverwaltung befinden sich gemeinsam in einem großen Kernel.
In begrenztem Umfang lassen sich Module dynamisch nachladen, wie z.B. Netzwerk- oder SCSI-Treiber. Typische
Betriebssysteme sind MS-DOS, Multics, Unix und Linux. Der Kernel läuft im privilegierten Kernel-Modus der
CPU ab, einzelne Bestandteile wie etwa Treiber lassen sich in Module auslagern. Das Linux Betriebssystem
nutzt diese Technik.
