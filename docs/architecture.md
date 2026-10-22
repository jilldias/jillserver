# Arquitetura

## Visão geral

O homelab é composto por um host Linux que executa serviços de arquivos, mídia e banco de dados. Podman é usado para aplicações em contêineres; Tailscale fornece conectividade privada; o firewall do host controla o tráfego permitido.

Este documento apresenta a arquitetura em nível lógico. Os endereços, nomes e caminhos usados nos exemplos são genéricos e não devem ser interpretados como uma cópia literal da configuração do host.

## Componentes

- **Host Linux:** sistema operacional e serviços básicos.
- **Podman:** ciclo de vida dos contêineres e rede de contêineres.
- **Nextcloud:** interface de nuvem pessoal e arquivos.
- **Jellyfin:** biblioteca de mídia.
- **MariaDB:** serviço de banco de dados.
- **Tailscale:** acesso privado a partir de dispositivos autorizados.
- **Firewall:** regras de entrada e encaminhamento.

## Fluxo lógico

1. Dispositivos autorizados conectam-se pela rede local ou pela rede privada.
2. O firewall limita o tráfego às portas e origens necessárias.
3. O acesso ao Nextcloud pode ser fornecido por um proxy HTTPS privado que encaminha ao serviço local.
4. O Jellyfin atende clientes autorizados por uma porta de aplicação.
5. Aplicações que precisam de banco de dados conectam-se à instância MariaDB por uma interface de rede explicitamente permitida.
6. Dados persistentes ficam em diretórios do host ou em volumes gerenciados.

## Exemplo de endereçamento

Os endereços abaixo são reservados para documentação ou são placeholders. Substitua-os apenas em uma cópia privada do documento, se for necessário registrar a configuração exata.

| Uso ilustrativo | Exemplo |
|---|---|
| Host em rede local | `192.0.2.10` |
| Endereço de serviço remoto de exemplo | `198.51.100.20` |
| Outro endereço de exemplo | `203.0.113.30` |
| Rede de contêineres de exemplo | `198.51.100.0/24` |

## Persistência e inicialização

Para cada contêiner, documente a imagem, as portas publicadas, os volumes, a política de reinício e o método que garante a inicialização após reboot. Não presuma que uma política de reinício isolada garanta a retomada do serviço; valide o comportamento no ambiente.

## Limites

Este documento não divulga o endereço real do host, o nome completo do tailnet, endereços reais de contêineres ou identificadores de dispositivos. Detalhes sensíveis devem ficar em documentação privada protegida, não em um repositório público.
