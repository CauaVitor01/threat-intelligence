Fundamentos de Linguagem Assembly x86

Este documento registra meu progresso no entendimento da linguagem Assembly, focada na engenharia reversa de binários compilados onde o código-fonte original não está disponível.

Por que Assembly?

Na análise de malware, o Assembly é a fonte de verdade mais confiável. Como nomes de variáveis e funções desaparecem na compilação, entender os Opcodes e Operandos é o que permite identificar o que o binário realmente executa "por baixo do pano".

Instruções e Operações de CPU

1. Movimentação e Endereçamento

MOV: Copia dados entre registradores e memória.

LEA (Load Effective Address): Calcula endereços rapidamente. Frequentemente usada por compiladores para aritmética otimizada.

NOP (No Operation): Usada em malwares para criar NOP Sleds, garantindo a execução estável de shellcodes.

2. Lógica e Aritmética

XOR: Além de operações lógicas, é a forma padrão de zerar registradores (xor eax, eax) e a base de algoritmos simples de ofuscação.

SHL / SHR & ROL / ROR: Deslocamento e rotação de bits, essenciais para entender rotinas de criptografia e manipulação de rede.

Controle de Fluxo e Decisão

O malware toma decisões manipulando o EFLAGS Register.

InstruçãoCondiçãoUso comum em MalwareTEST / CMPDefine FlagsVerifica se um debugger está presente ou se um arquivo existe.JZ / JESalta se Zero/IgualDesvia o fluxo se uma verificação de segurança for bem-sucedida.JNZ / JNESalta se não ZeroExecuta o payload caso uma condição de erro não seja encontrada.📥 Gestão da Pilha (Stack)

A pilha é uma estrutura LIFO (Last-In, First-Out) controlada pelo registrador ESP.

PUSH / POP: Adiciona ou remove dados da pilha.

PUSHAD / POPAD: Salva e restaura todos os registradores. Encontrá-los geralmente indica a transição entre um packer e o código original do malware (OEP).

CALL / RET: Gerencia a execução de funções, salvando o endereço de retorno para manter o fluxo do programa.

Conclusão Técnica

Este estudo consolidou cinco pilares críticos:

Tradução de Opcodes para comandos legíveis.

Mecânica de Instruções Gerais (Movimentação e Bits).

Lógica Aritmética aplicada a criptografia.

Ramificação Condicional para análise de lógica de infecção.

Manipulação de Memória via Pilha para identificação de shellcode.

📂 Documento Completo: X86_Assembly_Fundamentals.pdf
