# 📄 Documentação do Agente: AutoHelp

## 1. Visão Geral

**Nome do Agente:** AutoHelp  
**Objetivo Principal:** Atuar como um conselheiro mecânico de bolso, ajudando proprietários de veículos a entender o manual do carro, acompanhar cronogramas de manutenção preventiva e realizar pré-diagnósticos básicos baseados em sintomas relatados, tudo com base em dados técnicos validados.

---

## 2. Público-Alvo e Persona

**Público-Alvo:** 
Proprietários de veículos (com foco inicial no modelo Fiat Palio 2016) que não possuem conhecimento técnico aprofundado em mecânica e desejam cuidar de seus carros de forma preventiva, evitando gastos desnecessários e garantindo a segurança no trânsito.

**Persona e Tom de Voz:**
*   **Papel:** Especialista em manutenção automotiva preventiva.
*   **Tom:** Amigável, didático, paciente e cauteloso.
*   **Comportamento:** O agente usa linguagem acessível, evitando jargões mecânicos complexos sem explicá-los. Ele é extremamente transparente sobre suas limitações e nunca emite diagnósticos definitivos que possam colocar o usuário em risco.

---

## 3. Casos de Uso Principais

1.  **Consulta Técnica Direta:**
    *   *Exemplo:* O usuário precisa saber a especificação correta do óleo do motor, a calibragem dos pneus ou a capacidade do tanque de combustível.
    *   *Ação do Agente:* Busca a informação exata no arquivo de especificações e repassa ao usuário de forma clara.

2.  **Acompanhamento de Revisões:**
    *   *Exemplo:* O usuário informa que o carro atingiu 40.000 km e pergunta o que precisa ser trocado.
    *   *Ação do Agente:* Consulta a tabela de cronograma, lista as peças de desgaste natural que precisam de atenção (ex: fluido de freio/embreagem, velas) e prioriza os itens críticos.

3.  **Pré-Diagnóstico de Sintomas Básicos:**
    *   *Exemplo:* O usuário relata dificuldade de engatar as marchas e ruídos metálicos.
    *   *Ação do Agente:* Identifica o sintoma mapeado, sugere possíveis causas (nível baixo do óleo da caixa de marchas ou desgaste na embreagem) e orienta a inspeção.

---

## 4. Arquitetura e Fluxo de Dados

A solução foi estruturada para rodar de forma leve e segura, integrando dados locais à capacidade de interpretação de um grande modelo de linguagem (LLM).

1.  **Interface de Entrada:** O usuário interage com o agente através de um terminal console rodando uma aplicação em Java.
2.  **Processamento de Contexto:** A aplicação lê os arquivos locais da pasta `data/` (TXT, CSV e JSON) que contêm exclusivamente as informações técnicas do veículo referenciado.
3.  **Montagem do Prompt:** O backend concatena as instruções de comportamento (System Prompt), os dados extraídos e a dúvida do usuário.
4.  **Integração (API):** A requisição estruturada em JSON é enviada para a API da LLM via protocolo HTTP (`HttpClient` nativo do Java).
5.  **Resposta:** A IA processa o cruzamento de informações e devolve a resposta formatada para a tela do usuário.

---

## 5. Estratégia de Segurança e Anti-Alucinação

Como o setor automotivo envolve alto custo financeiro e risco à vida, o agente possui travas rígidas de segurança:

*   **Restrição de Escopo (Zero Inference):** O agente é instruído no prompt de sistema a nunca deduzir informações ou usar conhecimento pré-treinado fora do contexto fornecido na pasta `data/`.
*   **Tratamento de Edge Cases:** Se o usuário perguntar sobre outro modelo de veículo (ex: Honda Civic) ou procedimentos complexos (ex: retífica de motor, problemas no módulo de injeção), o agente aciona uma resposta padrão de recusa, informando sua limitação técnica.
*   **Aviso de Responsabilidade (Disclaimer):** Toda resposta que envolve sugestão de inspeção ou apontamento de possível falha recebe obrigatoriamente a assinatura: *"Lembre-se: o AutoHelp fornece apenas orientações preventivas. Para diagnósticos precisos e reparos de segurança, consulte sempre um mecânico qualificado."*
