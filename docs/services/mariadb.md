# MariaDB

## Função

MariaDB fornece armazenamento relacional para aplicações que dependem de um banco de dados.

## Itens a documentar

Registre se o banco roda no host ou em contêiner, versão, interfaces de escuta, aplicações dependentes e procedimento de backup. Não publique nomes de bancos privados, usuários, senhas ou dados pessoais.

Exemplo genérico de escuta local:

```text
127.0.0.1:<PORTA_DO_BANCO>
<IP_DA_REDE_INTERNA>:<PORTA_DO_BANCO>
```

O segundo endereço é apenas um placeholder, não uma recomendação para escutar em qualquer interface. Configure o banco para aceitar conexões somente das origens necessárias.

## Verificação local

```bash
systemctl status mariadb --no-pager
ss -lntp
```

Filtre a saída no terminal local e redija informações sensíveis antes de compartilhar.

## Backup e recuperação

Use um método consistente de exportação e mantenha as cópias em local protegido. Teste a restauração. Nunca versione dumps de produção no repositório público.
