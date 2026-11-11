# Hardening de red — Controles inspirados en CIS Benchmarks

## Alcance

Se documentan medidas reales de endurecimiento del router Cisco y el switch IOSvL2. La presencia de controles seleccionados **no equivale a una auditoría completa ni a certificación CIS**; los resultados deben contrastarse con el benchmark aplicable a la versión de IOS correspondiente.

## Medidas observadas

| Control | R1-SEDE | SW-SEDE | Objetivo |
|---|---|---|---|
| `service password-encryption` | Sí | Sí | Evitar contraseñas de texto claro en ciertos campos de configuración (ofuscación reversible, no cifrado fuerte) |
| `no ip source-route` | Sí | Sí | Reducir manipulación de rutas desde paquetes IP |
| `no ip http server` / `no ip http secure-server` | Sí | Sí | Eliminar administración web innecesaria |
| `ip ssh version 2` | Sí | Sí | Administración mediante SSHv2 |
| `transport input ssh` | Sí | Sí | Excluir Telnet de líneas VTY |
| `exec-timeout 5 0` en VTY | Sí | Sí | Cerrar sesiones administrativas remotas inactivas |
| Usuarios locales con `secret 5` | Sí | Sí | Credenciales locales sin contraseña literal en el comando (hash MD5 heredado) |
| SNMP `RO` limitado por ACL | No aplica | Sí, origen `10.21.40.20` | Restringir origen autorizado de monitoreo |
| AAA con NPS | Sí | No | Autenticación remota centralizada y registros |

## Verificación recomendada

```cisco
show running-config | include service password-encryption|no ip source-route|no ip http|ip ssh version
show running-config | section line vty
show ip ssh
```

En el switch también:

```cisco
show access-lists 10
show snmp
```

### Limitaciones detectadas y pendientes

- El router usa un IOS 12.4 antiguo y el switch IOSvL2 15.2; ambos tienen restricciones de algoritmos y compatibilidad.
- Las contraseñas locales en formato **secret 5 (MD5)** son heredadas.
- La VPN de laboratorio negoció DES, SHA-1 y DH2 por compatibilidad con FortiGate 7.0.9 sin licencia. Estos algoritmos **no se consideran seguros para producción**.
- SNMPv2c usa comunidad sin cifrado; en redes reales priorizar SNMPv3 autenticado y cifrado.
- La gestión del switch está en **VLAN 1**, no en VLAN de administración separada.
- Las líneas de consola/auxiliar del router muestran `exec-timeout 0 0`; no deben confundirse con el límite de cinco minutos ya aplicado en VTY.
- Las interfaces físicas sin uso del switch no figuran como administrativamente deshabilitadas en el running-config proporcionado.
- La advertencia `CDP-4-DUPLEX_MISMATCH` surgió entre R1 Fa0/1 (10 Mb/s, half-duplex) y Gi0/0 del switch con autonegociación. No se observaron errores CRC ni colisiones en la comprobación compartida; permanece como advertencia del entorno virtual, **no se afirma que haya sido corregida**.
- `no cdp log mismatch duplex` suprime avisos, pero **no corrige** el estado físico/virtual de la negociación.

## Evidencia requerida

Añadir capturas auténticas de los comandos del apartado de verificación y pruebas de SSH aceptado/Telnet rechazado. No sustituir evidencia real por salida de terminal escrita a mano.
