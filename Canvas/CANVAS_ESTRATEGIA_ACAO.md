# Canvas de Estratégia e Ação do Projeto - ScanSheet

## 1. Objetivo Estratégico Geral


**Objetivo:** Otimizar a digitalização de dados na área da saúde pública, automatizando o processo de conversão de imagens de fichas em planilhas estruturadas para aumentar a eficiência operacional e reduzir erros de transcrição manual.


## 2. Objetivos Estratégicos Secundários

**Objetivos Secundários:**
- Reduzir o tempo de digitalização manual de dados em mais de 100%.
- Facilitar o acesso a dados estruturados para análise em saúde pública.
- Reduzir custos operacionais relacionados à digitalização manual.


## 3. Resultados-Chave Esperados (Quantitativos)

**Resultados Esperados:**
- Reduzir o tempo de processamento de uma ficha de 5 minutos (em média) para 30s.
- Converter automaticamente dados em formato CSV para integração com sistemas existentes em 4 meses.
- Disponibilizar aplicativo mobile funcional para iOS e Android em 4 meses.


## 4. Indicadores-Chave de Sucesso (KPIs)

**KPIs Principais:**
- **Tempo de Processamento:** Tempo médio para processar uma imagem de ficha.
- **Taxa de Precisão:** Porcentagem de dados extraídos corretamente.
- **Taxa de Erro:** Porcentagem de dados com erros de transcrição.
- **Tempo de Resposta:** Tempo de resposta da API para processamento de imagens.


## 5. Requisitos Estratégicos e Restrições

**Requisitos Estratégicos:**
- A solução deve estar em conformidade com a LGPD para proteção de dados de saúde.
- Deve automatizar e preencher o arquivo CSV com os dados das fichas estruturados corretamente.

**Restrições:**
- Orçamento limitado para desenvolvimento e infraestrutura.
- Necessidade de APIs pagas (OpenAI) para processamento de IA.
- Limitação do uso de tokens em APIs de modelos LLM. (200000 tokens)

## 6. Priorização de Objetivos

**Instruções:** Classifique os objetivos em ordem de prioridade, com base em impacto no negócio, viabilidade técnica e urgência.

**Alta Prioridade:**
- Reduzir o tempo de digitalização manual de dados.
- Desenvolver MVP funcional com processamento básico de imagens.
- Disponibilizar aplicativo mobile para iOS e Android.

**Média Prioridade:**
- Implementar sistema de validação de dados extraídos.

**Baixa Prioridade:**
- Implementar funcionalidades avançadas de correção manual de dados.
- Integração com base da dados externas.


## 7. Ações e Recursos Necessários

**Ações Prioritárias:**
- **Ação 1:** Desenvolver e testar o agente de IA com OCR e extração de dados estruturados.
- **Ação 2:** Implementar backend FastAPI para processamento de imagens e conversão para CSV.
- **Ação 3:** Criar aplicativo mobile básico para captura e envio de imagens.
- **Ação 4:** Configurar pipeline de processamento completo (imagem → IA → CSV).
- **Ação 5:** Implementar testes automatizados para validação de qualidade.

**Recursos Necessários:**
- **Recurso Humano:** Equipe de desenvolvimento (3 desenvolvedores).
- **Recurso Técnico:** APIs de IA (OpenAI GPT-4, MistralAI) para processamento.
- **Recurso Infraestrutura:** Servidor para hospedagem do backend FastAPI.
- **Recurso Financeiro:** Orçamento para licenciamento de APIs de IA e infraestrutura.
- **Recurso de Dados:** Conjunto de imagens de formulários para treinamento e teste.

**Cronograma Estimado:**
- **Meses 1-3:** Desenvolvimento do agente de IA e backend básico.
- **Meses 3-4:** Desenvolvimento do aplicativo mobile e integração completa. Testes, refinamentos e implementação em ambiente de produção.