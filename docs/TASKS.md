# TASKS - Sprunki Hub

## Como usar este arquivo

- este arquivo acompanha microtasks operacionais das fases do roadmap
- `ROADMAP.md` continua sendo o plano macro por fase e versao
- cada task deve ter status explicito: `todo`, `doing`, `done`, `blocked`
- ao concluir uma task relevante, atualizar este arquivo na mesma sessao
- ao concluir a ultima task ativa da versao, encerrar a versao e limpar este arquivo
- ao encerrar a versao, manter apenas instruções + 1 linha curta de encerramento da versão finalizada
- ao iniciar nova versao remover o encerramento anterior e deixar apenas instruções + status atual + tasks da versão nova
- as tasks da versao seguinte so entram quando a nova versao for oficialmente iniciada
- nao manter backlog de qualquer tipo, ideias futuras ou tasks de versoes nao iniciadas neste arquivo

## Status atual

- v1.1 iniciada

## v1.1 - Suporte real a `.sb3`

### Fase 1 - Planejamento tecnico

- `done` revisar schema atual de `sb3-file` no `catalog.json`
- `done` definir formato final de resolucao para `source.path` e `source.url`
- `done` registrar decisao no `docs/ADR.md` se houver ajuste arquitetural

### Fase 2 - Implementacao

- `done` ajustar o player para abrir `.sb3` local via `source.path`
- `done` ajustar o player para abrir `.sb3` remoto via `source.url`
- `done` melhorar mensagens de erro para itens `.sb3` invalidos
- `done` incluir itens reais de teste `.sb3` no `catalog.json`

### Fase 3 - Validacao publicada

- `todo` publicar no GitHub Pages
- `todo` validar `sb3-file` com `source.path`
- `todo` validar `sb3-file` com `source.url`
- `todo` validar ausencia de regressao em `turbowarp-project`
