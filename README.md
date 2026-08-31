# 🎉 Página de Confirmação de Aniversário

Uma página interativa para convidados confirmarem sua presença no seu aniversário com banco de dados centralizado.

## ✨ Funcionalidades

- ✅ Formulário simples e festivo
- 🔄 Sincronização em tempo real com Supabase
- 📊 Contador de confirmados/não confirmados
- 🎨 Design responsivo com tema claro/escuro
- 💾 Dados persistentes e centralizados

## 🚀 Setup Rápido (Supabase)

### 1. Criar um projeto no Supabase

1. Acesse [supabase.com](https://supabase.com)
2. Clique em **"New Project"** e crie uma conta gratuita
3. Preencha as informações do seu projeto
4. Aguarde a criação estar completa

### 2. Criar a tabela de convidados

1. No painel do Supabase, vá para **SQL Editor**
2. Clique em **"New Query"**
3. Cole este código SQL:

```sql
CREATE TABLE IF NOT EXISTS birthday_guests (
  id BIGINT PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
  name TEXT NOT NULL UNIQUE,
  presence TEXT NOT NULL CHECK (presence IN ('yes', 'no')),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

ALTER TABLE birthday_guests ENABLE ROW LEVEL SECURITY;

CREATE POLICY "Allow public select" ON birthday_guests
  FOR SELECT USING (true);

CREATE POLICY "Allow public insert" ON birthday_guests
  FOR INSERT WITH CHECK (true);

CREATE POLICY "Allow public update" ON birthday_guests
  FOR UPDATE USING (true);
```

4. Clique em **"Run"** para executar

### 3. Obter suas credenciais

1. No Supabase, vá para **Settings** → **API**
2. Copie:
   - **Project URL** (algo como `https://seu-projeto.supabase.co`)
   - **Anon Public key** (uma chave longa)

### 4. Configurar o arquivo HTML

1. Abra o arquivo `index.html` em um editor de texto
2. Procure por estas linhas (perto do início do `<script>`):

```javascript
const SUPABASE_URL = 'https://seu-projeto.supabase.co';
const SUPABASE_KEY = 'sua-anon-key-aqui';
```

3. Substitua com suas credenciais:

```javascript
const SUPABASE_URL = 'https://seu-projeto-xyz.supabase.co';
const SUPABASE_KEY = 'eyJhbGciOiJIUzI1NiIsInR5...'; // Sua chave aqui
```

4. Salve o arquivo

### 5. Deploy (GitHub Pages)

Se estiver usando GitHub Pages:

```bash
git add index.html
git commit -m "Configure Supabase credentials"
git push origin main
```

A página ficará disponível em: `https://seu-usuario.github.io/birthday/`

## 📱 Como usar

1. Compartilhe o link da página com seus convidados
2. Cada convidado digita o nome
3. Escolhe "Vou estar lá!" ou "Não posso ir"
4. Clica em "Confirmar Presença"
5. A lista se atualiza em tempo real para todos!

## 🔄 Sincronização em Tempo Real

- A página verifica atualizações a cada 5 segundos
- Todos os visitantes veem as confirmações instantaneamente
- Indicador visual mostra quando está sincronizando

## 🛡️ Segurança

- O Supabase usa **Row Level Security (RLS)**
- Qualquer pessoa pode ler/inserir/atualizar (público)
- Para restringir, configure políticas no Supabase

## 📊 Ver os dados

No Supabase:

1. Vá para **Table Editor**
2. Clique em **birthday_guests**
3. Veja todos os convidados e suas respostas

## ⚙️ Troubleshooting

**Erro: "Configuração necessária"**
- Verifique se você editou SUPABASE_URL e SUPABASE_KEY
- Certifique-se de que copiou as credenciais corretas

**Dados não aparecem**
- Verifique se a tabela foi criada no Supabase
- Confirm que as políticas RLS estão habilitadas
- Abra o Console do navegador (F12) para ver erros

**Quero desabilitar acesso público?**
- No Supabase, vá para **Authentication** → **Policies**
- Customize as políticas de RLS conforme necessário

## 📝 Licença

Livre para usar e customizar!

---

**Criado com ❤️ para sua festa! 🎊**
