# Topología del laboratorio — Segundo parcial

## Diagrama y captura de GNS3

El laboratorio utiliza el router **R1-SEDE**, el switch **SW-SEDE**, un **FortiGate 7.0.9**, un servidor Windows **WIN-AD-NPS**, un servidor Ubuntu **ZABBIX-SRV** y dos clientes.

La captura auténtica del lienzo de GNS3 recibida durante la práctica está disponible en la conversación y debe almacenarse en esta carpeta como `Topologia.png`. El diagrama complementario puede guardarse como `Diagrama.png`; se debe indicar que es un diagrama esquemático, no una captura de GNS3. **Los archivos gráficos todavía no se han incorporado aquí**.

## Conexiones físicas

| Dispositivo origen | Puerto | Dispositivo destino | Puerto |
|---|---|---|---|
| R1-SEDE | FastEthernet0/0 | FortiGate | port1 |
| R1-SEDE | FastEthernet0/1 | SW-SEDE | GigabitEthernet0/0 |
| SW-SEDE | GigabitEthernet0/1 | WIN-AD-NPS | e0 |
| SW-SEDE | GigabitEthernet0/2 | ZABBIX-SRV | e0 / ens3 |
| SW-SEDE | GigabitEthernet0/3 | Usuario-1 | e0 |
| FortiGate | port2 | Usuario-2 | e0 |

## Esquema lógico

```mermaid
flowchart TB
    R["R1-SEDE<br/>Fa0/1: 10.21.40.1/25<br/>Fa0/0: 10.21.40.129/30"]
    F["FortiGate 7.0.9<br/>port1: 10.21.40.130/30<br/>port2: 10.21.40.137/29"]
    S["SW-SEDE<br/>VLAN 1: 10.21.40.2/25"]
    W["WIN-AD-NPS<br/>10.21.40.10/25"]
    Z["ZABBIX-SRV<br/>10.21.40.20/25"]
    U1["Usuario-1<br/>10.21.40.50/25"]
    U2["Usuario-2<br/>10.21.40.138/29"]
    R --- F
    R --- S
    S --- W
    S --- Z
    S --- U1
    F --- U2
```

**VPN:** `10.21.40.0/25` ↔ `10.21.40.136/29`.

Para el plan de redes y las pruebas de conectividad, consultar [Direccionamiento](../Direccionamiento/README.md).
