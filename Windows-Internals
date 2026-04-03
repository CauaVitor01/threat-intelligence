Windows Internals & Malware Analysis

Este repositório contém meus estudos aprofundados sobre os componentes internos do Windows e como eles são explorados em ataques modernos. O foco é entender a mecânica por trás da execução de códigos maliciosos para aprimorar técnicas de detecção e resposta.

 1. Processos e Threads: Os Motores de Execução

Entender a diferença entre o contêiner (Processo) e a unidade de execução (Thread) é vital para identificar injeções.

Processos: Monitoro o espaço de endereço virtual, PEB/TEB (mapas de memória) e as Handles (conexões com o sistema). Malwares abusam de processos nativos via Hollowing ou Masquerading.

Threads: São o alvo preferido para execução oculta. Analiso a Pilha (Stack) e a Estrutura de Contexto (registradores) para identificar Thread Hijacking ou injeções remotas.

 2. Gestão de Memória e Formato PE

Como o código é organizado e isolado no sistema.

Memória Virtual: O isolamento entre User Mode e Kernel Mode é a primeira linha de defesa. Malwares tentam quebrar esse isolamento para obter privilégios de SYSTEM.

Portable Executable (PE): O "DNA" do binário.

.text: Código executável.

.rdata/.idata: Lista de importações (APIs). Essencial para prever as capacidades do malware.

.rsrc: Onde payloads costumam ser escondidos.

🛠️ 3. Dynamic-Link Libraries (DLL)

As DLLs são o motor modular do Windows e o principal vetor de persistência e evasão.

TécnicaDescriçãoDLL InjectionForçar um processo limpo a carregar código malicioso.Side-LoadingExplorar a ordem de busca do Windows para carregar uma DLL falsa.Run-time LinkingUso de LoadLibrary e GetProcAddress para dificultar a análise estática.💉 4. Anatomia de uma Injeção de Código

Documentação do fluxo de APIs nativas utilizadas para manipulação de memória remota:

OpenProcess: Ganhar acesso ao alvo.

VirtualAllocEx: Alocar espaço com permissões RWX.

WriteProcessMemory: Escrever o shellcode.

CreateRemoteThread: Executar o código dentro do contexto do alvo.

Insight: A presença dessa sequência de chamadas é um indicador crítico de comportamento malicioso (T1055).

Ferramentas Utilizadas

Process Hacker 2 / Process Explorer: Visibilidade de threads e handles.

Procmon: Telemetria de eventos do sistema em tempo real.

x64dbg / Pe Bear: Análise de cabeçalhos PE e depuração de código.
