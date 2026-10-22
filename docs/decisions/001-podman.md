# ADR 001: Execução de aplicações com Podman

- **Status:** adotado
- **Data do registro:** 2026-10-21

## Contexto

O homelab usa contêineres para executar aplicações e manter os dados persistentes separados do ciclo de vida da imagem.

## Decisão

Usar Podman para gerenciar os contêineres de aplicação. Os dados importantes devem permanecer em diretórios ou volumes persistentes, com backup e restauração documentados.

## Consequências

**Vantagens**
- Isolamento entre aplicações.
- Implantação e atualização individual dos serviços.
- Mapeamento explícito de portas e armazenamento.

**Custos e riscos**
- A rede de contêineres e as portas publicadas precisam ser compreendidas e protegidas.
- Dados persistentes exigem backup independente.
- Inicialização após reboot precisa ser configurada e testada.
- Atualizações de imagem exigem validação e plano de reversão.

## Observação

Este ADR registra a decisão de arquitetura; não pretende ser uma comparação formal com todas as alternativas disponíveis.