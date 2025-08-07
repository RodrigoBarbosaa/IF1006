# Registro de Estratégia de Inteligência - ScanSheet

## 1. Objetivo da Inteligência
**Objetivo:** Processar imagens de fichas e documentos de saúde pública para extrair dados estruturados e convertê-los em formato JSON com valores e colunas organizadas. O sistema deve reconhecer automaticamente a estrutura de documentos, extrair informações relevantes e retornar dados tabulares prontos para uso em sistemas de saúde pública.

---

## 2. Abordagem Técnica Principal

- [ ] Treinamento de Modelo Customizado
- [ ] Fine-Tuning de Modelo de Fundação
- [ ] RAG (Retrieval-Augmented Generation)
- [x] **Engenharia de Prompt Avançada**
- [ ] Outra: ________________

**Justificativa:** A abordagem de Engenharia de Prompt Avançada foi escolhida por ser adequada para tarefas de extração e estruturação de dados de documentos, permitindo flexibilidade na definição de formatos de saída e adaptação rápida a diferentes tipos de formulários sem necessidade de retreinamento de modelos.

---

## 3. Componentes Chave da Arquitetura
**Componentes da Engenharia de Prompt Avançada:**

**ScanSheetAgent:** Componente principal que orquestra o processamento de imagens e geração de prompts.

**PromptBuilder:** Sistema de construção de prompts dinâmicos baseados em templates e variáveis de entrada.

**AIMessageModel:** Modelo de validação e serialização das mensagens trocadas com os modelos de IA.

**Modelos de IA:**
- **MistralAI:** Para reconhecimento de estrutura de imagens e extração de texto/markdown
- **OpenAI GPT- 4.1:** Para outra opção mais genérica de processamento de texto e processamento de linguagem natural. Além da extração de dados estruturados

**Sistema de Schemas:** Validação de tipos de documento através de `DocumentTypeEnum` e estruturas Pydantic.

---

## 4. Fonte de Dados / Conhecimento

**Dados de Entrada:**
- **Imagens de Documentos:** Fotos de fichas, formulários e documentos de saúde pública capturadas via aplicativo mobile
- **PDFs:** Documentos digitalizados em formato PDF
- **Tipos de Documento:** Categorização através de `DocumentTypeEnum` para diferentes tipos de formulários

**Dados de Processamento:**
- **Templates de Prompt:** Prompts estruturados para diferentes tipos de documento
- **Variáveis de Contexto:** Informações adicionais como títulos, tipos de formulário e parâmetros específicos
- **Dados de Saída:** Estruturas JSON com valores extraídos e colunas organizadas

**Formato dos Dados:**
- **Entrada:** Imagens (base64), PDFs (base64), metadados de documento
- **Processamento:** Texto extraído via OCR, estrutura reconhecida
- **Saída:** JSON estruturado com dados tabulares

---
## 5. Estratégia de Avaliação

**Métricas de Avaliação:**
-  Acurácia: 
  - Taxa de precisão na extração de dados
  - Comparação entre dados extraídos e dados reais (ground truth)

- Acurácia loose:
  - Taxa de precisão na extração de dados com tolerância a erros menores
  - Comparação entre dados extraídos e dados reais (ground truth) com margem de erro (acentos, maiúscula/minúscula)

**Precisão de Extração:**
- Taxa de sucesso na extração correta de dados de diferentes tipos de campos
- Comparação entre dados extraídos e dados reais (ground truth)

**Robustez:**
- Adaptação a diferentes layouts de formulários
- Datasets testes e predições

**Armazenamento de Resultados:**
- Uso de DVC (Data Version Control) para controle de versão dos datasets e resultados de avaliação
- Salvamento em diretório remoto do google drive

**Ferramentas de Avaliação:**
- **Testes Automatizados:** Suite de testes unitários e de integração
- **Validação de resultados:** Verificação de respostas dos modelos de IA
- **DVC:** Controle de versão dos datasets e resultados de avaliação, uso do DVC devido a escalabilidade de tamanho de arquivos de validação.

**Ferramentas:**
- Framework de testes Python (unittest)
- Scripts de validação de formato JSON
- Planilhas de avaliação manual de qualidade, salvamento de resultados e datasets com DVC
- Uso de processamento com DVC

---

## 6. Ferramentas e Time

**Instruções:** Liste as principais ferramentas e os responsáveis.

**Ferramentas Principais:**
- **LangChain:** Framework para orquestração de prompts e modelos de IA
- **OpenAI API:** Acesso ao modelo GPT-4 para processamento de linguagem natural
- **MistralAI API:** Reconhecimento de estrutura de imagens e OCR
- **Pydantic:** Validação de schemas e estruturas de dados
- **Python:** Linguagem principal de desenvolvimento
- **GitHub:** Versionamento e distribuição da biblioteca
- **FastAPI:** Framework para construção do backend e API de processamento
- **DVC:** Controle de versão de datasets e resultados de avaliação

**Ferramentas de Desenvolvimento:**
- **pip:** Gerenciamento de dependências e instalação
- **unittest:** Framework de testes automatizados
- **Base64:** Codificação/decodificação de imagens e PDFs

**Time Responsável:**
- **Guilherme Lopes:** Desenvolvimento do agente de IA e arquitetura do sistema
- **Mariana Amorim:** Desenvolvimento do backend e integração
- **Rodrigo Barbosa:** Desenvolvimento dos aplicativos mobile

**Responsabilidades Técnicas:**
- **Engenheiro(a) de IA:** Desenvolvimento e manutenção dos prompts e modelos
- **Desenvolvedor(a) Backend:** Integração da biblioteca com o sistema FastAPI
- **Desenvolvedor(a) Mobile:** Interface de captura de imagens e envio de dados 