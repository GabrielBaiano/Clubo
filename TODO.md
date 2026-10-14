# 📋 Clubo - Roadmap & TODO

Este documento rastreia as melhorias, novas funcionalidades, otimizações de performance e correções planejadas para o **Clubo**.

---

## ⚡ Fase 0: Performance & Arquitetura (Backend, DB & WebSockets)

- [x] **Modo WAL no SQLite & Otimização de Concorrência**
  - *Descrição:* Configurar `PRAGMA journal_mode = WAL;` e `PRAGMA synchronous = NORMAL;` para evitar locks de tabela durante leituras/escritas concorrentes.
  - *Arquivos envolvidos:* [`db.js`](file:///home/gabrielgama/repo-personal/foliate-jam/db.js)
- [x] **Índices no Banco de Dados SQLite**
  - *Descrição:* Adicionar índices explícitos para `room_id`, `discord_id` e `last_active` nas tabelas `room_members`, `highlights` e `rooms`.
  - *Arquivos envolvidos:* [`db.js`](file:///home/gabrielgama/repo-personal/foliate-jam/db.js)
- [x] **Throttling de Cursor ao Vivo via WebSockets**
  - *Descrição:* Aplicar throttling de 30-50ms na transmissão dos eventos `mousemove` do cursor dos leitores.
  - *Arquivos envolvidos:* [`bookclub.js`](file:///home/gabrielgama/repo-personal/foliate-jam/bookclub.js), [`server.js`](file:///home/gabrielgama/repo-personal/foliate-jam/server.js)
- [x] **Batching / Debounce de Posição (`handleRelocate`)**
  - *Descrição:* Manter a posição em memória e agrupar atualizações no banco SQLite para reduzir IO excessivo em navegação rápida.
  - *Arquivos envolvidos:* [`server.js`](file:///home/gabrielgama/repo-personal/foliate-jam/server.js)
- [x] **Eliminação de Chamadas N+1 ao Supabase Storage**
  - *Descrição:* Otimizar checagem de existência do arquivo EPUB no endpoint `/api/my-rooms` armazenando o estado na tabela `rooms` em vez de chamar `.list()` em loop.
  - *Arquivos envolvidos:* [`server.js`](file:///home/gabrielgama/repo-personal/foliate-jam/server.js)

---

## 🚪 Fase 1: Onboarding e Experiência Inicial (UX)

- [x] **Modo Convidado ("Read as Guest")**
  - *Descrição:* Permitir criar salas e entrar em salas sem obrigatoriedade imediata de login com o Discord, reduzindo a fricção inicial de novos leitores.
  - *Arquivos envolvidos:* [`server.js`](file:///home/gabrielgama/repo-personal/foliate-jam/server.js), [`bookclub.js`](file:///home/gabrielgama/repo-personal/foliate-jam/bookclub.js), [`reader.html`](file:///home/gabrielgama/repo-personal/foliate-jam/reader.html)
- [x] **Banner de Vinculação de Perfil Discord**
  - *Descrição:* Exibir opção para o leitor convidado migrar para uma conta Discord salva sem perder seu progresso ou destaques.
  - *Arquivos envolvidos:* [`bookclub.js`](file:///home/gabrielgama/repo-personal/foliate-jam/bookclub.js), [`reader.html`](file:///home/gabrielgama/repo-personal/foliate-jam/reader.html)

---

## 🎨 Fase 2: Personalização Tipográfica e Temas Visuais

- [x] **Seletor de Família de Fontes (Font Family)**
  - *Descrição:* Alternar entre Serif (Merriweather/Georgia), Sans-Serif (Inter), Monospace, OpenDyslexic e Padrão da Editora.
  - *Arquivos envolvidos:* [`reader.js`](file:///home/gabrielgama/repo-personal/foliate-jam/reader.js), [`reader.html`](file:///home/gabrielgama/repo-personal/foliate-jam/reader.html)
- [ ] **Ajuste de Margens Laterais e Largura da Coluna**
  - *Descrição:* Permitir alterar a largura útil do texto (Estrita, Normal, Larga).
  - *Arquivos envolvidos:* [`paginator.js`](file:///home/gabrielgama/repo-personal/foliate-jam/paginator.js), [`reader.js`](file:///home/gabrielgama/repo-personal/foliate-jam/reader.js)
- [x] **Novos Temas Visuais de Leitura**
  - *Descrição:* Adicionar temas OLED Black (`#000000`), Warm Parchment (Sepia suave) e Solarized Dark.
  - *Arquivos envolvidos:* [`reader.js`](file:///home/gabrielgama/repo-personal/foliate-jam/reader.js), [`reader.html`](file:///home/gabrielgama/repo-personal/foliate-jam/reader.html), [`bookclub.css`](file:///home/gabrielgama/repo-personal/foliate-jam/bookclub.css)

---

## 🤝 Fase 3: Recursos Colaborativos Avançados & Modos de Leitura

- [ ] **Modo "Seguir o Anfitrião" (Leader / Follower Mode)**
  - *Descrição:* Permitir que leitores sincronizem a tela com o host/mediador do clube do livro.
  - *Arquivos envolvidos:* [`bookclub.js`](file:///home/gabrielgama/repo-personal/foliate-jam/bookclub.js), [`server.js`](file:///home/gabrielgama/repo-personal/foliate-jam/server.js)
- [ ] **Reações com Emojis nos Destaques (❤️, 💡, 🤯, 📚)**
  - *Descrição:* Permitir que os leitores reajam aos destaques uns dos outros.
  - *Arquivos envolvidos:* [`bookclub.js`](file:///home/gabrielgama/repo-personal/foliate-jam/bookclub.js), [`server.js`](file:///home/gabrielgama/repo-personal/foliate-jam/server.js)
- [ ] **Drawer / Bottom Sheet Responsivo para Mobile**
  - *Descrição:* Painel lateral transformado em gaveta deslizante inferior em dispositivos móveis.
  - *Arquivos envolvidos:* [`bookclub.css`](file:///home/gabrielgama/repo-personal/foliate-jam/bookclub.css), [`reader.html`](file:///home/gabrielgama/repo-personal/foliate-jam/reader.html)

---

## ✍️ Fase 4: Anotações, Exportação & Estudo

- [ ] **Gerador de Imagem de Citação (Quote Cards)**
  - *Descrição:* Criar cartões com trechos estilizados do livro com marca d'água para compartilhamento em redes sociais.
  - *Arquivos envolvidos:* [`quote-image.js`](file:///home/gabrielgama/repo-personal/foliate-jam/quote-image.js), [`reader.js`](file:///home/gabrielgama/repo-personal/foliate-jam/reader.js)
- [ ] **Exportação de Destaques e Anotações (Markdown / Notion)**
  - *Descrição:* Exportar marcadores e notas coletivas em Markdown, TXT ou JSON.
  - *Arquivos envolvidos:* [`reader.js`](file:///home/gabrielgama/repo-personal/foliate-jam/reader.js)

---

## 🎮 Fase 5: Aplicativo Oficial para Discord (Discord Activity & Bot Companion)

Este bloco detalha o plano de ação técnico para rodar o Paperback nativamente como uma **Discord Activity** (leitura compartilhada dentro de canais de voz/texto) e opcionalmente com um **Bot de Slash Commands**.

### 5.1 Backend & Camada de Segurança para Iframes
- [ ] **Autenticação Resiliente a Iframes (Token Bearer & WebSocket Auth)**
  - *Descrição:* Adicionar suporte a autenticação via cabeçalho HTTP `Authorization: Bearer <token>` e via query string no handshake WebSocket (`wss://...?token=...`). Isso contorna o bloqueio de cookies de terceiros (*third-party cookies*) aplicado por navegadores dentro do iframe do Discord.
  - *Arquivos envolvidos:* [`server.js`](file:///home/gabrielgama/repo-personal/foliate-jam/server.js)
- [ ] **Endpoint de Troca de Token do Embedded App SDK (`/api/auth/discord/token`)**
  - *Descrição:* Criar endpoint para receber o código OAuth emitido pelo SDK do Discord dentro do cliente (`discordSdk.commands.authorize`) e trocá-lo pelo access token / JWT da sessão sem precisar de redirects externos.
  - *Arquivos envolvidos:* [`server.js`](file:///home/gabrielgama/repo-personal/foliate-jam/server.js)
- [ ] **Ajustes de CSP & Permissões de Frame Ancestors**
  - *Descrição:* Atualizar a política de Content Security Policy e headers HTTP para permitir `frame-ancestors 'self' https://*.discord.com https://discord.com;` e conectividade com os proxies do Discord (`/.proxy/...`).
  - *Arquivos envolvidos:* [`reader.html`](file:///home/gabrielgama/repo-personal/foliate-jam/reader.html), [`server.js`](file:///home/gabrielgama/repo-personal/foliate-jam/server.js)

### 5.2 Discord Activity (Embedded App SDK)
- [ ] **Integração do `@discord/embedded-app-sdk` no Frontend**
  - *Descrição:* Adicionar o SDK de Atividades, executar o handshake inicial (`discordSdk.ready()`) e detectar automaticamente se o app está rodando dentro do Discord ou como navegador standalone.
  - *Arquivos envolvidos:* [`reader.html`](file:///home/gabrielgama/repo-personal/foliate-jam/reader.html), [`bookclub.js`](file:///home/gabrielgama/repo-personal/foliate-jam/bookclub.js)
- [ ] **Mapeamento Automático de Sessão por Canal (`channelId` / `instanceId`)**
  - *Descrição:* Associar o `room_id` ao `channel_id` ou `instance_id` do Discord. Usuários que entrarem na mesma chamada de voz ou canal de texto entram automaticamente na mesma sessão de leitura sem precisar compartilhar códigos ou links.
  - *Arquivos envolvidos:* [`db.js`](file:///home/gabrielgama/repo-personal/foliate-jam/db.js), [`server.js`](file:///home/gabrielgama/repo-personal/foliate-jam/server.js), [`bookclub.js`](file:///home/gabrielgama/repo-personal/foliate-jam/bookclub.js)
- [ ] **Adaptação de Layout para Painel Lateral e Modo Teatro**
  - *Descrição:* Ajustar os menus, a barra de navegação e o drawer de membros para colapsar suavemente quando a Activity estiver rodando em dimensões compactas (ex: painel lateral do Discord com ~400px de largura).
  - *Arquivos envolvidos:* [`bookclub.css`](file:///home/gabrielgama/repo-personal/foliate-jam/bookclub.css), [`reader.html`](file:///home/gabrielgama/repo-personal/foliate-jam/reader.html)

### 5.3 Discord Bot Companion & Comandos de Barra (Opcional / Integrado)
- [ ] **Slash Commands para Leitura & Upload (`/paperback`)**
  - *Descrição:* Implementar comandos de barra (`/paperback ler`, `/paperback upload [arquivo]`, `/paperback estante`) permitindo subir arquivos `.epub` diretamente pelo chat e lançar a Activity via botão de ação.
  - *Arquivos envolvidos:* [`server.js`](file:///home/gabrielgama/repo-personal/foliate-jam/server.js) ou novo módulo de bot
- [ ] **Compartilhamento de Citações com Quote Cards no Chat**
  - *Descrição:* Comando para gerar e postar como embed/imagem no chat um cartão de citação gerado a partir dos destaques da sala.
  - *Arquivos envolvidos:* [`quote-image.js`](file:///home/gabrielgama/repo-personal/foliate-jam/quote-image.js)

### 5.4 Configuração & Publicação no Discord Developer Portal
- [ ] **Configuração do App no Developer Portal**
  - *Descrição:* Habilitar a funcionalidade de Activities, cadastrar os escopos de OAuth2 (`identify`, `applications.commands`), configurar os URL Mappings do proxy e definir metadados para a App Directory.

---

## 📚 Fase 6: Formatos Adicionais & Recursos Futuros

- [ ] **Suporte a Formatos Adicionais (MOBI, PDF, CBZ/Mangás)**
  - *Descrição:* Liberar upload e leitura de PDF, MOBI e arquivos CBZ para quadrinhos/mangás.
  - *Arquivos envolvidos:* [`server.js`](file:///home/gabrielgama/repo-personal/foliate-jam/server.js), [`reader.js`](file:///home/gabrielgama/repo-personal/foliate-jam/reader.js)
