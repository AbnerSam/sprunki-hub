# Sprunki Hub 🎵

Catálogo interativo de jogos Sprunki - **Sem Anúncios**.
Futuramente: PWA, **Funciona Offline**

## O que é?

Um um launcher/catálogo para diferentes versões e mods do Sprunki.

- ✅ Sem anúncios invasivos do Unity/APK
- ✅ Interface responsiva para tablets antigos
- ✅ Extensível (adicione jogos editando `catalog.json`)

## Estrutura do Projeto

``` fileTree
sprunki-hub/
├── index.html              # Entry point principal
└── README.md              # Este arquivo

Nota: Array no index (única fonte)
- Futuramente: **`public/catalog.json`**: será a única fonte de verdade para o catálogo de jogos.
```

## Como Funciona?

### 1. **Catálogo Dinâmico** - Futuramente: (`catalog.json`)

Para adicionar novos jogos:

```js
{
  id: '1172002412',
  title: 'SPRUNKI (modded) retextured',
  thumb: 'https://uploads.scratch.mit.edu/get_image/project/1172002412_480x360.png'
},
{
  id: '1260865301',
  title: 'sprunki definitive phase 12 (E.S.B 4768’s version) (V2)',
  thumb: 'https://uploads.scratch.mit.edu/get_image/project/1260865301_480x360.png'
},
{
  id: '1129445410',
  title: 'Incredibox - Sprunki Retake FINAL UPDATE remix',
  thumb: 'https://uploads.scratch.mit.edu/get_image/project/1129445410_480x360.png'
}
```

### 2. **Tipos de Source Suportados**

#### `turbowarp` (Recomendado para Scratch)

- Usa TurboWarp (compilador Scratch rápido)
- URL: `https://turbowarp.org/{id}/embed`

## Adicionando Novos Jogos

### Opção A: Projeto existente no Scratch

1. Encontre o ID do projeto no Scratch (URL: `scratch.mit.edu/projects/{ID}`)

### Opção B: Arquivo sb3

## Roadmap

- [ ] Implementação de sb3
- [ ] Suporte à salvar jogos de fontes como sb3 para ter biblioteca própria
- [ ] Suporte PWA
- [ ] Suporte a busca dinâmica
- [ ] Favoritos/biblioteca pessoal
- [ ] Sync com conta do usuário
- [ ] Estatísticas de gameplay
- [ ] Temas (dark/light mode)

## Licença

Este projeto é para fins educacionais. Respeite as licenças dos jogos/mods que você adiciona ao catálogo.
