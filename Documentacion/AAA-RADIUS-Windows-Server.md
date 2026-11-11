# Windows Server — Active Directory, NPS y AAA/RADIUS

## Identificación del servidor

| Parámetro | Valor |
|---|---|
| Host | `WIN-AD-NPS` |
| IPv4 | `10.21.40.10/25` |
| Gateway | `10.21.40.1` |
| DNS | `10.21.40.10` (el propio servidor) |
| Dominio de laboratorio | `parcial.test` |
| Servicios | AD DS, DNS, Network Policy Server (NPS) |
| Cuenta usada en la prueba | `adminradius` |

## Configuración funcional realizada

1. Se asignó direccionamiento estático al servidor Windows y se comprobaron respuestas ICMP hacia R1 y otros nodos LAN.
2. Se configuró el dominio de laboratorio `parcial.test` y su usuario `adminradius`.
3. Se instaló y habilitó **Network Policy Server (NPS)**.
4. Se dio de alta el cliente RADIUS **R1-SEDE**, con IP `10.21.40.1` y secreto compartido privado.
5. Se definió la política de red `ACCESO-SSH-CISCO`, con autenticación PAP y atributo **Service-Type: Administrative** para permitir sesiones EXEC administrativas en este Cisco IOS antiguo.
6. Se configuraron reglas de firewall para permitir UDP **1812** (autenticación) y **1813** (accounting) desde R1.
7. En el router se habilitaron autenticación y autorización con `group radius local`, y accounting de sesiones EXEC con `group radius`.

## Comandos de verificación en R1

```cisco
show aaa servers
show aaa user all
show running-config | include aaa|radius-server|ip radius
```

Estas comprobaciones mostraron solicitudes RADIUS con éxitos y rechazos, asociación del usuario `adminradius` a la sesión EXEC y actividad de accounting. Desde Windows se verificó acceso SSH exitoso a R1 con la cuenta del dominio.

## Auditoría en el servidor

En **Visor de eventos → Vistas personalizadas → Roles de servidor → Servicios de acceso y directivas de redes** se comprobaron:

- **Evento 6272:** NPS concedió acceso a una solicitud de autenticación.
- **Evento 6273:** NPS denegó acceso a una solicitud de autenticación.

La coexistencia de ambos eventos permite evidenciar pruebas positivas y negativas del servicio AAA. La fecha/hora del router Cisco debe verificarse por separado: durante la práctica se detectó una discrepancia del reloj de IOS respecto a Windows.

## Precauciones

PAP fue utilizado por compatibilidad con el laboratorio y **no se recomienda como solución genérica de autenticación sin protección del transporte**. No incluir en GitHub contraseñas, secretos compartidos ni hashes sin necesidad. Las imágenes de Windows/NPS deben ser capturas auténticas de la práctica.

**Archivos de evidencia todavía no adjuntados al repositorio:** capturas de AD DS, usuario, cliente/política NPS y eventos 6272/6273. Ver [inventario](../Evidencias/README.md).
