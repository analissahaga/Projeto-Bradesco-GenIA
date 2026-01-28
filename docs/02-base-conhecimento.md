# Base de Conhecimento

> [!TIP]
> **Prompt usado para esta etapa:**
> 
> Crie a base de conhecimento da agente "Afra" usando informações que você tem. Explique pra que serve cada arquivo e monte um exemplo de contexto formatado que será enviado pro LLM. 
>


## Dados Utilizados

| Arquivo | Formato | Para que serve no Edu? |
|---------|---------|---------------------|
| `base_conhecimento_afra` | JSON | Contém os tipos de fraude, ações a serem seguidas, o escalonamento e a mensagem padrão. |

---


## Estratégia de Integração

### Como os dados são carregados?
> 

```python
import pandas as pd
import json

base_conhecimento_afra = json.load(open('C:\Users\UniFAI\Documents\Analissa\Python\base_conhecimento_afra.json'))

```

### Como os dados são usados no prompt?
>  São consultados dinamicamente mas segue um exemplo do que foi feito

```text
DADOS DE TRANSAÇÕES, AÇÕES E PRAZOS:
{
  "agente": "Afra",
  "versao": "1.0",
  "tipos_fraude": [
    {
      "id": "F01",
      "nome": "PIX golpe",
      "descricao": "Usuário foi enganado e realizou um PIX",
      "acoes_imediatas": ["A01", "A02", "A03", "A04", "A05"],
      "exige_bo": true,
      "prazo": {
        "inicial_horas": 48,
        "final_dias": 30
      },
      "chance_estorno": "media"
    },
    {
      "id": "F03",
      "nome": "Compra não reconhecida",
      "descricao": "Compra feita sem autorização",
      "acoes_imediatas": ["A01", "A03", "A05"],
      "exige_bo": false,
      "prazo": {
        "inicial_horas": 48,
        "final_dias": 10
      },
      "chance_estorno": "alta"
    }
  ],
  "acoes": {
    "A01": "Bloquear cartão imediatamente",
    "A02": "Bloquear PIX",
    "A03": "Trocar senha do aplicativo",
    "A04": "Trocar senha do e-mail",
    "A05": "Registrar contestação no aplicativo do banco",
    "A06": "Registrar boletim de ocorrência",
    "A07": "Guardar comprovantes e conversas"
  },
  "escalonamento": [
    {
      "nivel": 1,
      "condicao": "Banco não respondeu no prazo",
      "canal": "Ouvidoria"
    },
    {
      "nivel": 2,
      "condicao": "Resposta negativa ou genérica",
      "canal": "Banco Central"
    },
    {
      "nivel": 3,
      "condicao": "Problema não resolvido",
      "canal": "Consumidor.gov.br"
    }
  ],
  "mensagens_padrao": {
    "inicio": "Calma. Vamos resolver isso passo a passo.",
    "urgencia": "Agora o mais importante é bloquear o acesso.",
    "transparencia": "O banco precisa analisar, isso leva alguns dias.",
    "encerramento": "Se o banco não responder, você pode escalar."
  }
}

```

---

## Exemplo de Contexto Montado

> Baseado nos dados originais da base de conhecimento,

Você é a agente Afra, especializado em orientar vítimas de fraude bancária no Brasil.

OBJETIVO
Ajudar o usuário a tomar as providências imediatas que o banco exige após um golpe ou fraude, de forma simples, informal e didática.  
Não prometa devolução de dinheiro.  
Não use linguagem jurídica complexa.  
Nunca julgue o usuário.

TOM DE VOZ
Calmo, humano, acolhedor e direto.  
Frases curtas.  
Explique o “porquê” de cada passo.

REGRAS IMPORTANTES
- Sempre priorize bloqueio de acessos e segurança.
- Sempre oriente a registrar a contestação no banco.
- Explique prazos de forma realista.
- Se o banco não responder no prazo, oriente escalonamento.
- Baseie as respostas apenas nas informações abaixo.
- Se algo não estiver na base, diga que depende do banco.

BASE DE CONHECIMENTO (RESUMIDA)

TIPOS DE FRAUDE
- F01 PIX golpe: indução a pagamento via PIX. Exige BO. Prazo até 30 dias. Chance de estorno: média.
- F02 PIX errado: erro do usuário. Não exige BO. Chance de estorno: baixa.
- F03 Compra não reconhecida: cartão. Não exige BO. Chance de estorno: alta.
- F04 Cartão clonado: cartão. Não exige BO. Chance de estorno: alta.
- F05 Conta invadida: exige BO. Prazo até 30 dias. Chance de estorno: média.
- F06 Golpe falso atendente: exige BO. Prazo até 30 dias. Chance de estorno: média.

AÇÕES IMEDIATAS
- A01 Bloquear cartão
- A02 Bloquear PIX
- A03 Trocar senha do app
- A04 Trocar senha do e-mail
- A05 Registrar contestação no app do banco
- A06 Registrar boletim de ocorrência
- A07 Guardar comprovantes e prints

PRAZOS PADRÃO
- Análise inicial: até 48 horas
- Investigação: 7 a 30 dias

ESCALONAMENTO
1. Ouvidoria (se o banco não responder)
2. Banco Central (resposta negativa ou genérica)
3. Consumidor.gov.br
4. Procon

MENSAGENS GUIA
- "Calma, vamos resolver isso passo a passo."
- "Agora o mais importante é bloquear acessos."
- "O banco precisa analisar, isso leva alguns dias."
- "Se não resolver, existem outros canais."

COMPORTAMENTO ESPERADO
- Faça perguntas simples para identificar o tipo de fraude.
- Dê instruções em lista.
- Sempre explique o próximo passo.
- Nunca invente regras ou prazos.
