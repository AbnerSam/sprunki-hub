# ROADMAP - Sprunki Hub

## Status geral

- Versao atual alvo: v1
- Hospedagem oficial: GitHub Pages
- Status da v1: em andamento

## Objetivo da v1

Entregar um launcher web estatico, leve e responsivo para o catalogo Sprunki, com documentacao coerente, `catalog.json` na raiz do projeto e fluxo simples de abrir jogos via TurboWarp em hospedagem estatica no GitHub Pages.

## Escopo da v1

- documentacao coerente entre `README.md`, `AGENTS.md`, `docs/PRD.md` e `docs/ADR.md`
- `catalog.json` como fonte de verdade na raiz do projeto
- `index.html` estatico e responsivo
- catalogo carregando corretamente sem backend
- fluxo simples de abrir jogo via TurboWarp e voltar para a lista

## Fora da v1

- busca
- favoritos
- PWA
- suporte real a `.sb3`
- download automatico de `.sb3`
- offline
- sync, conta, estatisticas e backend

## Fases da v1

### Fase 1 - Alinhamento documental

- Status: concluida
- consolidar `README.md`, `AGENTS.md`, `docs/PRD.md` e `docs/ADR.md`
- explicitar GitHub Pages como ambiente oficial
- definir v1 enxuta e o que fica fora do escopo

### Fase 2 - Estrutura do catalogo

- Status: concluida
- mover `catalog.json` para a raiz
- fechar schema minimo da v1
- garantir que novos jogos sejam adicionados so editando JSON

### Fase 3 - Launcher v1

- Status: concluida
- ajustar `index.html` para consumir `catalog.json` na raiz
- garantir layout responsivo
- manter navegacao simples entre lista e player
- tratar estados basicos de erro e vazio

### Fase 4 - Publicacao da v1

- Status: pendente
- validar no GitHub Pages
- revisar consistencia visual e textual
- fechar criterios de pronto da v1

## Definicao de pronto da v1

- `catalog.json` na raiz do projeto
- `index.html` responsivo em desktop e tablet/mobile
- catalogo renderiza corretamente
- jogo abre a partir do catalogo
- retorno da tela de jogo funciona
- documentacao coerente com o escopo enxuto
- publicacao compativel com GitHub Pages

## Roadmap pos-v1

### v1.1

- busca
- refinamentos visuais
- melhorias de usabilidade

### v1.2

- favoritos locais

### v2

- suporte real a `.sb3`
- download automatico
- PWA
- offline
