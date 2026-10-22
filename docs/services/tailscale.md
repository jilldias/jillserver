# Tailscale

## Função

Tailscale conecta dispositivos autorizados por meio de uma rede privada. A rede privada não elimina a necessidade de autenticação nos serviços e de regras de firewall.

## Padrões de uso

- Autorizar somente dispositivos necessários.
- Usar acesso privado para administração remota.
- Se for usado um proxy HTTPS privado, documentar qual aplicação ele encaminha sem divulgar o hostname real.
- Restringir no firewall as portas acessíveis pela interface Tailscale.
- Revisar periodicamente os dispositivos e permissões da rede.

## Valores públicos

Não inclua o hostname completo do tailnet, endereços Tailscale reais, IDs de dispositivos, nomes de dispositivos ou informações da conta. Use placeholders:

- Host: `<HOST_TAILSCALE>`
- Endereço privado: `<ENDERECO_TAILSCALE>`
- Endpoint HTTPS: `https://<HOST_PRIVADO>`

## Verificação local

```bash
tailscale status
tailscale ip -4
tailscale serve status
systemctl status tailscaled --no-pager
```

Esses comandos podem revelar metadados privados. Mantenha a saída no ambiente local ou redija-a antes de compartilhá-la.
