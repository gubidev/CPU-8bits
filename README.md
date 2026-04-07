# CPU 8-bits

Este repositório contém o projeto de uma Unidade Central de Processamento (CPU) de 8 bits desenvolvida do zero no simulador **Digital**.

O projeto implementa uma arquitetura simplificada baseada em Acumulador, contando com um Caminho de Dados (Datapath) customizado e uma Unidade de Controle com máquina de estados (Ring Counter).

## Vídeo de Apresentação

[![Apresentação da CPU](https://drive.google.com/file/d/1hf8uBHTbh2HQ-rNtZQ56JxIM_GCiwEaK/view?usp=sharing)
[![Repositorio ALU](https://github.com/gubidev/ALU-8bits)
## Arquitetura do Projeto

O processador foi dividido em dois blocos principais para gerenciar os ciclos de *Fetch* (Busca) e *Execute* (Execução):

### 1. Datapath (Caminho de Dados)
O coração matemático da CPU. Foca na execução de cálculos em hard-logic.
* **ALU (Unidade Lógica e Aritmética):** Construída puramente com portas lógicas (sem blocos aritméticos prontos). Suporta:
  * Soma e Subtração (Complemento de 2).
  * Shifts Lógicos (Esquerda e Direita).
  * **Multiplicação:** Implementada via matriz de portas AND e árvore de somadores de 16 bits.
  * **Divisão:** Implementada através do algoritmo de *Restoring Division*.
* **Registrador Acumulador (QA):** Armazena o resultado principal de 8 bits (ou os 8 LSB / Resto).
* **Registrador MQ:** Registrador auxiliar para cálculos complexos, armazenando os 8 MSB na multiplicação ou o Quociente na divisão.

### 2. Unidade de Controle
O "cérebro" sequencial que dita o ritmo da máquina. Utiliza a estratégia de **endereçamento em pilha** (instruções e operandos sequenciais na memória).
* **Contador em Anel (Ring Counter):** Máquina de estados dividida em 3 fases sincronizadas por Clock:
  * `T0` (Busca da Instrução): Lê a ROM e salva o Opcode no registrador de controle.
  * `T1` (Busca do Dado): O PC avança e a memória disponibiliza o operando no barramento `D`.
  * `T2` (Execução): A ALU finaliza a operação e os registradores QA/MQ recebem o sinal de `Enable` para salvar os resultados. O PC avança novamente para a próxima instrução.
 
### 3. OP CODES:
* 0 - **Soma** (Para usar a **Subtracao** ativar o botao da subtracao antes de clocar a soma, nao ative no comeco so depois do primeiro numero aparecer)
* 1 - **XOR**
* 2 - **NAND**
* 3 - **Shift Direita**
* 4 - **Shift Esquerda**
* 5 - **Multiplicacao**
* 6 - **Divisao** 

## Como Simular

1. Faça o download do software simulador [Digital](https://github.com/hneemann/Digital).
2. Baixe todos os .dig e abra no **Digital** o CPU.dig
