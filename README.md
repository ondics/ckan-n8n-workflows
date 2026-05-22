# ckan-n8n-workflows

Sammlung von n8n-Workflows zur Automatisierung von CKAN-Prozessen.

Die Workflows ermöglichen die Externalisierung und Automatisierung von 
CKAN-Abläufen mit n8n, um betriebliche Integrationen und wiederkehrende 
Prozesse einfacher umzusetzen.

---

# Installation

## Voraussetzungen

* laufende n8n-Instanz
* Zugriff auf eine CKAN-Instanz
* CKAN Site URL
* CKAN API Token (wenn Änderungen in CKAn durchgeführt werden sollen)

---

## Workflow importieren

1. Workflow-Datei oder RAW-GitHub-URL kopieren
2. In n8n:

   * `Workflows`
   * `Import from URL`
3. Workflow importieren
4. Konfiguration anpassen

---

# Workflows

## dataset-create

Automatische Erstellung von CKAN-Datensätzen.

* Erstellung neuer Datensätze
* Mapping von Metadaten
* Validierung von Pflichtfeldern
* Fehlerbehandlung

Getestet mit:

* CKAN 2.10.x
* Sprache: DE/EN

---


# Hinweise

* Die Workflows dienen als Referenzimplementierungen.
* Anpassungen an projektspezifische Anforderungen sind in der Regel erforderlich.
* Vor produktivem Einsatz wird ein Test in einer Entwicklungs- oder Staging-Umgebung empfohlen.
* Ondics haftet nicht für die korrekte Funktionsweise der Workflows.
* Viel Erfolg damit. Automatisiert und spart, wo Ihr könnt!

---

# Credits

* [CKAN](https://github.com/ckan/ckan)
* [n8n](https://n8n.io)

---

# Autor

**ondics GmbH**
Esslingen am Neckar, Deutschland, Baden-Württemberg, "im Schwäbischen onder Stuttgart"
https://ondics.de
[info@ondics.de](mailto:info@ondics.de)
