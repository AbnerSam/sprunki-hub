# Sprunki Hub 🎵

Catálogo interativo de jogos Sprunki - **Sem Anúncios**, **Funciona Offline**

## O que é?

Um PWA (Progressive Web App) que funciona como um launcher/catálogo para diferentes versões e mods do Sprunki. 

- ✅ Sem anúncios invasivos do Unity/APK
- ✅ Funciona offline (Service Worker com cache)
- ✅ Interface responsiva para tablets antigos
- ✅ Extensível (adicione jogos editando `catalog.json`)

## Estrutura do Projeto

```
sprunki-hub/
├── index.html              # Entry point principal
├── package.json            # Dependências e scripts
├── vite.config.js         # Configuração do Vite + PWA
├── public/
│   ├── catalog.json       # Catálogo de jogos (JSON dinâmico)
│   └── manifest.json      # PWA manifest
├── src/
│   ├── app.js             # Lógica principal (load catalog, render UI, play game)
│   └── sw.js              # Service Worker (cache + offline)
└── README.md              # Este arquivo

Nota: Catálogo (única fonte)
- **`public/catalog.json`**: é a única fonte de verdade para o catálogo de jogos. Edite esse arquivo para adicionar, remover ou atualizar entradas; o app carrega a versão mais recente ao abrir a página.
```

## Instalação & Início Rápido

### 1. Instalar dependências
```bash
npm install
```

### 2. Rodar dev server
```bash
npm run dev
```

Acesso em `http://localhost:5173` (ou URL que Vite informar)

### 3. Build para produção (GitHub Pages)
```bash
npm run build
```

Saída em `dist/` - enviar para GitHub Pages

## Como Funciona?

### 1. **Catálogo Dinâmico** (`catalog.json`)

Edit `public/catalog.json` para adicionar novos jogos:

```json
[
  {
    "id": "sprunki-classic",
    "name": "Sprunki",
    "icon": "🎵",
    "description": "O jogo original",
    "source_type": "turbowarp",
    "source_id": "1180826394",
    "version": "Clássico",
    "author": "Sprunki Original"
  },
  {
    "id": "sprunki-custom",
    "name": "Custom Sprunki",
    "icon": "🎸",
    "description": "Versão customizada",
    "source_type": "url",
    "source_url": "https://exemplo.com/sprunki.html",
    "version": "MOD",
    "author": "Seu Nome"
  }
]
```

### 2. **Tipos de Source Suportados**

#### `turbowarp` (Recomendado para Scratch)
```json
{
  "source_type": "turbowarp",
  "source_id": "1180826394"
}
```
- Usa TurboWarp (compilador Scratch rápido)
- URL: `https://turbowarp.org/embed/{id}`

#### `url` (Para arquivos .html customizados)
```json
{
  "source_type": "url",
  "source_url": "https://seu-dominio.com/jogo.html"
}
```

### 3. **Como o TurboWarp é Carregado?**

Quando você clica em "Jogar Agora", o app:
1. Lê o `catalog.json`
2. Constrói a URL do TurboWarp embed
3. Injeta um iframe com a URL
4. Service Worker cacheia os assets

```javascript
frameUrl = `https://turbowarp.org/embed/${currentGame.source_id}`;
```

### 4. **Cache & Offline**

Service Worker (`src/sw.js`):
- **Cache-first**: Assets estáticos (HTML, CSS, JSON)
- **Network-first**: TurboWarp player e assets do jogo (com fallback para cache)
- Sincronização automática ao reconectar

## Deployment (GitHub Pages)

1. **Build do projeto**
   ```bash
   npm run build
   ```

2. **Enviar para GitHub**
   ```bash
   git add -A
   git commit -m "feat: initial sprunki-hub"
   git push origin main
   ```

3. **Ativar GitHub Pages**
   - Repo → Settings → Pages
   - Source: Branch `main`, folder `/dist`

4. **PWA Installation**
   - Abrir no navegador
   - Clique no ícone de "instalar app" do navegador
   - O app aparecerá na home screen

## Adicionando Novos Jogos

### Opção A: Projeto existente no Scratch

1. Encontre o ID do projeto no Scratch (URL: `scratch.mit.edu/projects/{ID}`)
2. Edit `catalog.json`:

```json
{
  "id": "novo-jogo",
  "name": "Nome do Jogo",
  "icon": "🎮",
  "description": "Descrição curta",
  "source_type": "turbowarp",
  "source_id": "AQUI_VEM_O_ID",
  "version": "1.0",
  "author": "Autor"
}
```

### Opção B: Arquivo customizado

Hospede um `.html` em qualquer lugar (GitHub Pages, Vercel, etc) e use:

```json
{
  "source_type": "url",
  "source_url": "https://meu-dominio.com/meu-jogo.html"
}
```

## Troubleshooting

### "Jogo não carrega"
- Verifique internet (primeiro carregamento precisa de rede)
- Check console do browser (F12)
- Verifique se o projeto Scratch/TurboWarp ID é válido

### "Service Worker não está funcionando"
- Certifique-se que está em HTTPS (ou localhost)
- Limpe cache: DevTools → Application → Storage → Clear All
- Recarregue a página

### "Offline não funciona"
- PWA precisa que o site seja carregado **pelo menos uma vez** online
- Depois, Service Worker cacheia tudo

## Stack Técnico

- **Vite**: Build tool (rápido, moderno)
- **Vanilla JS**: Sem frameworks (leve)
- **PWA**: Service Worker + manifest.json
- **TurboWarp**: Compilador Scratch (compila para JS)
- **GitHub Pages**: Host gratuito

## Roadmap

- [ ] Suporte a busca dinâmica
- [ ] Favoritos/biblioteca pessoal
- [ ] Sync com conta do usuário
- [ ] Estatísticas de gameplay
- [ ] Temas (dark/light mode)

## Licença

Este projeto é para fins educacionais. Respeite as licenças dos jogos/mods que você adiciona ao catálogo.

## Contato & Contribuições

Dúvidas? Abra uma issue no repositório GitHub.

---

**Made with ❤️ for kids. No ads. No tracking.**
