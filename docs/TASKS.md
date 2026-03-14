# TASKS - Sprunki Hub

## Como usar este arquivo

- este arquivo acompanha microtasks operacionais das fases do roadmap
- `ROADMAP.md` continua sendo o plano macro por fase e versao
- cada task deve ter status explicito: `todo`, `doing`, `done`, `blocked`
- ao concluir uma task relevante, atualizar este arquivo na mesma sessao

## Fase 1 - Alinhamento documental

- `done` consolidar `README.md`, `AGENTS.md`, `docs/PRD.md` e `docs/ADR.md`
- `done` explicitar GitHub Pages como ambiente oficial de hospedagem e validacao
- `done` definir a v1 enxuta e registrar o que fica fora do escopo
- `done` registrar a decisao de escopo da v1 em `docs/ADR.md`
- `done` criar `docs/ROADMAP.md` para separar roadmap macro de documentacao de produto

## Fase 2 - Estrutura do catalogo

- `done` mover `public/catalog.json` para `catalog.json` na raiz do projeto
- `done` atualizar referencias documentais de `public/catalog.json` para `catalog.json`
- `done` validar o schema minimo da v1 com o arquivo na raiz
- `done` garantir que adicionar novos jogos exija apenas editar `catalog.json`

## Fase 3 - Launcher v1

- `done` ajustar `index.html` para consumir `./catalog.json`
- `done` revisar layout responsivo em desktop e tablet/mobile
- `done` revisar fluxo de abrir jogo e voltar para a lista
- `done` revisar estados basicos de carregamento, vazio e erro

## Fase 4 - Publicacao da v1

- `todo` validar o fluxo final no GitHub Pages
- `todo` revisar consistencia visual e textual da home e do player
- `todo` confirmar criterios de pronto da v1
