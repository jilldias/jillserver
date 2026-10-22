# Diagnóstico e solução de problemas

## Coleta inicial

```bash
date
uptime
free -h
df -hT
systemctl --failed
podman ps -a
```

Guarde a saída localmente. Antes de compartilhar, remova hostname, IPs, nomes de usuário, IDs, domínios e outros metadados privados.

## Aplicação em contêiner

```bash
podman ps -a
podman logs --tail 100 <NOME_DO_CONTAINER>
```

Confirme estado, logs e armazenamento antes de reiniciar ou recriar o contêiner. Não exclua volumes ou diretórios persistentes como primeira tentativa de correção.

## Aplicação web privada

Verifique separadamente:
1. se a aplicação responde localmente;
2. se o proxy está ativo e aponta para o destino correto;
3. se o dispositivo cliente está conectado à rede privada;
4. se o firewall permite o tráfego necessário.

## Banco de dados

```bash
systemctl status mariadb --no-pager
journalctl -u mariadb -n 100 --no-pager
```

Não publique configurações com senhas nem logs que contenham dados pessoais.

## Falha após reinicialização

Confira o estado dos serviços, o mecanismo de inicialização dos contêineres e os logs do boot. Não presuma que uma política de reinício garante a retomada sem teste.

## Regra de segurança

Se estiver conectado remotamente, não aplique alterações de firewall ou rede que possam bloquear seu único caminho de administração sem uma alternativa de acesso.
