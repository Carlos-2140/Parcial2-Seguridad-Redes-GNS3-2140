# Parcial 2 — Seguridad de Redes en GNS3

Laboratorio de infraestructura con router Cisco R1-SEDE, switch Cisco IOSvL2 SW-SEDE, FortiGate 7.0.9, Windows Server (Active Directory y NPS), Ubuntu Server (Zabbix) y dos clientes Windows.

## Documentación

- [Direccionamiento y conexiones físicas](Direccionamiento/README.md)
- [Hardening implementado y comprobaciones](Hardening-CIS/README.md)
- [Inventario de evidencias](imagenes/README.md)
- [Configuraciones de equipos de red](Show%20Running-config)

## Estado de implementación

| Requisito | Resultado comprobado |
|---|---|
| VPN Cisco–FortiGate | Verificado: IKE QM_IDLE, ESP activo, encaps 19 y decaps 16; ping exitoso entre LAN; caída tras Bring Down en GUI y recuperación tras Bring Up |
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

**FortiGate:** port1 10.21.40.130/30 y port2 10.21.40.137/29, verificados; LAN remota 10.21.40.136/29. Se corrigió el prefijo original /28 para evitar solapamiento con la WAN. VPN IPsec configurada con IKEv1, DES/SHA1 por limitación de la VM; túnel probado activo/inactivo/restaurado. Estos algoritmos son obsoletos y no equivalen a hardening CIS.

**Cliente Usuario-1:** Windows, dirección 10.21.40.50 por DHCP, pruebas de conectividad exitosas.

## Evidencias y demostración

Las imágenes originales deben incorporarse en la carpeta [imagenes](imagenes/README.md) y mostrarse incrustadas en este README una vez subidas. El video de demostración se incorporará al inicio cuando esté publicado en YouTube.

La VPN se probó activa, caída desde el monitor de FortiGate y restaurada. RADIUS/NPS registró eventos 6272 y 6273, y Cisco mostró solicitudes de accounting exitosas. Los archivos PNG originales siguen pendientes de incorporación al repositorio; no se representan como subidos.

## Seguridad de la documentación

No se publican contraseñas, hashes de autenticación, secretos compartidos RADIUS o IPsec, ni claves privadas. La publicación de configuraciones completas requiere sustituir estos valores por su descripción y conservar los archivos íntegros en un respaldo privado.

## Pruebas recientes de VPN y AAA/RADIUS

- VPN-CISCO: FortiGate GUI mostró `Up`, luego `Inactive` tras `Bring Down` y posteriormente `Up` tras restablecerla.
- Con VPN activa: ping Usuario-1 (10.21.40.50) a Usuario-2 (10.21.40.138) 4/4 antes de la caída; después de restaurarla 3/4 (primer paquete sin respuesta).
- Tras bajar el túnel: ping Usuario-1 a Usuario-2 con 0/4 respuestas. Esta secuencia documenta dependencia del túnel IPsec; la caída temporal por Bring Down no equivale a deshabilitación administrativa permanente.
- Cisco R1: `show crypto isakmp sa` mostró `QM_IDLE ACTIVE`; `show crypto ipsec sa` mostró 19 encapsulados y 16 desencapsulados, SAs ESP activas.
- NPS: eventos Windows Security 6272 (concedido) y 6273 (denegado); acceso SSH con `adminradius` exitoso. Cisco: accounting 5 solicitudes y 5 éxitos, `show aaa user all` mostró sesión EXEC por RADIUS.

- Comprobación adicional después de la restauración de VPN-CISCO: ping de Usuario-1 a 10.21.40.138 con 4/4 respuestas (0 % pérdida, media de 18 ms). Captura original identificada como `37_VPN_Restaurada.png`; pendiente incorporarla como archivo de imagen al repositorio.
