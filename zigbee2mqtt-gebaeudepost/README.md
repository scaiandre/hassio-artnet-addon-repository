# Zigbee2MQTT (Gebäude Post / SLZB-06p7)

Zusätzliche Zigbee2MQTT-Instanz für den netzwerkgebundenen SLZB-06p7-Koordinator im Gebäude Post (ehemaliges Restaurant „Zur Post", benannt nach der früheren Post-Station).

Ermöglicht den Parallelbetrieb **mehrerer** Zigbee-Netze an **einer** Home-Assistant-Instanz — ein Netz pro Gebäude bzw. pro stahlbeton-isolierter Zone, jeweils über einen eigenen LAN-Koordinator.

- Nutzt das offizielle Image `ghcr.io/zigbee2mqtt/zigbee2mqtt-{arch}` (kein eigener Build).
- Frontend über Ingress in der HA-Sidebar.
- Beliebig oft duplizierbar (ein Ordner je Zone).

Einrichtung und Duplikation: siehe [DOCS.md](DOCS.md).
