# 🤖 AutoHelp - Assistente de Manutenção Automotiva Preventiva

## Contexto

Os assistentes virtuais estão revolucionando a forma como lidamos com tarefas do dia a dia. Neste desafio, idealizamos e prototipamos um agente inteligente voltado para o setor automotivo que utiliza IA Generativa para:

- **Educar** proprietários de veículos sobre manutenções de rotina.
- **Diagnosticar preventivamente** problemas básicos com base em sintomas relatados.
- **Consultar manuais** de forma rápida e precisa (Foco inicial: Fiat Palio 2016).
- **Garantir segurança** não alucinando diagnósticos complexos e sempre recomendando um mecânico qualificado para casos críticos.

---

## O Que Foi Entregue

### 1. Documentação do Agente

Definição de **o que** o agente faz e **como** ele funciona:

- **Caso de Uso:** Auxiliar nas dúvidas sobre manutenção básica, troca de fluidos, calibragem de pneus e cronograma de revisões.
- **Persona e Tom de Voz:** Amigável, didático, paciente e focado na segurança do usuário.
- **Arquitetura:** Interação via terminal (ou interface simples), processando a dúvida do usuário, buscando no arquivo de contexto e enviando o prompt formatado para a API de LLM.
- **Segurança:** Regras estritas no System Prompt para evitar respostas inventadas sobre veículos ou peças não mapeadas na base.

📄 **Documentação:** [`docs/01-documentacao-agente.md`](./docs/01-documentacao-agente.md)

---

### 2. Base de Conhecimento

Utilizamos arquivos de texto locais na pasta [`data/`](./data/) para alimentar o agente, garantindo que ele não busque informações genéricas na internet:

| Arquivo | Formato | Descrição |
|---------|---------|-----------|
| `manual_palio2016.txt` | TXT | Especificações de fluidos, pneus e peças do veículo |
| `cronograma_revisoes.csv` | CSV | Tabela de quilometragem e tempo para manutenções |
| `guia_sintomas.json` | JSON | Mapeamento de sintomas comuns (ex: ruídos, trancos) e possíveis causas |

📄 **Documentação:** [`docs/02-base-conhecimento.md`](./docs/02-base-conhecimento.md)

---

### 3. Prompts do Agente

Documentação das instruções que definem o comportamento da IA:

- **System Prompt:** Instruções gerais obrigando o uso exclusivo da base de conhecimento e a inclusão de avisos de segurança ("consulte um mecânico").
- **Exemplos de Interação (Few-Shot):** Exemplos de como responder sobre o nível do óleo do câmbio e pressão dos pneus.
- **Tratamento de Edge Cases:** Respostas padronizadas para quando o usuário pergunta sobre um Honda Civic ou outro carro não suportado.

📄 **Documentação:** [`docs/03-prompts.md`](./docs/03-prompts.md)

---

### 4. Aplicação Funcional

Protótipo funcional do agente integrado com a LLM:

- Chatbot interativo via Terminal Console (construído em Java).
- Integração com a API via `HttpClient` (nativo do Java 11+).
- Leitura dinâmica dos arquivos da pasta `data/`.

📁 **Código Fonte:** [`src/AutoHelpApp.java`](./src/AutoHelpApp.java)

---

### 5. Avaliação e Métricas

Avaliação da qualidade das respostas do agente com base em cenários de teste:

**Métricas Aplicadas:**
- **Precisão:** Testes de perguntas diretas sobre dados do manual (ex: tipo de óleo).
- **Segurança (Anti-Alucinação):** Teste de recusa ao perguntar sobre defeitos elétricos complexos não mapeados.
- **Clareza:** Avaliação da presença do aviso de segurança no final de cada diagnóstico.

📄 **Documentação:** [`docs/04-metricas.md`](./docs/04-metricas.md)

---

### 6. Pitch

Apresentação final do valor do projeto:

- **Problema:** Falta de conhecimento técnico dos motoristas leva a negligência na manutenção e gastos altos em oficinas.
- **Solução:** Um assistente de bolso que traduz o manual do carro para uma conversa simples.
- **Inovação:** Informação hiper-personalizada por modelo de veículo com foco total em prevenção.

📄 **Documentação:** [`docs/05-pitch.md`](./docs/05-pitch.md)

---

## Estrutura do Repositório

```text
📁 dio-lab-bia-do-futuro/
│
├── 📄 README.md
│
├── 📁 data/                          # Base de conhecimento do assistente
│   ├── manual_palio2016.txt          # Especificações técnicas (TXT)
│   ├── cronograma_revisoes.csv       # Tabela de manutenções (CSV)
│   └── guia_sintomas.json            # Sintomas e diagnósticos básicos (JSON)
│
├── 📁 docs/                          # Documentação das etapas do projeto
│   ├── 01-documentacao-agente.md     # Definição e persona
│   ├── 02-base-conhecimento.md       # Estrutura dos dados
│   ├── 03-prompts.md                 # System prompts e regras
│   ├── 04-metricas.md                # Resultados dos testes
│   └── 05-pitch.md                   # Resumo do projeto
│
├── 📁 src/                           # Código da aplicação funcional
│   └── AutoHelpApp.java              # Lógica de integração e terminal em Java
│
└── 📁 assets/                        # Imagens e prints de tela do terminal
    └── ...
