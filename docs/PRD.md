# PRD - Sprunki Hub

## Visao do produto

Sprunki Hub e um launcher/catalogo web para reunir diferentes versoes e mods de Sprunki em uma experiencia leve, limpa e sem anuncios invasivos.
O produto deve funcionar bem em tablets antigos e navegadores moveis, priorizando rapidez, simplicidade e expansao progressiva.

Para a v1, o foco e propositalmente enxuto: documentacao coerente, `catalog.json` na raiz, `index.html` estatico e responsivo e fluxo basico de abrir jogos via TurboWarp em GitHub Pages.
Com a v1 concluida, a iteracao ativa passa a ser a v1.1, acompanhada em `docs/ROADMAP.md` (macro) e `docs/TASKS.md` (microtasks).

## Problema

As versoes mobile distribuidas como APK costumam ser pesadas, depender de internet constante, incluir rastreamento e carregar SDKs de anuncios desnecessarios.
Para o publico deste projeto, isso piora desempenho, experiencia de uso e confianca no app.

## Publico-alvo

- Pessoas que querem acessar varias versoes/mods de Sprunki em um unico lugar
- Usuarios com tablets antigos ou hardware limitado
- Responsaveis que querem uma experiencia mais limpa e segura para criancas
- Curadores que desejam manter um catalogo simples de mods baseados em Scratch/TurboWarp

## Proposta de valor

- Sem anuncios invasivos
- Muito mais leve do que APKs baseados em Unity
- Facil de expandir com novos jogos/mods
- Preparado para offline/PWA
- Experiencia simples de launcher: escolher e jogar

## Objetivos do produto

- Centralizar o acesso a mods e versoes de Sprunki
- Substituir a dependencia de APKs pesados por uma solucao web-first
- Permitir manutencao simples do catalogo
- Viabilizar suporte futuro a `.sb3`
- Oferecer experiencia adequada para uso recorrente em tablet

## Escopo atual

- Pagina unica em `index.html`
- Lista de jogos definida em `catalog.json` na raiz do projeto
- Cards com thumbnail, titulo e CTA para abrir o jogo
- Abertura do jogo por resolucao de `source.type`, com suporte atual a `turbowarp-project`, `scratch-mit-edu` e `sb3-file`
- Retorno do modo jogo para a lista principal

## Escopo alvo

- Catalogo dinamico via JSON
- `catalog.json` na raiz como fonte de verdade da v1
- `index.html` estatico e responsivo
- Fluxo simples de abrir jogo via TurboWarp e retornar para a lista
- Compatibilidade com GitHub Pages como ambiente oficial de publicacao

## Fora de escopo por enquanto

- Busca
- Favoritos ou biblioteca pessoal local
- PWA
- Suporte real a `.sb3`
- Download automatico de `.sb3`
- Offline
- Sincronizacao com conta de usuario
- Estatisticas de gameplay
- Backend proprio
- Sistema social ou multiplayer
- Reescrita em framework sem necessidade clara

## Requisitos funcionais

### RF-01 - Listagem de jogos

O sistema deve exibir um catalogo visual com os jogos disponiveis.

### RF-02 - Execucao de jogo

O sistema deve permitir abrir um jogo a partir do catalogo em um player integrado.

### RF-03 - Catalogo dinamico

O sistema deve carregar os itens do catalogo a partir de um arquivo JSON, sem exigir alteracao direta no HTML para adicionar novos jogos.

### RF-04 - Suporte a multiplas fontes

O sistema deve manter o catalogo estruturado para evolucao futura de tipos de origem, mesmo que a v1 opere apenas com o fluxo principal via TurboWarp.

### RF-05 - Navegacao simples

O usuario deve conseguir entrar e sair de um jogo com poucos toques/cliques.

### RF-06 - Busca e filtragem

Fora do escopo da v1.

### RF-07 - Favoritos locais

Fora do escopo da v1.

### RF-08 - Modo instalavel

Fora do escopo da v1.

## Requisitos nao funcionais

- Interface responsiva para desktop e mobile
- Boa usabilidade em tablets antigos
- Baixo peso de carregamento
- Ausencia de anuncios invasivos e trackers desnecessarios
- Arquitetura simples de manter
- Compatibilidade com hospedagem estatica
- GitHub Pages como ambiente padrao de hospedagem e validacao publicada
- O produto nao deve depender de servidor local de desenvolvimento para seu fluxo normal de uso ou manutencao basica

## Restricoes

- O projeto deve continuar funcionando sem backend obrigatorio
- A hospedagem preferencial e o GitHub Pages
- A implementacao deve evitar stack pesada sem ganho claro
- O catalogo precisa continuar facil de editar e versionar

## Schema inicial de `catalog.json`

Na v1, `catalog.json` sera mantido na raiz do projeto e tera um objeto raiz simples, preparado para crescer sem quebrar compatibilidade.

```json
{
  "version": 1,
  "items": [
    {
      "id": "1172002412",
      "slug": "sprunki-modded-retextured",
      "title": "SPRUNKI (modded) retextured",
      "thumb": "https://uploads.scratch.mit.edu/get_image/project/1172002412_480x360.png",
      "source": {
        "type": "turbowarp-project",
        "projectId": "1172002412"
      },
      "tags": ["sprunki", "scratch", "mod"]
    }
  ]
}
```

### Campos obrigatorios por item

- `id`: identificador estavel interno do item no catalogo
- `slug`: identificador legivel para URLs futuras, logs e referencias
- `title`: nome exibido ao usuario
- `thumb`: thumbnail do card
- `source.type`: tipo da origem do jogo

### Campos opcionais por item

- `source.projectId`: ID do projeto quando a origem for TurboWarp/Scratch
- `source.path`: caminho local de arquivo, pensado para `.sb3`
- `source.url`: URL remota quando a origem nao for local
- `source.projectUrl`: URL publica do projeto quando a origem depender de runtime externo publicado
- `tags`: marcadores simples para busca e filtros futuros
- `description`: texto curto opcional para detalhes futuros
- `featured`: destaque eventual na home

### Tipos de `source.type` previstos

- `turbowarp-project`: abre via projeto identificado por ID
- `scratch-mit-edu`: abre via embed direto de projeto publicado no Scratch
- `sb3-file`: aponta para arquivo `.sb3` local ou remoto
- `cocrea-gandi`: reserva para projetos publicados em runtime Gandi/Cocrea via embed externo
- `external-url`: reserva para compatibilidade futura com fontes externas controladas

### Regras de resolucao para `scratch-mit-edu`

- `scratch-mit-edu` usa `source.projectId` como identificador do projeto publicado no Scratch
- o launcher deve abrir esse tipo via embed oficial de `https://scratch.mit.edu/projects/{projectId}/embed`
- esse tipo e indicado quando o catalogo precisa apontar explicitamente para o player oficial do Scratch, sem passar pelo runtime do TurboWarp

### Regras previstas para `cocrea-gandi` (versao futura)

- `cocrea-gandi` nao faz parte do escopo implementado da v1.1
- esse tipo deve ser usado apenas para projetos publicados em plataforma/runtime compativel com extensoes Gandi
- a modelagem prevista deve priorizar `source.projectUrl` como URL publica do projeto/embed
- o launcher devera abrir esse tipo por embed/iframe do runtime compativel, sem tentar executar o projeto como `.sb3` no TurboWarp
- a introducao de suporte real deve acontecer antes da fase de PWA/offline

### Regras de resolucao para `sb3-file` (v1.1)

- `source.path` deve apontar para caminho local/relativo do `.sb3` dentro do site
- `source.path` sera resolvido para URL absoluta com base na URL atual da pagina
- `source.url` deve apontar para URL remota direta do `.sb3` usando `https` e CORS
- quando `source.path` e `source.url` coexistirem no mesmo item, `source.path` tem prioridade
- o launcher deve enviar a URL final resolvida para o TurboWarp via parametro `project_url`

### Convencao atual de organizacao de arquivos `.sb3`

- `public/sb3-files/scratch/` concentra arquivos `.sb3` exportados/originados do Scratch e executados pelo fluxo `sb3-file` via TurboWarp
- `public/sb3-files/turbowarp/` concentra arquivos `.sb3` destinados ao fluxo `sb3-file`
- `public/sb3-files/cocrea-gandi/` concentra arquivos `.sb3` identificados como dependentes de runtime/extensoes Gandi/Cocrea
- arquivos mantidos em `public/sb3-files/scratch/` podem ser cadastrados como `sb3-file` quando forem compativeis com execucao no TurboWarp
- arquivos mantidos em `public/sb3-files/cocrea-gandi/` nao devem ser considerados compativeis com `sb3-file`
- enquanto nao houver um `.sb3` compativel em `public/sb3-files/turbowarp/` ou `public/sb3-files/scratch/`, o `catalog.json` pode permanecer sem itens locais de teste para `sb3-file`

### Regras de modelagem

- o schema deve preservar compatibilidade com o hardcode atual de `id`, `title` e `thumb`
- o schema deve manter `source` como objeto para suportar multiplos tipos de origem sem proliferar campos soltos
- novos campos devem ser adicionados de forma opcional sempre que possivel
- a v1 do launcher deve ignorar com seguranca campos desconhecidos

## Definicao de pronto

O projeto sera considerado pronto em sua primeira versao robusta quando atender aos pontos abaixo:

- `catalog.json` na raiz do projeto
- launcher responsivo e estavel em mobile e desktop
- player integrado com fluxo claro de abrir/fechar jogo
- catalogo renderizando corretamente sem backend
- documentacao coerente entre `README.md`, `AGENTS.md`, `docs/PRD.md` e `docs/ADR.md`
- publicacao compativel com GitHub Pages

## Status da release

- v1: concluida
- ambiente de validacao oficial: GitHub Pages
- v1.1: em andamento
- proximas iteracoes: definidas no `docs/ROADMAP.md`

## Roadmap por fases

### Fase 1 - Base documental e alinhamento

- Status: concluida
- Consolidar PRD, ADR e guia operacional
- Revisar README para refletir a estrategia atual
- Explicitar GitHub Pages como ambiente oficial
- Definir v1 enxuta e o que fica fora do escopo

### Fase 2 - MVP estruturado

- Status: concluida
- Mover `catalog.json` para a raiz
- Fechar schema minimo da v1
- Garantir que novos jogos sejam adicionados so editando JSON

### Fase 3 - Catalogo dinamico

- Status: concluida
- Ajustar `index.html` para consumir `catalog.json` na raiz
- Garantir layout responsivo
- Manter navegacao simples entre lista e player
- Tratar estados basicos de erro e vazio

### Fase 4 - Publicacao da v1

- Status: concluida
- Validar no GitHub Pages
- Revisar consistencia visual e textual
- Fechar criterios de pronto da v1

## Metricas de sucesso

- abrir um jogo em poucos segundos em conexao comum
- navegar pelo catalogo sem travamentos perceptiveis
- adicionar novo item ao catalogo com edicao simples de dados

## Perguntas em aberto

- estrategia pos-v1 para suporte real a `.sb3`
- momento ideal de introduzir favoritos locais
