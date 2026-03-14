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
