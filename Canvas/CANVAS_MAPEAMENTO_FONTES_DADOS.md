# Canvas de Mapeamento de Fontes de Dados - ScanSheet

## 1. Nome da Fonte de Dados

**Nome:** Imagens de Fichas e Formulários de Saúde, porém, esses dados não serão armazenados, apenas processados em memória e descartados após a geração do CSV.

## 2. Descrição da Fonte de Dados

**Descrição:** Imagens digitalizadas ou fotografadas de fichas e formulários de saúde pública que contêm dados estruturados a serem extraídos. Estas imagens são o principal insumo para o sistema, que processará e extrairá as informações para convertê-las em formato CSV estruturado.

## 3. Origem dos Dados

**Origem:** Upload direto pelos usuários através do aplicativo mobile ScanSheet. Os usuários capturam imagens de formulários físicos usando a câmera do dispositivo ou selecionam imagens já armazenadas no dispositivo.

## 4. Tipo de Dados

**Tipo:** 
- Dados visuais (imagens de formulários)
- Dados estruturados (após extração e processamento)

## 5. Formato dos Dados

**Formato:** 
- **Entrada:** Imagens em formatos JPG, PNG ou PDF
- **Saída:** Arquivos CSV estruturados com colunas correspondentes aos campos dos formulários
- **Transferência:** Dados criptografados durante transmissão HTTP entre Frontend e Backend

## 6. Frequência de Atualização

**Frequência:** Em tempo real, conforme os usuários fazem upload das imagens para processamento. Não há um cronograma fixo de atualização, pois os dados são processados sob demanda.

## 7. Qualidade dos Dados

**Qualidade:** A qualidade dos dados de entrada depende diretamente da qualidade das imagens capturadas pelos usuários. Fatores como iluminação, ângulo e resolução da câmera podem afetar a precisão do OCR. O sistema implementará validações para identificar problemas de qualidade nas imagens e solicitar nova captura quando necessário.

## 8. Métodos de Coleta

**Métodos:** 
- Captura direta via câmera do dispositivo móvel
- Processamento em lote de múltiplas imagens

## 9. Acesso aos Dados

**Acesso:** 
- Frontend: Aplicativo mobile para iOS e Android para captura e envio de imagens
- Backend: API FastAPI para recebimento, processamento e retorno dos dados estruturados
- Agente de IA: Microsserviço dedicado para processamento OCR e processamento
- Transferência: Comunicação HTTP com criptografia simétrica para proteção dos dados em trânsito

## 10. Proprietário dos Dados

**Proprietário:** Instituições de saúde pública que utilizam o sistema ScanSheet para digitalização de seus formulários e fichas.

## 11. Restrições de Privacidade e Segurança

**Restrições:** 
- Implementação de criptografia simétrica para proteção dos dados durante a transmissão entre Frontend e Backend
- Chaves de criptografia armazenadas separadamente em cada frente (Frontend e Backend)
- Para o ambiente de avaliação, serão utilizados dados mockados e falsos, sem necessidade de anonimização
- Em ambiente de produção, conformidade com LGPD para proteção de dados sensíveis de saúde. Porém, nenhum dado será armazenado, todos serão processados em memória e descartados após a geração do CSV
- O uso de dados sensíveis no Agente de IA está assegurado devido às políticas de privacidade dos modelos da OpenAI e Mistral AI, que não armazenam os dados utilizados via API, conforme seus termos de serviço: [Mistral AI Terms of Service](https://mistral.ai/terms#terms-of-service) e [OpenAI Data Privacy Policy](https://openai.com/pt-BR/policies/row-privacy-policy)

## 12. Requisitos de Integração

**Requisitos:** 
- Integração entre aplicativo mobile e backend via API REST
- Processamento de imagens utilizando OCR e modelos de IA para extração de dados
- Conversão dos dados extraídos para formato CSV estruturado
- Armazenamento dos datasets de avaliação utilizando DVC (Data Version Control) para gerenciamento eficiente de grandes volumes de dados
- Não será necessária integração com bases de dados externas, pois o sistema não utilizará banco de dados para consumo
