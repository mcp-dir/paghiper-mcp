# PagHiper

### PagHiper para Claude, ChatGPT e agentes de IA

Emissão de boleto bancário registrado e Pix no PagHiper com a API oficial. Gera a cobrança e devolve o código Pix copia e cola, o QR Code e a linha digitável do boleto, consulta o status do pagamento, cancela cobrança não paga, lista transações por período e status, e lista as contas bancárias de saque. Autenticação por apiKey e token, gerados na sua conta PagHiper em Minha conta, Credenciais. Valor mínimo por cobrança de R$ 3,00. Pareia com o Banco MCP, o Banco mostra o dinheiro que entrou, o PagHiper emite a cobrança.

- 📊 **9 ferramentas**
- ✏️ **Leitura e escrita**
- 💬 **Funciona com qualquer cliente MCP**: Claude Desktop, Cursor, VS Code, Cline, Continue
- 🔑 **Login via magic-link (sem senha)**

[English version](README.en.md) · [Documentação completa](docs/) · [Skill pra agentes](skills/)

---

## Instalar em 1 clique

### Claude (Web e Desktop)

A Anthropic unificou a instalação de MCPs em `claude.ai/customize/connectors`. **O mesmo link serve pra Claude Web e Claude Desktop** (basta estar logado):

[➕ Abrir no Claude e conectar](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

**Manual** (se o deeplink não abrir): [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Adicionar conector personalizado** → cole **Nome** `PagHiper` e **URL** `https://api.mcp.ai/p_paghiper`.

### Cursor

[➕ Instalar PagHiper no Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=paghiper&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9wYWdoaXBlciJ9)

### VS Code (Copilot Chat)

[➕ Instalar PagHiper no VS Code](vscode:mcp/install?name=paghiper&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_paghiper%22%7D)

### ChatGPT, Manus, OpenClaw e mais 40+ clientes

Funciona em qualquer cliente MCP que suporte **MCP over HTTP**. A URL do servidor é sempre:

```
https://api.mcp.ai/p_paghiper
```

Detalhes por cliente: [INSTALL.md](INSTALL.md).

---

## Exemplos de uso

```
Gere um Pix de R$ 50 para o cliente João da Silva
Qual o status da cobrança que emiti ontem?
Liste os boletos pagos deste mês
```

---

## 9 ferramentas disponíveis

| Tool | Descrição |
|---|---|
| `paghiper_list_accounts` | Lista as conexões (contas) PagHiper vinculadas a este install — id, label. |
| `paghiper_create_pix` | Emite uma cobrança Pix no PagHiper e devolve o código copia-e-cola (`pix_code.emv`), o QR Code em PNG base64 (`pix_code.qrcode_base64`) e a URL da imagem (`pix_code.qrcode_image_url`), além do `transaction_id` pra con… |
| `paghiper_create_boleto` | Emite um boleto bancário registrado no PagHiper e devolve linha digitável, código de barras, URL do PDF e o `transaction_id`. |
| `paghiper_get_pix_status` | Consulta o status atual de uma cobrança Pix pelo `transaction_id`. |
| `paghiper_get_boleto_status` | Consulta o status atual de um boleto pelo `transaction_id`. |
| `paghiper_cancel_pix` | Cancela uma cobrança Pix ainda não paga, pelo `transaction_id`. |
| `paghiper_cancel_boleto` | Cancela um boleto ainda não pago, pelo `transaction_id`. |
| `paghiper_list_transactions` | Lista as transações da conta PagHiper. |
| `paghiper_list_bank_accounts` | Lista as contas bancárias cadastradas na conta PagHiper (destinos de saque). |

Detalhe de cada tool: [docs/ferramentas.md](docs/ferramentas.md)

---

## Preços

Planos a partir do tier grátis. Veja [docs/precos.md](docs/precos.md).

---

## Privacidade & LGPD

- **Sub-processadores**: PagHiper, o LLM host que você escolher (Claude, ChatGPT, Cursor, agente próprio). Lista completa em [docs/privacidade-lgpd.md](docs/privacidade-lgpd.md).
- Os dados retornados pelas tools são enviados ao **LLM host que você escolher**, sub-processador fora do nosso controle. Recomendamos planos com opt-out de treinamento.

---

## Perguntas frequentes

**O servidor é open source?**
O servidor é proprietário (hosted). Este repositório é o wrapper público com manifestos, docs e skills — tudo MIT.

**Posso usar com agente próprio (não Claude/Cursor)?**
Sim — qualquer cliente que suporte MCP over HTTP. URL: `https://api.mcp.ai/p_paghiper`.


---

## Suporte

- 📧 [paghiper@mcp.ai](mailto:paghiper@mcp.ai)
- 🐛 [GitHub Issues](https://github.com/mcp-dir/paghiper-mcp/issues)
- 📄 [docs/](docs/)

---

## Licença

MIT — veja [LICENSE](LICENSE). O servidor MCP em `api.mcp.ai/p_paghiper` é proprietário (hosted); este repositório (manifestos, docs, skills) é MIT.
