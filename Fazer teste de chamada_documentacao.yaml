# Documentação: Teste de Chamada (SQS / Script de teste)

Última atualização: 2025-11-03

---

## Objetivo

Documentar o procedimento e o payload de teste utilizados para acionar chamadas/fluxos (disparador) a partir de uma fila SQS / mecanismo de discador.

Este documento descreve onde enviar a mensagem, qual queue/SQS usar (quando aplicável) e o JSON de exemplo presente no arquivo original.

---

## Destino / fila

- Queue / SQS: `fl-discador-discar-prioridade`


---

## Payload de teste (exemplo)

Conteúdo JSON usado no teste (substitua `SEUNUMEROAQUI` pelo número que deseja testar):

```json
{
   "ucid":"TESTE_PIX",
   "chamada_teste":"Y",
   "numeros_devedores":"['SEUNUMEROAQUI']",
   "numero_devedor":"SEUNUMEROAQUI",
   "numero_devedor_flg":"Y",
   "nome_devedor":"JULIANA",
   "nome_gravado":"Y",
   "follow_agendamento":"N",
   "cpf_cnpj":"10195933770",
   "contrato":"",
   "produto":"FIBRA",
   "tipo_produto":"Fibra",
   "skill":"tahto_fibra",
   "campanha": "",
   "tipo_cliente":"nres",
   "regiao":"",
   "perfil_cliente":"a",
   "chamada_repetida":"N",
   "bloqueio_total":"N",
   "numero_fixo_flg":"N",
   "numero_contato":"SEUNUMEROAQUI",
   "contatos":["SEUNUMEROAQUI"],
   "motivadora":"2022-06-30",
   "categoria":"V",
   "elegivel_uc4":"Y",
   "elegivel_transfer":"N",
   "status_transfer":"N"
}
```

Notas importantes sobre o payload:
- Substitua *todas* as ocorrências de `SEUNUMEROAQUI` pelo número de telefone de teste no formato esperado pelo discador.
- Valide o campo `cpf_cnpj` antes do teste (o exemplo contém um CPF numérico sem formatação).
- `ucid` é um identificador de chamada; use uma string que facilite auditoria (ex.: `TESTE_<seunome>`).

---

## Como executar o teste (exemplo)

1. Atualize o JSON acima substituindo o(s) placeholder(s) (por exemplo, `SEUNUMEROAQUI`).
2. Envie a mensagem para a fila/serviço que alimenta o discador.

Exemplo (opcional) — se a fila for AWS SQS e você tiver AWS CLI configurado:

```powershell
# Salve o JSON em um arquivo local 'payload.json'
aws sqs send-message --queue-url <SUA_QUEUE_URL> --message-body (Get-Content .\payload.json -Raw)
```

Se o consumidor usar outro mecanismo (API HTTP, broker interno), envie o JSON conforme o método suportado.

---

## Comportamento esperado

- A chamada de teste deve ser disparada com as informações do payload.
- São usadas flags como `chamada_teste":"Y"` para diferenciar execução de produção de execução de teste; confirme com a equipe se essa flag é respeitada pelo discador.
- Se o fluxo depender de `elegivel_uc4` ou outras flags, o comportamento pode variar (ex.: abrir fluxo de negociação, envio de fatura, etc.).

---

## Riscos e cuidados

- Nunca execute testes em números reais de clientes sem autorização. Use um número de teste ou telefone de laboratório.
- Confirme se `chamada_teste` impede ações irreversíveis (cobranças, alterações em sistemas externos).
- Evite deixar JSONs de teste com dados reais sensíveis em repositórios públicos.

---

## Observações finais

- O script/payload neste documento foi extraído do arquivo original `Fazer teste de chamada.TXT` e organizado como documentação para facilitar testes.

---
