# Parcial 2 — Seguridad de Redes en GNS3

Laboratorio de infraestructura con router Cisco R1-SEDE, switch Cisco IOSvL2 SW-SEDE, FortiGate 7.0.9, Windows Server (Active Directory y NPS), Ubuntu Server (Zabbix) y dos clientes Windows.

## Documentación

- [Direccionamiento y conexiones físicas](Direccionamiento/README.md)
- [Hardening implementado y comprobaciones](Hardening-CIS/README.md)
- [Inventario de evidencias](imagenes/README.md)
- [Configuraciones de equipos de red](configuraciones/README.md)

## Estado de implementación

| Requisito | Resultado comprobado |
|---|---|
| VPN Cisco–FortiGate | Pendiente de configurar y demostrar |
| DHCP en router | Verificado: Usuario-1 recibió 10.21.40.50/25 desde 10.21.40.1 |
| SSH router y switch | Verificado: acceso remoto por SSHv2 en ambos; Telnet TCP/23 rechazado |
| Direccionamiento y conectividad | Verificada la LAN principal; pendiente la red remota |
| SNMP y Zabbix | Verificado: SNMP disponible y valores reales del switch recibidos en Zabbix |
| Configuraciones individuales y evidencias | En preparación |
| Hardening CIS | Controles implementados documentados; revisión y pruebas finales pendientes |
| AAA/RADIUS | Windows Server en proceso de configuración; pruebas pendientes |

## Resumen de servicios comprobados

**Router R1-SEDE:** FastEthernet0/1 10.21.40.1/25, FastEthernet0/0 10.21.40.129/30; DHCP en LAN y SSHv2.

**Switch SW-SEDE:** VLAN 1 10.21.40.2/25; SSHv2, solo SSH en VTY; SNMPv2c de lectura restringido a 10.21.40.20.

**Windows Server WIN-AD-NPS:** 10.21.40.10/25, gateway 10.21.40.1; conectividad comprobada. El servicio RADIUS todavía requiere pruebas de autenticación.

**Ubuntu ZABBIX-SRV:** 10.21.40.20/25; aplicación Zabbix 7.0 y sus servicios en ejecución; datos SNMP recientes de SW-SEDE visibles en la interfaz.

**Cliente Usuario-1:** Windows, dirección 10.21.40.50 por DHCP, pruebas de conectividad exitosas.

## Evidencias y demostración

Las imágenes originales deben incorporarse en la carpeta [imagenes](imagenes/README.md) y mostrarse incrustadas en este README una vez subidas. El video de demostración se incorporará al inicio cuando esté publicado en YouTube.

No se presentan pruebas de VPN, RADIUS ni hardening adicional como concluidas hasta realizar las verificaciones.

## Seguridad de la documentación

No se publican contraseñas, hashes de autenticación, secretos compartidos RADIUS o IPsec, ni claves privadas. La publicación de configuraciones completas requiere sustituir estos valores por su descripción y conservar los archivos íntegros en un respaldo privado.
