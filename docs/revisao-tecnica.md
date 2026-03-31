# Revisão Técnica | Technical Review — SafeVoice SST

---

## 🇧🇷 Português

## Visão geral

O **SafeVoice SST** é um protótipo funcional de assistente de voz para **orientação preliminar em Segurança do Trabalho**.

Na versão atual, o fluxo foi estruturado para funcionar **sem API key da OpenAI**, utilizando:

- gravação de áudio no navegador com **Google Colab + JavaScript**
- transcrição local com **Whisper**
- consulta a uma **base local de conhecimento**
- resposta em áudio com **gTTS**

Essa decisão tornou a solução mais viável para contexto acadêmico e de portfólio, evitando dependência de cobrança da API e mantendo a proposta funcional do projeto.

---

## Fluxo atual da solução

1. O usuário grava uma pergunta em áudio  
2. O sistema captura o áudio no navegador  
3. O áudio é transcrito localmente com Whisper  
4. A transcrição é analisada por uma base local de palavras-chave  
5. O sistema gera uma resposta orientativa  
6. A resposta é convertida em áudio com gTTS  
7. O usuário ouve o retorno da aplicação  

---

## Arquitetura adotada na versão atual

A implementação foi organizada com base em uma estrutura simples orientada a objetos, separando responsabilidades entre componentes principais:

- `SpeechToTextService`
- `KnowledgeBaseService`
- `TextToSpeechService`
- `SafeVoiceController`

Essa organização permite:
- melhor legibilidade do código
- menor acoplamento entre etapas do fluxo
- base inicial para futura modularização em arquivos Python

---

## Decisões técnicas da versão 1

### 1. Remoção da dependência da API da OpenAI
A proposta inicial do laboratório utilizava integração com a API do ChatGPT.  
No entanto, para esta versão do projeto, essa dependência foi removida devido à necessidade de chave de API e cobrança associada.

Com isso, a solução passou a operar com:
- transcrição local com Whisper
- base local de respostas
- síntese de voz com gTTS

### 2. Uso de base local de conhecimento
As respostas do sistema são atualmente definidas por uma estrutura local baseada em palavras-chave, permitindo consultas iniciais para temas como:

- trabalho em altura
- EPI
- incêndio
- espaço confinado
- máquinas e equipamentos

Essa abordagem simplifica a execução da V1 e mantém coerência com o escopo preliminar do projeto.

### 3. Manutenção do caráter orientativo
Como o projeto trata conteúdos de Segurança do Trabalho, foi mantido em toda a lógica o princípio de que a resposta é:

- preliminar
- orientativa
- não substitui análise técnica em campo
- não substitui interpretação formal da legislação

---

## Ajustes realizados durante a revisão

Durante a revisão técnica, foram identificados e tratados os seguintes pontos:

- remoção de blocos antigos relacionados à API da OpenAI
- eliminação de duplicações de imports e funções
- padronização do fluxo sem custo
- manutenção de apenas uma versão funcional coerente
- alinhamento entre notebook, README e estrutura do repositório

Também foi recomendada a troca de nomes de variáveis que remetiam a ChatGPT quando a resposta já não vinha mais da API, evitando confusão semântica no código.

---

## Limitações atuais

A versão atual do **SafeVoice SST** possui as seguintes limitações:

- utiliza base local simples por palavras-chave
- não realiza busca semântica avançada
- não interpreta normas de forma jurídica ou formal
- não substitui avaliação técnica presencial
- depende de internet para o funcionamento do gTTS
- ainda não está modularizado em arquivos Python separados

---

## Próximas evoluções recomendadas

### Curto prazo
- expandir a base local com mais NRs
- melhorar o matching com sinônimos e variações de escrita
- padronizar respostas por categoria normativa

### Médio prazo
- mover a base local para um arquivo `JSON`
- separar serviços em módulos Python
- criar estrutura `src/`, `data/` e `docs/`

### Longo prazo
- desenvolver interface web
- melhorar a busca por contexto
- evoluir para um assistente mais inteligente com base documental ampliada

---

## Conclusão

A versão atual do **SafeVoice SST** representa um protótipo funcional e coerente com o objetivo do projeto.

Mesmo sem o uso da API da OpenAI, a solução mantém o núcleo da proposta:
- entrada por voz
- transcrição automática
- processamento da consulta
- retorno em áudio

Essa abordagem permitiu consolidar uma primeira versão estável, adequada para fins acadêmicos, portfólio e evolução futura com foco em arquitetura e aplicação prática em Segurança do Trabalho.

---

## Observação importante

O **SafeVoice SST** possui caráter **preliminar e orientativo**, não substituindo:

- análise técnica em campo
- validação por profissional habilitado
- interpretação formal da legislação
- tomada de decisão operacional em contexto crítico

---

## 🇺🇸 English

## Overview

**SafeVoice SST** is a functional voice assistant prototype for **preliminary Occupational Safety guidance**.

In its current version, the workflow was designed to operate **without an OpenAI API key**, using:

- browser-based audio recording with **Google Colab + JavaScript**
- local transcription with **Whisper**
- consultation of a **local knowledge base**
- spoken response generation with **gTTS**

This decision made the solution more viable for academic and portfolio purposes, avoiding API billing dependency while preserving the project’s functional proposal.

---

## Current solution flow

1. The user records a spoken question  
2. The system captures the audio in the browser  
3. The audio is transcribed locally with Whisper  
4. The transcription is analyzed through a local keyword-based knowledge base  
5. The system generates a guidance response  
6. The response is converted into audio with gTTS  
7. The user listens to the application output  

---

## Architecture adopted in the current version

The implementation was organized using a simple object-oriented structure, separating responsibilities into core components:

- `SpeechToTextService`
- `KnowledgeBaseService`
- `TextToSpeechService`
- `SafeVoiceController`

This organization provides:
- improved code readability
- lower coupling between workflow stages
- an initial foundation for future modularization into Python files

---

## Version 1 technical decisions

### 1. Removal of OpenAI API dependency
The initial lab proposal used integration with the ChatGPT API.  
However, for this version of the project, that dependency was removed due to the need for an API key and associated billing.

As a result, the solution now operates with:
- local transcription using Whisper
- a local response base
- speech synthesis with gTTS

### 2. Use of a local knowledge base
System responses are currently defined through a local keyword-based structure, enabling initial queries for topics such as:

- work at height
- PPE
- fire prevention
- confined space
- machinery and equipment

This approach simplifies V1 execution and keeps the solution aligned with the project’s preliminary scope.

### 3. Preservation of a guidance-oriented character
Since the project handles Occupational Safety content, the logic consistently preserves the principle that responses are:

- preliminary
- guidance-oriented
- not a substitute for on-site technical assessment
- not a substitute for formal regulatory interpretation

---

## Adjustments made during the review

During the technical review, the following points were identified and addressed:

- removal of outdated blocks related to the OpenAI API
- elimination of duplicated imports and functions
- standardization of the no-cost workflow
- maintenance of a single coherent functional version
- alignment between notebook, README, and repository structure

It was also recommended to rename variables that referenced ChatGPT when the response was no longer generated by the API, avoiding semantic confusion in the code.

---

## Current limitations

The current version of **SafeVoice SST** has the following limitations:

- uses a simple keyword-based local knowledge base
- does not perform advanced semantic search
- does not interpret standards in a legal or formal sense
- does not replace in-person technical assessment
- depends on internet access for gTTS to work
- is not yet modularized into separate Python files

---

## Recommended next evolutions

### Short term
- expand the local knowledge base with more Regulatory Standards
- improve matching with synonyms and writing variations
- standardize responses by regulatory category

### Medium term
- move the local knowledge base to a `JSON` file
- separate services into Python modules
- create a `src/`, `data/`, and `docs/` structure

### Long term
- develop a web interface
- improve context-based search
- evolve into a more intelligent assistant with an expanded document base

---

## Conclusion

The current version of **SafeVoice SST** represents a functional prototype aligned with the project objective.

Even without using the OpenAI API, the solution preserves the core idea:
- voice input
- automatic transcription
- query processing
- spoken response

This approach made it possible to consolidate a stable first version, suitable for academic purposes, portfolio presentation, and future evolution focused on architecture and practical application in Occupational Safety.

---

## Important note

**SafeVoice SST** has a **preliminary and guidance-oriented** purpose and does not replace:

- on-site technical assessment
- validation by a qualified professional
- formal legal interpretation
- operational decision-making in critical contexts
