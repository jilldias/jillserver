# Nextcloud

## Função

Nextcloud oferece uma interface web para sincronização, armazenamento e acesso a arquivos pessoais.

## Itens a documentar

Ao registrar a implantação, inclua:
- imagem e versão utilizada;
- nome lógico do contêiner;
- portas e interfaces publicadas;
- diretórios ou volumes persistentes;
- banco de dados utilizado;
- proxy HTTPS ou mecanismo de acesso privado;
- política de atualização e backup.

Use valores genéricos na documentação pública. Por exemplo:

| Item | Exemplo genérico |
|---|---|
| Imagem | `nextcloud:<VERSAO>` |
| Porta local | `127.0.0.1:<PORTA_LOCAL>` |
| Diretório de dados | `<DIRETORIO_DE_DADOS>` |
| Endpoint privado | `https://<HOST_PRIVADO>` |

## Verificação local

```bash
podman ps
podman logs --tail 100 <NOME_DO_CONTAINER>
```

Substitua o nome de exemplo pelo nome real somente no terminal local. Revise a saída antes de compartilhá-la.

## Backup e recuperação

O backup deve contemplar arquivos, configuração e banco de dados, com consistência entre os componentes. Faça testes de restauração antes de considerar o procedimento confiável. Não inclua dados pessoais, dumps de banco ou credenciais no repositório.
