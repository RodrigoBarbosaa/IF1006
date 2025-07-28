# Diagramas de Arquitetura - ScanSheet

## Nível de Contexto

### Título: "Diagrama de Contexto para o ScanSheet"

**Descrição:** Mostra os atores externos (usuários, sistemas, dispositivos) e sua interação com o sistema de IA. Ideal para comunicar o propósito geral e o papel do assistente.

**Elementos e Interações:**

#### Sistema Central:
**ScanSheet:** Sistema principal que converte imagens de fichas em dados estruturados de saúde pública.

#### Atores (Usuários):
**Profissional de Saúde:** Funcionário da área da saúde que captura fotos de fichas físicas e precisa digitalizar os dados.

**Interação:** Captura fotos de documentos via aplicativo mobile e recebe planilhas estruturadas com os dados extraídos.

#### Atores (Sistemas Externos):
**Sistemas de Saúde Pública:** Sistemas legados que recebem os dados estruturados para análise e tomada de decisões.

**Interação:** O ScanSheet fornece dados estruturados em formato CSV para serem integrados com sistemas existentes/ou bases de dados.

**Dispositivos Móveis:** Smartphones iOS e Android utilizados pelos profissionais para captura de imagens.

**Interação:** Os dispositivos enviam imagens para o sistema e recebem os resultados processados.

---

## Nível de Contêiner

### Título: "Diagrama de Contêiner para o ScanSheet"

**Descrição:** Detalha os componentes principais do sistema, como serviços de backend, bancos de dados, interfaces de usuário e APIs.

**Elementos e Interações:**

#### Contêiner 1: Aplicativo Mobile (Frontend)
**Descrição:** Interface de usuário onde profissionais de saúde capturam e enviam imagens de documentos.

**Tecnologia:** 
- iOS: Swift e SwiftUI
- Android: Kotlin e Compose

**Interação:** Envia imagens capturadas para o Backend API e recebe dados estruturados para download.

#### Contêiner 2: Backend API (Backend)
**Descrição:** Orquestra o processamento de imagens, gerencia as requisições e coordena a comunicação entre componentes. Converte os dados extraídos em formatos estruturados (CSV) para uso em sistemas de saúde.

**Tecnologia:** Python (FastAPI, pandas)

**Interação:** Recebe imagens do Aplicativo Mobile; chama o Agente de IA para processamento; retorna dados estruturados para o frontend. Recebe dados do Agente de IA; gera arquivos CSV/.


#### Contêiner 3: Agente de IA
**Descrição:** Microsserviço dedicado que encapsula os modelos de IA para OCR e extração de dados estruturados.

**Tecnologia:** Python, LangChain, ChatGPT

**Interação:** Recebe imagens do Backend API; processa OCR e extrai dados; retorna informações estruturadas.


---

## Nível de Componente

#TODO: colocar FrontEnd

### Título: "Diagrama de Componentes para o Backend API"

**Descrição:** Detalha os componentes internos do contêiner Backend, mostrando como as funcionalidades são divididas e interligadas.

**Elementos e Interações:**

#### Componente 1: Controlador de API (API Controller)
**Descrição:** Ponto de entrada do serviço. Expõe os endpoints (ex: /processar-imagem) e valida as requisições recebidas do Aplicativo Mobile.

**Tecnologia:** FastAPI

**Interação:** Recebe imagens do frontend; delega processamento para o Gerenciador de Processamento; retorna resultados para o cliente.

#### Componente 2: Gerenciador de Processamento
**Descrição:** Orquestra o fluxo de processamento de imagens, coordenando a comunicação entre diferentes componentes.

**Tecnologia:** Python (lógica de negócio)

**Interação:** Recebe imagens; chama a biblioteca do Agente de IA; envia dados, recebe os dados estruturados e faz a conversão para arquivo CSV; retorna resultados.

#### Componente 3: Cliente do Agente de IA
**Descrição:** Encapsula a lógica de comunicação com o Agente de IA, incluindo tratamento de erros e retry logic.

**Tecnologia:** Biblioteca Python para comunicação HTTP

**Interação:** Envia imagens para o Agente de IA; recebe dados extraídos; trata erros de comunicação.

#### Componente 4: Conversor de Formatos
**Descrição:** Converte os dados extraídos pelo Agente de IA em formatos estruturados (CSV).

**Tecnologia:** pandas

**Interação:** Recebe dados do Gerenciador de Processamento (lógica interna); gera arquivos CSV; retorna para o Gerenciador.


### Título: "Diagrama de Componentes para o Agente de IA"

**Elementos e Interações:**

#### Componente 1: Controlador do Agente
**Descrição:** Ponto de entrada do Agente de IA. Gerencia as requisições de processamento de imagens.

**Tecnologia:** Python

**Interação:** Recebe imagens do Backend API; coordena o processamento; retorna dados estruturados.

#### Componente 2: Processador de OCR
**Descrição:** Realiza o reconhecimento óptico de caracteres nas imagens recebidas.

**Tecnologia:** OCR libraries (MistralAI, OpenAI)

**Interação:** Recebe imagens; extrai texto e markdown das imagens; retorna texto e estrutura reconhecidos.

#### Componente 3: Extrator de Dados Estruturados
**Descrição:** Utiliza IA para extrair dados específicos do texto OCR e estruturá-los em formato tabular.

**Tecnologia:** LangChain, ChatGPT, Pydantic

**Interação:** Recebe texto do Processador de OCR; extrai dados estruturados; retorna informações organizadas.

#### Componente 4: Gerador de Prompts
**Descrição:** Constrói prompts específicos para o ChatGPT baseados no tipo de documento e dados necessários.

**Tecnologia:** LangChain

**Interação:** Gera prompts para o Extrator de Dados; adapta prompts baseado no contexto do documento.

#### Componente 5: Cliente do ChatGPT
**Descrição:** Encapsula a comunicação com a API do ChatGPT para processamento de linguagem natural.

**Tecnologia:** OpenAI API client

**Interação:** Envia prompts para o ChatGPT; recebe respostas estruturadas; trata erros de API. 