# ckan-n8n-workflows

Sammlung von n8n-Workflows zur Automatisierung von CKAN-Prozessen.

Die Workflows ermöglichen die Externalisierung und Automatisierung von 
CKAN-Abläufen mit n8n, um betriebliche Integrationen und wiederkehrende 
Prozesse einfacher umzusetzen.

---

Inhalt

* [Installation](#installation)
* [Administrative Workflows](#administrative-workflows)
* [Autoren-bezogene Workflows](#autoren-bezogene-workflows)
* [Hinweise](#hinweise)

---

# Installation

Voraussetzungen

* laufende n8n-Instanz
* Zugriff auf eine CKAN-Instanz
* CKAN Site URL
* CKAN API Token (wenn Änderungen in CKAn durchgeführt werden sollen)

Workflow importieren

1. Workflow-Datei oder RAW-GitHub-URL kopieren
2. In n8n:

   * `Workflows`
   * `Import from URL`
3. Workflow importieren
4. Konfiguration anpassen

---

# Administrative Workflows

## DCAT-AP.de Kategorien einrichten

Die Standard-DCAT-AP.de Kategorien werden in CKAN angelegt. Und bei Bedarf auch gelöscht.
Quelle: [EU Vocabularies: data-theme](https://op.europa.eu/de/web/eu-vocabularies/concept-scheme/-/resource?uri=http://publications.europa.eu/resource/authority/data-theme)

* Hinzufügen der 13 DCAT-AP.de Kategorien/Gruppen (DCAT-AP Sprechweise: data themes)
* Vorhandene Kategorien werden erkannt und übersprungen
* Die Gruppenbeschreibungen sind auf deutsch
* Die Namen der Kategorien entsprechen dem DCAT-AP.de Standard (Beispiel: `agri`)
* Icons werden nicht konfiguriert

Getestet mit CKAN 2.11 und self-hosted n8n
Download/n8n-Url: [n8n-admin-workflows/DCAT-AP.de Kategorien anlegen (3).json](https://github.com/ondics/ckan-n8n-workflows/raw/refs/heads/main/n8n-admin-workflows/DCAT-AP.de Kategorien anlegen (3).json)

# Autoren-bezogene Workflows

## schaumermal, was da noch kommt...

noch nix.

# Hinweise

* Die Workflows dienen als Referenzimplementierungen.
* Anpassungen an projektspezifische Anforderungen sind in der Regel erforderlich.
* Vor produktivem Einsatz wird ein Test in einer Entwicklungs- oder Staging-Umgebung empfohlen.
* Ondics haftet nicht für die korrekte Funktionsweise der Workflows.
* Viel Erfolg damit. Automatisiert und spart, wo Ihr könnt!

---

# Credits

Danke an die, die solche Arbeiten erst ermöglichen: 

* [CKAN](https://github.com/ckan/ckan)
* [n8n](https://n8n.io)

---

# Autor

**ondics GmbH**
Esslingen am Neckar, Deutschland, Baden-Württemberg, "im Schwäbischen onder Stuttgart"
https://ondics.de
[info@ondics.de](mailto:info@ondics.de)
