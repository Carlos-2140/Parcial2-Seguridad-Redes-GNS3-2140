# Registro de evidencias visuales

Las imágenes deben ser capturas **auténticas**, sin modificaciones que alteren sus resultados. Se organizarán por requisito y se incrustarán en el README principal una vez que los archivos PNG estén incorporados al repositorio.

## Capturas ya producidas durante la práctica

| Carpeta propuesta | Nombre del archivo | Contenido observado |
|---|---|---|
| `Direccionamiento/` | `01_Router_Interfaces.png` | FastEthernet0/0 y FastEthernet0/1 en estado up/up |
| `Direccionamiento/` | `02_Switch_Conectividad.png` | VLAN 1 10.21.40.2 y ping exitoso a R1 |
| `DHCP/` | `03_DHCP_Windows.png` | Usuario-1 recibió 10.21.40.50 por DHCP |
| `DHCP/` | `04_DHCP_Router.png` | Concesión de 10.21.40.50 en R1 |
| `Direccionamiento/` | `05_Conectividad_LAN.png` | Usuario-1 alcanza router y switch |
| `Direccionamiento/` | `06_Windows_Server_IP.png` | WIN-AD-NPS 10.21.40.10/25 estática |
| `Direccionamiento/` | `07_Zabbix_IP_Conectividad.png` | ZABBIX-SRV 10.21.40.20/25 y pruebas ping |
| `SSH/` | `08_Router_SSH_Config.png` | SSHv2 y VTY solo SSH |
| `SSH/` | `09_Router_SSH_Acceso.png` | Acceso SSH exitoso desde Windows a R1 |
| `SSH/` | `11_Switch_SSH_Acceso.png` | Acceso SSH exitoso desde Windows a SW-SEDE |
| `SSH/` | `12_Telnet_Bloqueado.png` | TCP/23 no disponible en R1 y SW-SEDE |
| `SNMP-Zabbix/` | `13_Switch_SNMP_Config.png` | Comunidad SNMP restringida a 10.21.40.20 |
| `SNMP-Zabbix/` | `15_Zabbix_SNMP_Disponibilidad.png` | Indicador SNMP verde en Zabbix |
| `SNMP-Zabbix/` | `16_Zabbix_SNMP_LatestData.png` | Contacto, ubicación, nombre y uptime del switch |

Los nombres son convenciones de archivo para organizar las capturas existentes, no enlaces a imágenes ya cargadas. Las capturas todavía deben incorporarse al repositorio.

## Evidencias todavía pendientes

- FortiGate por GUI: túnel VPN operativo y caída de comunicación al desactivar VPN.
- Active Directory/NPS: dominio, cliente RADIUS, política y registros de accesos exitoso y fallido.
- Hardening adicional aplicado y demostrado.
- Topología final con interfaces, y video de YouTube con fecha/hora, rostro y voz.
