---
tipo: diagramas
titulo: Diagramas — Módulo 1 (Introdução a Testes de Performance)
title: 📐 Diagramas — Módulo 1
modulo: 1
data: 2026-06-07
tags: [performance, diagramas, mermaid, pilares, tipos, metricas]
---

# 📐 Diagramas — Módulo 1 (Introdução a Testes de Performance)

> Versão publicada dos diagramas do Módulo 1 (os mesmos do `diagramas.canvas`, aqui em
> Mermaid para renderizar no site). Texto do módulo: [[modulo-1/_index|1️⃣ Índice do Módulo 1]].
>
> Organização: **🏛️ Conceito** (como as ideias se conectam) → **⚙️ Workflow** (o que o código
> faz, em ordem) → **🎓 A lição** (o fecho pedagógico).

---

## 🏛️ Conceito — Os 3 pilares

> Estrutura: como as ideias se conectam. Os 3 pilares (tempo · capacidade · recursos) viram
> métricas e servem ao objetivo final.

```mermaid
flowchart TB
    PERF(["⚡ Teste de Performance<br/>o sistema funciona bem sendo usado?"]):::raiz
    PERF --> P1["⏱️ Comportamento do Tempo<br/>velocidade de resposta<br/>(ponta-a-ponta → ciclos de CPU)"]:::p1
    PERF --> P2["📦 Capacidade<br/>limites de operação<br/>(usuários, volume de dados)"]:::p2
    PERF --> P3["🧠 Utilização de Recursos<br/>RAM e processador<br/>(evita desperdício, acha gargalo)"]:::p3
    P1 -.->|vira métrica| M1["latência"]:::met
    P2 -.->|vira métrica| M2["throughput · usuários"]:::met
    P3 -.->|vira métrica| M3["uso de recursos"]:::met
    OBJ["🎯 Objetivo final:<br/>boa experiência do usuário<br/>em qualquer dispositivo/condição"]:::obj
    P1 --> OBJ
    P2 --> OBJ
    P3 --> OBJ
    classDef raiz fill:#0d1b2a,stroke:#1f6feb,color:#e6edf3,stroke-width:3px;
    classDef p1 fill:#0d4429,stroke:#2ea043,color:#e6edf3;
    classDef p2 fill:#3b2300,stroke:#9e6a03,color:#e6edf3;
    classDef p3 fill:#2a0d2a,stroke:#a371f7,color:#e6edf3;
    classDef met fill:#1c2b3a,stroke:#388bfd,color:#e6edf3;
    classDef obj fill:#341a00,stroke:#bb8009,color:#e6edf3,stroke-width:2px;
```

---

## 🗂️ Conceito — Os 7 tipos de teste

> Cinco dos sete tipos viram módulos da mentoria; *escalabilidade* e *capacidade* aparecem só
> citados na introdução.

```mermaid
flowchart TB
    T(["🗂️ 7 tipos de teste de performance"]):::raiz
    T --> C["📈 Carga<br/>comportamento esperado"]:::mod
    T --> E["🔥 Estresse<br/>além do limite"]:::mod
    T --> ESC["📊 Escalabilidade<br/>capacidade de expansão"]:::cit
    T --> PI["⚡ Pico<br/>variações bruscas"]:::mod
    T --> R["⏳ Resistência<br/>longo período"]:::mod
    T --> CO["🔀 Concorrência<br/>conflitos simultâneos"]:::mod
    T --> CAP["🧱 Capacidade<br/>quantidade suportada"]:::cit
    C --> Mod["✅ viram MÓDULOS<br/>desta mentoria (5)"]:::nota
    E --> Mod
    PI --> Mod
    R --> Mod
    CO --> Mod
    ESC --> So["⚠️ só citados<br/>na introdução"]:::aviso
    CAP --> So
    classDef raiz fill:#0d1b2a,stroke:#1f6feb,color:#e6edf3,stroke-width:3px;
    classDef mod fill:#0d4429,stroke:#2ea043,color:#e6edf3;
    classDef cit fill:#3b2300,stroke:#9e6a03,color:#e6edf3;
    classDef nota fill:#1c2b3a,stroke:#388bfd,color:#e6edf3,stroke-width:2px;
    classDef aviso fill:#3d1d00,stroke:#bd561d,color:#e6edf3;
```

---

## 🔗 Conceito — Como as métricas se relacionam sob carga

> À medida que a carga aumenta: a latência sobe, o throughput sobe até saturar, e os erros
> começam a aparecer. O exemplo numérico é o do material.

```mermaid
flowchart LR
    U["👥 Carga aumenta<br/>(mais usuários)"]:::carga
    U --> L["⏱️ Latência<br/>AUMENTA"]:::sobe
    U --> TP["🚀 Throughput<br/>aumenta… até saturar"]:::sobe
    U --> ER["❌ Erros<br/>começam a aparecer"]:::erro
    TP --> SAT["📉 Throughput<br/>estabiliza ou CAI"]:::queda
    subgraph EX["Exemplo do material"]
      direction TB
      X1["10 usuários → Lat. baixa · TP baixo · 0% erro"]:::ok
      X2["50 → Lat. média · TP alto · 0%"]:::ok
      X3["100 → Lat. alta · TP muito alto · 1%"]:::warn
      X4["200 → Lat. muito alta · TP estável · 5%"]:::bad
    end
    SAT --> EX
    ER --> EX
    classDef carga fill:#0d1b2a,stroke:#1f6feb,color:#e6edf3,stroke-width:3px;
    classDef sobe fill:#0d4429,stroke:#2ea043,color:#e6edf3;
    classDef erro fill:#3d1d00,stroke:#bd561d,color:#e6edf3;
    classDef queda fill:#3b2300,stroke:#9e6a03,color:#e6edf3;
    classDef ok fill:#0d4429,stroke:#2ea043,color:#e6edf3;
    classDef warn fill:#2d2a00,stroke:#d4a72c,color:#f8f8e6;
    classDef bad fill:#3d1d00,stroke:#bd561d,color:#e6edf3;
```

---

## ⚙️ Workflow — O fluxo do código (exercício em Python)

> Processo no tempo: o que o `teste-performance.py` faz, em ordem, para cada carga.

```mermaid
flowchart TD
    Start(["▶️ python teste-performance.py"]):::ini
    Start --> Loop{{"para cada carga<br/>[10, 25, 50, 100, 200]"}}:::dec
    Loop --> R1["1· resetar_metricas()<br/>zera latências, requisições, erros"]:::exp
    R1 --> R2["2· executar_teste(usuarios)<br/>ThreadPoolExecutor: 1 thread por usuário"]:::exp
    R2 --> T["🧵 cada thread roda usuario()<br/>em loop por 30s"]:::web
    T --> G["GET /delay/0.2 (timeout=3s)"]:::web
    G --> Ok{"status 200?"}:::dec
    Ok -->|sim| Lat["🔒 lock → guarda latência<br/>+1 requisição"]:::dado
    Ok -->|não / exceção| Err["🔒 lock → +1 erro"]:::erro
    Lat --> Sleep["sleep 0.1–0.5s<br/>(simula humano)"]:::web
    Err --> Sleep
    Sleep --> Fim{"tempo acabou?"}:::dec
    Fim -->|não| G
    Fim -->|sim| An["3· analisar_metricas()<br/>throughput · lat min/média/máx · p95/p99 · taxa erro"]:::dado
    An --> Print[("🖨️ imprime RESULTADOS")]:::dado
    Print --> Loop
    Loop -->|fim das cargas| End(["🏁 fim"]):::fim
    classDef ini fill:#1f6feb,stroke:#388bfd,color:#fff,stroke-width:2px;
    classDef web fill:#0d4429,stroke:#2ea043,color:#e6edf3;
    classDef exp fill:#341a00,stroke:#bb8009,color:#e6edf3;
    classDef dado fill:#1c2b3a,stroke:#388bfd,color:#e6edf3,stroke-width:2px;
    classDef erro fill:#3d1d00,stroke:#bd561d,color:#e6edf3;
    classDef dec fill:#2d2a00,stroke:#d4a72c,color:#f8f8e6;
    classDef fim fill:#161b22,stroke:#6e7681,color:#e6edf3;
```

---

## 🎓 A lição — QA júnior vs QA sênior

> O fecho pedagógico do módulo: a diferença não é coletar o número, é interpretá-lo e
> contextualizá-lo. Detalhe em [[modulo-1/02-metricas#🎓 O que esperar da análise do QA?|📊 Métricas]].

```mermaid
flowchart LR
    D[("📊 Resultado:<br/>5% de erro a 200 usuários")]:::dado
    D --> JR["🟥 QA júnior:<br/>'deu 5% de erro.'"]:::jr
    D --> SR["🟩 QA sênior:<br/>'escala até 100 usuários,<br/>degrada acima disso (latência + erros),<br/>NÃO suporta o pico esperado,<br/>satura com 200.'"]:::sr
    JR --> X["❌ só COLETA o número"]:::ruim
    SR --> V["✅ INTERPRETA e CONTEXTUALIZA"]:::bom
    classDef dado fill:#1c2b3a,stroke:#388bfd,color:#e6edf3,stroke-width:2px;
    classDef jr fill:#3d1d00,stroke:#bd561d,color:#e6edf3;
    classDef sr fill:#0d4429,stroke:#2ea043,color:#e6edf3;
    classDef ruim fill:#3d1d00,stroke:#bd561d,color:#e6edf3;
    classDef bom fill:#0d4429,stroke:#2ea043,color:#e6edf3,stroke-width:2px;
```

---

## ⏭️ Para onde ir agora

- Voltar ao texto do módulo → [[modulo-1/_index|1️⃣ Índice do Módulo 1]]
- As métricas em detalhe → [[modulo-1/02-metricas|📊 Métricas]]
- Diagramas do próximo módulo → [[modulo-2/diagramas|📐 Diagramas — Módulo 2]]
