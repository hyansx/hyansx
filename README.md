<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0d1117,50:1f6feb,100:8b5cf6&height=180&section=header&text=hyansx&fontSize=56&fontColor=ffffff&fontAlignY=38&desc=Backend%20%E2%80%A2%20Dados%20%E2%80%A2%20IA%20aplicada&descAlignY=60&descSize=18&animation=fadeIn" width="100%"/>

<a href="https://github.com/hyansx">
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=20&duration=3000&pause=800&color=58A6FF&center=true&vCenter=true&width=680&lines=sistemas+que+movem+dinheiro+de+verdade+%F0%9F%92%B8;agentes+de+IA+rodando+em+produ%C3%A7%C3%A3o+%F0%9F%A4%96;teste+verde+%C3%A9+hip%C3%B3tese%2C+n%C3%A3o+prova+%F0%9F%A7%AA;multi-tenant+com+menor+privil%C3%A9gio+%F0%9F%94%90" alt="typing" />
</a>

</div>

---

```python
class Hyan:
    role     = "Software Engineer — backend, dados & IA aplicada"
    based_in = "🇧🇷 Brasil"
    domains  = ["conciliação financeira", "RPA", "agentes LLM", "SaaS multi-tenant"]
    practice = ["mutation testing", "aceite contra cópia real de produção", "postmortem"]
    studying = ["AppSec", "threat modeling", "pentest web/API"]

    def principle(self):
        return "se não foi medido contra dado real, não está pronto"
```

Construo e opero **plataformas SaaS multi-tenant** onde erro custa dinheiro: conciliação financeira, automação de coleta de dados e agentes de IA atendendo cliente final. Trabalho do schema ao deploy: modelagem, motor de regras, filas, observabilidade, CI/CD e operação em produção.

> 🔒 Meu trabalho é majoritariamente em repositórios privados, sob confidencialidade. Os sistemas abaixo estão descritos de forma genérica, sem clientes, volumes ou detalhes de infraestrutura.

---

## 🏗️ O que eu construo

### 💸 Plataforma financeira B2B — RPA + conciliação
`Python` `FastAPI` `PostgreSQL` `Celery/Redis` `Playwright` `LLM` `React` `React Native`

- **RPA com IA para portais de terceiros.** Cada conector vira uma **receita determinística versionada em git**; o LLM entra para gerar a receita, não a cada execução, o que derruba o custo da execução recorrente para centavos.
- **Certificação automática de conector.** O resultado é validado pelo **conteúdo** do documento, não pelo status da execução, e a coleta precisa ser **repetível e exaustiva**. Isso pega o robô que "passa" trazendo só parte dos arquivos.
- **Execução resiliente a falha de banco.** O ciclo é dividido em fases com persistência independente e um *reaper* para execuções órfãs. As exceções de desconexão foram classificadas **medindo contra um banco real derrubado de propósito**, não por suposição.
- **Motor de conciliação N→1** com rateio pró-rata, piso de tolerância e detecção de **reemissão de documento por conteúdo**, porque o hash do arquivo não é confiável.
- **Controles de custo:** disjuntor de gasto de LLM por conector e alarmes.

### 📊 Conciliação de vendas × pagamentos
`TypeScript` `Node.js` `SQL Server` `React`

- **Performance guiada por medição.** O diagnóstico pelo Query Store mostrou que o gargalo era paralelismo, não falta de índice. Com índices de cobertura dimensionados pelo tamanho real das linhas, as consultas ficaram **de 4× a 10× mais rápidas** e o painel principal ficou **−75%** mais leve.
- **Conciliação 1→N por grupo de referência**, com uma *regra de âncora* que impede a divergência de ser contada várias vezes nos totais.
- **Migrations ensaiadas em cópia isolada** antes de produção; as invariantes ficam no banco, não só na aplicação.

### 🤖 Agentes de IA conversacionais
`Python` `FastAPI` `LangGraph` `MCP` `Redis`

- Webhooks com **verificação de assinatura (HMAC + timestamp)**, fila assíncrona e **idempotência contra reentrega** do provedor.
- Deploy **GitOps** e servidor **MCP** próprio com cache para proteger a cota das APIs externas.
- Hardening para pico de uso: limite de concorrência, timeouts, retries, healthchecks e rollback com versão de baseline.

### 🧠 SaaS de IA / RAG
`Java` `Spring Boot` `pgvector` `React`

- RAG com embeddings em **pgvector** e orquestração ReAct com *function calling* sobre os dados do cliente.
- Evolução de schema em produção sem perda de dado, incluindo migrations fora de ordem.

### 🏢 SaaS vertical multi-tenant
`FastAPI` `Celery` `Next.js` `PostgreSQL`

- **Multi-tenant desde o schema:** Row-Level Security com role de aplicação sem privilégio de owner e **meta-teste que reprova tabela nova sem policy**.
- **Refresh token rotativo com detecção de reuso**, eventos de domínio pós-commit e monitoramento de *heartbeat* nos workers.
- Infra sem exposição desnecessária e **rollback ensaiado** como parte do critério de pronto.

---

## 🧪 Qualidade: como eu provo que funciona

- **Mutation testing por commit.** Todo commit que muda comportamento leva o mutante que reintroduz o bug, e o teste tem que matá-lo.
- **Portões de CI com milhares de testes** (pytest, Vitest, Jest, e2e), mais testes de convenção de schema e de migration.
- **Aceite com dado realista.** O código roda contra um ambiente isolado com volume de produção, não só contra fixture.
- **Flakiness tratada como dado:** meço a taxa-base antes de aceitar um verde (1 verde em 16 não prova nada; 16 em 16 prova).
- **Postmortem** de incidente, e cada lição vira uma guarda automática no pipeline.

## 🔐 Segurança

**Na prática:**
- Isolamento multi-tenant com **Row-Level Security** e princípio do menor privilégio
- Verificação de assinatura de webhooks, rotação de tokens e detecção de reuso de refresh token
- Acesso a infraestrutura por rede privada, segredos fora do código e das imagens
- Revisão de privacidade de SDKs de terceiros antes de irem para produção

**Em estudo:** AppSec ofensiva e defensiva — OWASP Top 10 / ASVS, threat modeling e testes de intrusão em aplicações web e APIs.

---

## 🛠️ Stack

<p align="left">
  <img src="https://skillicons.dev/icons?i=python,fastapi,ts,nodejs,java,spring,react,nextjs,tailwind&theme=dark" />
  <br/>
  <img src="https://skillicons.dev/icons?i=postgres,redis,prisma,docker,kubernetes,nginx,cloudflare,linux,bash&theme=dark" />
  <br/>
  <img src="https://skillicons.dev/icons?i=githubactions,git,jest,vitest,vercel&theme=dark" />
</p>

<p align="left">
  <img src="https://img.shields.io/badge/LangGraph-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white" />
  <img src="https://img.shields.io/badge/LLMs%20%2F%20RAG-8B5CF6?style=for-the-badge&logo=openai&logoColor=white" />
  <img src="https://img.shields.io/badge/MCP-000000?style=for-the-badge&logo=anthropic&logoColor=white" />
  <img src="https://img.shields.io/badge/pgvector-336791?style=for-the-badge&logo=postgresql&logoColor=white" />
  <img src="https://img.shields.io/badge/Celery-37814A?style=for-the-badge&logo=celery&logoColor=white" />
  <img src="https://img.shields.io/badge/Playwright-2EAD33?style=for-the-badge&logo=playwright&logoColor=white" />
  <img src="https://img.shields.io/badge/pytest-0A9EDC?style=for-the-badge&logo=pytest&logoColor=white" />
  <img src="https://img.shields.io/badge/React%20Native%20%2F%20Expo-000020?style=for-the-badge&logo=expo&logoColor=white" />
  <img src="https://img.shields.io/badge/SQL%20Server-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white" />
  <img src="https://img.shields.io/badge/ArgoCD-EF7B4D?style=for-the-badge&logo=argo&logoColor=white" />
  <img src="https://img.shields.io/badge/Tailscale-242424?style=for-the-badge&logo=tailscale&logoColor=white" />
  <img src="https://img.shields.io/badge/n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white" />
</p>

---

## 📊 Atividade

<div align="center">

<img src="https://streak-stats.demolab.com?user=hyansx&theme=tokyonight&hide_border=true&locale=pt_BR" width="49%" />

<img src="https://github-readme-activity-graph.vercel.app/graph?username=hyansx&theme=tokyo-night&hide_border=true&area=true" width="100%" />

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/hyansx/hyansx/output/github-snake-dark.svg" />
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/hyansx/hyansx/output/github-snake.svg" />
  <img alt="snake comendo as contribuições" src="https://raw.githubusercontent.com/hyansx/hyansx/output/github-snake.svg" />
</picture>

</div>

<details>
<summary>🗂️ Projetos de estudo públicos</summary>

<br/>

| Projeto | O que é | Stack |
|---|---|---|
| 💬 [n8n-ai-chat-widget](https://github.com/hyansx/n8n-ai-chat-widget) | Widget de chat flutuante, zero dependências, plugado num agente de IA | `JavaScript` |
| 🍼 [Controle-de-fraldas](https://github.com/hyansx/Controle-de-fraldas) | Controle de estoque e gastos com gráficos | `Next.js` `Prisma` `Docker` |
| 📝 [formulario-cadastro](https://github.com/hyansx/formulario-cadastro) | CRUD fullstack de usuários e endereços | `Express` `PostgreSQL` `Docker` |
| 🏧 [terminal-atm](https://github.com/hyansx/terminal-atm) | Caixa eletrônico no terminal | `Node.js` `SQLite` |

</details>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:8b5cf6,50:1f6feb,100:0d1117&height=110&section=footer" width="100%"/>
