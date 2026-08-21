---
name: paghiper-mcp
description: Skill da REST API do PagHiper na MCP.AI: 9 endpoints em /api/paghiper. Emissão de boleto bancário registrado e Pix no PagHiper com a API oficial. Gera a cobrança e devolve o código Pix copia e cola, o QR Code e a linha digitável do boleto, consulta o status do pagamento, cancela cobrança não paga, lista transações por período e status, e lista as contas bancárias de saque. Autenticação por apiKey e token, gerados na sua conta PagHiper em Minha conta, Credenciais. Valor mínimo por cobrança de R$ 3,00. Pareia com o Banco MCP, o Banco mostra o dinheiro que entrou, o PagHiper emite a cobrança. Autentique com workspace API key (sk_live) gerada em app.mcp.ai/settings/api-keys. Use quando o usuário pedir algo coberto pelos endpoints.
---

# PagHiper — REST API skill

Você tem acesso à **PagHiper** REST API na MCP.AI.

> Emissão de boleto bancário registrado e Pix no PagHiper com a API oficial. Gera a cobrança e devolve o código Pix copia e cola, o QR Code e a linha digitável do boleto, consulta o status do pagamento, cancela cobrança não paga, lista transações por período e status, e lista as contas bancárias de saque. Autenticação por apiKey e token, gerados na sua conta PagHiper em Minha conta, Credenciais. Valor mínimo por cobrança de R$ 3,00. Pareia com o Banco MCP, o Banco mostra o dinheiro que entrou, o PagHiper emite a cobrança.

## Base URL

```
https://api.mcp.ai/api/paghiper
```

Todo endpoint é um **POST** na Base URL + o path abaixo. Os parâmetros vão no corpo JSON.

## Autenticação

Inclua em toda request:

```
Authorization: Bearer sk_live_...
Content-Type: application/json
```

> Gere sua chave em **https://app.mcp.ai/settings/api-keys** (workspace API key `sk_live_…`, não expira, revogável). Uma única chave serve pra todos os seus MCPs.

## Formato de resposta

```json
{ "ok": true, "tool": "<tool_id>", "result": <payload> }
```

## Exemplo cURL

```bash
curl -X POST https://api.mcp.ai/api/paghiper/cancel/boleto \
  -H "Authorization: Bearer sk_live_..." \
  -H "Content-Type: application/json" \
  -d '{"transaction_id":"..."}'
```

## Reportar problemas

Se um endpoint retornar erro, vazio ou dado inesperado, reporte (não desista calado): **POST /api/paghiper/report** com `{ "message": "...", "context"?: "...", "conversation"?: [...] }`. Isso notifica o time da MCP.AI.

## Endpoints (9)

#### `paghiper_cancel_boleto`

Cancela um boleto ainda não pago, pelo `transaction_id`. _(POST /api/paghiper/cancel/boleto)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `transaction_id` | string | Sim | transaction_id devolvido na emissão da cobrança |
| `account` | string | Não | Quando há múltiplas contas PagHiper conectadas: id ou label da conexão. Veja paghiper_list_accounts. |
| `transaction_ids` | string[] | Não | Bulk mode: multiple values for transaction_id |

#### `paghiper_cancel_pix`

Cancela uma cobrança Pix ainda não paga, pelo `transaction_id`. _(POST /api/paghiper/cancel/pix)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `transaction_id` | string | Sim | transaction_id devolvido na emissão da cobrança |
| `account` | string | Não | Quando há múltiplas contas PagHiper conectadas: id ou label da conexão. Veja paghiper_list_accounts. |
| `transaction_ids` | string[] | Não | Bulk mode: multiple values for transaction_id |

#### `paghiper_create_boleto`

Emite um boleto bancário registrado no PagHiper e devolve linha digitável, código de barras, URL do PDF e o `transaction_id`. _(POST /api/paghiper/create/boleto)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `order_id` | string | Sim | Código interno do lojista pra identificar a transação (seu id de pedido) |
| `payer_name` | string | Sim | Nome completo ou razão social do pagador |
| `payer_email` | string | Sim | E-mail do pagador |
| `payer_cpf_cnpj` | string | Sim | CPF ou CNPJ do pagador, só dígitos (ex.: 00000000191). Obrigatório. |
| `payer_phone` | string | Não | Telefone fixo ou móvel do pagador, só dígitos com DDD |
| `items` | object[] | Sim | Itens da cobrança. O total (itens - desconto + frete) precisa ser >= 300 centavos (R$ 3,00). |
| `discount_cents` | integer | Não | Desconto em centavos |
| `shipping_price_cents` | integer | Não | Frete em centavos |
| `shipping_methods` | string | Não | Método de envio (ex.: PAC, SEDEX) |
| `days_due_date` | integer | Não | Dias até o vencimento (default do PagHiper se omitido) |
| `notification_url` | string | Não | URL que recebe o retorno automático de mudança de status |
| `fixed_description` | boolean | Não | Fixa a descrição dos itens na cobrança |
| `payer_street` | string | Sim | Logradouro do pagador |
| `payer_number` | string | Sim | Número |
| `payer_district` | string | Sim | Bairro |
| `payer_city` | string | Sim | Cidade |
| `payer_state` | string | Sim | UF, apenas a sigla (ex.: SP) |
| `payer_zip_code` | string | Sim | CEP, só dígitos (ex.: 01452002) |
| `payer_complement` | string | Não | Complemento |
| `type_bank_slip` | string | Não | Tipo do boleto no PagHiper (ex.: boletoA4). Opcional. |
| `account` | string | Não | Quando há múltiplas contas PagHiper conectadas: id ou label da conexão. Veja paghiper_list_accounts. |
| `order_ids` | string[] | Não | Bulk mode: multiple values for order_id |

#### `paghiper_create_pix`

Emite uma cobrança Pix no PagHiper e devolve o código copia-e-cola (`pix_code.emv`), o QR Code em PNG base64 (`pix_code.qrcode_base64`) e a URL da imagem (`pix_code.qrcode_image_url`), além do `transa _(POST /api/paghiper/create/pix)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `order_id` | string | Sim | Código interno do lojista pra identificar a transação (seu id de pedido) |
| `payer_name` | string | Sim | Nome completo ou razão social do pagador |
| `payer_email` | string | Sim | E-mail do pagador |
| `payer_cpf_cnpj` | string | Sim | CPF ou CNPJ do pagador, só dígitos (ex.: 00000000191). Obrigatório. |
| `payer_phone` | string | Não | Telefone fixo ou móvel do pagador, só dígitos com DDD |
| `items` | object[] | Sim | Itens da cobrança. O total (itens - desconto + frete) precisa ser >= 300 centavos (R$ 3,00). |
| `discount_cents` | integer | Não | Desconto em centavos |
| `shipping_price_cents` | integer | Não | Frete em centavos |
| `shipping_methods` | string | Não | Método de envio (ex.: PAC, SEDEX) |
| `days_due_date` | integer | Não | Dias até o vencimento (default do PagHiper se omitido) |
| `notification_url` | string | Não | URL que recebe o retorno automático de mudança de status |
| `fixed_description` | boolean | Não | Fixa a descrição dos itens na cobrança |
| `account` | string | Não | Quando há múltiplas contas PagHiper conectadas: id ou label da conexão. Veja paghiper_list_accounts. |
| `order_ids` | string[] | Não | Bulk mode: multiple values for order_id |

#### `paghiper_get_boleto_status`

Consulta o status atual de um boleto pelo `transaction_id`. _(POST /api/paghiper/get/boleto/status)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `transaction_id` | string | Sim | transaction_id devolvido na emissão da cobrança |
| `account` | string | Não | Quando há múltiplas contas PagHiper conectadas: id ou label da conexão. Veja paghiper_list_accounts. |
| `transaction_ids` | string[] | Não | Bulk mode: multiple values for transaction_id |

#### `paghiper_get_pix_status`

Consulta o status atual de uma cobrança Pix pelo `transaction_id`. _(POST /api/paghiper/get/pix/status)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `transaction_id` | string | Sim | transaction_id devolvido na emissão da cobrança |
| `account` | string | Não | Quando há múltiplas contas PagHiper conectadas: id ou label da conexão. Veja paghiper_list_accounts. |
| `transaction_ids` | string[] | Não | Bulk mode: multiple values for transaction_id |

#### `paghiper_list_accounts`

Lista as conexões (contas) PagHiper vinculadas a este install — id, label. _(POST /api/paghiper/list/accounts)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas PagHiper conectadas: id ou label da conexão. Veja paghiper_list_accounts. |

#### `paghiper_list_bank_accounts`

Lista as contas bancárias cadastradas na conta PagHiper (destinos de saque). _(POST /api/paghiper/list/bank/accounts)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há múltiplas contas PagHiper conectadas: id ou label da conexão. Veja paghiper_list_accounts. |

#### `paghiper_list_transactions`

Lista as transações da conta PagHiper. _(POST /api/paghiper/list/transactions)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `status` | string | Não | Filtra pelo status atual da transação (pending, reserved, canceled, paid, processing, refunded) |
| `initial_date` | string | Não | Data inicial, formato AAAA-MM-DD |
| `final_date` | string | Não | Data final, formato AAAA-MM-DD |
| `filter_date` | string | Não | Qual data o intervalo filtra. Obrigatório quando há intervalo; default create_date. (create_date, paid_date, due_date) |
| `account` | string | Não | Quando há múltiplas contas PagHiper conectadas: id ou label da conexão. Veja paghiper_list_accounts. |

---

Este MCP também funciona via **conexão MCP** (Claude / Cursor) em `https://api.mcp.ai/p_paghiper` — veja o [README](../../README.md). A skill acima é pra consumir a **REST API** direto (agente próprio / código).
