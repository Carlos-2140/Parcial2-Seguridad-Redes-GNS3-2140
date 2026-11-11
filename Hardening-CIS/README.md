# Hardening de red — controles implementados

Este documento relaciona medidas de endurecimiento presentes en el laboratorio con principios de los CIS Benchmarks para plataformas Cisco. No constituye una certificación de cumplimiento integral. La correspondencia exacta de controles debe validarse con la versión del benchmark aplicable a las imágenes IOS empleadas.

| Medida | Equipo | Motivo | Evidencia técnica observada |
|---|---|---|---|
| Acceso remoto mediante SSHv2 | R1-SEDE y SW-SEDE | Evitar transmitir credenciales administrativas por Telnet | `show ip ssh` indicó versión 2.0; acceso desde Windows exitoso a 10.21.40.1 y 10.21.40.2 |
| Restringir protocolos en VTY | R1-SEDE y SW-SEDE | Reducir superficie de ataque de administración | `transport input ssh`, `login local` en líneas VTY |
| Caducidad por inactividad en sesiones | R1-SEDE y SW-SEDE | Limitar sesiones administrativas desatendidas | `exec-timeout 5 0` en VTY |
| Usuario local con secreto no almacenado en texto claro | R1-SEDE y SW-SEDE | Evitar contraseña legible en configuración | `username admin privilege 15 secret 5 ...` observado; no se publica el hash |
| Servicio SNMP restringido al servidor de monitoreo | SW-SEDE | Reducir equipos que pueden consultar información de gestión | Comunidad `RO` vinculada a ACL 10: `permit host 10.21.40.20` |
| Deshabilitar Telnet en administración | R1-SEDE y SW-SEDE | Bloquear autenticación administrativa sin cifrado | `Test-NetConnection` desde 10.21.40.50 al puerto 23 devolvió `TcpTestSucceeded : False` para ambas IP |

## Limitaciones identificadas

- El router R1-SEDE negoció SSH mediante algoritmos antiguos (`diffie-hellman-group1-sha1`, `ssh-rsa`, `aes128-cbc`). Su uso se limitó al cliente de la práctica GNS3. **No equivale a endurecimiento criptográfico conforme a estándares actuales.**
- Las contraseñas `secret 5` utilizan un hash heredado tipo 5; si la plataforma permite `secret 8` o `secret 9`, resulta preferible migrar a un algoritmo más robusto.
- SNMPv2c usa comunidad sin cifrado en tránsito. Una lista de acceso limita las fuentes, pero SNMPv3 sería preferible si el requisito y la plataforma lo permitieran.
- Actualmente la IP de administración del switch está en VLAN 1. Una VLAN dedicada de administración y restricciones adicionales mediante ACL son mejoras pendientes de evaluar.
- Aún se deben documentar y probar las medidas de registros AAA/RADIUS, protección de contraseñas y restricciones adicionales que efectivamente sean aplicadas.

## Pruebas de funcionamiento

Las evidencias originales de SSH, rechazo de Telnet y SNMP/Zabbix se incorporarán en [imagenes](../imagenes/README.md). Se documentará únicamente lo que se haya ejecutado y observado en el entorno GNS3.

## Verificación adicional en R1-SEDE

Captura de consola del 11/11/2026: `show run | include service password-encryption` devolvió `service password-encryption`; `show run | include ip http` devolvió `no ip http server` y `no ip http secure-server`; `show run | include ip source-route` devolvió `no ip source-route`. Se verificó la presencia de estas directivas en configuración. La captura original se identificó como `38_Hardening_Router.png` y aún debe incorporarse como imagen a GitHub.

Estas medidas reducen exposición de servicios de administración y evitan opciones de enrutamiento de origen, pero `service password-encryption` usa ofuscación reversible para contraseñas tipo 7 y no sustituye hashes robustos.
