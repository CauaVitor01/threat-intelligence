# Tactical Detection Engineering & Threat Intelligence Operationalization

Este repositório documenta a implementação de estratégias avançadas de defesa cibernética, focando na transição de Inteligência de Ameaças (CTI) para mecanismos de detecção e resposta automatizados. O projeto demonstra a aplicação prática de conceitos de Blue Team em ambientes SIEM.

---

## Visão Geral Estratégica
A fundação deste projeto baseia-se no ciclo de vida da Inteligência de Ameaças, segmentado em níveis táticos e técnicos. Como consumidor de inteligência, o foco é a ingestão de Indicadores de Comprometimento (IOCs) para a redução do ruído de alertas e otimização do MTTR (Mean Time to Respond).



---

## Implementações Técnicas

### 1. Prevenção Ativa e DNS Sinkhole
Implementação de controles em múltiplas camadas para interrupção da Cyber Kill Chain.
* **Redirecionamento de DNS:** Configuração de Sinkhole para domínios maliciosos, forçando a resolução para IPs de loopback (0.0.0.0).
* **Sensor de Alta Fidelidade:** Utilização do tráfego redirecionado como indicador imediato de hosts comprometidos, eliminando falsos positivos e otimizando a triagem.



### 2. Detection as Code (Sigma & ElastAlert)
Operacionalização de detecções agnósticas utilizando a linguagem Sigma para garantir portabilidade entre plataformas.
* **Pipeline de Automação:** Tradução de regras via Uncoder.io para o framework ElastAlert.
* **Monitoramento Proativo:** Criação de alertas baseados em anomalias de rede e resoluções de DNS suspeitas no índice filebeat-*.



### 3. Threat Hunting & SIEM Analysis
Metodologia de busca ativa baseada em hipóteses e inteligência técnica para identificação de ameaças persistentes:
* **Correlação de Eventos:** Uso de KQL (Kibana Query Language) para identificar comunicações de Comando e Controle (C2) e algoritmos de geração de domínio (DGA).
* **Auditoria de Logs:** Validação de regras através da análise quantitativa de Query Hits vs. Matches.

---

## Ciclo de Resposta e Validação
A eficácia das detecções é validada através de auditorias retroativas nos logs do SIEM, garantindo que a telemetria capture o comportamento do adversário com precisão e minimize o impacto de falsos negativos.

```bash
# Execução de auditoria detalhada via ElastAlert para validação de regras
elastalert --start 2023-02-16T00:00:00 --verbose 2>&1 | tee output.txt
Tecnologias e Frameworks
SIEM: Elastic Stack (Kibana / Elasticsearch)

Linguagens de Consulta: KQL, Lucene, Sigma

Alerting Framework: ElastAlert

Protocolos e Auditoria: DNS Security, SACLs, Windows Event Analysis
