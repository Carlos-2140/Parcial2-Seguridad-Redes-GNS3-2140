# VPN Site-to-Site — Cisco R1 y FortiGate

## Objetivo

Permitir tráfico entre la LAN de sede `10.21.40.0/25` y la LAN remota `10.21.40.136/29` únicamente cuando el túnel IPsec esté operativo. La administración del túnel en FortiGate se realizó mediante la GUI.

## Extremos y rutas

| Elemento | Dirección / configuración |
|---|---|
| Router Cisco R1-SEDE, Fa0/0 | `10.21.40.129/30` |
| FortiGate, port1 | `10.21.40.130/30` |
| LAN Cisco | `10.21.40.0/25` |
| FortiGate, port2 | `10.21.40.137/29` |
| Usuario-2 | `10.21.40.138/29`, puerta de enlace `10.21.40.137` |
| Ruta estática en R1 | `10.21.40.136/29 via 10.21.40.130` |

Se corrigió el prefijo de la red remota a `/29` para eliminar el solapamiento de la propuesta previa con la red de tránsito `/30`.

## Parámetros del túnel observados

| Elemento | Valor |
|---|---|
| Nombre del túnel FortiGate | `VPN-CISCO` |
| IKE | IKEv1 |
| Negociación IKE | DES, SHA-1, grupo DH 2 |
| IPsec ESP | DES + HMAC-SHA1 |
| PFS | Desactivado |
| Selectores | `10.21.40.0/25` ↔ `10.21.40.136/29` |
| Cisco | `crypto map VPN-MAP`, `VPN-TS`, ACL 110 |
| NAT entre subredes del túnel | No habilitado en las políticas VPN observadas |

Las propuestas criptográficas corresponden a las capacidades de las imágenes utilizadas en el laboratorio. **DES, SHA-1 y DH2 son tecnologías obsoletas y no deben reutilizarse en producción.** La clave precompartida no se reproduce en este documento.

## Prueba de funcionamiento

1. En la GUI de FortiGate, observar `VPN-CISCO` activo en **Dashboard → Network → IPsec Monitor**.
2. En R1, verificar `show crypto isakmp sa`: sesión `QM_IDLE` / activa.
3. En R1, verificar `show crypto ipsec sa`: SAs ESP activas y contadores de tráfico cifrado y descifrado mayores que cero.
4. Desde Usuario-1, realizar ping a `10.21.40.138`; se verificaron respuestas **4/4** con el túnel activo.
5. Desde la GUI de FortiGate, usar **Bring Down** y comprobar el estado `Inactive`; el ping registró **0/4** respuestas durante la prueba.
6. Restablecer el túnel con **Bring Up**; la conectividad volvió después de la renegociación.

**Evidencia pendiente de adjuntar al repositorio:** capturas auténticas del monitor IPsec en estados activo e inactivo, comandos Cisco con SAs y terminales Windows con ping exitoso/fallido. Ver [inventario de evidencias](../Evidencias/README.md).
