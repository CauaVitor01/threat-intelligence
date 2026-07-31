# Relatório de Investigação: Análise de Documentos Maliciosos (MalDocs)

Este relatório detalha a análise técnica de artefatos maliciosos em formatos PDF, Office (.doc) e OneNote (.one), simulando o fluxo de trabalho de um Analista de SOC N2.

## 1. Análise de PDF Malicioso (CVE-2021-26084 Context)
**Ferramentas:** `pdfid.py`, `pdf-parser.py`, `peepdf`

- **Descoberta:** Identificação de objetos `/OpenAction` e `/JavaScript` para execução automática de código.
- **Extração:** Descompressão de streams e identificação de flag de controle.
- **IOCs:** Flag identificada: `THM{Luckily_This_Isn't_Harmful}`.

## 2. Ofuscação de JavaScript (Análise Dinâmica)
**Ferramentas:** `box-js` (Node.js Sandbox)

- **Técnica:** Emulação de objetos ActiveX e WScript para desofuscar scripts Droppers.
- **Resultados:** - Total de URLs únicas: 9
  - Endpoint Crítico: `hxxp://aristonbentre[.]com/slideshow/O1uPzXd2YscA/`
  - Artefato de saída: `urls.json`

## 3. Microsoft Office & OneNote Forensics
**Ferramentas:** `oleid`, `olevba`, `onedump.py`

### Documento Word (.doc)
- **Metadados:** Autor identificado como `CMNatic`.
- **Vetor:** Uso de macros `AutoOpen` (Fluxos 7 e 8) para download de segundo estágio (`stage2.exe`).

### OneNote (.one)
- **Cadeia de Ataque:** O documento utiliza `curl.exe` para baixar um payload disfarçado de imagem (`index1.png`).
- **Persistência:** Escrita em chaves de registro `HKCU\SOFTWARE\Andromedia`.
- **Evasão:** Uso de função `sleep(15000)` para retardar a análise dinâmica.

---
**Habilidades Demonstradas:** Análise estática/dinâmica, Desofuscação de código, Extração de IOCs e Engenharia Reversa básica.
