# Guia de Contribuição

Obrigado pelo interesse em contribuir com o Claude War Room! Este guia explica como participar do projeto.

---

## Primeiros Passos

1. **Fork** o repositório
2. **Clone** seu fork:
   ```bash
   git clone https://github.com/SEU_USUARIO/claude-war-room.git
   cd claude-war-room
   ```
3. **Crie uma branch** para sua mudança:
   ```bash
   git checkout -b feat/meu-novo-agente
   ```

---

## Estrutura de um Agente

Todo agente deve seguir esta estrutura no arquivo `.md`:

### Frontmatter YAML (obrigatório)

```yaml
---
name: "Nome do Agente"
description: "Descrição curta do que o agente faz. Usado pelo Claude Code para decidir quando invocar."
model: opus
tools:
  - Read
  - Glob
  - Grep
  - Bash
  - Agent
---
```

**Campos obrigatórios:**
- `name` — Nome descritivo do agente
- `description` — O que faz e quando usar (o Claude Code usa isso para routing)
- `model` — `opus` (recomendado), `sonnet` ou `haiku`
- `tools` — Lista de ferramentas que o agente pode usar

### Corpo do Agente (obrigatório)

Seções que todo agente deve ter:

```markdown
# Título do Agente

## Role
{Quem é o agente e qual sua especialidade}

## Foco de Análise
{Lista numerada dos pontos de atenção}

## Protocolo de Execução
### Fase 1: {Nome}
### Fase 2: {Nome}
### Fase 3: Entrega

## Estrutura Obrigatória de Resposta
{Template entre ``` com as seções exatas que o agente deve produzir}

## Persona e Tom de Voz
{Como o agente se comunica}

## Diretrizes Inegociáveis
{Regras que o agente nunca deve quebrar}
```

### Convenções

- **Diagramas Mermaid obrigatórios** na estrutura de resposta
- **Tabelas** para dados estruturados (gargalos, riscos, ações)
- **Referências a arquivo:linha** sempre que afirmar algo sobre código
- **Última diretriz** deve ser: "Respeite o CLAUDE.md do repositório sendo analisado, se existir."

---

## Como Testar um Agente

1. Copie o agente para `~/.claude/agents/`:
   ```bash
   cp agents/meu-agente.md ~/.claude/agents/
   ```

2. Abra o Claude Code em um projeto real:
   ```bash
   cd /caminho/do/projeto
   claude
   ```

3. Invoque o agente diretamente (sem o War Room completo):
   - O Claude Code vai usar o agente automaticamente quando a descrição casar com a tarefa
   - Ou mencione explicitamente: "Use o agente [Nome] para analisar..."

4. Verifique:
   - O agente segue o protocolo de fases?
   - O output segue a estrutura obrigatória?
   - Os diagramas Mermaid renderizam corretamente?
   - As referências a arquivo:linha estão corretas?

---

## Se For Adicionar ao Pipeline

Se o agente deve fazer parte do fluxo War Room:

1. **Prefixe o arquivo** com o número da posição: `03-meu-agente.md`
2. **Atualize** `memory/feedback_war_room_mode.md` adicionando o agente na posição correta
3. **Atualize** `install.sh` adicionando o mapeamento no array `AGENT_FILES`
4. **Atualize** docs: `ARCHITECTURE.md`, `EXAMPLES.md` e o README

---

## Convenções de Commit

Usamos [Conventional Commits](https://www.conventionalcommits.org/):

```
feat: adiciona agente Security Auditor ao pipeline
fix: corrige validação de frontmatter no CI
docs: atualiza exemplos de saída do SRE-CHAOS
chore: atualiza markdownlint config
```

**Tipos:**
- `feat` — Novo agente, nova funcionalidade
- `fix` — Correção de bug
- `docs` — Apenas documentação
- `chore` — CI, configs, manutenção
- `refactor` — Reestruturação sem mudar comportamento

---

## Processo de Pull Request

1. Faça suas mudanças na branch
2. Rode o lint localmente (se possível):
   ```bash
   # Markdown lint
   npx markdownlint-cli2 "**/*.md"

   # ShellCheck
   shellcheck install.sh
   ```
3. Abra um PR para `main`
4. Preencha o template do PR
5. Aguarde review e CI passar

---

## O que NÃO fazer

- Não remova agentes do pipeline sem discussão (abra uma issue antes)
- Não mude o comando de ativação (`ativar modo war room:`) sem consenso
- Não adicione dependências externas (o projeto é zero-dependency)
- Não inclua dados reais de projetos nos exemplos
- Não faça push direto para `main` (use PR)

---

## Ideias de Contribuição

- Traduzir agentes para inglês
- Criar agentes para novos domínios (FinTech, HealthTech, SaaS)
- Melhorar templates de output dos agentes
- Adicionar mais cenários ao `docs/EXAMPLES.md`
- Criar agente de Security Audit (OWASP Top 10)
- Criar agente de Performance Profiling
- Melhorar o `install.sh` com suporte a mais shells
