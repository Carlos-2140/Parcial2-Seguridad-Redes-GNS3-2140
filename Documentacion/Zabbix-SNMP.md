# Monitoreo SNMP — Ubuntu Server, Zabbix y Cisco IOSvL2

## Arquitectura

- **ZABBIX-SRV:** Ubuntu Server 24.04.5 LTS, `10.21.40.20/25`, gateway `10.21.40.1`.
- **SW-SEDE:** Cisco IOSvL2, IP de administración VLAN 1 `10.21.40.2/25`.
- **Zabbix:** serie 7.0 LTS; servicios de Zabbix Server, Agent, MariaDB y Apache.
- **Comunicación de monitoreo:** SNMPv2c en UDP 161, comunidad de solo lectura y lista de control de acceso.

## Restricción SNMP en Cisco

La configuración del switch incorpora ACL 10 con el origen autorizado:

```cisco
access-list 10 permit 10.21.40.20
snmp-server community <COMUNIDAD_PRIVADA> RO 10
snmp-server location LAB-GNS3
snmp-server contact Administrador-Red
```

El nombre real de la comunidad se oculta aquí por seguridad. En SNMPv2c una comunidad equivale a una credencial compartida y **no cifra el tráfico**.

## Instalación y servicios

El procedimiento documentado de instalación, repositorio Zabbix, MariaDB, importación del esquema, configuración del frontend y verificación de servicios está en [Scripts/ZABBIX-SRV_Instalacion_Config.txt](../Scripts/ZABBIX-SRV_Instalacion_Config.txt). El TXT es una guía de los pasos realizados, no un historial automático de Bash.

Pruebas documentadas:

```bash
sudo systemctl is-active mariadb zabbix-server zabbix-agent apache2
snmpget -v2c -c '<COMUNIDAD_PRIVADA>' 10.21.40.2 1.3.6.1.2.1.1.5.0
snmpget -v2c -c '<COMUNIDAD_PRIVADA>' 10.21.40.2 1.3.6.1.2.1.1.3.0
```

El host `SW-SEDE` fue agregado a la web de Zabbix (`http://10.21.40.20/zabbix`) con dirección `10.21.40.2`, interfaz SNMP y plantilla **Cisco IOS by SNMP**.

## Resultado comprobado

Los servicios aparecieron **active**, el indicador SNMP de Zabbix se mostró en verde y se observaron valores de **System name, System contact, System location, System description y Uptime**. Falta adjuntar al repositorio las capturas originales de la pantalla de host y sus últimos datos.

La interfaz NAT adicional de Ubuntu se utilizó temporalmente para instalación de paquetes; no forma parte de la ruta de producción prevista del laboratorio.
