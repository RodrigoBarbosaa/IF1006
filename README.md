# 📊 ScanSheet: Transforme Imagens em Dados de Saúde Pública

ScanSheet é um aplicativo projetado para **revolucionar a digitalização de dados na área da saúde pública**, convertendo imagens de fichas em planilhas estruturadas de forma eficiente e precisa.


## ✨ Visão Geral do Projeto

No setor de saúde pública, a digitalização manual de dados é um processo demorado e propenso a erros. O ScanSheet surge para automatizar essa tarefa crítica, permitindo que profissionais capturem ou carreguem fotos de documentos, que são então processadas por inteligência artificial para extrair informações relevantes e apresentá-las em um formato de planilha. Isso resulta em maior eficiência, redução de erros e acesso mais rápido a dados vitais.

## 🎯 Objetivos e Funcionalidades Principais

* **Eficiência Aprimorada:** Reduzir drasticamente o tempo gasto na digitalização manual de dados.
* **Precisão de Dados:** Utilizar IA para garantir a extração precisa de informações.
* **Acessibilidade:** Oferecer uma solução amigável e de fácil uso.
* **Conversão Inteligente:** Converter imagens (fotos ou uploads) em planilhas (xlsx ou csv).

## ⚙️ Como Funciona?

1.  O usuário captura uma foto ou faz upload de uma imagem via **aplicativo mobile (iOS/Android)**.
2.  A imagem é enviada para o **backend** do ScanSheer via API.
3.  No backend, um **agente de IA** é ativado para realizar o **OCR (Reconhecimento Óptico de Caracteres)**.
4.  Com base no OCR, os dados são processados e uma **tabela é construída** usando Python.
5.  As informações são então devolvidas ao aplicativo prontas para uso.

## 📱 Vídeos demonstração
1. [iOS](https://drive.google.com/file/d/1_SIaqRTP-p4EHnx05HS7RPCziw1yMKWD/view)
2. [Android](https://drive.google.com/file/d/1IR1efO0H506qiNNA4sP-77YGRGOXj9uc/view)

## 💻 Tecnologias

O ScanSheet é composto por três componentes principais: o **aplicativo móvel**, o **backend** e o **agente de IA**.
 O link leva para o repositório de cada um.

* **Mobile Apps:**

    * **[iOS](https://github.com/RodrigoBarbosaa/ScanSheet-iOS):** Swift e SwiftUI

    * **[Android](https://github.com/RodrigoBarbosaa/ScanSheet-Android):** Kotlin e Compose

* **[Backend](https://github.com/mrbsa/ScanSheet-API):** Python

* **[Agente](https://github.com/guilopesrbc/ScanSheet-agent):** Langchain para orquestração e ChatGPT como modelo

## 👨‍💻 Desenvolvedores:
* **Guilherme Lopes**
* **Mariana Amorim**
* **Rodrigo Barbosa**
