---
tipo: diagramas
titulo: Diagramas — Módulo 2 (Teste de Carga)
title: 📐 Diagramas — Módulo 2
modulo: 2
data: 2026-06-07
tags: [performance, diagramas, mermaid, carga, locust, dimensionamento]
---

# 📐 Diagramas — Módulo 2 (Teste de Carga)

> Versão publicada dos diagramas do Módulo 2 (os mesmos do `diagramas.canvas`, aqui em
> Mermaid para renderizar no site). Texto do módulo: [[modulo-2/_index|2️⃣ Índice do Módulo 2]].
>
> Organização: **🏛️ Conceito** (onde a carga se posiciona) → **⚙️ Workflow** (o Locust em ação).

---

## 🏛️ Conceito — Carga vs Estresse vs Pico

> Estrutura: onde a carga se posiciona. O teste de carga fica **dentro** do limite da
> aplicação; estresse vai além, pico sobe brusco.

```mermaid
flowchart TB
    subgraph LIM["⛔ Limite da aplicação"]
      direction TB
      CARGA["📈 TESTE DE CARGA<br/>carga ESPERADA<br/>DENTRO do limite<br/>→ valida performance + estabilidade"]:::carga
    end
    ESTRESSE["🔥 Estresse<br/>ALÉM do limite<br/>até falhar (ruptura)"]:::estresse
    PICO["⚡ Pico<br/>salto BRUSCO e curto<br/>(burst)"]:::pico
    CARGA -.->|ultrapassa o limite| ESTRESSE
    CARGA -.->|sobe muito rápido| PICO
    classDef carga fill:#0d4429,stroke:#2ea043,color:#e6edf3,stroke-width:3px;
    classDef estresse fill:#3d1d00,stroke:#bd561d,color:#e6edf3;
    classDef pico fill:#2a0d2a,stroke:#a371f7,color:#e6edf3;
```

---

## 📈 Conceito — Por que fazer teste de carga

> Os três motivos do material: detecção precoce, linha de base e planejamento de capacidade.

```mermaid
flowchart LR
    C(["📈 Por que fazer<br/>teste de carga?"]):::raiz
    C --> D1["🔍 Detecção precoce<br/>acha problemas antes<br/>de afetar usuários reais"]:::b
    C --> D2["📏 Linha de base<br/>compara performance<br/>ao longo do tempo"]:::b
    C --> D3["📐 Planejamento de capacidade<br/>aguenta o nº esperado<br/>sem degradar?"]:::b
    classDef raiz fill:#0d1b2a,stroke:#1f6feb,color:#e6edf3,stroke-width:3px;
    classDef b fill:#0d4429,stroke:#2ea043,color:#e6edf3;
```

---

## 📐 Conceito — Dimensionamento proporcional

> A regra de ouro: simule uma fração da carga de produção proporcional aos recursos do
> laboratório, com ramp up suave e o mesmo perfil de requisições.

```mermaid
flowchart TB
    PROD[("🏭 PRODUÇÃO<br/>10 CPUs · 64 GB<br/>pico: 5.000 CCU")]:::prod
    PROP{{"📐 calcular proporção"}}:::dec
    LAB[("🧪 LABORATÓRIO<br/>2 CPUs · 8 GB<br/>= 20% dos recursos")]:::lab
    PROD --> PROP
    LAB --> PROP
    PROP --> R["✅ simular ~20% da carga<br/>≈ 1.000 usuários"]:::ok
    R --> RAMP["🐢 ramp up suave<br/>(ex.: 10 min até o pico)"]:::nota
    R --> PERFIL["🔁 mesmo perfil de requisições<br/>(endpoints, dados, frequência)"]:::nota
    classDef prod fill:#1c2b3a,stroke:#388bfd,color:#e6edf3,stroke-width:2px;
    classDef lab fill:#341a00,stroke:#bb8009,color:#e6edf3;
    classDef dec fill:#2d2a00,stroke:#d4a72c,color:#f8f8e6;
    classDef ok fill:#0d4429,stroke:#2ea043,color:#e6edf3,stroke-width:2px;
    classDef nota fill:#0d1b2a,stroke:#1f6feb,color:#e6edf3;
```

---

## ⚙️ Workflow — O ciclo de um usuário Locust

> Processo no tempo: o que cada usuário (`HttpUser`) faz em loop, do GET ao `wait_time`.

```mermaid
flowchart TD
    U(["🦗 Locust cria N usuários (HttpUser)"]):::ini
    U --> T["@task fazer_requisicao()"]:::web
    T --> G["self.client.get('/delay/0.2')<br/>catch_response=True"]:::web
    G --> Ok{"status == 200?"}:::dec
    Ok -->|sim| Suc["✅ sucesso<br/>(métrica registrada)"]:::dado
    Ok -->|não| Fail["❌ response.failure()<br/>registra falha"]:::erro
    Suc --> W["⏲️ wait_time between(0.1, 0.5)<br/>simula humano"]:::web
    Fail --> W
    W --> T
    classDef ini fill:#1f6feb,stroke:#388bfd,color:#fff,stroke-width:2px;
    classDef web fill:#0d4429,stroke:#2ea043,color:#e6edf3;
    classDef dec fill:#2d2a00,stroke:#d4a72c,color:#f8f8e6;
    classDef dado fill:#1c2b3a,stroke:#388bfd,color:#e6edf3,stroke-width:2px;
    classDef erro fill:#3d1d00,stroke:#bd561d,color:#e6edf3;
```

---

## ⚙️ Workflow — Como executar (web vs headless)

> Os dois modos de rodar: interface web em tempo real, ou headless em lote gerando CSV.

```mermaid
flowchart TD
    Start(["▶️ rodar o teste"]):::ini
    Start --> Modo{"qual modo?"}:::dec
    Modo -->|🌐 Web| A1["locust -f teste_carga.py"]:::web
    A1 --> A2["abrir http://localhost:8089"]:::web
    A2 --> A3["definir usuários + spawn rate<br/>monitorar em tempo real"]:::web
    A3 --> Fim
    Modo -->|⌨️ Headless| B1["python run_tests.py"]:::exp
    B1 --> B2["loop nas CARGAS [10,25,50,100,200]<br/>subprocess chama locust --headless"]:::exp
    B2 --> B3[("--csv=results<br/>gera results_stats.csv")]:::dado
    B3 --> Fim(["📊 interpretar CSV:<br/>requests, failures, median,<br/>avg, min/max, req/sec"]):::fim
    classDef ini fill:#1f6feb,stroke:#388bfd,color:#fff,stroke-width:2px;
    classDef web fill:#0d4429,stroke:#2ea043,color:#e6edf3;
    classDef exp fill:#341a00,stroke:#bb8009,color:#e6edf3;
    classDef dado fill:#1c2b3a,stroke:#388bfd,color:#e6edf3,stroke-width:2px;
    classDef dec fill:#2d2a00,stroke:#d4a72c,color:#f8f8e6;
    classDef fim fill:#161b22,stroke:#6e7681,color:#e6edf3;
```

---

## ⏭️ Para onde ir agora

- Voltar ao texto do módulo → [[modulo-2/_index|2️⃣ Índice do Módulo 2]]
- O exercício com Locust → [[modulo-2/03-exercicio-locust|🦗 Exercício com Locust]]
- Diagramas do módulo anterior → [[modulo-1/diagramas|📐 Diagramas — Módulo 1]]
