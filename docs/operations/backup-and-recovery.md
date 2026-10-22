# Backup e recuperação

## Objetivo

Definir como proteger os dados e demonstrar que podem ser restaurados. A existência de uma cópia não comprova que ela seja íntegra ou recuperável.

## Escopo a avaliar

- dados persistentes das aplicações;
- arquivos de configuração;
- bancos de dados;
- configurações de rede e firewall necessárias para reconstruir os serviços;
- instruções de instalação e recuperação.

Mantenha segredos separados do repositório público. Escolha destino independente do disco principal, retenção adequada e proteção contra acesso não autorizado.

## Procedimento mínimo

1. Identifique os dados necessários para cada serviço.
2. Escolha um método consistente para copiar arquivos e exportar bancos de dados.
3. Registre data, duração, resultado e tamanho da cópia.
4. Proteja os backups com permissões apropriadas e, quando necessário, criptografia.
5. Teste a restauração em ambiente separado.
6. Atualize o documento com os resultados e limitações observadas.

## Critério de sucesso

O backup só deve ser considerado validado depois de restaurar os dados e verificar o funcionamento da aplicação. Não publique arquivos pessoais, dumps de produção ou credenciais como evidência do teste.
