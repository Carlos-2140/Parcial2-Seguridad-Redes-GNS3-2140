# Evidencias del laboratorio

**Estado:** inventario documental. Las capturas originales aún **no están cargadas en esta carpeta**. No se presentan enlaces de imagen inexistentes.

## Evidencias para incorporar

| Archivo sugerido | Qué debe verse | Requisito |
|---|---|---|
| `01-topologia-gns3.png` | Vista completa de R1, switch, FortiGate y las cuatro máquinas | Topología |
| `02-dhcp-usuario1.png` | `ipconfig /all` con `10.21.40.50` y gateway `10.21.40.1` | DHCP |
| `03-dhcp-router.png` | `show ip dhcp binding` en R1 | DHCP |
| `04-ssh-router-switch.png` | Acceso SSH autorizado y pruebas de Telnet denegadas | SSH |
| `05-vpn-activa.png` | Monitor IPsec de FortiGate en estado `Up` | VPN |
| `06-vpn-isakmp-ipsec.png` | `QM_IDLE` y contadores IPsec en R1 | VPN |
| `07-vpn-ping-activa.png` | Comunicación Usuario-1 ↔ Usuario-2 con túnel activo | VPN |
| `08-vpn-inactiva.png` | Monitor FortiGate `Inactive` y ping sin respuesta | VPN |
| `09-zabbix-snmp.png` | Switch en Zabbix, indicador SNMP verde y valores recientes | SNMP |
| `10-nps-cliente-politica.png` | Cliente RADIUS y política `ACCESO-SSH-CISCO` en NPS | AAA |
| `11-nps-evento-6272.png` | Solicitud aceptada en Visor de eventos | AAA |
| `12-nps-evento-6273.png` | Solicitud rechazada en Visor de eventos | AAA |
| `13-aaa-router.png` | `show aaa servers` / `show aaa user all` | AAA |
| `14-hardening-router.png` | Configuración segura SSH, HTTP deshabilitado y timeout | CIS |
| `15-hardening-switch.png` | Configuración segura SSH, HTTP deshabilitado y SNMP ACL | CIS |

## Reglas de presentación

1. Utilizar **solo capturas reales** obtenidas en GNS3, Windows, FortiGate, Ubuntu y Zabbix.
2. Nombrar cada PNG de forma descriptiva y colocarla aquí.
3. Mostrar contexto suficiente para verificar dirección IP, equipo, comando/GUI y resultado.
4. Evitar secretos visibles: contraseñas, PSK, comunidad SNMP y claves RADIUS.
5. Tras cargarlas, insertar las imágenes dentro del **README principal** mediante Markdown (por ejemplo, `![VPN activa](Evidencias/05-vpn-activa.png)`).
6. Si se adjunta el documento Word de Windows Server, debe mantener sus imágenes originales e identificar que es documentación complementaria, no evidencia sustituida.


## Paquete de capturas originales identificado en el chat

Se han seleccionado **23 archivos de evidencia** (incluida una copia DOCX de Windows Server) y un archivo de instrucciones en un paquete ZIP de transferencia, **todavía no incorporado al repositorio**. La separación sigue el esquema de carpetas del laboratorio de referencia:

| Carpeta destino | Archivos preparados | Descripción |
|---|---|---|
| `Topologia/` | `Topologia.png` | Captura original del escenario GNS3 del segundo parcial |
| `Evidencias/Windows-Server/` | `WS-01.png` a `WS-15.png` | Capturas originales de IP, AD DS, usuarios, NPS y RADIUS |
| `Evidencias/` | `Evidencias_Windows_Server_AD_NPS_Sin_Fuentes.docx` | Documento Word con 15 evidencias auténticas |
| `Evidencias/VPN/` | `VPN-Up.png`, `VPN-Inactive.png`, `VPN-Politicas.png` | Estados VPN-CISCO activo/inactivo y políticas FortiGate sin NAT |
| `Evidencias/Zabbix/` | `Zabbix-Host.png`, `Zabbix-SNMP.png`, `Zabbix-Latest-Data.png` | Capturas de la consola web de monitoreo |

El archivo ZIP está preparado como artefacto de la conversación; GitHub no muestra estas imágenes hasta subir los archivos extraídos. Una vez presentes, se incrustarán individualmente en el README principal con pies de figura y sin imágenes generadas.
