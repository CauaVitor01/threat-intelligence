# Threat Hunting & Intelligence Strategy

Este repositório documenta a metodologia e a visão estratégica aplicadas à Busca Ativa de Ameaças (Threat Hunting) e ao uso de Inteligência de Ameaças para o fortalecimento da postura de segurança defensiva em ambientes corporativos.

---

## Visão Geral

A segurança moderna exige a transição de um modelo puramente reativo para um modelo proativo. Esta abordagem foca na identificação de adversários que possam ter contornado as defesas automáticas, utilizando o Threat Hunting como ferramenta para reduzir o Dwell Time (tempo de permanência) do invasor e aprimorar continuamente os mecanismos de detecção do SOC.

---

## Mentalidade e Estratégia de Busca

### 1. Proatividade vs. Reatividade

A Resposta a Incidentes (RI) e o Threat Hunting são disciplinas complementares, porém com naturezas e gatilhos distintos:

* **Resposta a Incidentes:** Inerentemente reativa, é disparada por notificações ou alertas iniciais e foca na contenção de ameaças já identificadas.
* **Threat Hunting:** Inerentemente proativa, é guiada por hipóteses e Inteligência de Ameaças, focando na descoberta de atividades maliciosas ainda não detectadas.

### 2. Objetivos Estratégicos da Investigação

A prática de caça fundamenta-se em quatro pilares:

1. **Identificação Proativa:** Localizar o agente malicioso antes que ele consolide seus objetivos no ambiente.
2. **Descoberta de Ameaças Ocultas:** Expor atividades que escapam das regras de detecção automática, transformando o "indetectável" em visível.
3. **Minimização do Dwell Time:** Reduzir a janela de oportunidade do atacante para explorar o ambiente, preservando a tríade CIA (Confidencialidade, Integridade e Disponibilidade).
4. **Ciclo de Feedback:** Utilizar os achados da caçada para criar novos mecanismos de detecção automática no SOC.

---

## Metodologias e Ferramentas

### Inteligência de Ameaças (Threat Intel)

O uso de dados precisos é essencial para direcionar a investigação. A base de inteligência utilizada compreende:

* **Inteligência Exclusiva (Interna):** Análise de Indicadores de Comprometimento (IOCs) e resíduos de intrusões anteriores na própria infraestrutura.
* **Fontes Open Source:** Utilização de plataformas colaborativas como o MISP para troca de inteligência comunitária.
* **Provedores Especializados:** Consulta a feeds de inteligência para compreensão de Táticas, Técnicas e Procedimentos (TTPs) de grupos específicos.

### Mapeamento com MITRE ATT&CK Navigator

O ATT&CK Navigator foi utilizado como ferramenta central para visualizar a cobertura defensiva através do seguinte processo:

* **Criação de Camadas (Layers):** Mapeamento individual de ameaças específicas (ex: WannaCry, Stuxnet e Conficker).
* **Análise de Calor (Heatmap):** Agregação de camadas para identificar técnicas comuns entre múltiplos adversários. Tons mais escuros no mapa indicam técnicas compartilhadas, permitindo a priorização de defesas onde o risco é convergente.

---

## Alvos da Busca

A investigação foca em evidências técnicas acionáveis e imediatas:

* **Malware Relevante:** Análise de ferramentas utilizadas por agentes que visam o setor da organização, utilizando repositórios como o theZoo e a Enciclopédia de Ameaças da Trend Micro.
* **Resíduos de Ataque (Artifacts):** Identificação de vestígios digitais que divergem do comportamento normal (Baseline) do sistema.
* **Vulnerabilidades (CVEs):** Verificação de ativos vulneráveis a falhas críticas e análise retroativa de logs para identificar possíveis explorações prévias.

---

## Conclusão da Caçada

Diferente de um cenário de CTF (Capture The Flag), onde a ausência de uma flag indica falha, no Threat Hunting a ausência de achados após um processo rigoroso é um resultado positivo. Este desfecho valida que, com base na inteligência disponível, o ambiente está livre daquelas ameaças específicas. O sucesso é determinado pela aderência metódica ao plano de busca.
