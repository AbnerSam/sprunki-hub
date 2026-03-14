# AGENTS.md

## Visao rapida

Sprunki Hub e um launcher/catalogo web de jogos e mods do universo Sprunki.
O projeto atual e um site estatico em HTML, CSS e JavaScript puro que lista jogos e abre cada um via embed do TurboWarp.
O objetivo do produto e evoluir para um hub leve, sem anuncios, bom para tablets antigos, com catalogo dinamico, suporte a `.sb3` e funcionamento offline via PWA.

## Fonte de verdade

Leia nesta ordem ao iniciar uma sessao:

1. `README.md`
2. `docs/PRD.md`
3. `docs/ADR.md`
4. `docs/ROADMAP.md`
5. `docs/TASKS.md`
6. `index.html`
7. `docs/Relatório Técnico_ Ecossistema Sprunki e Estratégias de Implementação.md`

Se houver divergencia entre documentos, siga esta prioridade:

1. `docs/ADR.md`
2. `docs/PRD.md`
3. `README.md`

## Estado atual

- App estatico com catalogo em `catalog.json`
- Player via iframe do TurboWarp
- Hospedagem-alvo em GitHub Pages
- v1 concluida e validada em ambiente publicado
- v1.1 concluida com suporte real a `.sb3`
- Sem build step
- Sem testes automatizados
- Com schema inicial de `catalog.json` ja definido
- Sem PWA/service worker

## Objetivo atual do agent

Priorizar a evolucao do projeto nesta sequencia:

1. Manter estabilidade e coerencia documental da v1.1
2. Preparar backlog detalhado da v2
3. Avancar para suporte futuro a `cocrea-gandi`, depois download automatico de `.sb3`, PWA e offline nas fases seguintes

## Convencoes de trabalho

- Preserve a proposta web-first e leve do projeto
- Prefira HTML, CSS e JavaScript puro enquanto isso mantiver a simplicidade
- Nao introduza frameworks sem registrar a decisao em `docs/ADR.md`
- Mantenha compatibilidade com tablets antigos e navegadores moveis modernos
- Evite dependencias que aumentem peso, complexidade ou custo operacional
- Preserve compatibilidade com GitHub Pages como ambiente padrao de deploy
- Nao trate servidor local de desenvolvimento como requisito do projeto
- Trate `catalog.json` na raiz como fonte de verdade da v1
- Trate `public/sb3-files/scratch/` como area de `.sb3` exportados/originados do Scratch e executados via `sb3-file` no TurboWarp
- Trate `public/sb3-files/turbowarp/` como area de `.sb3` compativeis com TurboWarp
- Trate `public/sb3-files/cocrea-gandi/` como area de `.sb3` dependentes de runtime Gandi/Cocrea
- Use `docs/ROADMAP.md` apenas para definicoes macro por versao/fase
- Use `docs/TASKS.md` para rastrear microtasks da versao ativa
- Ao concluir a ultima task ativa de `docs/TASKS.md`, encerre a versao e limpe o arquivo
- Ao encerrar a versao, mantenha apenas as instrucoes do arquivo e um registro curto de encerramento da versao concluida
- Ao iniciar uma nova versao, remova o encerramento anterior e deixe apenas instrucoes + status atual + tasks da versao nova
- As tasks da versao seguinte so devem ser adicionadas quando a nova versao for oficialmente iniciada
- Nao manter backlog de qualquer tipo, ideias futuras ou tasks de versoes nao iniciadas em `docs/TASKS.md`
- Ao tomar uma decisao arquitetural relevante, registre em `docs/ADR.md`
- Ao mudar escopo, requisitos ou definicao de pronto, atualize `docs/PRD.md`

## Como validar mudancas

- Para mudancas estaticas simples, valide preferencialmente em ambiente publicado no GitHub Pages
- Para fluxos do catalogo, priorize validacao em ambiente publicado no GitHub Pages, conferindo renderizacao dos cards, carregamento do player e retorno da tela de jogo
- Servidor local pode ser usado apenas como apoio temporario, nunca como dependencia do fluxo oficial
- Para `sb3-file`, considere que servidores locais simples podem falhar por CORS ao servir o `project_url` para o TurboWarp embed; valide preferencialmente no GitHub Pages
- Para recursos offline/PWA, validar instalacao, cache e comportamento sem rede
- Se algum comando novo de validacao surgir no projeto, documente aqui

## O que nao quebrar

- A capacidade de abrir jogos do catalogo
- A navegacao simples entre lista e player
- O foco em experiencia sem anuncios e sem wrappers pesados de APK
- A compatibilidade com GitHub Pages e com o catalogo em JSON

## Entregavel esperado por sessao

Ao finalizar uma tarefa relevante:

- atualize a documentacao afetada
- mantenha coerencia com `docs/PRD.md`
- registre decisoes em `docs/ADR.md` quando necessario
- descreva com clareza o que mudou e o que falta
