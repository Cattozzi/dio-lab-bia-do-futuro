# Avaliação e Métricas

## Como Avaliar seu Agente

A avaliação pode ser feita de duas formas complementares:

1. **Testes estruturados:** Você define perguntas e respostas esperadas;
2. **Feedback real:** Pessoas testam o agente e dão notas.

---

## Métricas de Qualidade

| Métrica | O que avalia | Exemplo de teste |
|---------|--------------|------------------|
| **Assertividade** | O agente respondeu o que foi perguntado? | Perguntar a especificação do óleo e receber "5W30" |
| **Segurança (Anti-Alucinação)** | O agente evitou inventar informações? | Perguntar sobre manutenção de um Honda Civic e ele admitir que não sabe |
| **Coerência** | A resposta faz sentido para o cenário relatado? | Sugerir troca da correia dentada quando o usuário informa 60.000 km |

> [!TIP]
> Peça para 3-5 pessoas (amigos, família, colegas) testarem seu agente e avaliarem cada métrica com notas de 1 a 5. Isso torna suas métricas mais confiáveis! Caso use os arquivos da pasta `data`, lembre-se de contextualizar os participantes sobre o **veículo de referência** mapeado nesses dados (Fiat Palio 2016).

---

## Exemplos de Cenários de Teste

Crie testes simples para validar seu agente:

### Teste 1: Consulta técnica direta
- **Pergunta:** "Qual a calibragem recomendada para os pneus?"
- **Resposta esperada:** Valor exato (28 a 32 psi) baseado no `manual_palio2016.txt`, acompanhado do aviso de segurança.
- **Resultado:** [ ] Correto  [ ] Incorreto

### Teste 2: Diagnóstico preventivo estruturado
- **Pergunta:** "Meu carro chegou aos 60.000 km, o que preciso revisar?"
- **Resposta esperada:** Retorno dos itens críticos (ex: Correia dentada e tensor) baseados no `cronograma_revisoes.csv`.
- **Resultado:** [ ] Correto  [ ] Incorreto

### Teste 3: Pergunta fora do escopo do sistema
- **Pergunta:** "Qual investimento rende mais na bolsa?"
- **Resposta esperada:** Agente informa que é especializado exclusivamente em manutenção automotiva preventiva.
- **Resultado:** [ ] Correto  [ ] Incorreto

### Teste 4: Procedimento de risco ou não mapeado
- **Pergunta:** "Como faço para trocar o módulo de injeção eletrônica?"
- **Resposta esperada:** Agente admite não ter essa informação técnica complexa na base e reforça que o usuário deve buscar um mecânico qualificado.
- **Resultado:** [ ] Correto  [ ] Incorreto

---

## Resultados

Após os testes, registre suas conclusões:

**O que funcionou bem:**
- A extração de dados técnicos (como tipos de fluidos) foi extremamente precisa.
- O agente bloqueou 100% das tentativas de pedir manuais de veículos concorrentes.

**O que pode melhorar:**
- Perguntas muito curtas ("carro falhando") precisam gerar respostas melhores solicitando mais contexto ao invés de adivinhar o problema.

---

## Métricas Avançadas (Opcional)

Para quem quer explorar mais, algumas métricas técnicas de observabilidade também podem fazer parte da sua solução, como:

- Latência e tempo de resposta;
- Consumo de tokens e custos;
- Logs e taxa de erros.

Ferramentas especializadas em LLMs, como [LangWatch](https://langwatch.ai/) e [LangFuse](https://langfuse.com/), são exemplos que podem ajudar nesse monitoramento. Entretanto, fique à vontade para usar qualquer outra que você já conheça!
