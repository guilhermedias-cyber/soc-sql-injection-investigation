# 🔴 SQL Injection Investigation

### Let's Defend Lab #01

`SOC165` · `Web Attack` · `MITRE ATT&CK T1190`

> Investigação de um alerta relacionado a uma tentativa de SQL Injection contra um servidor web.

---

## 🎯 Objetivo

Investigar o alerta **SOC165 — Possible SQL Injection Payload Detected**, validar a atividade observada, analisar as evidências disponíveis e determinar se houve exploração bem-sucedida.

A investigação foi conduzida em um ambiente de treinamento do **Let's Defend**.

---

## 🔎 Investigation Workflow

```text
ALERTA
   ↓
VALIDAÇÃO
   ↓
ANÁLISE DOS LOGS
   ↓
ANÁLISE DO PAYLOAD
   ↓
THREAT INTELLIGENCE
   ↓
INVESTIGAÇÃO DO ENDPOINT
   ↓
AVALIAÇÃO DA EXPLORAÇÃO
   ↓
CLASSIFICAÇÃO
📊 Case Summary
Indicador	Resultado
Incident Type	Web Attack
Alert	SOC165
Attack Type	SQL Injection
MITRE ATT&CK	T1190 — Exploit Public-Facing Application
Severity	High
Source IP	167.99.169.17
Destination	172.16.17.18
Hostname	WebServer1001
Traffic Direction	Internet → Company Network
Device Action	Permitted
Final Classification	True Positive
Successful Exploitation	Not demonstrated
Exfiltration	No evidence observed
Post-Exploitation	No evidence observed
Tier 2 Escalation	No


🧪 Initial Analysis
O alerta indicava uma possível tentativa de SQL Injection direcionada ao servidor web WebServer1001.
Durante a análise dos eventos, foram observadas requisições HTTP GET direcionadas ao endpoint /search/, contendo parâmetros com padrões compatíveis com tentativa de manipulação de consultas SQL.
Entre os indicadores observados estavam expressões como:
' OR '1
OR 1=1
--

Os eventos apresentaram comportamento diferente da requisição de referência, incluindo respostas HTTP 500.
Uma resposta HTTP 500, isoladamente, não demonstra que a exploração foi bem-sucedida. Ela apenas indica que a aplicação apresentou um erro ao processar a requisição.

🌐 Traffic Analysis
A atividade analisada apresentou o seguinte fluxo:
Internet
    │
    │ HTTP GET
    ▼
167.99.169.17
    │
    ▼
172.16.17.18
WebServer1001

A ação registrada pelo dispositivo foi:
Device Action: Permitted

Isso significa que a requisição alcançou o ambiente analisado, tornando necessária a investigação do comportamento posterior.
💉 Payload Analysis
Os parâmetros observados nas requisições apresentavam padrões associados a tentativas de SQL Injection.
Um dos indicadores analisados foi:
%27%20OR%20%271

Após a decodificação:
' OR '1

Também foram observadas variações envolvendo:
OR 1=1

e sintaxe de comentário SQL:
--

A combinação desses elementos sustentou a classificação da atividade como uma tentativa maliciosa de SQL Injection.
🌎 Threat Intelligence
Foram realizadas consultas de Threat Intelligence para o endereço de origem:
167.99.169.17

A consulta realizada no Threat Intelligence do laboratório não apresentou dados associados ao IP.
Também foram realizadas consultas externas para complementar a análise.
A ausência de informações em uma fonte de Threat Intelligence não deve ser interpretada isoladamente como evidência de atividade legítima.

As informações externas foram utilizadas como evidência contextual, não como fator único para a classificação do incidente.
🖥️ Endpoint Investigation
O endpoint analisado foi:
Hostname: WebServer1001
IP:       172.16.17.18
OS:       Windows Server 2019
User:     webadmin

Foram analisados diferentes artefatos disponíveis no laboratório, incluindo:
- Processos
- Histórico do navegador
- Histórico de terminal
- Conexões de rede
- Informações do endpoint
A análise não revelou evidências claras de atividade de pós-exploração associada ao evento investigado.
Também foram observados artefatos relacionados a atividades administrativas e de configuração anteriores ao incidente.
🧩 Attack Success Assessment
A investigação buscou determinar se a tentativa de SQL Injection resultou em comprometimento efetivo.
Evidências observadas
✓ Requisição maliciosa
✓ Payload compatível com SQL Injection
✓ Aplicação processou a requisição
✓ Resposta HTTP 500

Evidências não observadas
✗ Exfiltração de dados
✗ Pós-exploração
✗ Execução de comandos
✗ Comprometimento demonstrado

Conclusão
Successful exploitation: Not demonstrated
A evidência disponível foi suficiente para confirmar a tentativa maliciosa, mas não para demonstrar que a exploração foi concluída com sucesso.
🎯 Final Classification
Decision	Result
Traffic Malicious	Yes
Attack Type	SQL Injection
True Positive	Yes
Attack Successful	No
Tier 2 Escalation	No
Planned Test	Not Planned


Final Verdict
True Positive — Malicious SQL Injection Attempt

A atividade foi corretamente identificada como uma tentativa de SQL Injection.
Entretanto, a investigação não encontrou evidências suficientes para demonstrar exploração bem-sucedida, exfiltração de dados ou atividade de pós-exploração.
🧠 Key Findings
01 — Malicious activity confirmed
O payload e o contexto das requisições sustentaram a classificação como atividade maliciosa.
02 — Detection was correct
O alerta identificou corretamente uma tentativa de exploração contra uma aplicação web.
03 — Attempt ≠ compromise
A existência de uma tentativa de SQL Injection não significa necessariamente que o sistema tenha sido comprometido.
04 — Endpoint investigation matters
A investigação do endpoint foi importante para avaliar possíveis sinais de atividade posterior à tentativa.
05 — Threat Intelligence is contextual
A ausência ou presença de reputação de um IP deve ser interpretada em conjunto com as demais evidências.
📸 Evidence
As principais evidências utilizadas na investigação estão organizadas no diretório:
[`/evidence`](./evidence/)
Evidências selecionadas
1. Alert Overview
2. HTTP Request / Payload
3. Threat Intelligence
4. Endpoint Investigation
5. Final Classification
📄 Technical Report
O relatório técnico completo está disponível em:
[SOC165 — SQL Injection Technical Report](./report/SOC165-SQL-Injection-Technical-Report.pdf)
📝 Technical Article
A investigação também foi documentada em formato narrativo no Medium:
Read the full investigation on Medium
Link será adicionado após a publicação do artigo.

🛡️ Environment Disclaimer
Esta investigação foi realizada exclusivamente em um ambiente de treinamento do Let's Defend.
Os endereços IP, hostnames, eventos e demais informações técnicas apresentados neste repositório pertencem ao cenário de treinamento e não representam um incidente corporativo real.
<div align="center">

Segurança não é apenas detectar alertas.
É entender o que aconteceu.
</div>
```
