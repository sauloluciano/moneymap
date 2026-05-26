# MoneyMap — Guia de Deploy (Supabase + Vercel)

## O que você vai ter no final
- App acessível em `https://moneymap-xxxxx.vercel.app`  
- Dados salvos no Supabase (PostgreSQL na nuvem)  
- Funciona no celular, tablet e desktop  
- Múltiplos usuários acessando os mesmos dados

---

## PASSO 1 — Criar projeto no Supabase

1. Acesse **supabase.com** → Login → **New Project**
2. Preencha:
   - **Name:** `moneymap`
   - **Database Password:** anote em lugar seguro
   - **Region:** escolha `South America (São Paulo)` para menor latência
3. Aguarde ~2 minutos até o projeto estar pronto

---

## PASSO 2 — Criar as tabelas

1. No painel do Supabase, clique em **SQL Editor** (menu lateral)
2. Clique em **New query**
3. Copie todo o conteúdo do arquivo `supabase_schema.sql`
4. Cole no editor e clique em **Run** (▶)
5. Deve aparecer "Success. No rows returned"

---

## PASSO 3 — Pegar as credenciais do Supabase

1. No menu lateral, clique em **Project Settings** → **API**
2. Anote:
   - **Project URL** — ex: `https://xyzxyz.supabase.co`
   - **anon public** key — string longa começando com `eyJ...`

---

## PASSO 4 — Configurar o index.html

1. Abra o arquivo `index.html` num editor de texto (Notepad, VS Code, etc.)
2. Encontre as linhas perto do topo do `<script>`:
   ```
   const SUPABASE_URL = 'COLE_SUA_URL_AQUI';
   const SUPABASE_KEY = 'COLE_SUA_ANON_KEY_AQUI';
   ```
3. Substitua pelos valores do Passo 3
4. Salve o arquivo

---

## PASSO 5 — Subir para o GitHub

1. Crie conta em **github.com** se não tiver
2. Clique em **New repository** → nome: `moneymap` → **Create**
3. Faça upload dos 3 arquivos desta pasta:
   - `index.html`
   - `vercel.json`
   - `supabase_schema.sql` (opcional, só para referência)

   **Forma mais fácil:** arraste os arquivos direto na página do repositório no GitHub

---

## PASSO 6 — Deploy no Vercel

1. Acesse **vercel.com** → Login com sua conta GitHub
2. Clique em **Add New Project**
3. Selecione o repositório `moneymap`
4. Clique em **Deploy** (sem alterar nenhuma configuração)
5. Em ~30 segundos seu app estará em `https://moneymap-xxxxx.vercel.app`

---

## PASSO 7 — Migrar os dados que você já tem

Dentro do app, na aba **Config → Backup**:

1. No seu arquivo HTML local (o que você usa hoje):
   - Clique **Exportar configurações** → salva `moneymap-config-YYYY-MM-DD.json`
   - Clique **Exportar transações** → salva `moneymap-transacoes-YYYY-MM-DD.json`

2. No novo app hospedado (`https://moneymap-xxxxx.vercel.app`):
   - Clique **Restaurar configurações** → selecione o arquivo de configurações
   - Clique **Restaurar transações** → selecione o arquivo de transações
   - Configure a **chave de API** (Anthropic) em Config → Chave de API

---

## PASSO 8 — Compartilhar com outros usuários

Simplesmente envie o link: `https://moneymap-xxxxx.vercel.app`

Todos acessam os mesmos dados. Não há login — qualquer pessoa com o link acessa. Se quiser restringir o acesso:
- **Opção simples:** renomeie o projeto no Vercel para um nome difícil de adivinhar
- **Opção mais segura:** adicione uma senha básica (posso implementar depois se precisar)

---

## Atualizações futuras

Quando o Claude gerar uma nova versão do app:
1. Baixe o novo `financas-pessoais.html`
2. Edite as linhas `SUPABASE_URL` e `SUPABASE_KEY` (iguais às anteriores)
3. Renomeie para `index.html` e substitua no GitHub
4. O Vercel redeploya automaticamente em segundos

---

## Custos

| Serviço | Plano gratuito |
|---------|----------------|
| Supabase | 500MB banco, 2GB transferência/mês — mais que suficiente |
| Vercel | Unlimited deploys, 100GB banda/mês — mais que suficiente |
| **Total** | **R$ 0,00** |
