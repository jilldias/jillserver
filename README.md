
<div align="center">
  <img width="250" height="250" alt="Ícone JS binário" src="https://github.com/user-attachments/assets/45eff1aa-51aa-40c6-bf05-4a3fee4d0b57" />

  <br/><br/>

  <p align="center">
    <strong>JILLSERVER HOMELAB</strong><br/>
    Infraestrutura própria • Linux • Serviços autohospedados
  </p>

  <br/>

  <p align="justify">
    Um laboratório pessoal para hospedar serviços, administrar sistemas Linux e explorar soluções de armazenamento e mídia em uma infraestrutura própria.
  </p>
</div>

<p align="center">
  <a href="#arquitetura">Arquitetura</a> ·
  <a href="#serviços">Serviços</a> ·
  <a href="#segurança-e-acesso">Segurança</a> ·
  <a href="#operação-e-manutenção">Operação</a> ·
  <a href="#próximos-passos">Próximos passos</a>
</p>

---

## Visão geral

<p align="justify">
O <strong>Jillserver</strong> é um servidor doméstico construído a partir de um notebook reaproveitado e administrado com <strong>Debian GNU/Linux</strong>, sem depender de uma interface gráfica local. O projeto combina serviços autohospedados, gerenciamento de contêineres, acesso remoto privado e práticas de administração de sistemas.
</p>

<p align="justify">
Além de atender a necessidades pessoais, o servidor funciona como um laboratório prático para estudar Linux, redes, segurança, armazenamento, implantação e manutenção de serviços.
</p>

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

<p align="justify">
Os serviços são mantidos com responsabilidades separadas. O Nextcloud é voltado ao gerenciamento de arquivos; o Jellyfin, à biblioteca e reprodução de mídia.
</p>

## Segurança e acesso

<p align="justify">
A configuração prioriza o acesso administrativo e remoto por uma rede privada, evitando depender de exposição direta dos serviços à internet.
</p>

Princípios adotados no projeto:

- **Acesso remoto privado:** uso do Tailscale para conectar dispositivos autorizados.
- **Administração remota:** SSH para tarefas de manutenção.
- **Filtragem de tráfego:** regras de firewall ajustadas conforme os serviços e fluxos necessários.
- **Isolamento de aplicações:** uso de contêineres Podman para os serviços conteinerizados.
- **Redução da exposição:** evitar publicar portas na internet quando o acesso privado atende à necessidade.
- **Separação de dados e aplicações:** organização dos diretórios persistentes utilizados pelos serviços.

<p align="justify">
A existência dessas medidas não representa uma garantia absoluta de segurança. As regras efetivas, permissões, atualizações e serviços ativos devem ser revisados periodicamente.
</p>

## Operação e manutenção

<p align="justify">
A administração é feita remotamente, principalmente por SSH. Os comandos abaixo são exemplos genéricos de inspeção; execute-os com uma conta que tenha as permissões necessárias.
</p>

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

<p align="justify">
Substitua <code>NOME_DO_CONTAINER</code> pelo nome real do contêiner que deseja investigar.
</p>

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

<p align="justify">
Antes de alterar regras de firewall, confirme como o tráfego do host, do Tailscale e das redes de contêineres é encaminhado. Alterações genéricas ou a remoção de tabelas podem interromper serviços existentes.
</p>

## Dados persistentes e recuperação

<p align="justify">
Os dados de aplicações autohospedadas precisam ser tratados separadamente do ciclo de vida dos contêineres. Antes de atualizar, recriar ou remover um contêiner, identifique os volumes e diretórios persistentes associados.
</p>

Boas práticas para a continuidade do serviço:

- Manter cópias de segurança dos arquivos e das configurações relevantes.
- Incluir bancos de dados e metadados no plano de backup, quando aplicável.
- Testar a restauração; a existência de um backup, por si só, não comprova que ele pode ser recuperado.
- Registrar alterações relevantes na configuração.
- Atualizar o sistema operacional, imagens e aplicações de forma controlada.
- Verificar o estado dos serviços após reinicializações e atualizações.

<p align="justify">
<strong>Importante:</strong> este README descreve o projeto e não substitui um inventário operacional atualizado nem um procedimento de recuperação testado.
</p>

## Próximos passos

<p align="justify">
A evolução do Jillserver pode incluir:
</p>

- Automatização e verificação de inicialização dos serviços.
- Rotina de backup e testes de restauração.
- Monitoramento de recursos e disponibilidade.
- Revisão periódica de firewall, permissões e atualizações.
- Documentação dos fluxos de rede e dos procedimentos de recuperação.

## Identidade visual

<p align="justify">
O design foi inspirado em uma representação simplificada do átomo de silício. Os três anéis representam suas três camadas eletrônicas ocupadas. No núcleo, as iniciais "JS" vêm do host Jillserver, e os números 0 e 1, posicionados logo abaixo, fazem referência à representação binária utilizada na computação.
</p>

<p align="justify">
O azul escuro foi escolhido para transmitir estabilidade e criar uma associação visual com tecnologia e infraestrutura.
</p>

---

<div align="center">
  <p align="justify">
    <sub>Documentação mantida como parte do laboratório doméstico. Não publique endereços privados, nomes de dispositivos, credenciais, tokens ou configurações sensíveis em repositórios públicos.</sub>
  </p>
</div>
