# Sprunki Hub

Launcher/catalogo web de jogos e mods do universo Sprunki.

O projeto existe para oferecer uma experiencia leve, sem anuncios invasivos e adequada para tablets antigos, usando a web como plataforma principal em vez de APKs pesados.

## Estado atual

- app estatico em `index.html`
- catalogo em `catalog.json` na raiz
- player via embed do TurboWarp
- fluxo pensado para hospedagem no GitHub Pages
- sem build step
- sem testes automatizados
- schema inicial de `catalog.json` definido
- sem PWA/offline ainda

## Direcao do projeto

O objetivo e evoluir o launcher nesta ordem:

1. alinhar documentacao e escopo da v1
2. consolidar `catalog.json` na raiz
3. fechar o launcher estatico e responsivo
4. publicar e validar a v1 no GitHub Pages

## Documentacao principal

- `AGENTS.md` - instrucao operacional viva para agents e sessoes futuras
- `docs/PRD.md` - fonte de verdade do produto
- `docs/ADR.md` - historico de decisoes ja tomadas
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
|- AGENTS.md
|- README.md
|- index.html
|- docs/
|  |- ADR.md
|  |- PRD.md
|  \- Relatório Técnico_ Ecossistema Sprunki e Estratégias de Implementação.md
\- sb3Files/
```

## Proximos marcos

- concluir o alinhamento documental da v1
- validar `catalog.json` na raiz
- ajustar `index.html` para consumir o catalogo na raiz
- validar a publicacao no GitHub Pages

## Licenca

Projeto com fins educacionais. Respeite as licencas e creditos dos jogos/mods adicionados ao catalogo.
