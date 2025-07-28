# Canvas de Design de Prompts - ScanSheet Agent

## Registro de Design de Prompt: EXTRACAO-FICHA-CADASTRAL-01

### 1. Metadados
**Propósito:** Extrair informações estruturadas de fichas cadastrais (imagens e texto markdown) e convertê-las em formato JSON padronizado para geração de CSV.

**Modelo(s) Alvo:** OpenAI GPT-4 (com capacidade de processamento de imagens)

**Versão do Registro:** 1.0

### 2. Estrutura do Prompt

**Contexto de Entrada Necessário:**
- Texto markdown extraído via OCR da ficha cadastral
- Imagem base64 da ficha cadastral
- Tipo de documento (para MVP: ficha_cadastro_individual ou outros)
- Instruções específicas do tipo de documento

**Template do Prompt (com variáveis):**
```
Você é um sistema especialista na geração de estrutura CSV em formato JSON a partir de textos markdowns e imagens com conteúdos de fichas cadastrais.

O usuário fornecerá texto markdown e uma imagem que descreve uma ficha de cadastro ou de atendimento, essa ficha terá uma estrutura de campos e respostas, sejam respostas objetivas ou escritas.
A tarefa é analisar o texto e estrutura do markdown e gerar um JSON que contenha as informações relevantes para gerar um CSV.
Você deve seguir as seguintes instruções para extrair corretamente as informações:

<general_system_instructions>
1. Analise a estrutura do texto markdown e da imagem em conjunto, utilize sua análise dos dois documentos para preenchimento.
2. Identifique a estrutura dos campos e respostas.
3. Preste atenção em campos de multipla escolha, identifique corretamente qual campo está marcado, pode ser ser uma alternativa com a letra "X" ou assinalado com um círculo. Entenda corretamente qual campo foi selecionado.
4. Preste atenção para identificar qual campo corresponde uma alternativa no campo de seleção.
5. Ignore campos agregadores, campos que os valores são um bloco de outros campos e nao possui um valor diretamente.
6. Para cada campo gere um par chave-valor no JSON de resposta.
7. Certifique-se de que o JSON esteja formatado corretamente, com todas as chaves e valores necessários.
8. O JSON de resposta deve conter uma chave 'title' com o título do documento enviado, que será fornecido pelo usuário, e uma chave 'content' que conterá os campos e valores extraídos, o formato e instruções do valor da chave 'content será especificada em specific_fields_instructions.
9. Me retorne somente a string json conforme o <response_json_example>, não faça nenhuma consideração, nem escreva algum texto, somente a string do JSON gerado e seguindo as instruções passadas.
10. Atenção: Não retorne com chaves duplas conforme o exemplo, o exemplo só foi utilizado para evitar conflitos com input_variables, retorne com chaves simples, igual um JSON convencional.
11. Atenção: Você deve retorne o JSON de resposta com apas duplas, sem aspas simples. Para validação melhor
12. Não invente valores, apenas extraia os valores conforme estão na imagem, não escreva valores caso não identifique um campo, ou não tenha certeza do valor, nesse caso o valor será null.
</general_system_instructions>

<general_fields_instructions>
1. Caso o valor seja um campo de seleção com valores como 'Sim' ou 'Não', começará com 'fl_*', e serão considerados booleanos transforme o valor em uma string true ou false, <example> fl_ex1: True, fl_ex2: False</example>.
2. Campos de seleção com múltiplas opções, começarão com 'ls_*', em seguida o valor é conforme será definido conforme as instruções do modelo especificado na tag <specific_fields_instructions>
3. Transforme o valor dos campos de seleção com múltiplas opções (com inicio 'ls_*') em uma lista de strings, <example> ls_example: ['opcao1', 'opcao2'] </example>.
4. Os campos de data, começarão com 'dt_*', em seguida o valor desse campo será descrito conforme as instruções do modelo especificado na tag <specific_fields_instructions>
5. Transforme o valor de campos de datas em uma string no formato 'YYYY-MM-DD', <example> '2023-10-01' </example>.
6. Os demais campos que não começarem com 'fl_*', 'ls_*', ou 'dt_*', mesmo que seja campos com opções (sendo esses de uma escolha) serão campos de texto livre, o valor desse campo será descrito conforme as instruções do modelo especificado na tag <specific_fields_instructions>
7. Caso o campo não tenha valor, ou seja, esteja vazio, o valor desse campo será null, <example> 'campo_vazio': null </example>.
</general_fields_instructions>

O valor do campo 'title' deve ser esse: '{{title_instructions}}'

O valor do campo 'content' deve conter os seguintes campos, e devem satisfazer as instruções abaixo:
<specific_fields_instructions>
{{document_instructions}}
</specific_fields_instructions>

<response_json_example>
{{
    'title': 'ficha_teste',
    'content': {{
        'cns_cpf_cidadao': '12345678901',
        'dt_nasc': '2023-10-01',
        'nome': 'João da Silva',
        'raca_cor': 'Branca',
        'ls_deficiencia': ['auditiva', 'visual'],
        'fl_informar_orientacao_sexual': False,
    }}
}}
</response_json_example>

Conteúdo markdown:
{{markdown_content}}

Imagem:
{{image_content}}
```

### 3. Estrutura da Resposta

**Intenção da Resposta:** JSON estruturado contendo título do documento e conteúdo extraído com campos padronizados conforme o tipo de documento.

**Exemplo de Saída Ideal:**
```json
{
    "title": "ficha_cadastro_individual",
    "content": {
        "cns_cpf_cidadao": "12345678901",
        "dt_nasc": "1990-05-15",
        "nm_completo": "João da Silva Santos",
        "sexo": "M",
        "raca_cor": "Branca",
        "fl_deficiencia": true,
        "ls_deficiencia": ["auditiva", "visual"],
        "fl_informar_orientacao_sexual": false,
        "dt_preenchimento": "2024-01-20"
    }
}
```

### 4. Teste e Qualidade

**Critérios de Aceite / Métricas de Qualidade:**
1. O JSON DEVE ser válido e bem formatado
2. DEVE conter apenas as chaves 'title' e 'content'
3. Campos booleanos (fl_*) DEVE ter valores true/false como string
4. Campos de lista (ls_*) DEVE ser arrays de strings
5. Campos de data (dt_*) DEVE estar no formato YYYY-MM-DD
6. NÃO DEVE inventar valores - campos não identificados devem ser null
7. DEVE usar aspas duplas em todo o JSON
8. NÃO DEVE incluir comentários ou texto adicional além do JSON

**Parâmetros Recomendados:**
- Modelo: GPT 4.1 (Modelo mais avançado atualmente, com melhor poder de vision)

### 5. Notas Adicionais

**Instruções:**
- O sistema utiliza OCR do Mistral AI para extrair texto markdown das imagens
- Diferentes tipos de documento têm instruções específicas (ficha_cadastro_individual vs outros)
- Campos vazios ou não identificados devem retornar null
- O sistema valida a resposta usando Pydantic models
- Atenção especial para campos de múltipla escolha marcados com "X" ou círculos
- Campos agregadores devem ser ignorados conforme especificado

---

## Registro de Design de Prompt: FICHA-CADASTRO-INDIVIDUAL-01

### 1. Metadados
**Propósito:** Extrair informações específicas de fichas de cadastro individual do SUS, seguindo estrutura padronizada com campos específicos.

**Modelo(s) Alvo:** OpenAI GPT-4 (com capacidade de processamento de imagens)

**Versão do Registro:** 1.0

### 2. Estrutura do Prompt

**Contexto de Entrada Necessário:**
- Texto markdown da ficha de cadastro individual
- Imagem da ficha de cadastro individual
- Instruções específicas dos campos da ficha

**Template do Prompt (com variáveis):**
```
[SYSTEM TEMPLATE + INSTRUÇÕES ESPECÍFICAS]

Essas são as instruções para a geração do valor do campo 'content' para JSON de resposta a partir da ficha de cadastro individual:

<instructions>
- <campo>digitado_por</campo>
  - <nome_do_campo>"DIGITADO POR"</nome_do_campo>
  - <descricao_do_campo>"Nome ou identificação de quem realizou a digitação dos dados da ficha."</descricao_do_campo>
- <campo>conferido_por</campo>
  - <nome_do_campo>"CONFERIDO POR"</nome_do_campo>
  - <descricao_do_campo>"Nome ou identificação de quem realizou a conferência dos dados da ficha."</descricao_do_campo>
- <campo>num_folha</campo>
  - <nome_do_campo>"FOLHA Nº"</nome_do_campo>
  - <descricao_do_campo>"Número que identifica a folha ou registro da ficha."</descricao_do_campo>
- <campo>dt_preenchimento</campo>
  - <nome_do_campo>"DATA"</nome_do_campo>
  - <descricao_do_campo>"Data em que a ficha foi preenchida (formato YYYY-MM-DD)."</descricao_do_campo>
- <campo>cns_prof</campo>
  - <nome_do_campo>"CNS DO PROFISSIONAL"</nome_do_campo>
  - <descricao_do_campo>"Número do CNS do profissional responsável."</descricao_do_campo>
- <campo>cbo</campo>
  - <nome_do_campo>"CBO"</nome_do_campo>
  - <descricao_do_campo>"Número do CBO."</descricao_do_campo>
- <campo>cnes</campo>
  - <nome_do_campo>"CNES"</nome_do_campo>
  - <descricao_do_campo>"Código do estabelecimento de saúde onde o atendimento foi realizado."</descricao_do_campo>
- <campo>ine</campo>
  - <nome_do_campo>"INE"</nome_do_campo>
  - <descricao_do_campo>"Indicador de registro no Instituto Nacional de Estudos ou similar."</descricao_do_campo>
- <campo>dt_ficha</campo>
  - <nome_do_campo>"DATA"</nome_do_campo>
  - <descricao_do_campo>"Data em que a ficha foi preenchida (formato YYYY-MM-DD)."</descricao_do_campo>
- <campo>cns_cpf_cidadao</campo>
  - <nome_do_campo>"CNS OU CPF DO CIDADAO*"</nome_do_campo>
  - <descricao_do_campo>"Número do CNS ou CPF do cidadão."</descricao_do_campo>
- <campo>cns_cpf_respon_familiar</campo>
  - <nome_do_campo>"CNS OU CPF DO RESPONSÁVEL FAMILIAR"</nome_do_campo>
  - <descricao_do_campo>"Número do documento (CNS/CPF) do responsável familiar."</descricao_do_campo>
- <campo>fl_cidadao_respon_familiar</campo>
  - <nome_do_campo>"CIDADÃO É O RESPONSÁVEL FAMILIAR?"</nome_do_campo>
  - <opcoes>
    - ("Sim (true)")
    - ("Não (false)")
  - </opcoes>
- <campo>microarea</campo>
  - <nome_do_campo>"MICROÁREA"</nome_do_campo>
  - <descricao_do_campo>"Identificação da microárea de atuação ou residência."</descricao_do_campo>
- <campo>nm_completo</campo>
  - <nome_do_campo>"NOME COMPLETO*"</nome_do_campo>
  - <descricao_do_campo>"Nome completo do cidadão."</descricao_do_campo>
- <campo>nm_social</campo>
  - <nome_do_campo>"NOME SOCIAL"</nome_do_campo>
  - <descricao_do_campo>"Nome social, se utilizado."</descricao_do_campo>
- <campo>dt_nasc</campo>
  - <nome_do_campo>"DATA DE NASCIMENTO*"</nome_do_campo>
  - <descricao_do_campo>"Data de nascimento do cidadão (formato YYYY-MM-DD)."</descricao_do_campo>
- <campo>sexo</campo>
  - <nome_do_campo>"SEXO"</nome_do_campo>
  - <descricao_do_campo>"Indicador de sexo, valores informados como M ou F."</descricao_do_campo>
- <campo>raca_cor</campo>
  - <nome_do_campo>"RAÇA/COR"</nome_do_campo>
  - <opcoes>
    - ("Branca")
    - ("Parda")
    - ("Preta")
    - ("Amarela")
    - ("Indígena")
  - </opcoes>
[... continua com todos os campos específicos da ficha de cadastro individual ...]
</instructions>
```

### 3. Estrutura da Resposta

**Intenção da Resposta:** JSON com campos específicos da ficha de cadastro individual, incluindo dados pessoais, médicos e demográficos.

**Exemplo de Saída Ideal:**
```json
{
    "title": "ficha_cadastro_individual",
    "content": {
        "digitado_por": "Maria Silva",
        "cns_cpf_cidadao": "12345678901",
        "nm_completo": "João da Silva Santos",
        "dt_nasc": "1990-05-15",
        "sexo": "M",
        "raca_cor": "Branca",
        "nm_completo_mae": "Maria Santos",
        "fl_deficiencia": true,
        "ls_deficiencia": ["auditiva"],
        "fl_gestante": false,
        "fl_hipertensao_arterial": true,
        "fl_diabetes": false
    }
}
```

### 4. Teste e Qualidade

**Critérios de Aceite / Métricas de Qualidade:**
1. DEVE extrair todos os campos obrigatórios da ficha de cadastro individual
2. Campos de data DEVE estar no formato YYYY-MM-DD
3. Campos booleanos DEVE ser true/false como string
4. Listas de deficiências/doenças DEVE ser arrays de strings
5. NÃO DEVE inventar valores para campos não preenchidos
6. DEVE respeitar as opções válidas para campos de seleção

**Parâmetros Recomendados:**
- Modelo: GPT 4.1 (Modelo mais avançado atualmente, com melhor poder de vision)

### 5. Notas Adicionais

**Instruções:**
- Campos específicos da ficha de cadastro individual do SUS
- Validação rigorosa de formatos de data e campos obrigatórios
- Tratamento especial para campos de saúde (doenças, deficiências, gestação)
- Campos de identificação pessoal devem ser extraídos com precisão

---

## Registro de Design de Prompt: OUTROS-DOCUMENTOS-01

### 1. Metadados
**Propósito:** Processar documentos genéricos que não possuem estrutura específica definida, extraindo campos dinamicamente.

**Modelo(s) Alvo:** OpenAI GPT-4 (com capacidade de processamento de imagens)

**Versão do Registro:** 1.0

### 2. Estrutura do Prompt

**Contexto de Entrada Necessário:**
- Texto markdown do documento genérico
- Imagem do documento genérico
- Instruções para processamento dinâmico

**Template do Prompt (com variáveis):**
```
[SYSTEM TEMPLATE + INSTRUÇÕES DINÂMICAS]

Essas são as instruções para a geração do valor do campo 'content' para JSON de resposta a partir de outros documentos, documentos esses que não possuem uma estrutura no nosso schema de modelos, mas que ainda assim devem ser processados para gerar um JSON válido:

<instructions>
1. Extraia o nome completo do campo, exemplo: "CNS OU CPF DO CIDADAO".
2. Transforme o nome em uma string lower case utilizando o nome completo do campo, exemplo: "cns_ou_cpf_do_cidadao".
3. Não utilize caracter especiais, espaços ou acentos no nome do campo, remova interrogação se houver, caso tenha alguma barra, parenteses e/ou outro tipo de caracter que não seja letras substitua-os por "_", exemplo: campo "TEM DOENÇA RESPIRATÓRIA/NO PULMÃO?" = "tem_doenca_respiratorio_no_pulmao".
4. Extraia o valor do arquivo, se esse valor for um valor escrito, nesse caso, campo "cns_ou_cpf_do_cidadao" terá o valor "12345678901" por exemplo.
5. Os campos que forem referentes a seleção com apenas duas opções, o prefixo desse campo será substituido por "fl_", por exemplo, o campo 'tem_doenca_respiratoria' que conforme a regra seria 'tem_doenca_respiratoria', será 'fl_tem_doenca_respiratoria'.
6. Os campos que forem referentes a seleção com multiplas opções, o prefixo desse campo será substituido por  "ls_", por exemplo, o campo 'deficiência' que conforme a regra seria 'deficiencia', será 'ls_deficiencia'.
7. Caso esse campo de multipla opção tenha relação com alguma campo de seleção com apenas duas opções, o nome dessa campo será igual ao campo de seleção com apenas duas opções, somente substituindo o prefixo 'fl_*' por 'ls_*'.
8. Se o valor for um campo de data, transforme o valor em uma string no formato "YYYY-MM-DD", por exemplo, "2023-10-01".
9. Os campos que forem referentes a data, o prefixo desse campo será substituido por "dt_", por exemplo, o campo 'data de nascimento' que conforme a regra seria 'data_de_nascimento', será 'dt_de_nascimento'.
</instructions>
```

### 3. Estrutura da Resposta

**Intenção da Resposta:** JSON com campos extraídos dinamicamente do documento, seguindo convenções de nomenclatura.

**Exemplo de Saída Ideal:**
```json
{
    "title": "outros",
    "content": {
        "nome_completo": "João Silva",
        "dt_nascimento": "1990-05-15",
        "fl_tem_doenca_respiratoria": true,
        "ls_deficiencias": ["auditiva", "visual"],
        "telefone": "11987654321",
        "endereco": "Rua das Flores, 123"
    }
}
```

### 4. Teste e Qualidade

**Critérios de Aceite / Métricas de Qualidade:**
1. DEVE extrair campos dinamicamente baseado no conteúdo do documento
2. Nomes de campos DEVE seguir convenções (lowercase, underscores)
3. Prefixos DEVE ser aplicados corretamente (fl_, ls_, dt_)
4. Campos de data DEVE estar no formato YYYY-MM-DD
5. Campos booleanos DEVE ser true/false como string
6. Listas DEVE ser arrays de strings

**Parâmetros Recomendados:**
- Modelo: GPT 4.1 (Modelo mais avançado atualmente, com melhor poder de vision)

### 5. Notas Adicionais

**Instruções:**
- Processamento dinâmico para documentos não estruturados
- Conversão automática de nomes de campos para formato padronizado
- Aplicação inteligente de prefixos baseada no tipo de campo
- Flexibilidade para diferentes tipos de formulários não catalogados

---