# Análise do Skill readme

  Este é um skill de documentação técnica avançada projetado para criar README.md extremamente
  completos. Aqui está a análise:

## 🎯 Propósito Principal

  Criar README.md "absurdamente thorough" (exaustivos) que servem três propósitos:

  1. Desenvolvimento Local - Ajudar desenvolvedores a rodar o app localmente em minutos
  2. Entendimento do Sistema - Explicar detalhadamente como o app funciona
  3. Deploy de Produção - Cobrir tudo necessário para deploy e manutenção

## 📋 Quando Usar

  Use este skill quando:

- User quer criar/atualizar um README.md
- Commands like "write readme", "create readme"
- Solicitações de documentação do projeto
- Ajuda com README.md

## ⚙️  Metodologia

  O skill exige duas fases obrigatórias antes de escrever:

  Phase 1: Exploração Profunda do Codebase

  ✓ Project Structure → Identificar framework, entry points, organização de diretórios
  ✓ Configuration Files → .env.example, Dockerfiles, CI/CD configs
  ✓ Database → Schema, migrations, seeds
  ✓ Key Dependencies → Gemfile/package.json, native gems
  ✓ Scripts and Commands → bin/* scripts, Rake tasks, Procfile

  Phase 2: Identificar Target de Deployment

  Detectar automaticamente plataforma baseado em arquivos como fly.toml, render.yaml, .vercel/,
  etc. Se não houver configuração de deploy, fornecer orientação genérica com Docker recomendado.

## 📐 Estrutura do README (12 Sections)

  O skill escreve seções na ordem:

```bash
  ┌─────┬──────────────────────┬──────────────────────────────────────────────────────────────┐
  │  #  │       Section        │                      Conteúdo Principal                      │
  ├─────┼──────────────────────┼──────────────────────────────────────────────────────────────┤
  │ 1   │ Project Title &      │ Descrição, key features                                      │
  │     │ Overview             │                                                              │
  ├─────┼──────────────────────┼──────────────────────────────────────────────────────────────┤
  │ 2   │ Tech Stack           │ Linguagem, framework, database, etc.                         │
  ├─────┼──────────────────────┼──────────────────────────────────────────────────────────────┤
  │ 3   │ Prerequisites        │ Dependências necessárias (Node.js, PostgreSQL, pnpm)         │
  ├─────┼──────────────────────┼──────────────────────────────────────────────────────────────┤
  │ 4   │ Getting Started      │ CLI completo passo-a-passo para setup local                  │
  ├─────┼──────────────────────┼──────────────────────────────────────────────────────────────┤
  │ 5   │ Architecture         │ Estrutura de diretórios, lifecycle do request, data flow,    │
  │     │ Overview             │ database schema                                              │
  ├─────┼──────────────────────┼──────────────────────────────────────────────────────────────┤
  │ 6   │ Environment          │ Variáveis required vs optional em tabelas formatadas         │
  │     │ Variables            │                                                              │
  ├─────┼──────────────────────┼──────────────────────────────────────────────────────────────┤
  │ 7   │ Available Scripts    │ Tabela de comandos e descrições (bin/dev, bin/rails test)    │
  ├─────┼──────────────────────┼──────────────────────────────────────────────────────────────┤
  │ 8   │ Testing              │ Como rodar testes, estrutura da suite, exemplos (Minitest +  │
  │     │                      │ RSpec)                                                       │
  ├─────┼──────────────────────┼──────────────────────────────────────────────────────────────┤
  │ 9   │ Deployment           │ Instruções para múltiplas plataformas: Kamal, Docker,        │
  │     │                      │ Heroku, Fly.io, Render, VPS manual                           │
  ├─────┼──────────────────────┼──────────────────────────────────────────────────────────────┤
  │ 10  │ Troubleshooting      │ Common errors e soluções com comandos copy-pasteáveis        │
  ├─────┼──────────────────────┼──────────────────────────────────────────────────────────────┤
  │ 11  │ Contributing         │ Se for open source ou projeto de equipe                      │
  │     │ (Opcional)           │                                                              │
  ├─────┼──────────────────────┼──────────────────────────────────────────────────────────────┤
  │ 12  │ License (Opcional)   │ Informação sobre licença do projeto                          │
  └─────┴──────────────────────┴──────────────────────────────────────────────────────────────┘
```

## ✍️  Princípios de Escrita

  1. **Seja Absurdamente Exaustivo** - Quando dúvida, inclua mais detalhes
  2. **Use Code Blocks Liberalmente** - Cada command copy-pasteável
  3. **Mostre Example Output** - O que o usuário deve ver
  4. **Explique o Porquê** - Não apenas "rode este comando"
  5. **Suponha Máquina Fresca** - Como se leitor nunca viu esse codebase
  6. **Use Tabelas para Reference** - Para env vars, scripts, opções
  7. **Mantenha Comandos Atuais** - Use pnpm vs npm conforme projeto
  8. **Include Table of Contents** - Para READMEs > ~200 lines

## 🎁 Formato de Output

  O skill gera:

- Markdown formatado corretamente
- Code blocks com language hints (bash, typescript)
- Tabelas onde apropriado (environment variables, scripts)
- Hierarquia clara seções
- Linkable TOC para documentos longos

  Escrito diretamente em README.md no root do projeto.

## ⚠️  Limitações Importantes

  ❌ Não usar quando tarefa não claramente matcha escopo descrito
  ❌ Output não é substitute de validação específica ao environment, testing, ou expert review
  ⏸ Stop e pedir clarification se required inputs/permissions/success criteria estão missing

## 📚 Origem & Metadata

- Source: GitHub - Shpigford's skills repository
- Date Added: 2026-02-27
- Risk Level: safe (não requer permissões especiais)
- Metadata:
  type: reference (provavelmente user-defined ou skill library)
  description: Documentation generator for comprehensive README.md files

  ---
  Veredito Final: Este é um skill especializado para documentação técnica de alta qualidade. Ideal
  para projetos que precisam manter README bem estruturado e atualizado conforme mudanças no
  codebase.
