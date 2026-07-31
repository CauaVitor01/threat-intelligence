Deep Dive: Portable Executable (PE) Structure

Neste módulo, documentei a análise técnica de binários Windows, explorando desde os cabeçalhos legados até as técnicas de ocultação utilizadas por malwares modernos.

Estrutura do Cabeçalho PE

A análise foi realizada utilizando wxHexEditor para inspeção de bytes brutos e pe-tree para visualização estrutural.

Componentes Críticos Identificados:

IMAGE_DOS_HEADER: Contém a assinatura MZ (4D 5A) e o ponteiro e_lfanew (0x3C), essencial para localizar o início do cabeçalho NT.

DOS STUB: Trecho de código legado. Usei a análise de Entropia aqui para verificar se há dados escondidos em seções que deveriam ser apenas texto informativo.

IMAGE_NT_HEADERS:

Signature: Assinatura PE (50 45).

File Header: Define a arquitetura (x86/x64) e o número de seções.

Optional Header: Onde reside o AddressOfEntryPoint (AEP) — o ponto de partida da execução — e o ImageBase.

Identificação de Packers e Ofuscação

Uma parte vital do estudo foi aprender a identificar quando um executável está "empacotado" para evadir análise estática.

Sinais de Alerta (Red Flags):

IndicadorCaracterística em Arquivo PackadoNomes de SeçõesNomes incomuns (UPX0, etc) ou seções sem nome.EntropiaValores próximos a 8.0 (indicando compressão/criptografia).PermissõesSeções com RWE (Read, Write, Execute) simultâneos.TamanhoVirtualSize muito maior que o RawData (expansão em memória).ImportaçõesPoucas APIs, geralmente limitadas a LoadLibrary e GetProcAddress.🛠️ Ferramentas Utilizadas

wxHexEditor: Manipulação de arquivos em nível de byte.

pe-tree / pecheck: Visualização de structs e cálculo de hashes/entropia.

Documentação MSDN: Referência técnica para mapeamento de structs.

Conclusão

O domínio do formato PE permite realizar uma triagem rápida de arquivos suspeitos. Ao entender onde o código começa e como ele solicita funções ao sistema (IAT), é possível prever o comportamento de um malware antes mesmo de permitir que ele seja executado em uma sandbox.
