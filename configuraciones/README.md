# Configuraciones individuales de equipos de red

Se mantendrá un archivo por equipo conforme al requisito de entrega:

- `R1-SEDE.txt`: router Cisco, direccionamiento, DHCP, SSH, hardening y, cuando estén verificados, AAA y VPN.
- `SW-SEDE.txt`: switch Cisco IOSvL2, administración, puertos, SSH, SNMP y hardening.
- `FortiGate.txt`: configuración relevante exportada/documentada desde la GUI FortiGate 7.0.9, una vez implementada y comprobada la VPN.

Se agregarán los archivos a partir de las configuraciones **reales** exportadas de los equipos. No se generarán archivos que simulen configuraciones no ejecutadas.

Antes de subir cualquier configuración a este repositorio público se deben suprimir los secretos de RADIUS, contraseñas, hashes, comunidades SNMP privadas y claves precompartidas IPsec. La configuración original completa se guarda fuera del repositorio público.
