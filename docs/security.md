# Segurança

## Objetivo

Reduzir a superfície de ataque e evitar que a documentação pública revele detalhes desnecessários do servidor.

## Controles de rede

- Permitir somente portas e origens necessárias.
- Usar uma rede privada para administração remota quando apropriado.
- Evitar expor serviços de banco de dados diretamente à internet.
- Manter regras do firewall sob controle de versão em arquivos revisados, sem incluir dados secretos.
- Não editar manualmente tabelas gerenciadas por ferramentas como Podman ou Tailscale sem compreender como elas são recriadas.

## Segredos e metadados que não devem ser publicados

Não publique:
- senhas, tokens, chaves privadas, cookies ou arquivos `.env`;
- IPs reais da LAN, endereços Tailscale, IPv6, nomes de dispositivos e hostname privado;
- domínio completo do tailnet ou URLs privadas;
- números de série, UUIDs, MAC addresses ou identificadores de conta;
- nomes de usuário locais, caminhos que revelem nomes pessoais e inventários de arquivos;
- saídas completas de `podman inspect`, `tailscale status`, `ip address` ou configurações de banco sem revisão.

## Revisão antes do commit

1. Pesquise no repositório por IPs, hostnames, domínios, e-mails, tokens e nomes pessoais.
2. Inspecione arquivos novos e modificados.
3. Confirme que os exemplos usam placeholders ou blocos reservados para documentação.
4. Lembre-se de que remover um segredo do arquivo atual não apaga esse segredo do histórico Git. Se um segredo real já foi commitado, revogue-o e trate a limpeza do histórico separadamente.

## Firewall

A política de firewall deve ser avaliada a partir da configuração efetivamente carregada. Regras repetidas, tabelas criadas por contêineres e regras gerenciadas por ferramentas de rede devem ser analisadas antes de qualquer alteração. Teste mudanças com um caminho alternativo de administração para evitar perder o acesso remoto.
