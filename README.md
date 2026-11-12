# Como conectar o Claude no WhatsApp

Agora dá pra conectar o Claude no WhatsApp Business usando o **conector MCP oficial da Meta** (WhatsApp Business Tools). Depois de conectado, você pede em português e o Claude executa na sua conta do WhatsApp Business.

> ⚠️ **Beta:** o conector está em beta e sendo liberado aos poucos. Pode ser que ainda não esteja disponível para a sua conta.

---

## O que dá pra fazer

- Listar suas empresas, contas do WhatsApp Business e números
- Adicionar, verificar e registrar um número novo
- Criar, editar, listar e apagar **templates de mensagem**
- **Enviar mensagens** (texto livre ou template aprovado), sempre com confirmação antes
- Configurar **webhooks**
- Configurar forma de pagamento e iniciar a verificação da empresa

> ℹ️ O Claude **não vira um chatbot que responde clientes sozinho**. Ele opera a sua conta quando **você** pede. Atendimento automático continua exigindo uma integração própria via webhook.

---

## Antes de começar

1. **Claude Desktop** ou **Claude Code** atualizados (o guia de conexão da Meta também cita o Claude na web).
2. **Acesso de administrador** a uma empresa no Gerenciador de Negócios da Meta.
3. Um **app no [Meta for Developers](https://developers.facebook.com/apps)** com o WhatsApp ativado, ligado a essa empresa, em que você também seja admin.
4. Os **Termos de Serviço da WhatsApp Business Cloud API aceitos** na empresa. Sem isso, envio de mensagens e registro de número ficam bloqueados.

---

## Passo 1: adicionar o conector

### Claude Desktop / Claude na web

1. Abra **Configurações → Conectores**.
2. Clique em **Adicionar conector personalizado**.
3. Preencha:

| Campo | Valor |
|---|---|
| Nome | `WhatsApp Business Tools` |
| URL | `https://mcp.facebook.com/whatsapp_business_tools` |

Não precisa de Client ID, chave ou token.

### Claude Code (terminal)

```bash
claude mcp add --transport http whatsapp_biz https://mcp.facebook.com/whatsapp_business_tools --scope user
```

Depois, dentro do Claude Code, rode `/mcp`, selecione `whatsapp_biz` e autentique. Também dá pra fazer pelo terminal:

```bash
claude mcp login whatsapp_biz
```

---

## Passo 2: fazer login com a Meta

1. Entre com a conta do Facebook que administra a empresa.
2. Revise as permissões pedidas:
   - `business_management`: acessar as empresas que você escolher
   - `whatsapp_business_management`: gerenciar contas, números, templates e webhooks
   - `whatsapp_business_messaging`: enviar mensagens
3. **Escolha quais empresas** o Claude pode acessar.
4. Aprove e volte para o Claude.

---

## Passo 3: testar

Peça ao Claude:

> Lista as empresas que eu administro no WhatsApp Business.

Se as suas empresas aparecerem, a conexão está funcionando ✅

No Claude Code, também dá pra conferir com:

```bash
claude mcp list
```

---

## Passo 4: usar

Exemplos de pedidos:

- *"Quais números eu tenho no WhatsApp Business?"*
- *"Cria um template de lembrete de consulta com nome e horário como variáveis."*
- *"Quais templates já estão aprovados?"*
- *"Envia o template de lembrete para o número +55…"*
- *"Configura o webhook com a URL https://meusite.com/webhook."*

---

## Atenção

- **Janela de 24 horas:** mensagem de texto livre só é entregue dentro de 24h depois da última mensagem do cliente. Fora disso, só com **template aprovado**.
- **Cobrança:** para mensagens cobradas, a conta precisa ter uma forma de pagamento configurada.
- **Limite de uso:** existe limite por usuário e por ferramenta. Se aparecer erro de limite, espere um pouco e tente de novo.

## Problemas comuns

| Mensagem | O que fazer |
|---|---|
| "It looks like this app isn't available" | Sua conta ainda não recebeu acesso ao beta. Aguarde. |
| "Dynamic registration is not available for this client" | Use um cliente suportado (Claude Desktop ou Claude Code). |
| Login funciona mas nenhuma ferramenta aparece | Reconecte ou reinicie o Claude. |
| Erro de permissão | Faça login de novo e marque a empresa ou permissão que faltou. |
| "Mcp-Session-Id is unknown or has expired" | Reconecte o conector. |

## Como remover o acesso

Facebook → **Configurações → Sua atividade → Integrações comerciais** → selecione a integração → remover.

No Claude Code:

```bash
claude mcp remove whatsapp_biz
```

---

## Fontes oficiais

- [WhatsApp Business Tools MCP (Meta)](https://developers.facebook.com/documentation/mcp/whatsapp-business-tools-mcp)
- [Como conectar um cliente MCP (Meta)](https://developers.facebook.com/documentation/mcp/connect-an-mcp-client)
