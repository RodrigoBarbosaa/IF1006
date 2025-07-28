# Canvas de Ideação de Soluções - ScanSheet

## 1. Problema a Ser Resolvido


**Problema:** Digitalização manual demorada e propensa a erros de dados na área da saúde pública. Profissionais de saúde gastam muito tempo digitando manualmente informações de fichas físicas em sistemas digitais, resultando em processos ineficientes, alto risco de erros de transcrição e atrasos no acesso a dados vitais para tomada de decisões.


## 2. Ideias de Solução (Brainstorming)

**Ideia A:** Conversão de imagens em planilhas estruturadas via OCR e IA
- Captura de fotos de documentos via app mobile
- Processamento com OCR e IA para extração de dados
- Conversão automática para formatos xlsx/csv

**Ideia B:** Automação das fichas com integração direta com banco de dados
- Sistema completo de digitalização com conexão direta a bancos de dados hospitalares
- Validação automática de dados em tempo real
- Sincronização instantânea com sistemas existentes

**Ideia C:** Ideia A, com possibilidade de input de dados faltantes
- Interface para correção manual de dados não reconhecidos
- Sistema de validação humana para dados críticos
- Fluxo de aprovação para dados sensíveis


## 3. Matriz de Priorização (Impacto vs. Esforço)

**Impacto Potencial:** Quão significativamente esta ideia resolve o problema e contribui para os objetivos?
**Esforço/Complexidade:** Quão difícil, demorado ou custoso é implementar um protótipo desta ideia?

| Impacto / Esforço | Baixo Esforço | Alto Esforço |
|-------------------|---------------|--------------|
| **Alto Impacto** | **(Foco Principal / Vitórias Rápidas)**<br><br>**Ideia A:** Conversão de imagens em planilhas estruturadas via OCR e IA<br><br>• Alto impacto: Resolve diretamente o problema de digitalização manual<br>• Baixo esforço: Tecnologias OCR e IA já maduras<br>• MVP viável com recursos disponíveis | **(Projetos Maiores / Estratégicos)**<br><br>**Ideia B:** Automação das fichas com integração direta com banco de dados<br><br>• Alto impacto: Solução completa e integrada<br>• Alto esforço: Requer desenvolvimento de APIs, integrações complexas e validações de segurança |
| **Baixo Impacto** | **(Tarefas de Preenchimento / Opcionais)**<br><br>**Ideia C:** Possibilitar input de dados faltantes<br><br>• Baixo impacto: Funcionalidade complementar<br>• Baixo esforço: Interface simples de correção | **(Armadilhas / Descartar)**<br><br>Nenhuma ideia posicionada aqui |


## 4. Solução Priorizada para Prototipagem

**Solução Escolhida:** Conversão de imagens em planilhas estruturadas via OCR e IA

**Justificativa:**
- **Alto Impacto:** Resolve diretamente o problema principal de digitalização manual, reduzindo drasticamente o tempo de processamento e erros de transcrição
- **Baixo Esforço:** Utiliza tecnologias já maduras (OCR, IA) e pode ser desenvolvida com recursos disponíveis
- **MVP Viável:** Permite demonstração rápida do conceito e validação com usuários reais
- **Escalabilidade:** Base sólida para futuras funcionalidades mais complexas

**Componentes da Solução:**
- Aplicativo mobile para captura de imagens (iOS/Android)
- Backend em Python para processamento
- Agente de IA com Langchain e ChatGPT para OCR e extração de dados
- Conversão automática para formatos xlsx/csv
- Interface web para visualização e download dos resultados 