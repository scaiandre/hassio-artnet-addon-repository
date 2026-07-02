# Zigbee2MQTT (Gebäude Post / SLZB-06p7)

Zusätzliche Zigbee2MQTT-Instanz für den Koordinator im **Gebäude Post** (ehemaliges Restaurant „Zur Post", benannt nach der früheren Post-Station) — **ein** netzwerkgebundener Koordinator (SLZB-06p7 über Ethernet/PoE, angesprochen per TCP). Nutzt das **offizielle** Zigbee2MQTT-Add-on-Image `ghcr.io/zigbee2mqtt/zigbee2mqtt-{arch}` — also identische Container wie das offizielle Add-on, nur unter eigenem Slug, damit mehrere Instanzen parallel laufen können.

## Wann brauche ich das?

Home Assistant kann das offizielle Zigbee2MQTT-Add-on nur **einmal** installieren. Für **jeden weiteren Koordinator** (weiteres Gebäude / weitere stahlbeton-isolierte Zone) braucht es eine **eigene Instanz** — dieses Add-on. Regel: **1 Koordinator = 1 Instanz = 1 Zigbee-Netz.**

## Voraussetzungen

- Ein MQTT-Broker (z. B. das **Mosquitto broker** Add-on) — alle Instanzen nutzen **denselben** Broker.
- Der SLZB-06p7 ist im LAN erreichbar, hat eine **feste IP** und ist im SLZB-OS auf Modus **`Zigbee2MQTT`** (TCP-Port **6638**) gestellt.

## Konfiguration

Alle Startwerte stehen im Reiter **Konfiguration**:

```yaml
data_path: /config/zigbee2mqtt_gebaeudepost   # eindeutiger Datenpfad je Instanz
mqtt:
  base_topic: zigbee2mqtt_gebaeudepost        # MUSS je Instanz eindeutig sein
  server: mqtt://core-mosquitto:1883       # bei Mosquitto-Add-on
  user: mqtt_z2m
  password: DEIN_PASSWORT
serial:
  port: tcp://192.0.2.21:6638              # feste IP des SLZB-06p7
  adapter: zstack                          # CC2652P7 = TI-Chip
```

Alle übrigen Einstellungen (Kanal, Netzwerkschlüssel, Geräte) verwaltet Zigbee2MQTT selbst und legt sie unter `data_path` in `configuration.yaml` ab.

> **Netzwerkschlüssel / kein Big-Bang:** Beim ersten Start erzeugt Z2M einen Netzwerkschlüssel und sichert die Konfiguration als `configuration.yaml.bk` im Datenpfad. **Nicht** löschen — sonst bildet sich ein neues Netz und alle Geräte müssten neu angelernt werden.

## Frontend (Ingress)

`ingress` ist aktiv. Über **Einstellungen → Add-ons → dieses Add-on → „In Seitenleiste anzeigen"** erscheint das Z2M-Frontend direkt in der HA-Sidebar — ohne eigenen Port. Der Sidebar-Name entspricht dem Add-on-Namen, daher trägt jede Zone einen sprechenden Namen (hier „… Gebäude Post").

## Geräte anlernen (Pairing)

1. Dieses Add-on starten, Frontend öffnen.
2. **„Permit join"** aktivieren (mit Zeitlimit).
3. Gerät in den Pairing-Modus versetzen → es erscheint in Z2M und per MQTT-Discovery automatisch in HA.
4. **„Permit join" wieder ausschalten.**

Immer nur an **einer** Instanz gleichzeitig „Permit join" aktivieren.

## Weitere Zonen hinzufügen

Diesen Ordner kopieren (z. B. `zigbee2mqtt-hauptgebaeude`) und in der `config.json` **eindeutig** ändern:

- `slug` (z. B. `zigbee2mqtt_hauptgebaeude`)
- `name` / `description`
- `options.data_path` (z. B. `/config/zigbee2mqtt_hauptgebaeude`)
- `options.mqtt.base_topic` (z. B. `zigbee2mqtt_hauptgebaeude`)
- `options.serial.port` (IP des jeweiligen SLZB)

Danach im Add-on-Store **neu laden** — die neue Instanz erscheint als eigenes Add-on. So sind **beliebig viele** Zonen möglich.
