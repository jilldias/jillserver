# Jellyfin

## Função

Jellyfin organiza e transmite uma biblioteca de mídia para clientes compatíveis.

## Itens a documentar

Registre a imagem e sua versão, portas publicadas, volumes de configuração, cache e mídia, política de reinício e clientes testados. Use placeholders na versão pública.

| Item | Exemplo genérico |
|---|---|
| Imagem | `jellyfin/jellyfin:<VERSAO>` |
| Porta da aplicação | `<PORTA_JELLYFIN>` |
| Configuração | `<DIRETORIO_CONFIG>` |
| Cache | `<DIRETORIO_CACHE>` |
| Biblioteca de mídia | `<DIRETORIO_DA_MIDIA>` |

Evite publicar o caminho exato de arquivos pessoais ou nomes de pastas que revelem informações privadas.

## Diagnóstico

```bash
podman ps
podman logs --tail 150 <NOME_DO_CONTAINER>
```

Se a reprodução falhar, compare o mesmo arquivo em clientes diferentes e verifique os logs. Registre versão do cliente e tipo de reprodução; não conclua que o servidor é a causa sem evidências.

## Backup

Preserve a configuração do serviço e os arquivos de mídia de acordo com a estratégia de backup definida. Cache normalmente é reconstruível, mas valide as necessidades da instalação antes de excluí-lo.
