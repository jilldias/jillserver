# Rede e conectividade

## Princípios

O servidor pode ser acessado por uma rede local e por uma rede privada sobreposta. As aplicações devem escutar apenas nas interfaces necessárias. O acesso remoto deve usar autenticação e não deve depender da publicação indiscriminada de portas na internet.

## Endereços de exemplo

Os valores desta tabela são exemplos reservados para documentação; não correspondem ao ambiente real.

| Finalidade | Exemplo |
|---|---|
| Host na rede local | `192.0.2.10` |
| Gateway ilustrativo | `192.0.2.1` |
| Rede de contêineres ilustrativa | `198.51.100.0/24` |
| Serviço ilustrativo | `203.0.113.30` |

Prefira placeholders (`<IP_DO_SERVIDOR>`, `<REDE_LAN>`, `<ENDERECO_TAILSCALE>`) quando um endereço de exemplo possa ser confundido com uma configuração real.

## Padrões de acesso

### Aplicação web privada

Uma aplicação pode escutar apenas no loopback do host e ser exposta por um proxy HTTPS privado. Isso reduz a exposição direta da porta da aplicação, mas exige que o proxy e as políticas de acesso estejam configurados corretamente.

### Aplicação de mídia

Uma aplicação de mídia pode ser acessível pela rede local e pela rede privada. Restrinja as portas no firewall às origens necessárias e confirme se o serviço está ou não exposto à internet pública.

### Banco de dados

Evite expor a porta do banco de dados diretamente à rede local ou à internet se os clientes puderem conectar-se por uma interface interna controlada. Conceda permissões de banco de dados com privilégio mínimo.

## Comandos de diagnóstico local

```bash
ip -br address
ip route
ss -lntup
podman ps
```

Estes comandos podem revelar endereços reais, nomes de interfaces, portas e topologia. Use-os localmente; redija os resultados antes de compartilhá-los.
