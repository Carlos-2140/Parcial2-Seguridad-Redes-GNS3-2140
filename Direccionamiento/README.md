# Direccionamiento IP — Parcial 2 GNS3

## Plan de subredes

| Segmento | Red y prefijo | Máscara | Uso |
|---|---|---|---|
| LAN principal | 10.21.40.0/25 | 255.255.255.128 | Router, switch, servidores y Usuario-1 |
| Enlace R1–FortiGate | 10.21.40.128/30 | 255.255.255.252 | Conexión entre extremos de VPN |
| LAN remota | 10.21.40.136/28 | 255.255.255.240 | FortiGate Port2 y Usuario-2 |

## Equipos y direcciones

| Equipo | Interfaz | Dirección IPv4 | Puerta de enlace | Estado de comprobación |
|---|---|---|---|---|
| R1-SEDE (LAN) | FastEthernet0/1 | 10.21.40.1/25 | — | Verificada: up/up |
| R1-SEDE (hacia FortiGate) | FastEthernet0/0 | 10.21.40.129/30 | — | Verificada: up/up |
| SW-SEDE | VLAN 1 (administración) | 10.21.40.2/25 | 10.21.40.1 | Verificada: up/up y ping exitoso |
| WIN-AD-NPS | Ethernet | 10.21.40.10/25 | 10.21.40.1 | Verificada, estática |
| ZABBIX-SRV | ens3 | 10.21.40.20/25 | 10.21.40.1 | Verificada, estática |
| Usuario-1 (Windows) | Ethernet | 10.21.40.50/25 | 10.21.40.1 | Verificada por DHCP |
| FortiGate (enlace Cisco) | Port1 | 10.21.40.130/30 | — | Planificada; pendiente de prueba |
| FortiGate (LAN remota) | Port2 | 10.21.40.137/28 | — | Planificada; pendiente de prueba |
| Usuario-2 (Windows) | Ethernet | 10.21.40.138/28 | 10.21.40.137 | Planificada; pendiente de prueba |

Las direcciones del FortiGate y Usuario-2 son parte del plan y no se presentan como configuraciones verificadas. El túnel IPsec y la política de acceso entre LAN están pendientes.

## Conexiones físicas en GNS3

| Origen | Puerto | Destino | Puerto |
|---|---|---|---|
| R1-SEDE | FastEthernet0/0 | FortiGate | Port1 |
| R1-SEDE | FastEthernet0/1 | SW-SEDE | GigabitEthernet0/0 |
| SW-SEDE | GigabitEthernet0/1 | WIN-AD-NPS | Ethernet e0 |
| SW-SEDE | GigabitEthernet0/2 | ZABBIX-SRV | e0 (ens3) |
| SW-SEDE | GigabitEthernet0/3 | Usuario-1 | Ethernet e0 |
| FortiGate | Port2 | Usuario-2 | Ethernet e0 |

Se agregó temporalmente un nodo NAT de GNS3 conectado a la segunda interfaz de Ubuntu (e1) para instalar paquetes. Debe retirarse al finalizar las descargas y antes de la demostración final de la VPN.

## DHCP de LAN principal

- Servidor DHCP: R1-SEDE, 10.21.40.1.
- Pool: `LAN-USUARIOS`.
- Red: `10.21.40.0/25`.
- Direcciones excluidas: `10.21.40.1–10.21.40.49`.
- Rango dinámico: `10.21.40.50–10.21.40.126`.
- Puerta de enlace entregada: `10.21.40.1`.
- DNS observado inicialmente en Usuario-1: `8.8.8.8`.
- Concesión verificada: Usuario-1 recibió `10.21.40.50`; R1 confirmó la concesión mediante `show ip dhcp binding`.

El DNS del DHCP deberá actualizarse a `10.21.40.10` cuando el servicio DNS de Active Directory esté operativo, si los clientes se integrarán al dominio.

## Comprobaciones realizadas

- R1-SEDE: FastEthernet0/0 y FastEthernet0/1 en estado `up/up`.
- SW-SEDE: VLAN 1 en `up/up`; ping a `10.21.40.1` con 5/5 respuestas en la segunda prueba.
- Usuario-1: ping a `10.21.40.1` y `10.21.40.2` con 4/4 respuestas.
- WIN-AD-NPS: ping a router `10.21.40.1` y Usuario-1 `10.21.40.50` con 4/4 respuestas.
- ZABBIX-SRV: ping a `10.21.40.1` con 4/4 respuestas y respuestas de `10.21.40.2` y `10.21.40.10`.

## Nota de seguridad

No incluir contraseñas, secretos RADIUS, comunidades SNMP privadas ni claves VPN en los archivos públicos del repositorio.
