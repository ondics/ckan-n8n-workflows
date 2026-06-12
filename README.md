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

Download/n8n-Url: [n8n-admin-workflows/dcatapde-groups.json](https://github.com/ondics/ckan-n8n-workflows/raw/refs/heads/main/n8n-admin-workflows/dcatapde-groups.json)

---

## PEGELONLINE Pegelstände nach CKAN aktualisieren

Aktuelle Wasserstandsmesswerte werden alle 10 Minuten von der PEGELONLINE-API abgerufen und im CKAN DataStore gespeichert. 
Neue Messwerte werden eingefügt, geänderte aktualisiert, unveränderte übersprungen.

* Alle 13 Schritte sind nummeriert und mit erklärenden Sticky Notes dokumentiert
* Konfiguration zentral in Node 02 Konfiguration bearbeiten (CKAN-URL, Resource-ID, Messstellen)
* Beliebig viele Messstellen konfigurierbar, einzeln aktivier- und deaktivierbar
* Messstellen werden anhand ihrer PEGELONLINE-UUID identifiziert
* CKAN-API-Token wird als n8n Credential hinterlegt, nicht im Workflow


### Einrichtung in n8n

Nach dem Import des Workflows müssen die CKAN-Zugangsdaten und die Konfiguration angepasst werden.

#### 1. CKAN-API-Token hinterlegen

Der CKAN-API-Token wird nicht direkt im Workflow gespeichert, sondern als n8n Credential hinterlegt.

In n8n:

1. Einen der CKAN **HTTP Request Nodes** öffnen  
2. Unter **Authentication** auswählen:

```text
Generic Credential Type
````

3. Als Credential wählen:

```text
Header Auth
```

4. Neue Credentials anlegen und folgenden Header hinterlegen:

| Name            | Wert                  |
| --------------- | --------------------- |
| `Authorization` | `DEIN_CKAN_API_TOKEN` |

5. Credential speichern und in allen CKAN HTTP Nodes auswählen

Der Token wird dann automatisch bei allen Requests an CKAN mitgesendet und muss nicht im Workflow selbst gespeichert werden.

> Hinweis: PEGELONLINE benötigt keine Authentifizierung. Der API-Token wird ausschließlich für CKAN-Schreibzugriffe verwendet.

#### 2. Konfiguration im Workflow anpassen

Die wichtigsten Werte werden zentral im Node **02 Konfiguration bearbeiten** gepflegt.

Dort müssen folgende Werte angepasst werden:

| Einstellung | Beschreibung |
|------------|--------------|
| `ckanBaseUrl` | Basis-URL der CKAN-Instanz, z. B. `https://datenportal.example.de` |
| `pegelwerteResourceId` | Resource-ID der dynamischen CKAN-DataStore-Ressource für Pegelwerte |
| `messstellenResourceId` | Resource-ID der statischen Messstellen-Ressource |
| `timezone` | Zeitzone für Zeitstempel, z. B. `Europe/Berlin` |
| `pegelApiBaseUrl` | Basis-URL der PEGELONLINE-API |
| `messstellen` | Liste der Messstellen mit interner ID und PEGELONLINE-UUID |

#### 3. HTTP Request Nodes prüfen

In den CKAN-HTTP-Nodes muss die CKAN-URL aus der Konfiguration verwendet werden.

Typische CKAN-Endpunkte im Workflow sind:

| Zweck | CKAN Action |
|------|-------------|
| Datensätze suchen | `/api/3/action/datastore_search` |
| Datensätze einfügen oder aktualisieren | `/api/3/action/datastore_upsert` |
| Ressourceninformationen abrufen | `/api/3/action/resource_show` |

Bei schreibenden Requests muss der Header `Authorization` gesetzt sein.

#### 4. Messstellen eintragen

Messstellen werden über ihre PEGELONLINE-UUID identifiziert.

Beispiel:

{
  "messstelle_id": 1,
  "name": "Plochingen",
  "pegelonline_uuid": "BEISPIEL-UUID",
  "aktiv": true
}

Nur Messstellen mit `"aktiv": true` werden im Workflow verarbeitet.

### Struktur der Pegelstandsdaten

Die dynamische Ressource speichert historische Pegelstände der Messstellen und wird regelmäßig aktualisiert.

| Feld | Typ | Beschreibung | Pflichtfeld |
|-------|------|---------------|--------------|
| `zeitstempel` | Timestamp | Zeitpunkt der Messung des Pegelstands | Ja |
| `messstelle_id` | Integer | Eindeutige ID der zugehörigen Messstelle (Referenz auf Messstelle) | Ja |
| `pegelstand_in_m` | Numeric | Gemessener Pegelstand in Metern | Ja |

Quelle: PEGELONLINE REST-API v2
Getestet mit CKAN 2.11 und self-hosted n8n

Download/n8n-URL: n8n-admin-workflows/pegelstaende-ckan-pegelonline-template.json

---

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
