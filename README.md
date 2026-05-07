# AM · Ficha de Fechamento Comercial — Acelerador Médico

## Estrutura do Projeto

```
comercial/
├── index.html       ← App completo (single file)
└── README.md        ← Este arquivo
```

## O que é

App usado pelo time comercial para registrar fechamentos. Após preencher os dados do lead, o app dispara automaticamente uma mensagem formatada no grupo **Time Comercial GAM** via WhatsApp.

## Acesso

### Vendedor
- Acessa pela aba **Vendedor**
- Digita o e-mail cadastrado pelo admin
- Se o e-mail existir, entra direto — sem senha

### Admin (Giuseppe / Gabriel)
- Acessa pela aba **Admin**
- Loga com e-mail + senha (cadastrados no Supabase Auth)
- Gerencia vendedores: adicionar, editar e remover

## Como gerenciar vendedores

1. Acessa `comercial.aceleradormedico.com.br`
2. Clica na aba **Admin**
3. Loga com e-mail e senha
4. Adiciona ou remove vendedores pelo painel

Não é necessário mexer no código para isso.

## Como subir alterações no GitHub

1. Edite o `index.html`
2. No repositório GitHub, clique em **index.html → Edit (lápis)**
3. Cole o conteúdo atualizado
4. Clique em **Commit changes**

O GitHub Pages atualiza automaticamente em ~1 minuto.

## Integrações

| Serviço | Uso |
|---|---|
| Supabase | Tabela `closers` (nome + e-mail dos vendedores) + Auth para admins |
| Z-API | Envio da ficha formatada para o grupo WhatsApp |
| ViaCEP | Preenchimento automático de endereço pelo CEP |

## Variáveis de configuração

Todas no topo do `<script>` dentro do `index.html`:

```js
const SUPABASE_URL = '...'   // URL do projeto Supabase
const ANON_KEY     = '...'   // Chave anon pública
const SERVICE_KEY  = '...'   // Chave service_role (acesso admin à tabela)
const ZAPI_BASE    = '...'   // Endpoint Z-API da instância
const GROUP_ID     = '...'   // ID do grupo WhatsApp destino
```

## Supabase — estrutura da tabela

```sql
create table closers (
  id uuid default gen_random_uuid() primary key,
  nome text not null,
  email text not null unique,
  created_at timestamptz default now()
);
```
