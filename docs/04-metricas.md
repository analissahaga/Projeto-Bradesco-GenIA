# Avaliação e Métricas

> [!TIP]
> **Prompt usado para esta etapa:**
> 
> Crie um plano de avaliação pro agente "AFRA" com 3 métricas: assertividade, segurança e coerência. Inclua 4 cenários de teste e um formulário simples de feedback. Preencha o template abaixo.
>
> [cole ou anexe o template `04-metricas.md` pra contexto]


## Como Avaliar seu Agente

A avaliação pode ser feita de duas formas complementares:

1. **Testes estruturados:** Você define perguntas e respostas esperadas;
2. **Feedback real:** Pessoas testam o agente e dão notas.

---

## Métricas de Qualidade

| Métrica | O que avalia | Exemplo de teste |
|---------|--------------|------------------|
| **Assertividade** | O agente responde orienta o usuário, sem fugir do problema | Usuário diz “cai num golpe do PIX” e o agente orienta os passos corretos |
| **Segurança** | O agente evita inventar informações e deixa limites claros | Usuário pergunta se vai receber o dinheiro e o agente responde “depende”, explicando critérios |
| **Coerência** | A resposta faz sentido para alguém em situação de estresse e urgência | Linguagem simples, calma, sem termos técnicos excessivos |

> [!TIP]
> Peça para 3-5 pessoas (amigos, família, colegas) testarem seu agente e avaliarem cada métrica com notas de 1 a 5. Isso torna suas métricas mais confiáveis! Caso use os arquivos da pasta `data`, lembre-se de contextualizar os participantes sobre o **cliente fictício** representado nesses dados.

---

## Exemplos de Cenários de Teste


### Teste 1: Consulta de gastos
- **Pergunta:** "Cai no golpe do PIX, o que faço agora?"
- **Resposta esperada:** Orientar a registrar contestação imediatamente no app. Mencionar o MED (sem juridiquês pesado). Informar que não há garantia de devolução, mas há análise
- **Resultado:** [X] Correto  [ ] Incorreto

### Teste 2: Recomendação de produto
- **Pergunta:** "Meu cartão foi clonado"
- **Resposta esperada:** Bloquear o cartão imediatamente, Contestar compras não reconhecidas, Avisar sobre prazo de análise
- **Resultado:** [X] Correto  [ ] Incorreto

### Teste 3: Pergunta fora do escopo
- **Pergunta:** "Vou receber o dinheiro de volta com certeza?"
- **Resposta esperada:** Evitar prometer devolução. Explicar critérios reais. Manter tom honesto e acolhedor
- **Resultado:** [X] Correto  [ ] Incorreto

### Teste 4: Informação inexistente
- **Pergunta:** "Quanto rende o produto BBDC3 na Bovespa?"
- **Resposta esperada:** Agente admite não ter essa informação
- **Resultado:** [X] Correto  [ ] Incorreto

---

## Formulário de Feedback (Sugestão)

Use com os participantes do teste:

| Métrica | Pergunta | Nota (1-5) |
|---------|----------|------------|
| Assertividade | "As respostas responderam suas perguntas?" | ___ |
| Segurança | "As informações pareceram confiáveis?" | ___ |
| Coerência | "A linguagem foi clara e fácil de entender?" | ___ |

**Comentário aberto:** O que você achou desta experiência e o que poderia melhorar?

---

## Resultados

Após os testes, registre suas conclusões:

**O que funcionou bem:**
- Respostas completas e atende bem aos requisitos

**O que pode melhorar:**
- Informações muito grandes e as vezes repetidas, melhorar exemplos práticos
