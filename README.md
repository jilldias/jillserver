<img src="assets/jillserver-logo.png" alt="Identidade visual JS 1.0 do Jillserver" width="280">

# Jillserver

**Servidor doméstico · Debian · Infraestrutura autogerenciada**

Um laboratório pessoal para hospedar serviços, administrar sistemas Linux e explorar soluções de armazenamento e mídia em uma infraestrutura própria.

[Arquitetura](#arquitetura) · [Serviços](#serviços) · [Segurança](#segurança-e-acesso) · [Operação](#operação-e-manutenção) · [Próximos passos](#próximos-passos)

</div>

---

## Visão geral

O **Jillserver** é um servidor doméstico construído a partir de um notebook reaproveitado e administrado com **Debian GNU/Linux**, sem depender de uma interface gráfica local. O projeto combina serviços autohospedados, gerenciamento de contêineres, acesso remoto privado e práticas de administração de sistemas.

Além de atender a necessidades pessoais, o servidor funciona como um laboratório prático para estudar Linux, redes, segurança, armazenamento, implantação e manutenção de serviços.

## Arquitetura

```text
                         Dispositivos autorizados
                                   |
                             Rede privada
                               Tailscale
                                   |
                            +--------------+
                            |  jillserver  |
                            | Debian Linux |
                            +--------------+
                                   |
                 +-----------------+-----------------+
                 |                 |                 |
              Podman          Armazenamento      Serviços do host
                 |                                   |
          +------+-------+                       SSH / rede
          |              |
      Nextcloud        Jellyfin
      Arquivos       Filmes e mídia
```

> Diagrama conceitual. Não representa todas as regras de rede nem todos os detalhes de implantação.

## Serviços

| Componente | Finalidade |
|---|---|
| **Debian GNU/Linux** | Sistema operacional do servidor, administrado em modo headless. |
| **Podman** | Execução e isolamento de aplicações em contêineres. |
| **Nextcloud** | Acesso e gerenciamento de arquivos por uma interface web e clientes compatíveis. |
| **Jellyfin** | Organização e reprodução de filmes e outros conteúdos de mídia em dispositivos compatíveis. |
| **Tailscale** | Conectividade privada entre dispositivos autorizados e o servidor. |
| **OpenSSH** | Administração remota por terminal. |
| **nftables** | Ferramenta de filtragem de tráfego utilizada no gerenciamento de regras de rede. |

Os serviços são mantidos com responsabilidades separadas. O Nextcloud é voltado ao gerenciamento de arquivos; o Jellyfin, à biblioteca e reprodução de mídia.

## Segurança e acesso

A configuração prioriza o acesso administrativo e remoto por uma rede privada, evitando depender de exposição direta dos serviços à internet.

Princípios adotados no projeto:

- **Acesso remoto privado:** uso do Tailscale para conectar dispositivos autorizados.
- **Administração remota:** SSH para tarefas de manutenção.
- **Filtragem de tráfego:** regras de firewall ajustadas conforme os serviços e fluxos necessários.
- **Isolamento de aplicações:** uso de contêineres Podman para os serviços conteinerizados.
- **Redução da exposição:** evitar publicar portas na internet quando o acesso privado atende à necessidade.
- **Separação de dados e aplicações:** organização dos diretórios persistentes utilizados pelos serviços.

A existência dessas medidas não representa uma garantia absoluta de segurança. As regras efetivas, permissões, atualizações e serviços ativos devem ser revisados periodicamente.

## Operação e manutenção

A administração é feita remotamente, principalmente por SSH. Os comandos abaixo são exemplos genéricos de inspeção; execute-os com uma conta que tenha as permissões necessárias.

### Verificar o sistema

```bash
hostnamectl
uptime
free -h
df -h
```

### Verificar contêineres

```bash
podman ps
podman ps -a
podman stats --no-stream
```

### Consultar logs de um contêiner

```bash
podman logs --tail 100 NOME_DO_CONTAINER
```

Substitua `NOME_DO_CONTAINER` pelo nome real do contêiner que deseja investigar.

### Verificar serviços de rede

```bash
systemctl --no-pager --type=service --state=running
systemctl status ssh --no-pager
tailscale status
```

### Revisar as regras de firewall

```bash
sudo nft list ruleset
```

Antes de alterar regras de firewall, confirme como o tráfego do host, do Tailscale e das redes de contêineres é encaminhado. Alterações genéricas ou a remoção de tabelas podem interromper serviços existentes.

## Dados persistentes e recuperação

Os dados de aplicações autohospedadas precisam ser tratados separadamente do ciclo de vida dos contêineres. Antes de atualizar, recriar ou remover um contêiner, identifique os volumes e diretórios persistentes associados.

Boas práticas para a continuidade do serviço:

- Manter cópias de segurança dos arquivos e das configurações relevantes.
- Incluir bancos de dados e metadados no plano de backup, quando aplicável.
- Testar a restauração; a existência de um backup, por si só, não comprova que ele pode ser recuperado.
- Registrar alterações relevantes na configuração.
- Atualizar o sistema operacional, imagens e aplicações de forma controlada.
- Verificar o estado dos serviços após reinicializações e atualizações.

**Importante:** este README descreve o projeto e não substitui um inventário operacional atualizado nem um procedimento de recuperação testado.

## Próximos passos

A evolução do Jillserver pode incluir:

- Automatização e verificação de inicialização dos serviços.
- Rotina de backup e testes de restauração.
- Monitoramento de recursos e disponibilidade.
- Revisão periódica de firewall, permissões e atualizações.
- Documentação dos fluxos de rede e dos procedimentos de recuperação.

## Identidade visual

A marca **JS 1.0** utiliza um símbolo atômico em azul-escuro e uma referência binária no centro. A identidade representa a relação entre sistemas, computação e experimentação técnica que orienta o projeto.

---

<div align="center">

<sub>Documentação mantida como parte do laboratório doméstico. Não publique endereços privados, nomes de dispositivos, credenciais, tokens ou configurações sensíveis em repositórios públicos.</sub>

</div>