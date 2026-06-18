# SPEC: Portal de Documentação e Catálogo de Skills

## 1. Intenção e Contexto (Problem Statement)

O sistema atual carece de uma interface centralizada que sirva simultaneamente a dois propósitos distintos:

1. Fornecer documentação técnica legível e navegável para desenvolvedores e usuários humanos.
2. Atuar como um repositório estruturado de metadados ("Skills") consumível por agentes de inteligência artificial baseados no ecossistema Google Antigravity.

**Objetivo:** Desenvolver um portal estático utilizando Docusaurus (v3+) que isole conceitual e tecnicamente a documentação instrucional do catálogo de "Skills", garantindo a renderização visual dinâmica e a aderência estrita aos contratos de dados exigidos pelas IAs.

## 2. Requisitos do Sistema (System Requirements)

### 2.1. Ambiente Alvo

* **Engine:** Node.js v20+
* **Controle de Versão:** Git
* **Framework:** Docusaurus v3+

### 2.2. Separação de Domínios (Domain Isolation)

O portal deve segregar o conteúdo em dois domínios de acesso e processamento:

* **Domínio de Documentação (`/docs/`):** Guias de uso geral, tutoriais e diretrizes de arquitetura. Funciona sob o padrão clássico do Docusaurus.
* **Domínio de Skills (`/skills/`):** Repositório de marcação (Markdown) que documenta as habilidades dos agentes. Exige uma sidebar autogerada isolada e roteamento exclusivo.

## 3. Regras de Negócio e Contratos de Dados (Business Rules)

### 3.1. O Contrato Híbrido (Front-Matter)

Todo documento inserido no domínio de Skills (`/skills/*.md`) é obrigado a declarar um bloco de metadados YAML compatível tanto com o renderizador React quanto com o parser do Google Antigravity.

**Regras de Validação do Schema:**

* `name` (String): ID lógico para a IA. Formato restrito a minúsculas e hifens (kebab-case). Exigência do Antigravity.
* `title` (String): Nome de exibição humano. Exigência do Docusaurus para renderização de UI.
* `description` (String): Resumo operacional máximo de 150 caracteres. Consumido pela IA (para entender a skill) e pelo frontend (para os cards).

### 3.2. Tolerância Zero a Falhas de Contrato (Fail-Fast)

O sistema de CI/CD não pode permitir a publicação de artefatos que quebrem o Contrato Híbrido. A ausência de qualquer uma das chaves (`name`, `title`, `description`) no front-matter dos arquivos dentro de `/skills/` deve resultar em falha imediata do build (exit code > 0) antes da etapa de deploy.

## 4. Comportamento da Interface (UI/UX Behavior)

### 4.1. Catálogo Dinâmico (Skill Cards)

O sistema deve expor um componente React reutilizável via MDX (`<SkillCards/>`) que:

* Leia dinamicamente os metadados da instância isolada de `/skills/`.
* Renderize um grid responsivo de cartões.
* Cada cartão deve exibir o `title` e a `description` da skill.
* Cada cartão deve conter um CTA (Call to Action) com redirecionamento válido e testado para a página de detalhe da respectiva skill.

## 5. Critérios de Aceite (Acceptance Criteria)

Para que a implementação do `PLAN.md` seja considerada concluída e validada conforme esta especificação, os seguintes cenários devem passar:

* [ ] **CA01:** Acessar a rota `/docs/` exibe apenas guias gerais e sua respectiva sidebar. Acessar `/skills/` exibe apenas os arquivos da pasta skills e sua sidebar autogerada.
* [ ] **CA02:** O componente `<SkillCards/>`, ao ser injetado em uma página MDX, renderiza com sucesso todos os arquivos da pasta `/skills/` sem retornar `undefined` para título ou descrição.
* [ ] **CA03:** A navegação através do botão do card redireciona corretamente para a rota estática da skill (ex: `/skills/analisador-logs`).
* [ ] **CA04:** O build local (via Node.js v20) falha intencionalmente se um arquivo `.md` for adicionado à pasta `/skills/` faltando a chave `name`, `title` ou `description` no YAML.
* [ ] **CA05:** O pipeline de CI/CD compila o site e publica os artefatos estáticos sem links quebrados detectados pelo core do Docusaurus.
