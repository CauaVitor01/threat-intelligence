# Windows Internals & Malware Analysis

Este repositório contém meus estudos aprofundados sobre os componentes internos do Windows e como eles são explorados em ataques modernos. O foco é entender a mecânica por trás da execução de códigos maliciosos para aprimorar técnicas de detecção e resposta.

---

## 1. Processos e Threads: Os Motores de Execução

Entender a diferença entre o contêiner (Processo) e a unidade de execução (Thread) é vital para identificar injeções.

* **Processos:** Monitoro o espaço de endereço virtual, PEB/TEB (mapas de memória) e as Handles (conexões com o sistema). Malwares abusam de processos nativos via Process Hollowing ou Masquerading.
* **Threads:** São o alvo preferido para execução oculta. Analiso a Pilha (Stack) e a Estrutura de Contexto (registradores) para identificar Thread Hijacking ou injeções remotas.

---

## 2. Gestão de Memória e Formato PE

Compreender como o código é organizado e isolado no sistema é o alicerce da análise estrutural.

* **Memória Virtual:** O isolamento entre User Mode e Kernel Mode é a primeira linha de defesa. Malwares tentam quebrar esse isolamento para obter privilégios de SYSTEM.
* **Portable Executable (PE):** O "DNA" do binário, dividido em seções cruciais:
  * `.text`: Onde reside o código executável real da aplicação.
  * `.rdata` / `.idata`: Lista de importações (APIs). Essencial para prever as capacidades e intenções do malware.
  * `.rsrc`: Seção de recursos onde payloads secundários e artefatos costumam ser escondidos.

---

## 3. Dynamic-Link Libraries (DLL)

As DLLs representam o motor modular do ecossistema Windows e são amplamente abusadas como vetor primário de persistência e evasão.

| Técnica | Descrição |
| :--- | :--- |
| **DLL Injection** | Forçar um processo legítimo a alocar e carregar código malicioso em seu espaço de memória. |
| **Side-Loading** | Explorar a ordem de busca (Search Order) do Windows para induzir um programa legítimo a carregar uma DLL falsa (maliciosa). |
| **Run-time Linking** | Resolução dinâmica de APIs usando `LoadLibrary` e `GetProcAddress` para ocultar intenções da análise estática. |

---

## 4. Anatomia de uma Injeção de Código

Documentação do fluxo de chamadas a APIs nativas do Windows utilizadas sistematicamente para manipulação de memória remota:

1. **`OpenProcess`:** Ganhar um *handle* com permissões adequadas de acesso ao processo alvo.
2. **`VirtualAllocEx`:** Alocar espaço de memória dentro do processo alvo, preferencialmente com permissões de Leitura, Gravação e Execução (RWX).
3. **`WriteProcessMemory`:** Escrever o payload ou shellcode malicioso no espaço recém-alocado.
4. **`CreateRemoteThread`:** Instruir o processo alvo a iniciar uma nova thread para executar o código injetado.

> **Insight Operacional:** A detecção sequencial dessa cadeia exata de chamadas de API é um indicador crítico e de alta fidelidade para comportamento malicioso, classificado na técnica T1055 do MITRE ATT&CK (Process Injection).

---

## 5. Ferramentas Utilizadas

* **Process Hacker 2 / Process Explorer:** Visibilidade detalhada e monitoramento em tempo real de processos, threads e handles.
* **Procmon (Process Monitor):** Telemetria profunda de eventos de sistema, registro e sistema de arquivos.
* **x64dbg / PE-bear:** Ferramentas dedicadas para análise estrutural de cabeçalhos PE e depuração de código em nível de assembly.
