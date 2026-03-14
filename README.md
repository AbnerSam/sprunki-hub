# Sprunki Hub

Launcher/catalogo web de jogos e mods do universo Sprunki.

O projeto existe para oferecer uma experiencia leve, sem anuncios invasivos e adequada para tablets antigos, usando a web como plataforma principal em vez de APKs pesados.

URL público atual=<https://abnersam.github.io/sprunki-hub/>

## Estado atual

- app estatico em `index.html`
- catalogo em `catalog.json` na raiz
- player via embed do TurboWarp
- fluxo pensado para hospedagem no GitHub Pages
- v1 concluida e validada em ambiente publicado
- sem build step
- sem testes automatizados
- schema inicial de `catalog.json` definido
- sem PWA/offline ainda

## Direcao atual

Com a v1 concluida, os proximos incrementos estao no roadmap pos-v1:

1. v1.1: suporte real a `.sb3`
2. v2: busca, refinamentos visuais, usabilidade e favoritos locais
3. v2.1: download automatico de `.sb3`
4. v2.2: PWA e offline

## Documentacao principal

- `AGENTS.md` - instrucao operacional viva para agents e sessoes futuras
- `docs/PRD.md` - fonte de verdade do produto
- `docs/ADR.md` - historico de decisoes ja tomadas
- `docs/ROADMAP.md` - definicoes macro por versao/fase
- `docs/TASKS.md` - rastreamento de microtasks da versao ativa
- `docs/Relatório Técnico_ Ecossistema Sprunki e Estratégias de Implementação.md` - contexto tecnico sobre o ecossistema Sprunki e a motivacao web-first

## Como funciona hoje

- a tela inicial carrega o catalogo a partir de JSON e renderiza os cards de jogos/mods
- ao clicar em `Jogar`, o site resolve a URL do player com base em `source.type`
- o usuario pode voltar do player para a lista principal sem recarregar a pagina

## Stack atual

- HTML
- CSS
- JavaScript puro
- TurboWarp embed

## Principios do projeto

- web-first e leve
- sem anuncios invasivos
- compativel com tablets antigos
- GitHub Pages como hospedagem padrao do projeto
- sem dependencia de servidor local de desenvolvimento como requisito de uso
- sem frameworks sem necessidade clara

## Hospedagem e validacao

- o ambiente padrao do projeto e o GitHub Pages
- alteracoes devem continuar compativeis com hospedagem estatica
- a validacao principal deve considerar o comportamento publicado no GitHub Pages
- servidor local pode ser usado apenas como apoio eventual, nunca como requisito do fluxo do projeto

## Estrutura atual

```text
sprunki-hub/
|- catalog.json
|- AGENTS.md
|- README.md
|- index.html
|- docs/
|  |- ADR.md
|  |- PRD.md
|  |- ROADMAP.md
|  |- TASKS.md
|  \- Relatório Técnico_ Ecossistema Sprunki e Estratégias de Implementação.md
\- sb3-files/
```

## Proximos marcos

- executar as tasks da v1.1 em `docs/TASKS.md`
- preparar backlog detalhado da v2
- manter consistencia de docs a cada fase concluida

## Licenca

Projeto com fins educacionais. Respeite as licencas e creditos dos jogos/mods adicionados ao catalogo.
