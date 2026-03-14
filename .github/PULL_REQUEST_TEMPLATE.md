## Descrição

<!-- Descreva o que essa PR faz e por quê -->

## Tipo de Mudança

- [ ] Novo agente
- [ ] Melhoria em agente existente
- [ ] Correção de bug
- [ ] Documentação
- [ ] Infraestrutura (CI, scripts)

## Checklist

- [ ] Testei localmente com Claude Code
- [ ] Agentes têm frontmatter YAML válido (`name`, `description`, `model`, `tools`)
- [ ] Agentes seguem a estrutura obrigatória (Role, Protocolo, Estrutura de Resposta, Persona, Diretrizes)
- [ ] Documentação atualizada (se aplicável)
- [ ] `install.sh` atualizado (se adicionei/removi agente)
- [ ] `feedback_war_room_mode.md` atualizado (se alterei o pipeline)

## Como Testar

<!-- Descreva como reproduzir/testar a mudança -->

1. Instale os agentes: `./install.sh --force`
2. Abra Claude Code em um projeto
3. Execute: `ativar modo war room: [feature]`
4. Verifique que...
