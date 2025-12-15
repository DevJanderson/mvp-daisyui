# Guia Completo: MCP do Supabase com Claude Code

## O que é MCP?

**MCP (Model Context Protocol)** é um padrão aberto que permite integrar o Claude com serviços externos como bancos de dados, APIs e ferramentas. Com o MCP do Supabase, o Claude consegue acessar diretamente seu banco de dados, autenticação e storage.

### Como funciona?

- MCP servers expõem ferramentas, bancos de dados e APIs para o Claude Code
- O Claude pode acessar e usar esses serviços externos diretamente no seu workflow
- É similar a function calling, mas projetado para integração com sistemas externos complexos

---

## Pre-requisitos

1. **Conta no Supabase** - Gratuita em https://supabase.com
2. **Um projeto criado** no dashboard do Supabase
3. **Suas credenciais:**
   - Project URL (Settings > API)
   - API Key (Settings > API)
4. **Claude Code instalado** na sua máquina

---

## Passo a Passo para Configurar

### 1. Verificar instalação do Claude Code

```bash
claude --version
```

### 2. Listar servidores MCP existentes (opcional)

```bash
claude mcp list
```

### 3. Adicionar o MCP do Supabase

```bash
claude mcp add --transport http supabase https://mcp.supabase.com/mcp \
  --header "Authorization: Bearer SUA_API_KEY_AQUI"
```

### 4. Verificar se foi instalado

```bash
claude mcp list
```

Você deve ver:
```
supabase (http)
```

### 5. Dentro do Claude Code

Digite `/mcp` para ver e gerenciar os servidores conectados.

---

## Escopos de Instalação

Você pode escolher onde o servidor MCP fica armazenado:

### Local (padrão - privado para você no projeto atual)

```bash
claude mcp add --transport http supabase https://mcp.supabase.com/mcp \
  --header "Authorization: Bearer SUA_KEY"
```

### Projeto (compartilhado com o time via `.mcp.json`)

```bash
claude mcp add --transport http supabase https://mcp.supabase.com/mcp \
  --header "Authorization: Bearer SUA_KEY" \
  --scope project
```

### Usuário (disponível em todos os seus projetos)

```bash
claude mcp add --transport http supabase https://mcp.supabase.com/mcp \
  --header "Authorization: Bearer SUA_KEY" \
  --scope user
```

---

## O que você pode fazer com o Supabase MCP?

### Operações de Banco de Dados

- Consultar tabelas diretamente
- Inserir, atualizar ou deletar registros
- Executar queries SQL complexas
- Obter informações do schema
- Gerenciar conexões

### Autenticação

- Gerenciar contas de usuário
- Trabalhar com tokens JWT
- Gerenciar sessões

### Storage (Supabase Storage)

- Upload/download de arquivos
- Gerenciar buckets
- Configurar permissões de arquivos

### Exemplos de prompts que você pode usar

```
> "Liste todos os usuários da tabela users"

> "Insira um novo registro na tabela products com esses dados: [dados]"

> "Mostre o schema da tabela orders"

> "Faça upload deste arquivo para o bucket documents"

> "Encontre todos os registros onde status = 'pending' e atualize para 'processed'"
```

---

## Configuração para Times

### Criar arquivo `.mcp.json` na raiz do projeto

```json
{
  "mcpServers": {
    "supabase": {
      "type": "http",
      "url": "https://mcp.supabase.com/mcp",
      "headers": {
        "Authorization": "Bearer ${SUPABASE_API_KEY}"
      }
    }
  }
}
```

### Adicionar ao `.gitignore`

```
.env
.env.local
```

### Cada membro do time configura sua própria API key

```bash
export SUPABASE_API_KEY="sua-api-key"
```

---

## Segurança - Boas Práticas

### Nunca faça isso:

- Commitar API keys no controle de versão
- Compartilhar credenciais em snippets de código
- Usar chaves de desenvolvimento em produção

### Sempre faça isso:

- Use variáveis de ambiente para credenciais
- Armazene valores sensíveis em arquivos `.env` (adicionados ao `.gitignore`)
- Use chaves diferentes para ambientes diferentes
- Rotacione as chaves regularmente
- Restrinja permissões das API keys

### Usando variáveis de ambiente

```bash
export SUPABASE_API_KEY="sua-chave-aqui"

claude mcp add --transport http supabase https://mcp.supabase.com/mcp \
  --header "Authorization: Bearer ${SUPABASE_API_KEY}"
```

### Para Supabase especificamente:

- Use Row Level Security (RLS) nas suas tabelas
- Crie API keys com escopos mínimos necessários
- Use chaves diferentes para operações públicas vs privadas

---

## Gerenciando Servidores MCP

```bash
# Listar todos os servidores MCP
claude mcp list

# Ver detalhes de um servidor específico
claude mcp get supabase

# Remover um servidor
claude mcp remove supabase

# Resetar escolhas de autenticação
claude mcp reset-project-choices
```

---

## Troubleshooting

### Servidor não conecta

- Verifique se sua API key é válida
- Confirme que seu projeto Supabase está ativo
- Certifique-se de que a URL está correta

### Erros de autenticação

- Execute `/mcp` para re-autenticar
- Limpe a autenticação com `/mcp` > "Clear authentication"
- Verifique se o token não expirou

### Warnings de output

Se você ver warnings sobre limite de output do MCP:

```bash
export MAX_MCP_OUTPUT_TOKENS=50000
claude
```

### Timeout do servidor

```bash
export MCP_TIMEOUT=10000
```

---

## Links Úteis

- [Documentação MCP](https://code.claude.com/docs/en/mcp.md)
- [Configurações do Claude Code](https://code.claude.com/docs/en/settings.md)
- [Documentação do Supabase](https://supabase.com/docs)
- [Guia de Segurança](https://code.claude.com/docs/en/security.md)
