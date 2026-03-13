### Site Reliability Engineer (SRE)

### Requisitos Técnicos

### **Networking e Protocolos**

- DNS: resolução recursiva, authoritative vs recursive servers, TTL
    
- TCP: entender por que connections se acumulam, quando usar TCP vs UDP, impacto de latência em handshake
    
- HTTP: status codes (429, 503, 504), streaming vs request-response, HTTP/2 multiplexing
    
- TLS: handshake overhead, certificate chain validation
    
- Load balancing: L4 vs L7, health checks, sticky sessions e o seus impactos.


**Linux**

- Troubleshooting: strace, perf, ftrace
    
- Recursos: CPU steal time, memory pressure, disk I/O wait, load average
    
- Kernel: OOM killer, file descriptor limits, network buffer tuning
    
- Saber ler /proc e /sys quando não tem ferramenta instalada no container


**Observabilidade**

- SLI/SLO/SLA: olhar mais para o Business e XP do Usuário, menos métrica técnica: CPU Utilization
    
- Error budgets: calcular, gastar conscientemente, defender quando produto quer velocidade
    
- Golden Signals: latency, traffic, errors, saturation - nessa ordem quando estiver debugando
    
- Distributed tracing: entender span, context propagation, sampling strategies
    
- Alerting: on-call (famoso plantão do ódio), alert fatigue


**Sistemas Distribuídos**

- CAP theorem aplicado: quorum, consistency levels, split-brain
    
- Consensus: Raft/Paxos conceitos, por que leader election é difícil
    
- Idempotência e retries: exponential backoff, jitter, circuit breakers
    
- Timeouts: cascading failures, por que timeout infinito é um suicídio
    
- Bulkheads e isolamento: falha contida não vira catástrofe


**Bancos de Dados (Performance e Confiabilidade)**

- Locks e deadlocks: quando acontecem, como detectar, como evitar
    
- Replicação: lag, consistency trade-offs, failover que não perde dados
    
- Backup e recovery: RPO/RTO, point-in-time recovery, testar restore (sempre)
    
- Query performance: execution plans, índices, cache hit ratio
    
- Connection pooling: sizing, timeout configs, por que "just add connections" é uma morte horrível


**Capacidade e Performance**

- Capacity planning: growth projections, headroom, por que 80% não é margem de segurança
    
- Performance testing: load vs stress vs soak tests, realistic traffic patterns
    
- Profiling: CPU, memory, I/O - achar o bottleneck real
    
- Autoscaling: metrics que importam, cooldown periods, por que scale-down é perigoso


**Ferramentas**

- Kubernetes
    
- Prometheus/Grafana: PromQL, recording rules, alerting rules
    
- Service mesh: quando ajuda, quando atrapalha, overhead de latência
    
- Chaos engineering: injetar falha de propósito, testar resiliência


## Requisitos Técnicos Diferenciais

**O que diferencia SRE "baum memo":**

- Desenhar sistemas para degradar gracefully, não só para funcionar
    
- Calcular blast radius antes do deploy
    
- Balancear toil reduction com trabalho que faz sentido, que tem impacto
    
- Experiência real com multi-region failover (não só no papel)
    
- Saber quando aceitar downtime planejado vs correr risco
    
- Ter vivido incident complexo e coordenar Incident Response


## Requisitos Não-Técnicos

### Incident Management

- Comandar war room
    
- Comunicar status: interno, stakeholders, clientes - tons diferentes
    
- Delegar tasks em crise sem micromanage
    
- Saber quando trazer mais gente vs resolver com quem tem
    
- Postmortem blameless de verdade: timeline, root cause, action items


### Mindset SRE

- Tudo é trade-off: uptime custa, perfeição é impossível, good enough é baum
    
- Error budget não é punição, é ferramenta de negociação
    
- Toil é inimigo: se faz 2x, automatiza na 3x
    
- On-call sustentável: se acorda todo dia, o sistema tá quebrado, não você
    
- "Hope is not a strategy": assumir falha, planejar para ela


### Colaboração

- Negociar SLO com produto: defender realismo, educar sobre custos
    
- Code review focado em reliability: race conditions, edge cases, failure modes
    
- Dizer "não" tecnicamente fundamentado, não por ego
    
- Ensinar devs sobre operabilidade sem arrogância


### Documentação e Runbooks

- Runbook que foi escrito 2pm e funciona as 2am
    
- Postmortems que viram ação, não ficam no Confluence
    
- Arquitetura documentada: não como é, mas como falha
    
- Oncall handoff: context que importa, não cuspir informação


## Red Flags

- Acha que 99.99% uptime é sempre possível (ou necessário)
    
- Nunca calculou error budget ou acha que é métrica de vaidade
    
- Acredita que "importante é ter um alerta" sem saber ação
    
- Otimiza latência de P50 ignorando P99
    
- Zero experiência com incident real de produção
    
- Culpa dev quando quebra ao invés de melhorar sistema
    
- Trata on-call como punição ao invés de responsabilidade


---

# Requisitos para DevOps Engineer

## Requisitos Técnicos

### **Sistemas Operacionais e Automação**

- Bash/Python proficiente: não só scripts, mas código mantível e testável
    
- Linux administration: users, permissions, services, systemd, cron
    
- Package management: apt/yum/apk, repositórios, dependency hell
    
- Configuration management: idempotência, state drift, reconciliation


**Networking para CI/CD**

- Firewall rules, security groups, network policies
    
- DNS para ambientes: dev, staging, prod - isolamento e roteamento
    
- Proxy/reverse proxy: nginx, HAProxy, Envoy - casos de uso
    
- VPN, bastion hosts, fundamentos de zero-trust


**Infrastructure as Code**

- Terraform/Pulumi/CloudFormation: state management, modules, workspaces
    
- Immutable infrastructure: por que mutate-in-place é grudar chiclete na cruz
    
- Drift detection e remediação
    
- Secrets management: nunca no código, rotação, acesso auditado


**CI/CD Pipelines**

- Pipeline como código: Jenkinsfile, GitHub Actions, GitLab CI
    
- Build optimization: cache, artifacts, parallel jobs
    
- Testing na pipeline: unit, integration, security, performance
    
- Deploy strategies: blue-green, canary, rolling, rollback rápido
    
- GitOps: pull vs push models, reconciliation loops


**Containers e Orquestração**

- Docker: não só FROM e RUN, mas multi-stage builds, layer caching, security scanning
    
- Container registries: versioning, cleanup policies, vulnerability scanning
    
- Kubernetes: deployments, services, ingress, configmaps/secrets, RBAC
    
- Helm/Kustomize: templating, environments, valores que mudam


**Cloud Platforms (AWS/Azure/GCP)**

- IAM: roles, policies, least privilege, service accounts
    
- Compute: VMs, containers, serverless - quando usar cada um
    
- Storage: block vs object vs file, backup strategies, lifecycle policies
    
- Networking: VPC, subnets, routing, peering, transit gateway


**Security e Compliance**

- Secret scanning em repos e containers
    
- Vulnerability management: scan, prioritize, patch
    
- Compliance as code: policy enforcement, audit trails
    
- Certificate management: rotation, expiry monitoring


## Requisitos Técnicos Diferenciais

**O que separa executor de engenheiro:**

- Pipeline self-service: devs deployam sem ticket
    
- Infra testável: validar antes de apply, rollback automático
    
- Cost optimization: rightsizing, spot instances, reserved capacity
    
- Disaster recovery: backup testado, RTO/RPO realistas
    
- Multi-cloud/hybrid: abstração sem vendor lock-in total


## Requisitos Não-Técnicos

### Colaboração Dev/Ops

- Bridge cultural: traduzir "precisa ser seguro" para "como fazer rápido E seguro"
    
- Empatia com devs: entender pressão de entrega, não só dizer "não pode"
    
- Empatia com ops: entender on-call pain, desenhar operabilidade desde início
    
- Code review construtivo: infra code é código também


### Decisão de Automação

- Saber quando automatizar vs quando documentar processo manual
    
- Automação que quebra é pior que processo manual
    
- KISS principle: solução simples que funciona > solução elegante que quebra
    
- Technical debt consciente: quando "quick fix" vale a pena


### Documentação

- README que ensina: como rodar, como testar, como debugar
    
- Diagramas de arquitetura atualizados (não só no onboarding)
    
- Decisões arquiteturais documentadas (ADRs): por que escolhemos X, não só o quê
    
- Runbooks para time: não só para você


### Comunicação

- Explicar impacto de mudança de infra para produto
    
- Defender security/compliance sem ser "blocker team"
    
- Estimar tempo realisticamente: infra changes são imprevisíveis
    
- Comunicar breaking changes com antecedência


### Mindset

- Infrastructure é produto: tem usuários (devs), precisa de UX boa
    
- Self-service > tickets: empoderar, não controlar
    
- Cattle, not pets: infra descartável, não servidores com nome (sim, essa tá cansada, eu sei)
    
- Shift-left: segurança e qualidade cedo, não no final


## Red Flags

- Só sabe clicar no console, não conhece API/CLI
    
- Terraform plan sem review: "parece OK, vou aplicar"
    
- Pipeline sem testes: "se buildou, tá pronto"
    
- Hardcoded values: configs no código, secrets em plain text
    
- "Works on my laptop" como pronto para produção
    
- Zero experiência debugando pipeline com falha
    
- Acha que automation é escrever script e esquecer