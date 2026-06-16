<!--@sts:ignore-->
# AI Skills Workspace 🤖

**Projeto** para análise, desenvolvimento e manutenção de skills (Skills), com foco na criação de agentes inteligentes especializados em tarefas específicas. Este workspace contém uma coleção de habilidades que ampliam as capacidades nativas de agentes de IA.

---

## 📋 Sumário

- [AI Skills Workspace 🤖](#ai-skills-workspace-)
  - [📋 Sumário](#-sumário)
    - [Objetivos do Projeto 🎯](#objetivos-do-projeto-)
  - [Projeto de Análise e Manutenção de Skills de Agentes de IA](#projeto-de-análise-e-manutenção-de-skills-de-agentes-de-ia)
  - [Estrutura do Projeto](#estrutura-do-projeto)

### Objetivos do Projeto 🎯

1. **Centralizar skills de alta qualidade** para tarefas comuns em desenvolvimento com Claude Code, incluindo: criação de plugins (superpowers), automação documental, geração e manutenção de CLAUDE.md
2. **Estabelecer padrões reprodutíveis** validados pela Anthropic através do framework official `@obra/superpowers`
3. **Documentar gotchas críticos**, falhas comuns em empacotamento de skills, problemas de validação da estrutura JSON e técnicas para evitar erros no processo de build

## Projeto de Análise e Manutenção de Skills de Agentes de IA

Para um projeto de análise e manutenção de skills de agentes de IA (no formato com SKILL.md, scripts e arquivos de referência), uma estrutura que costuma funcionar bem é separar claramente "skills em desenvolvimento", "skills empacotadas/prontas" e "ferramentas de apoio". Algo assim:

## Estrutura do Projeto

**Diretório real da workspace atual:**

- `skills/skill-creator/SKILL.md` - Skill completa com scripts (package_skill.py, init_skill.py)
- `skills/readme/` → estrutura em desenvolvimento para README Generator skill
- `skills/_template/SKILL.md` - Template mínimo (name + description obrigatório)

**Comandos de Empacotamento e Validação:**

```bash
# Criar nova技能 a partir do template:
python /mnt/c/Users/jocil/Downloads/ai-skills-workspace/skills/readme/scripts/package_skill.py my-skill --path ./skills/my-skill

# Validar skill antes de empacar (verifica frontmatter, diretórios obrigatórios):
python /mnt/c/Users/jocil/Downloads/ai-skills-workspace/docs/checks.py skills/readme > report.md

# Gerar zip file fora da workspace:
cd /tmp && python package_skill.py ./skills/my-skill my-output.zip

```

Alguns pontos que ajudam bastante na manutenção:

A separação entre `skills/` (fonte editável) e `packaged/` (saída do empacotamento) evita confusão entre o que está em desenvolvimento e o que já foi distribuído — útil principalmente quando você tem casos como o `python-mentor`, que teve erro de empacotamento e ainda precisa de ajuste.

Um diretório `tools/` centralizado com o script de empacotamento e um validador (que checa frontmatter do SKILL.md, referências quebradas, arquivos faltando) ajuda a pegar erros de empacotamento antes de gerar o pacote final, em vez de descobrir só depois.

Manter um `_template/` com a estrutura mínima esperada (SKILL.md com frontmatter correto, pastas reference/scripts/examples) acelera a criação de novas skills e mantém consistência entre elas.

Um `changelog.md` simples por skill (ou um geral em `docs/`) ajuda a rastrear o que mudou entre versões, especialmente se você for iterando sobre as mesmas skills repetidamente.

Se o projeto crescer muito, vale considerar também um arquivo `manifest.json` ou `.yaml` na raiz listando todas as skills, versão atual e status (em desenvolvimento, empacotada, com erro, etc.) — funciona como um painel rápido de status do projeto inteiro.
