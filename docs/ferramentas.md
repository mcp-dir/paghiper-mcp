# Ferramentas

PagHiper expõe 9 ferramentas.

### 1. `paghiper_list_accounts`
**Input**: `account` (opcional)

Lista as conexões (contas) PagHiper vinculadas a este install — id, label.

### 2. `paghiper_create_pix`
**Input**: `order_id`, `payer_name`, `payer_email`, `payer_cpf_cnpj`, `payer_phone` (opcional), `items`, `discount_cents` (opcional), `shipping_price_cents` (opcional), `shipping_methods` (opcional), `days_due_date` (opcional), `notification_url` (opcional), `fixed_description` (opcional), `account` (opcional), `order_ids` (opcional)

Emite uma cobrança Pix no PagHiper e devolve o código copia-e-cola (`pix_code.emv`), o QR Code em PNG base64 (`pix_code.qrcode_base64`) e a URL da imagem (`pix_code.qrcode_image_url`), além do `transaction_id` pra con…

### 3. `paghiper_create_boleto`
**Input**: `order_id`, `payer_name`, `payer_email`, `payer_cpf_cnpj`, `payer_phone` (opcional), `items`, `discount_cents` (opcional), `shipping_price_cents` (opcional), `shipping_methods` (opcional), `days_due_date` (opcional), `notification_url` (opcional), `fixed_description` (opcional), `payer_street`, `payer_number`, `payer_district`, `payer_city`, `payer_state`, `payer_zip_code`, `payer_complement` (opcional), `type_bank_slip` (opcional), `account` (opcional), `order_ids` (opcional)

Emite um boleto bancário registrado no PagHiper e devolve linha digitável, código de barras, URL do PDF e o `transaction_id`.

### 4. `paghiper_get_pix_status`
**Input**: `transaction_id`, `account` (opcional), `transaction_ids` (opcional)

Consulta o status atual de uma cobrança Pix pelo `transaction_id`.

### 5. `paghiper_get_boleto_status`
**Input**: `transaction_id`, `account` (opcional), `transaction_ids` (opcional)

Consulta o status atual de um boleto pelo `transaction_id`.

### 6. `paghiper_cancel_pix`
**Input**: `transaction_id`, `account` (opcional), `transaction_ids` (opcional)

Cancela uma cobrança Pix ainda não paga, pelo `transaction_id`.

### 7. `paghiper_cancel_boleto`
**Input**: `transaction_id`, `account` (opcional), `transaction_ids` (opcional)

Cancela um boleto ainda não pago, pelo `transaction_id`.

### 8. `paghiper_list_transactions`
**Input**: `status` (opcional), `initial_date` (opcional), `final_date` (opcional), `filter_date` (opcional), `account` (opcional)

Lista as transações da conta PagHiper.

### 9. `paghiper_list_bank_accounts`
**Input**: `account` (opcional)

Lista as contas bancárias cadastradas na conta PagHiper (destinos de saque).

## Prompts de exemplo

```
Gere um Pix de R$ 50 para o cliente João da Silva
Qual o status da cobrança que emiti ontem?
Liste os boletos pagos deste mês
```
