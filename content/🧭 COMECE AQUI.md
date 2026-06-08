---
tipo: guia-navegacao
titulo: Comece aqui — guia da mentoria Sementes 2
title: Comece aqui — guia da mentoria Sementes 2
data: 2026-06-07
tags: [navegacao, guia, entrada, performance, mentoria]
---

# 🧭 Comece aqui

> A porta de entrada **para humano**. Prefere ver o todo de forma visual? Abra o
> **[[mapa-visual|🗺️ Mapa Visual]]**. Prefere a lista completa? Veja o
> [[00-MOC|MOC]]. Esta nota acha o que você precisa **pela pergunta que você chega fazendo.**

---

## Em 10 segundos: o que é este lugar

Material da **mentoria Sementes 2** — **QA / Teste de Performance** para a **Unicred**,
organizado para Obsidian. Cobre os **Módulos 1 e 2**.

> **1️⃣ Conceitos + teste manual em Python** → **2️⃣ o mesmo, com Locust + métricas a fundo.**

- **1️⃣ [[modulo-1/_index|Introdução a Testes de Performance]]** — o quê, por quê, métricas, 1º teste.
- **2️⃣ [[modulo-2/_index|Teste de Carga]]** — carga esperada, dentro do limite, com Locust.

Cada módulo tem **4 notas** (teoria → métricas → exercício → implementação real) + uma nota
de **diagramas**.

---

## O que você quer fazer agora?

| Eu quero… | Módulo 1 (Python) | Módulo 2 (Locust) |
|---|---|---|
| **Entender o conceito** | [[modulo-1/01-o-que-e-performance\|🏛️ o que é performance]] | [[modulo-2/01-o-que-e-carga\|🏛️ o que é carga]] |
| **Aprender as métricas** | [[modulo-1/02-metricas\|📊 métricas (o quê)]] | [[modulo-2/02-definindo-metricas\|📊 definir métricas (como)]] |
| **Colocar a mão na massa** | [[modulo-1/03-exercicio-pratico\|🧪 exercício Python]] | [[modulo-2/03-exercicio-locust\|🦗 exercício Locust]] |
| **Aplicar no meu trabalho** | [[modulo-1/04-implementacao-real\|🚀 implementação real]] | [[modulo-2/04-implementacao-real\|🚀 implementação real]] |
| **Ver os diagramas** | [[modulo-1/diagramas\|📐 Diagramas M1]] | [[modulo-2/diagramas\|📐 Diagramas M2]] |

---

## 🎓 Se você só puder levar uma ideia da mentoria

> [!important] A diferença entre QA júnior e sênior
> **Júnior:** "deu 5% de erro."
> **Sênior:** "escala até 100 usuários, degrada acima disso, não suporta o pico esperado,
> satura com 200." → **Não é coletar o número, é interpretá-lo.**
> Detalhe em [[modulo-1/02-metricas#🎓 O que esperar da análise do QA?|📊 Métricas]].

---

## Como o cofre está organizado

```
📁 _cofre-mentoria/
   🧭 COMECE AQUI · 00-MOC · mapa-visual   ← você está aqui
   📁 modulo-1/   ← 1️⃣ Introdução (Python)
      _index · 01-o-que-e-performance · 02-metricas
      03-exercicio-pratico · 04-implementacao-real · diagramas
   📁 modulo-2/   ← 2️⃣ Teste de Carga (Locust)
      _index · 01-o-que-e-carga · 02-definindo-metricas
      03-exercicio-locust · 04-implementacao-real · diagramas
```

> 💡 **Regra de ouro:** em cada módulo, comece pelo **`_index`** (mapa do módulo) e siga a
> ordem numérica das notas. O material-fonte original continua em `Modules/` (fora do cofre).

> ⚠️ **Sobre fidelidade ao material:** cada nota cita no topo (`fonte:`) o arquivo original
> que resume. Onde o mentor acrescentou algo que **não estava** no original, há um callout
> **💡 Complemento** — assim você sabe o que é fonte e o que é adição.
