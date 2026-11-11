# Configuración de Windows Server — Active Directory y NPS

**Servidor:** WIN-AD-NPS · **IP:** `10.21.40.10/25` · **Gateway:** `10.21.40.1` · **Dominio:** `parcial.test`.

## Servicios implementados

- **Active Directory Domain Services (AD DS)** y DNS.
- **Network Policy Server (NPS)** como servidor RADIUS para la autenticación administrativa del router `R1-SEDE`.
- Usuario de dominio de prueba `adminradius`.
- Cliente RADIUS con dirección `10.21.40.1` y puertos UDP `1812` / `1813`.
- Política `ACCESO-SSH-CISCO`, con atributo **Administrative**.
- Registro de sesiones aceptadas y denegadas en el Visor de eventos: **6272** y **6273**.

## Evidencias originales

Durante el laboratorio se recopilaron capturas de la configuración y las pruebas de Windows Server y se preparó un documento Word de evidencias. Las capturas y el Word deben subirse aquí o a `Evidencias/` para que queden accesibles desde GitHub. **Todavía no se encuentran en este repositorio**.

## Detalle técnico

[Ver documentación completa de Active Directory, NPS y AAA/RADIUS](../Documentacion/AAA-RADIUS-Windows-Server.md).

No publicar contraseñas, claves compartidas RADIUS ni datos privados del dominio.
