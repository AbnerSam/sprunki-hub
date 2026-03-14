# **Relatório Técnico: Arquitetura e Engenharia Reversa dos Apps Sprunki (Android)**

Este relatório detalha a stack tecnológica e os métodos de desenvolvimento utilizados na criação dos aplicativos Android baseados no universo Sprunki, após a análise exaustiva de três amostras representativas.

## **1\. Stack Tecnológica Dominante**

Diferente da versão web original (Scratch), as versões mobile distribuídas em lojas de APKs não são WebViews.  
•Engine de Jogo: Unity (Versões 2021.x a 2022.x).  
•Scripting Backend: IL2CPP (Intermediate Language To C++). O código C\# é convertido em C++ e compilado nativamente (libil2cpp.so), o que melhora a performance, mas dificulta a engenharia reversa.  
•Arquitetura de Assets: Unity Addressables. Os apps não contêm todos os sons e imagens localmente. Eles baixam "bundles" (pacotes de assets) de CDNs (como CloudFront) durante a execução. Isso explica por que o jogo exige internet mesmo parecendo simples.

## **2\. Anatomia do Aplicativo**

Análise do primeiro APK concluída (sprunki-all-phases-beat-maker-v0.3.5-mod.apk).  
Diagnóstico Técnico:  
Este APK não é um simples WebView. Ele foi desenvolvido utilizando a engine Unity (versão 2022.3.62f2).  
Estrutura: Possui bibliotecas nativas (libunity.so, libil2cpp.so) e utiliza o sistema de Addressables da Unity para carregar os assets do jogo (sons e imagens) dinamicamente de servidores remotos (CloudFront).  
Anúncios: Encontrei uma quantidade massiva de SDKs de publicidade integrados (AppLovin, Facebook Audience Network, Pangle, Google Ads, Unity Ads, etc.). Mesmo sendo uma versão "MOD", o código base está saturado de ganchos para monetização.  
Conexão: O jogo demanda internet para baixar os "bundles" de assets que não estão inclusos no APK base (isso explica por que "desligar a internet não resolve" nos outros jogos que você testou).  
Conclusão: É um app nativo (Unity), mas extremamente pesado e dependente de servidores externos para o conteúdo do jogo, além de possuir muitos rastreadores de anúncios.  
Pode me enviar o segundo arquivo para eu comparar se ele segue a mesma linha ou se é o wrapper que suspeitávamos.

Análise do segundo arquivo concluída (DuoMix\_7.10\_APKPure.xapk).  
Diagnóstico Técnico:  
Este arquivo é um XAPK (Bundle) que também utiliza a engine Unity.  
Arquitetura: Assim como o primeiro, é um app nativo Unity (libunity.so, libil2cpp.so). Ele foi dividido em múltiplos APKs (Split APKs), onde o código nativo está no arquivo de configuração (config.arm64\_v8a.apk).  
Anúncios e Rastreamento: Possui permissões extremamente invasivas, incluindo READ\_PHONE\_STATE (para identificar o aparelho), ACCESS\_WIFI\_STATE, e múltiplos SDKs de anúncios (AppLovin, Google Ads).  
Particularidade: Ele utiliza o sistema de localização da Unity e também o sistema de Addressables para carregar assets via CDN.  
Resumo da comparação:  
Ambos os APKs (LiteAPKs e APKPure) não são apenas WebViews, mas jogos Unity nativos. No entanto, eles são "re-skins" ou ports não oficiais do projeto original do Scratch, recheados de publicidade e rastreadores. Eles são "pesados" para um tablet antigo não apenas pelo jogo em si, mas por toda a infraestrutura de anúncios rodando em background.

Os apps são estruturados como "Recipientes de Monetização":  
•Core do Jogo: Um player de áudio/animação implementado em Unity que replica a lógica do Scratch original.  
•Camada de Publicidade (Ad-Stack): O ponto mais crítico. Todos os apps analisados possuem:  
•Mediation SDKs: AppLovin (MAX), IronSource, Mintegral.  
•Ad Networks: Facebook Audience Network, Pangle (TikTok Ads), Google AdMob, Unity Ads.  
•Analytics/Trackers: Firebase Analytics, AppsFlyer, Adjust, Crashlytics.  
•Permissões Invasivas: Permissões como READ\_PHONE\_STATE, ACCESS\_WIFI\_STATE e AD\_ID são usadas para criar perfis de usuário e direcionar anúncios, o que é desnecessário para um jogo de música infantil.

## **3\. Por que isso é ruim para o seu caso?**

•Hardware Antigo: O tablet antigo sofre para rodar a engine Unity \+ os processos de background dos 5+ SDKs de anúncios que ficam tentando carregar vídeos em cache.  
•Consumo de Dados: Como os assets são baixados via Addressables, o app consome internet constantemente.

## **4\. Veredito e Recomendação**

Os APKs analisados são "bloatware" de publicidade.  

A melhor solução técnica:  
1.Ignorar os APKs: Eles não oferecem uma base limpa para modificação.  
2.Solução Web Pura (Caminho Turbowarp): Usar o código original do Scratch compilado via TurboWarp.  
•Vantagem: É JS puro, roda no navegador do tablet (Chrome/Samsung Internet), não tem processos de background e podemos embutir todos os sons no arquivo para funcionar offline.  
•Customização: Posso criar para você um index.html único que você hospeda no GitHub Pages.  
Análise Finalizada. Estou pronto para preparar o seu ambiente "limpo" se desejar seguir por este caminho.

1\. TurboWarp  
Ter um único Player (o motor) e carregar diferentes arquivos de jogos (assets \+ lógica) dinamicamente.  
2\. Tornando o Catálogo Dinâmico (Estilo "Mihon" para Sprunki)  
implementar um sistema de "Fontes/repos". Em vez de um arquivo HTML estático para cada jogo, criando um Dashboard/Launcher simples:  
O Launcher: Uma Page (hospedado no GitHub Pages) leve.  
O Catálogo: Um arquivo catalog.json que contém links para os arquivos .sb3 de diferentes versões do Sprunki.  
O Player: Quando o sobrinho clica em uma versão, o Launcher carrega o motor do TurboWarp e faz o "fetch" do arquivo .sb3 correspondente.  
3\. Implementando "Fontes" (Mihon-like)  
Podemos estruturar a solução para que possa adicionar novos jogos apenas enviando um novo arquivo .sb3 para uma pasta no GitHub ou adicionando uma URL externa no JSON:  
O motor do TurboWarp que recebe o ID/URL do jogo via Query String.  
sources.json  
Onde você cadastra os novos Sprunkis (nome, ícone, link do .sb3).  
Ele será:  
PWA (Progressive Web App): Você "instala" no tablet e ele ganha ícone de app, rodando em tela cheia sem barras de navegador.  
Cache Inteligente: Uma vez que ele carregar um Sprunki, o Service Worker pode salvar os assets, permitindo que ele jogue offline depois.  
Extensível: só precisará editar um JSON para adicionar novos mods que encontrar no Itch.io ou Cocrea.

Vamos pensar na stack. A: Web-First (PWA/Launcher):  
Vantagem: Extremamente leve para o tablet antigo. Gerencia perfeitamente versões baseadas em Scratch/TurboWarp.

2\. A Abordagem "Mihon": O Mihon funciona com extensions (JS/DEX). Para Sprunki, as "extensões" seriam os arquivos .sb3 (Scratch). É muito mais fácil tratar cada mod como um arquivo de dados (.sb3) do que como um executável (.apk).  
Se o objetivo é ter um catálogo dinâmico que aceite "fontes":  
Padronização: Transformar tudo em Web-based. Mesmo os mods que hoje estão em APK, a maioria nasceu no Scratch. É mais eficiente localizar o .sb3 original do que lutar contra o APK Unity.  
Arquitetura de Fontes:  
engine: TurboWarp Wrapper.
offline\_support: se deve fazer cache total.
Tenho host hostinger compartilhada, roda php e nodejs, embora eu prefira rodar isso no githubpages, cloudflare workers ou outra alternativa free.
GitHub Pages.
Usaremos o turbowarp-player via Iframe ou injeção direta de script para carregar os arquivos .sb3 local ou de fonte link.
Um arquivo catalog.json no repositório. Para adicionar um novo Sprunki, você só adiciona um objeto no JSON.

3\. Arquitetura do Catálogo (O segredo da dinamicidade)  
Podemos estruturar o seu catalog.json

4\. A Stack "Pé no Chão" Para rodar liso no seu GitHub Pages e no tablet:  
Estrutura: HTML5 simples
CSS puro para o layout dos cards ser responsivo e bonito sem esforço.  
Vanilla JS para ler o JSON e injetar o Iframe do TurboWarp.

## **6\. Fontes**

<https://turbowarp.org/1172002412>
<https://turbowarp.org/1260865301>
<https://turbowarp.org/1129445410>

<https://scratch.mit.edu/studios/36388352>
<https://scratch.mit.edu/studios/50687547>
<https://scratch.mit.edu/studios/35868177>

<https://itch.io/search?q=sprunk>

## **7\. Estrutura Embed TurboWarp**

<https://turbowarp.org/${currentGame.source_id}/embed>

## **8\. Doc TurboWarp**

<https://docs.turbowarp.org/embedding>
