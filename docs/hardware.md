# Hardware e sistema operacional

## Objetivo

Registrar as características relevantes para entender o dimensionamento do homelab, sem expor identificadores exclusivos do equipamento.

## Inventário público

| Item | Descrição |
|---|---|
| Tipo de equipamento | Notebook reaproveitado como servidor |
| Arquitetura | x86-64 |
| Sistema operacional | Debian GNU/Linux 13 (trixie), conforme inventário de referência |
| Kernel | Versão exata omitida do documento público |
| CPU, memória e armazenamento | Equipamento de baixo consumo e recursos limitados; valores exatos omitidos |

O fabricante, modelo detalhado, número de série, UUID e demais identificadores físicos não são necessários para explicar a arquitetura pública e foram omitidos.

## Coleta local

Os comandos abaixo podem ser executados no próprio servidor para manutenção privada:

```bash
hostnamectl
lscpu
free -h
lsblk -o NAME,SIZE,FSTYPE,MOUNTPOINTS
df -hT
uptime
```

Antes de publicar qualquer saída, remova nome do host, números de série, UUIDs, nomes de usuário, identificadores de volume e outros dados que possam identificar o ambiente.
