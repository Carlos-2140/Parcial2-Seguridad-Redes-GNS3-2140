# Configuración de Zabbix — Ubuntu Server

**Servidor:** ZABBIX-SRV · **Ubuntu:** 24.04.5 LTS · **Zabbix:** 7.0 LTS · **IP:** 10.21.40.20/25

## Implementación

El servicio de monitoreo se instaló en Ubuntu Server con **Zabbix Server, Zabbix Agent, MariaDB y Apache**. Se utilizó temporalmente acceso a NAT en una segunda interfaz para instalar los paquetes.

El switch `SW-SEDE` (`10.21.40.2`) quedó registrado en Zabbix utilizando **SNMPv2c**, comunidad de solo lectura y lista de acceso que limita las consultas al servidor `10.21.40.20`.

## Comprobaciones

- Servicios `mariadb`, `zabbix-server`, `zabbix-agent` y `apache2` en estado `active`.
- Disponibilidad SNMP del switch con indicador verde en Zabbix.
- Lectura de datos reales: `System name`, `System contact`, `System location`, `System description` y `Uptime`.

## Documentos

- [Procedimiento y comandos de instalación](../Scripts/ZABBIX-SRV_Instalacion_Config.txt)
- [Configuración de SNMP y comprobaciones](../Documentacion/Zabbix-SNMP.md)
- [Inventario de capturas por incorporar](../Evidencias/README.md)

Cuando se agregue el informe de imágenes reales, puede publicarse aquí como `Configuracion_Zabbix.pdf`. El archivo **no está cargado actualmente** en esta carpeta.
