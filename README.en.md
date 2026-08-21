# PagHiper

### PagHiper for Claude, ChatGPT and AI agents

Issue registered Brazilian bank slips (boleto) and Pix charges on PagHiper with the official API. Creates the charge and returns the Pix copy and paste code, the QR Code and the boleto barcode line, checks payment status, cancels an unpaid charge, lists transactions by period and status, and lists the bank accounts used for withdrawals. Authentication via apiKey and token, generated in your PagHiper account under My account, Credentials. Minimum charge of R$ 3.00. Pairs with the Banco MCP, the Banco shows the money that arrived, PagHiper issues the charge.

- 📊 **9 tools**
- ✏️ **Read and write**
- 💬 **Works with any MCP client**: Claude Desktop, Cursor, VS Code, Cline, Continue
- 🔑 **Magic-link login (no password)**

[Portuguese version](README.md) · [Full docs (PT-BR)](docs/)

---

## One-click install

### Claude (Web and Desktop)

[➕ Open in Claude and connect](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

Manual: [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Add custom connector** → name `PagHiper`, URL `https://api.mcp.ai/p_paghiper`.

### Cursor

[➕ Install in Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=paghiper&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9wYWdoaXBlciJ9)

### VS Code (Copilot Chat)

[➕ Install in VS Code](vscode:mcp/install?name=paghiper&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_paghiper%22%7D)

### Any other MCP-over-HTTP client

```
https://api.mcp.ai/p_paghiper
```

---

## 9 tools

| Tool | Description |
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

---

## Pricing

See [docs/precos.md](docs/precos.md) (PT-BR).

---

## License

MIT — see [LICENSE](LICENSE). The MCP server at `api.mcp.ai/p_paghiper` is proprietary (hosted); this repo (manifests, docs, skills) is MIT.
