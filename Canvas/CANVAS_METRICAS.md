# Canvas de Métricas de Escala e Impacto

## Descrição

O Canvas de Métricas de Escala e Impacto organiza e documenta as métricas essenciais para monitorar a operação da solução ScanSheet em escala, avaliando seu desempenho, uso e impacto no negócio. Ele ajuda a garantir que o sistema mantenha qualidade e eficiência à medida que cresce.

## 1. Objetivo do Monitoramento

Garantir que a solução ScanSheet atinja e mantenha seus objetivos de eficiência operacional, redução de erros de transcrição e economia de tempo na digitalização de dados de saúde, validando seu impacto positivo e orientando melhorias contínuas à medida que o uso aumenta.

## 2. Métricas de Uso

- **Volume de Processamento:** Número de fichas processadas por dia/semana.
- **Usuários Ativos:** Quantidade de profissionais de saúde utilizando o aplicativo (diário, semanal, mensal).
- **Taxa de Adoção:** Percentual de fichas digitalizadas via ScanSheet em comparação com o método manual tradicional na instituição.
- **Frequência de Uso:** Média de sessões de digitalização por usuário por semana.

## 3. Métricas de Desempenho

- **Tempo Médio de Processamento:** Tempo total desde o upload da imagem até a disponibilização do arquivo CSV para o usuário.
- **Latência da API:** Tempo de resposta do backend e do agente de IA.
- **Taxa de Erro do Sistema:** Percentual de falhas que impedem o processamento completo de uma ficha.

### Acurácia de Extração de Dados (Exemplo: Ficha de Cadastro Individual):

- **Acurácia de campos boolean (sim/não, etc.):** 85,5% 
- **Acurácia de campos de list (múltipla escolha):** 78,5% 
- **Acurácia de campos de text (texto livre):** 75,5% 

## 4. Métricas de Impacto no Negócio

- **Redução de Tempo de Digitalização:** Total de horas de trabalho economizadas que seriam gastas em transcrição manual.
- **Redução de Custos Operacionais:** Custo economizado com base nas horas de trabalho reduzidas.
- **Redução de Erros de Transcrição:** Comparativo da taxa de erro do ScanSheet com a taxa de erro histórica da digitalização manual.
- **Aceleração na Disponibilização de Dados:** Tempo reduzido entre a coleta da ficha física e a disponibilidade dos dados estruturados para análise.

## 5. Métricas de Satisfação do Usuário

- **Pontuação de Satisfação do Cliente (CSAT):** Nota média de satisfação coletada através de pesquisas no aplicativo.
- **Taxa de Retenção de Usuários:** Percentual de profissionais que continuam usando a solução após o primeiro mês.
- **Volume de Feedback:** Quantidade de sugestões de melhoria ou relatos de erros de extração enviados pelos usuários.

## 6. Ferramentas de Monitoramento

- **Uso e Desempenho:** Logs da API (FastAPI), monitoramento de desempenho das requisições.

## 7. Benchmarks

- **Tempo de Processamento Ideal:** ≤ 30 segundos por ficha.
- **Acurácia Geral de Extração (Meta):** ≥ 95%.
- **Metas de Acurácia por Campo:** Elevar a acurácia de list para ≥ 90% e de text para ≥ 85%.
- **Satisfação do Cliente Ideal:** ≥ 4.5 de 5.

## 8. Acompanhamento de Tendências

- **Relatórios semanais** de uso, desempenho e acurácia por tipo de formulário.
- **Análise mensal** comparando as métricas atuais com os benchmarks e o histórico.
- **Identificação** dos tipos de formulários ou campos com menor precisão para priorizar melhorias.

## 9. Ações Baseadas nas Métricas

- **Acurácia Baixa:** Se a acurácia de um formulário estiver abaixo da meta, iniciar um ciclo de refinamento do prompt de IA correspondente.
- **Lentidão:** Se o tempo de processamento exceder 45 segundos, investigar gargalos no backend, na rede ou na latência das APIs de IA.

## 10. Relatórios e Compartilhamento

- **Relatórios periódicos** de desempenho e uso enviados para a equipe de produto e stakeholders do projeto.
