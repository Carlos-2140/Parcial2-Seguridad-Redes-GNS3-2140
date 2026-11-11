# FortiGate 7.0.9 — VPN con Cisco R1

La configuración se realizó desde la **interfaz gráfica de FortiGate**, como exige el laboratorio.

| Elemento | Valor |
|---|---|
| Interfaz de enlace | `port1` — `10.21.40.130/30` |
| LAN de usuario remoto | `port2` — `10.21.40.137/29` |
| Túnel | `VPN-CISCO` |
| Red local protegida | `10.21.40.136/29` |
| Red remota protegida | `10.21.40.0/25` |
| Autenticación | Clave precompartida, omitida |
| IKE | IKEv1, DES/SHA-1/DH2 (limitación del laboratorio) |
| IPsec | ESP-DES con SHA-1; PFS desactivado |

Las rutas y las políticas de firewall permitieron tráfico entre los dos segmentos **sin NAT**, condicionado al túnel. El monitor IPsec mostró el estado activo, posteriormente inactivo al utilizar **Bring Down**, y activo de nuevo mediante **Bring Up**. La prueba ICMP entre usuarios confirmó la pérdida y recuperación de conectividad.

## Documentación

[Ver parámetros, rutas y comprobaciones de VPN](../Documentacion/VPN-IPsec.md).

## Evidencias pendientes de archivo

- Monitor IPsec: túnel `Up`.
- Comandos Cisco: `QM_IDLE` y contadores de tráfico cifrado.
- Ping entre redes cuando la VPN está activa.
- Monitor `Inactive` y ping sin respuesta.
- Monitor nuevamente `Up` y ping recuperado.

**Precaución:** la clave precompartida no debe mostrarse en capturas ni en copias públicas de la configuración. El cifrado DES/SHA-1 y DH2 no son apropiados para producción.
