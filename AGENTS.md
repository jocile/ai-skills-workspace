# AGENTS.md - Guia Operacional do Repositório

## Contexto e Propósito

Este repositório atua sob uma arquitetura de dupla responsabilidade, gerenciada por uma infraestrutura **Docusaurus (v3+) em Múltiplas Instâncias**. Ele armazena pacotes de habilidades (Skills) autônomos que estendem as capacidades do **Google Antigravity**, ao mesmo tempo em que gera um portal de documentação estático interativo para humanos.

O objetivo deste documento é estabelecer as regras rígidas de contribuição, formatação e validação para qualquer agente ou desenvolvedor que crie ou modifique arquivos dentro deste projeto.

## Fronteiras de Diretórios (Directory Boundaries)

A arquitetura exige separação estrita de domínios. Respeite os escopos abaixo:

* **Raiz `/**`: Documentação do projeto (README.md, PLAN.md, SPEC.md, AGENTS.md) e arquivos de configuração global (`docusaurus.config.js`).
* **`/docs/` (Domínio de Documentação)**: Instância primária. Contém apenas guias técnicos abstratos, tutoriais e manuais de uso para humanos.
* **`/skills/` (Domínio de Skills)**: Instância isolada. Diretório fonte exclusivo para definições de skills. **Nenhuma skill deve ser criada fora desta pasta**. Os arquivos Markdown aqui alimentam simultaneamente o agente do Antigravity e o catálogo de componentes React.
* **`/src/`**: Código-fonte do frontend (Componentes React, CSS Modules). Agentes de criação de conteúdo não devem alterar esta pasta a menos que especificado.

## A Regra de Ouro: O Contrato de Dados Híbrido (Front-Matter)

Antes de processar, ler ou criar qualquer arquivo na pasta `/skills/`, o agente DEVE garantir que o bloco de metadados YAML (front-matter) cumpra o **Contrato Híbrido**. Ele é o núcleo do Spec-Driven Development deste projeto.

Todo arquivo em `/skills/` deve conter estritamente:

```yaml
---
name: string          # OBRIGATÓRIO (Antigravity): ID único lógico, em kebab-case.
title: string         # OBRIGATÓRIO (Docusaurus): Nome amigável e legível para a UI.
description: string   # OBRIGATÓRIO (Ambos): Resumo operacional de até 150 caracteres.
---

```

*A ausência de qualquer uma destas chaves causará uma falha crítica na renderização do componente `<SkillCards />` e na injeção de contexto do Antigravity.*

## Regras de Validação e CI/CD (Fail-Fast)

O repositório opera sob a política de "Tolerância Zero a Falhas de Contrato", conforme o `SPEC.md`.

1. **Validação de Metadados:** Scripts de CI (via GitHub Actions) farão o linting da pasta `/skills/` antes de cada build. Se o Contrato Híbrido for violado, o build (exit code > 0) e o PR serão bloqueados.
2. **Testes de Roteamento:** O Docusaurus validará nativamente links quebrados. Nunca referencie um caminho `.md` ou um asset que não exista fisicamente no repositório. Use rotas resolvidas (ex: `/skills/nome-da-skill`).
3. **Arquivos Auxiliares:** Se uma skill precisar de scripts determinísticos (`/scripts/`) ou bases de conhecimento (`/references/`), eles devem ser documentados dentro do próprio markdown da skill e estar estruturados de forma a não interferir no build estático do frontend.

## Estilo de Escrita para as SKILLs

Ao redigir o conteúdo interno dos arquivos em `/skills/`:

* **Forma Imperativa:** Escreva toda a skill de forma imperativa e direta. Em vez de *"Você pode usar esta ferramenta quando..."*, utilize *"Esta skill deve ser invocada quando..."*.
* **Foco no Agente:** Evite "fluff" (textos genéricos de marketing ou introduções longas). O conteúdo deve ser otimizado para o que o agente (ex: Antigravity) precisa ler para atuar com precisão. Forneça fluxos de trabalho concretos, regras de decisão claras e padrões reutilizáveis.
* **Limite de Tamanho:** Mantenha o conteúdo direto. Para referências massivas (ex: schemas JSON acima de 5k palavras), não as embuta diretamente no Markdown; referencie-as como arquivos externos, para que o Docusaurus não sofra penalidades de performance no parse do MDX.

## Comandos Essenciais do Repositório

Como este projeto roda primariamente sobre Node.js/Docusaurus, os comandos base para atuar no ambiente de desenvolvimento são:

```bash
# Iniciar o servidor local para validar o frontend e as rotas isoladas
npm run start

# Executar build de produção (Dispara também a validação nativa de links)
npm run build

# Onde aplicável (se houver scripts customizados de validação de SDD)
npm run validate-skills

```

*(Nota: Certifique-se de que a instância dupla do Docusaurus esteja ativa para acessar tanto `localhost:3000/docs/` quanto `localhost:3000/skills/` com sucesso antes de efetuar commits).*
