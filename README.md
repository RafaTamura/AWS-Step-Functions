# Explorando Workflows Automatizados com AWS Step Functions

Este repositório documenta o estudo e a aplicação prática do **AWS Step Functions**, focando na orquestração de fluxos de trabalho *serverless* para coordenar serviços distribuídos.

Desenvolvido como parte dos estudos do **Bootcamp Santander Code Girls | DIO**.

---

## Sobre o AWS Step Functions

O AWS Step Functions é um serviço que permite modelar, visualizar e executar fluxos de trabalho (workflows) resilientes e escaláveis, utilizando a orquestração baseada em estados (State Machine). Ele substitui a necessidade de código complexo para gerenciar a lógica do fluxo, *retries*, e *timeouts*.

### Características Chave

* **Serverless:** Totalmente gerenciado, sem a necessidade de gerenciar servidores.
* **Definição Visual:** Os fluxos são definidos e visualizados como diagramas.
* **Linguagem de Definição:** Utiliza a **Amazon States Language (ASL)**, uma estrutura baseada em JSON, para descrever cada etapa do fluxo.
* **Resiliência:** Possui tratamento de erros e *retries* nativos para garantir que o fluxo complete a execução, mesmo em caso de falhas temporárias.

---

## Aplicação Prática: O Fluxo de Trabalho Implementado

Foi implementado um fluxo de trabalho simples na Step Functions, demonstrando os seguintes estados e a lógica condicional:

### 1. **Componentes Essenciais (Serviços Integrados)**
| Serviço | Função no Workflow |
| :--- | :--- |
| **Step Functions** | Orquestrador principal. Define a ordem de execução. |
| **AWS Lambda** | Funções *serverless* que executam a lógica de negócios em cada etapa. |
| **ASL (Amazon States Language)** | Linguagem JSON utilizada para declarar e visualizar o fluxo de estados. |

### 2. **Estrutura da Máquina de Estados**

O *State Machine* construído demonstrou a orquestração de uma lógica condicional usando o **Estado `Choice`**:

* **Estado 1 (`Task`):** Invoca a primeira Função Lambda (*funcao-inicio*) para receber um *input*.
* **Estado 2 (`Choice`):** Analisa o valor de um campo (`$.status`) na saída da Função 1.
    * **Se `true`:** Segue para o **Estado `Success`**.
    * **Se `false`:** Segue para o **Estado `Fail`** (simulando uma falha de validação).
* **Estados Finais (`Succeed` e `Fail`):** Encerram o fluxo com diferentes resultados, demonstrando o controle de fluxo.

---

## Principais Aprendizados e Insights

* **Orquestração vs. Coreografia:** Entendimento prático de como o Step Functions atua como um orquestrador central, sendo superior à coreografia (onde os serviços se chamam mutuamente) em fluxos complexos.
* **ASL na Prática:** A proficiência na leitura e escrita da Amazon States Language, crucial para definir transições, manipular dados (Input/Output) e configurar a lógica de repetição e falha.
* **Visualização e Debug:** A principal vantagem na prática é o diagrama visual, que torna o *debugging* de fluxos complexos significativamente mais rápido e eficiente do que analisar logs de várias funções Lambda.
* **Resiliência Integrada:** Compreensão da importância de configurar *Retries* e *Catch* states para criar fluxos de trabalho que se recuperam automaticamente de erros transitórios.
