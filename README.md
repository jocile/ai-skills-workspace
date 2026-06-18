<!--@sts:ignore-->
# AI Skills Workspace & Documentation Portal 🤖

**Projeto** para análise, desenvolvimento e manutenção de skills (Skills), com foco na criação de agentes inteligentes especializados em tarefas específicas. Este workspace contém uma coleção de habilidades que ampliam as capacidades nativas de agentes de IA.

Simultaneamente, o projeto utiliza o **Docusaurus (v3+)** configurado com **Múltiplas Instâncias (Multi-instance)** para gerar de forma estática e automatizada um portal de documentação técnica para humanos e um catálogo visual interativo em formato de cartões (cards) alimentado dinamicamente pelos metadados das próprias habilidades.

---

## 📋 Sumário

- [AI Skills Workspace \& Documentation Portal 🤖](#ai-skills-workspace--documentation-portal-)
  - [📋 Sumário](#-sumário)
  - [Objetivos do Projeto 🎯](#objetivos-do-projeto-)
  - [Arquitetura de Isolamento de Domínios 🏛️](#arquitetura-de-isolamento-de-domínios-️)
  - [Estrutura do Projeto (Blueprint) 📂](#estrutura-do-projeto-blueprint-)
  - [O Contrato de Dados Híbrido (Front-Matter) 📄](#o-contrato-de-dados-híbrido-front-matter-)
    - [Exemplo Base em Conformidade (`skills/analisador-logs.md`)](#exemplo-base-em-conformidade-skillsanalisador-logsmd)
  - [Comandos Essenciais do Ecossistema 💻](#comandos-essenciais-do-ecossistema-)
  - [Pipeline de Entrega e Validação Contínua (CI/CD) 🚀](#pipeline-de-entrega-e-validação-contínua-cicd-)

---

## Objetivos do Projeto 🎯

1. **Centralização e Governança de Skills:** Prover um ambiente unificado e estritamente tipado para o desenvolvimento de habilidades utilizadas por agentes autônomos do Google Antigravity.
2. **Dupla Responsabilidade dos Artefatos:** Garantir que cada arquivo Markdown dentro de `skills/` sirva perfeitamente como fonte de contexto para IAs (metadados operacionais) e como página de documentação rica para usuários humanos.
3. **Catálogo Dinâmico e Isolado:** Fornecer uma interface visual em React que consuma exclusivamente os metadados do repositório de habilidades, mantendo a documentação conceitual (`docs/`) e o catálogo operacional (`skills/`) em escopos de roteamento totalmente independentes.

---

## Arquitetura de Isolamento de Domínios 🏛️

Para eliminar colisões de dados e garantir a escalabilidade do portal, o Docusaurus gerencia duas instâncias independentes:

- **Domínio de Documentação (`/docs/`):** Abriga guias conceituais, tutoriais de uso, manuais de arquitetura e diretrizes de contribuição gerais.
- **Domínio de Skills (`/skills/`):** Repositório exclusivo de habilidades estruturadas. Este domínio conta com uma barra lateral (*sidebar*) gerada de forma 100% automatizada e serve seus metadados diretamente para o componente React `<SkillCards/>`.

---

## Estrutura do Projeto (Blueprint) 📂

```bash
/
├── .github/
│   └── workflows/
│       └── deploy.yml         # Pipeline de CI/CD (Linting de Contrato + Build + Deploy)
├── docs/                      # Instância Default: Guias conceituais e documentação técnica geral
├── skills/                    # Instância Skills: Arquivos Markdown de cada skill do sistema
│   ├── _template.md           # Modelo base para criação de novas skills
│   ├── analisador-logs.md     # Exemplo de especificação de skill operacional
│   └── readme-generator.md    # Skill especializada em documentação automatizada
├── src/
│   ├── components/
│   │   └── SkillCards/
│   │       ├── index.js       # Componente lógico React (Consome dados globais da instância 'skills')
│   │       └── styles.module.css # Estilização encapsulada (CSS Modules) para o grid de cards
│   └── pages/
├── docusaurus.config.js       # Arquivo central de configuração do ecossistema e plugins
├── package.json               # Gerenciador de dependências e scripts do ambiente Node.js
├── sidebars.js                # Controle de navegação e menu do domínio /docs/
└── sidebarsSkills.js          # Controle de navegação autogerado do domínio /skills/

```

---

## O Contrato de Dados Híbrido (Front-Matter) 📄

A conformidade com o **Spec-Driven Development (SDD)** exige tolerância zero a falhas na declaração de metadados. Todo arquivo contido obrigatoriamente dentro da pasta `skills/` deve iniciar com o bloco YAML abaixo:

```yaml
---
name: string          # OBRIGATÓRIO (Antigravity): ID lógico da skill em formato kebab-case (Ex: skill-ia-resumos)
title: string         # OBRIGATÓRIO (Docusaurus): Nome amigável que será renderizado no título da página e menus
description: string   # OBRIGATÓRIO (Ambos): Resumo conciso de atuação da skill (Máximo de 150 caracteres)
---

```

### Exemplo Base em Conformidade (`skills/analisador-logs.md`)

```markdown
---
name: analisador-logs
title: Analisador de Logs
description: Monitora arquivos de log do sistema e identifica anomalias críticas usando padrões regex predefinidos.
---

# Documentação da Skill: Analisador de Logs

Instruções imperativas de como o agente Antigravity deve interpretar e executar os parâmetros desta skill...

```

---

## Comandos Essenciais do Ecossistema 💻

O projeto é executado nativamente sob o ecossistema Node.js (v18+). Utilize os comandos abaixo no seu terminal para manutenção e testes locais:

```bash
# Instalar as dependências do projeto
npm install

# Iniciar o servidor de desenvolvimento local (Live Reload)
# Acesse /docs para guias e /skills para ver o catálogo de habilidades
npm run start

# Compilar a aplicação para produção
# Este comando aciona o validador nativo do Docusaurus contra links quebrados
npm run build

# Executar scripts customizados de validação de esquemas Markdown (Quando aplicável)
npm run validate-skills

```

---

## Pipeline de Entrega e Validação Contínua (CI/CD) 🚀

Toda alteração submetida para a branch principal (`main`) passa por um fluxo rígido automatizado via **GitHub Actions**:

1. **Sanity Check & Linter:** O pipeline analisa se novos arquivos adicionados à pasta `skills/` violam o Contrato Híbrido de Dados (ausência de `name`, `title` ou `description`). Qualquer violação interrompe o processo imediatamente (*Fail-Fast*).
2. **Integridade de Roteamento:** O processo de build compila o portal estático e valida se há referências cruzadas ou hyperlinks quebrados.
3. **Deployment:** Após a validação total dos critérios de aceite descritos em `SPEC.md`, a aplicação estática é publicada automaticamente no provedor de hospedagem configurado (GitHub Pages / Vercel).
