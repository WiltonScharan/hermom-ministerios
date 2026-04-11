# Igreja Hermom — Controle de Ministérios

Ferramenta web single-page para controle de cooperadores, ministérios e presença nas reuniões. Atualização em tempo real via Firebase Realtime Database.

## Como subir no ar (Vercel + Firebase)

### 1) Criar o projeto Firebase (uma vez só)

1. Acesse https://console.firebase.google.com/ e clique em **Adicionar projeto**. Dê um nome (ex: `hermom-ministerios`).
2. Ignore o Google Analytics (não é necessário).
3. No menu lateral, clique em **Build → Realtime Database → Criar banco de dados**.
   - Localização: escolha **us-central1** (ou a mais próxima).
   - Regras: comece em **modo de teste** (depois ajustamos).
4. Ainda no Firebase, clique no ícone de engrenagem → **Configurações do projeto** → role até **Seus apps** → clique no ícone **</>** (Web) → registre um app com qualquer apelido → copie os valores:
   - `apiKey`
   - `projectId`
   - `databaseURL` (ex: `https://hermom-ministerios-default-rtdb.firebaseio.com`)
5. Volte em **Realtime Database → Regras** e cole:
   ```json
   {
     "rules": {
       "hermom": {
         ".read": true,
         ".write": true
       }
     }
   }
   ```
   Clique em **Publicar**.
   > ⚠️ Isso deixa o banco aberto para quem tiver o link. Para uso interno da igreja está OK. Se quiser restringir depois, podemos adicionar autenticação.

### 2) Subir no Vercel

**Opção A — Drag & drop (mais fácil):**
1. Acesse https://vercel.com e faça login (pode usar conta Google).
2. No dashboard, clique em **Add New → Project → Import Third-Party Git Repository** e escolha **Deploy without Git** (ou arraste a pasta direto na interface nova).
3. Arraste a pasta `Hermom - Ministérios` inteira.
4. Clique em **Deploy**. Pronto — você recebe um link `https://hermom-ministerios.vercel.app`.

**Opção B — Via GitHub (recomendado se for editar depois):**
1. Crie um repositório no GitHub, faça upload dos arquivos.
2. No Vercel: **Add New → Project → Import** → selecione o repo → **Deploy**.
3. Cada alteração que você fizer no GitHub vai atualizar o site automaticamente.

### 3) Conectar o Firebase no site

1. Abra o link do Vercel no navegador.
2. Clique em **Firebase** no canto superior direito.
3. Cole **API Key**, **Project ID** e **Database URL** que você copiou no passo 1.4.
4. Clique em **Conectar**. Na primeira conexão o sistema importa automaticamente os 188 cooperadores e os 20 ministérios da planilha.
5. Compartilhe o link com quem precisar — todos veem as mudanças em tempo real.

## Funcionalidades

- **Dashboard** — totais, ranking de ministérios, taxa de presença, gráfico de evolução e aniversariantes do mês.
- **Ministérios** — criar, renomear, excluir; editar membros, funções (líder/co-líder/membro), crachás, acompanhamento pastoral, pastor responsável.
- **Cooperadores** — cadastro completo com telefone/WhatsApp, aniversário, data de entrega de crachá, status de acompanhamento, observações. Filtros por nome, ministério, status e crachá.
- **Presença** — marcação por célula (presente / ausente / justificativa com texto livre / ainda não era membro), visão por reunião única ou todas as reuniões, visão macro de todos os ministérios.
- **Marcação em lote** — marcar todos os membros de um ministério de uma vez (útil para começar uma reunião com todos como presentes).
- **Exportar CSV** — relatórios para abrir no Excel.
- **Tempo real** — qualquer mudança feita em um dispositivo aparece instantaneamente nos outros que estão com o link aberto.

## Arquivos

- `index.html` — aplicação completa (single-file, nenhum build necessário)
- `vercel.json` — configuração do Vercel (cache desativado para atualizações imediatas)
- `README.md` — este arquivo
