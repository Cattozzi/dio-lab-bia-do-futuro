# Base de Conhecimento

## Dados Utilizados

Os arquivos financeiros originais da pasta `data` foram substituídos por dados automotivos focados em manutenção preventiva, garantindo um escopo fechado e preciso para o agente:

| Arquivo | Formato | Utilização no Agente |
|---------|---------|---------------------|
| `manual_palio2016.txt` | TXT | Contextualizar a IA com especificações técnicas e capacidades de fluidos. |
| `cronograma_revisoes.csv` | CSV | Fornecer uma estrutura tabular de tempo e quilometragem para manutenções periódicas. |
| `guia_sintomas.json` | JSON | Personalizar o pré-diagnóstico cruzando queixas comuns com possíveis causas. |

---

## Adaptações nos Dados

Os dados mockados originais (voltados para finanças e investimentos) foram totalmente removidos. No lugar, criei um dataset estruturado focado exclusivamente no **Fiat Palio 2016**. A separação em três formatos (TXT, CSV e JSON) foi intencional para simular diferentes fontes de dados que uma aplicação real precisaria consumir, desde textos não estruturados até dados perfeitamente tabulados.

---

## Estratégia de Integração

### Como os dados são carregados?
Os arquivos são lidos na inicialização da aplicação backend (utilizando classes nativas de leitura de arquivos em Java) e mapeados em memória. O arquivo CSV é processado utilizando uma lógica relacional estruturada, simulando o comportamento de consultas em um banco de dados SQL Server, cruzando a quilometragem informada pelo usuário com a linha correspondente do arquivo antes de injetar a informação na LLM. O JSON tem suas chaves e valores extraídos para mapeamento de sintomas.

### Como os dados são usados no prompt?
Os dados não ficam soltos. Eles são concatenados dinamicamente ao final do **System Prompt** sob a tag `[CONTEXTO DE DADOS]`. Se o usuário pergunta sobre revisão, apenas o trecho do CSV e do TXT é injetado, economizando tokens e mantendo a IA focada apenas na informação necessária para aquela interação específica.

---

## Exemplo de Contexto Montado

```text
[INSTRUÇÕES DO SISTEMA]
Você é o AutoHelp, assistente de manutenção preventiva. Responda apenas com base nos dados abaixo.

[CONTEXTO DE DADOS]
Veículo: Fiat Palio 2016

Dados Técnicos Relevantes:
- Óleo do motor: Sintético 5W30 (Troca a cada 10.000 km ou 12 meses).
- Câmbio manual: Verificar nível a cada 20.000 km.

Diagnóstico Mapeado:
- Sintoma Relatado: "Dificuldade de engatar marchas"
- Causa Possível: Baixo nível de óleo na caixa ou desgaste na embreagem.

[PERGUNTA DO USUÁRIO]
Meu carro está com 20.000 km e as marchas estão raspando. O que eu faço e qual óleo de motor eu uso?
