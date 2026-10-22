# Manutenção

Este documento é um roteiro de operação. Antes de executar mudanças, confirme os nomes dos serviços e o estado atual do host.

## Inspeção básica

```bash
uptime
free -h
df -hT
systemctl --failed
podman ps -a
podman stats --no-stream
```

## Atualizações

1. Verifique espaço disponível e estado dos serviços.
2. Confirme a existência de backup recente.
3. Atualize o sistema e as imagens em uma janela planejada.
4. Leia os logs e valide os serviços depois da atualização.
5. Registre a mudança, o teste e o procedimento de reversão.

## Contêineres

```bash
podman ps -a
podman logs --tail 100 <NOME_DO_CONTAINER>
podman inspect <NOME_DO_CONTAINER>
```

`podman inspect` pode expor variáveis de ambiente, caminhos e configurações. Não publique a saída integral.

## Reinicialização do host

Verifique se os contêineres e serviços necessários iniciam corretamente após reboot. Documente o mecanismo de inicialização e teste-o em uma janela de manutenção.

## Registro de mudanças

Para cada mudança relevante, registre motivo, componentes afetados, procedimento, resultado do teste e plano de reversão. Não inclua credenciais ou endereços reais no repositório público.
