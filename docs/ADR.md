# ADR - Sprunki Hub

Este arquivo registra decisoes arquiteturais e estruturais ja tomadas no projeto.

---

## ADR-001 - Adotar abordagem web-first para substituir APKs pesados

- Status: aceito

### Contexto

Apps Android do ecossistema Sprunki costumam usar Unity, SDKs de anuncios, trackers e carregamento remoto de assets, o que prejudica desempenho e simplicidade de uso em tablets antigos.

### Decisao

O projeto seguira uma abordagem web-first, usando launcher web leve como principal forma de acesso aos jogos.

### Consequencias

- melhor adequacao a hardware fraco
- menos dependencia de wrappers nativos
- hospedagem e manutencao mais simples

---

## ADR-002 - Usar HTML, CSS e JavaScript puro na fase atual

- Status: aceito

### Contexto

O projeto ainda esta em fase inicial e precisa manter simplicidade operacional, baixo peso e facilidade de hospedagem estatica.

### Decisao

Manter a implementacao atual em HTML, CSS e JavaScript puro ate que exista motivacao clara para mudar de stack.

### Consequencias

- onboarding tecnico simples
- menor custo de build e deploy
- necessidade de disciplina manual na organizacao do codigo conforme o projeto crescer

---

## ADR-003 - Usar TurboWarp embed como estrategia inicial de player

- Status: aceito

### Contexto

Os jogos atuais do catalogo derivam do ecossistema Scratch/Sprunki e ja podem ser acessados por ID via TurboWarp.

### Decisao

Na fase atual, os jogos serao abertos por iframe usando `https://turbowarp.org/{id}/embed`.

### Consequencias

- entrega inicial mais rapida
- suporte imediato a projetos baseados em Scratch/TurboWarp
- suporte a `.sb3` ainda depende de evolucao posterior

---

## ADR-004 - Mover o catalogo para JSON como fonte de verdade

- Status: aceito

### Contexto

Hoje o catalogo esta hardcoded em `index.html`, o que dificulta manutencao e expansao.

### Decisao

O projeto migrara para um arquivo JSON de catalogo como fonte de verdade dos jogos exibidos no launcher.

### Consequencias

- adicionar itens ficara mais simples
- dados e interface ficarao desacoplados
- sera necessario definir schema e estrategia de carregamento

---

## ADR-005 - Centralizar contexto operacional e de produto em arquivos dedicados

- Status: aceito

### Contexto

Para agents e futuras sessoes trabalharem com consistencia, o projeto precisa externalizar contexto em arquivos rastreaveis no repositorio.

### Decisao

Adotar a seguinte estrutura documental:

- `AGENTS.md` como instrucao operacional viva
- `docs/PRD.md` como fonte de verdade do produto
- `docs/ADR.md` como historico de decisoes ja tomadas

### Consequencias

- melhor continuidade entre sessoes
- menor dependencia de contexto de chat
- necessidade de manter documentacao atualizada a cada mudanca importante

---

## ADR-006 - Definir `catalog.json` com objeto raiz e `source` tipado por item

- Status: aceito

### Contexto

O hardcode atual do catalogo usa apenas `id`, `title` e `thumb`, o que basta para o caso atual, mas nao acomoda bem a evolucao para multiplas origens como projetos TurboWarp e arquivos `.sb3`.

### Decisao

Adotar `catalog.json` na raiz do projeto com um objeto raiz no formato abaixo:

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

Cada item deve preservar os campos equivalentes ao hardcode atual e encapsular a origem em `source`, com `type` explicito.

### Consequencias

- a migracao do hardcode atual fica direta
- o catalogo ganha espaco para evoluir para `.sb3` sem refatoracao brusca
- o launcher precisara resolver o player com base em `source.type`
- o arquivo passa a suportar metadados de catalogo, como `version`, sem quebrar os itens

---

## ADR-007 - Adotar GitHub Pages como ambiente padrao de hospedagem e validacao

- Status: aceito

### Contexto

O projeto e um site estatico, sem backend obrigatorio, e o objetivo e manter uma publicacao simples, gratuita e compativel com tablets antigos. Tambem foi definido que o fluxo normal do projeto nao deve depender de servidor local de desenvolvimento.

### Decisao

Adotar GitHub Pages como ambiente padrao de hospedagem e validacao publicada do Sprunki Hub.
Servidor local pode existir apenas como apoio opcional de depuracao, nunca como requisito operacional do projeto.

### Consequencias

- as alteracoes precisam continuar compativeis com hospedagem estatica no GitHub Pages
- a documentacao deve tratar GitHub Pages como referencia principal de deploy e validacao
- o projeto evita introduzir ferramentas ou fluxos que obriguem ambiente local de desenvolvimento persistente

---

## ADR-008 - Definir a v1 como release enxuta focada em launcher estatico

- Status: aceito

### Contexto

O projeto possui varias possibilidades futuras, como busca, favoritos, PWA, offline e suporte real a `.sb3`, mas a prioridade imediata e fechar uma primeira versao estavel, simples e compativel com GitHub Pages.

### Decisao

Definir a v1 com o seguinte escopo:

- documentacao coerente entre `README.md`, `AGENTS.md`, `docs/PRD.md` e `docs/ADR.md`
- `catalog.json` como fonte de verdade na raiz do projeto
- `index.html` estatico e responsivo
- catalogo carregando corretamente sem backend
- fluxo simples de abrir jogo via TurboWarp e voltar para a lista

Ficam explicitamente fora da v1:

- busca
- favoritos
- PWA
- suporte real a `.sb3`
- download automatico de `.sb3`
- offline
- sync, conta, estatisticas e backend

### Consequencias

- a v1 prioriza entrega rapida e previsivel
- funcionalidades avancadas passam para roadmap pos-v1
- a documentacao deve refletir esse corte de escopo de forma explicita

---

## ADR-009 - Definir escopo da v1.1 com suporte real a `.sb3` preservando GitHub Pages

- Status: aceito

### Contexto

Com a v1 concluida, o proximo passo e habilitar suporte real a `.sb3`. Ao mesmo tempo, o projeto precisa manter as restricoes da arquitetura atual: hospedagem estatica, sem backend obrigatorio e compatibilidade integral com GitHub Pages.

### Decisao

Definir a v1.1 com foco em suporte real a `.sb3` via `source.path` e `source.url`, mantendo o fluxo principal do launcher e sem introduzir dependencia de servidor backend.

Definir como inegociavel que toda implementacao da v1.1 continue compativel com GitHub Pages como ambiente oficial de publicacao e validacao.

### Consequencias

- a v1.1 avanca capacidade funcional do catalogo sem mudar o modelo de deploy
- implementacoes que exijam backend ficam fora da v1.1
- download automatico, PWA e offline continuam para fases posteriores
- a documentacao operacional passa a usar `docs/ROADMAP.md` para macro e `docs/TASKS.md` para microtasks

---

## ADR-010 - Separar roadmap macro e tasks micro por versao

- Status: aceito

### Contexto

Havia mistura entre planejamento de release e rastreamento de tarefas operacionais, o que dificulta manutencao e gera retrabalho entre sessoes.

### Decisao

Definir o seguinte modelo documental:

- `docs/ROADMAP.md` para definicoes macro por versao/fase
- `docs/TASKS.md` para microtasks da versao ativa

Ao concluir a ultima task ativa de uma versao, `docs/TASKS.md` deve ser limpo, mantendo apenas as instrucoes do arquivo e um registro curto de encerramento da versao concluida.

Ao iniciar uma nova versao, o encerramento anterior deve ser removido e o arquivo deve conter apenas instrucoes + status atual + tasks da versao nova.

As tasks da versao seguinte so devem ser adicionadas quando a nova versao for oficialmente iniciada.

Nao deve haver backlog, ideias futuras ou tasks de versoes nao iniciadas em `docs/TASKS.md`.

### Consequencias

- melhor visibilidade de progresso por nivel (macro e micro)
- menos ruido historico em tasks operacionais
- onboarding mais rapido para novos agents/sessoes

---

## ADR-011 - Padronizar resolucao de `sb3-file` para `source.path` e `source.url`

- Status: aceito

### Contexto

A v1.1 introduz suporte real a `.sb3` sem backend, mantendo compatibilidade total com GitHub Pages.
Para evitar ambiguidade na montagem da URL do player e reduzir erros de catalogo, era necessario definir regras unicas para `source.path` e `source.url` em itens com `source.type = sb3-file`.

### Decisao

Para itens `sb3-file`, o launcher deve seguir as regras abaixo:

- `source.path` representa caminho local/relativo do arquivo `.sb3`, versionado junto ao site
- `source.path` deve ser resolvido para URL absoluta com base na URL atual da pagina antes de enviar ao TurboWarp via `project_url`
- `source.url` representa URL remota direta para o arquivo `.sb3`, com `https` e CORS habilitado
- quando `source.path` e `source.url` existirem ao mesmo tempo, `source.path` tem prioridade
- o valor efetivo resolvido (de `path` ou `url`) e sempre enviado para o player TurboWarp no parametro `project_url`

### Consequencias

- o catalogo ganha padrao claro para fontes locais e remotas de `.sb3`
- reduz falhas de execucao por caminhos relativos mal resolvidos em ambiente publicado
- mantem o projeto compativel com GitHub Pages e sem dependencia de backend

---

## ADR-012 - Reservar `cocrea-gandi` como tipo de origem futuro antes de PWA

- Status: aceito

### Contexto

Durante a validacao da v1.1 foi identificado que alguns projetos do ecossistema Sprunki dependem de extensoes do runtime Gandi/Cocrea, como `GandiQuake`, e portanto nao sao compativeis com execucao direta via TurboWarp usando `.sb3`.

O projeto precisa registrar uma extensao futura do schema sem implementar imediatamente esse suporte e sem misturar essa entrega com a fase posterior de PWA/offline.

### Decisao

Reservar `cocrea-gandi` como novo valor futuro de `source.type` no `catalog.json`.

Esse tipo representara projetos que exigem runtime/publicacao compativel com Gandi/Cocrea, preferencialmente via URL publica de projeto/embed em `source.projectUrl`.

O suporte real a `cocrea-gandi` deve ser planejado para uma versao futura anterior a PWA/offline.

### Consequencias

- o schema passa a acomodar projetos Gandi/Cocrea sem forcar compatibilidade falsa com `sb3-file`
- a v1.1 continua focada em `.sb3` compativel com TurboWarp
- a ordem do roadmap passa a tratar suporte Gandi/Cocrea antes de PWA/offline

### Convencao operacional derivada

- arquivos `.sb3` exportados/originados do Scratch e compativeis com TurboWarp devem ficar em `public/sb3-files/scratch/`
- arquivos `.sb3` compativeis com TurboWarp devem ficar em `public/sb3-files/turbowarp/`
- arquivos `.sb3` dependentes de runtime/extensoes Gandi/Cocrea devem ficar em `public/sb3-files/cocrea-gandi/`
- arquivos em `public/sb3-files/scratch/` podem entrar no catalogo como `sb3-file` quando a execucao no TurboWarp for valida
- mover um arquivo para `public/sb3-files/cocrea-gandi/` sinaliza que ele nao deve entrar no catalogo como `sb3-file` ate existir suporte real a `cocrea-gandi`

---

## ADR-013 - Suportar `scratch-mit-edu` como origem oficial de embed do Scratch

- Status: aceito

### Contexto

O catalogo ja suporta abertura via TurboWarp e `.sb3`, mas alguns itens podem precisar apontar diretamente para o player oficial do Scratch, sem intermediacao do runtime TurboWarp.

### Decisao

Adicionar `scratch-mit-edu` como novo valor suportado de `source.type`.

Esse tipo reutiliza `source.projectId` e deve resolver a execucao para o embed oficial do Scratch em `https://scratch.mit.edu/projects/{projectId}/embed`.

### Consequencias

- o catalogo passa a diferenciar explicitamente projetos que devem abrir no player oficial do Scratch
- `source.projectId` continua reutilizavel entre TurboWarp e Scratch, sem introduzir campo redundante
- o launcher mantem a logica de resolucao centralizada por `source.type`
