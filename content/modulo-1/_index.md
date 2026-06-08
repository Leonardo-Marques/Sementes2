---
tipo: indice-modulo
titulo: Módulo 1 — Introdução a Testes de Performance
title: "1️⃣ Módulo 1 — Introdução"
modulo: 1
projeto: sementes-2
data: 2026-06-07
tags: [performance, qa, istqb, introducao, indice, unicred]
---

# 1️⃣ Introdução a Testes de Performance — índice do módulo

> Porta de entrada do **Módulo 1**. Daqui você navega pelas 4 notas de conteúdo na ordem
> sugerida da mentoria. Base teórica: **ISTQB CT-PT**. Prática: **Python** (`requests` + `ThreadPoolExecutor`).

> 👉 Perdido no todo? Veja o **[[🧭 COMECE AQUI]]** ou o **[[mapa-visual|🗺️ Mapa Visual]]**.

Voltar pro [[00-MOC|Mapa de Conteúdo]] · Próximo módulo: [[modulo-2/_index|2️⃣ Teste de Carga]]

---

## O que é, em uma frase

O módulo-**fundação**: o que é teste de performance, seus **3 pilares** (tempo, capacidade,
recursos), os **7 tipos**, as **métricas** principais e o **primeiro teste real** em Python,
simulando múltiplos usuários e analisando o comportamento sob cargas progressivas.

## 🎯 Objetivos do módulo (do material)

- Compreender os diferentes tipos de testes de performance;
- Introdução às principais métricas;
- Possibilitar a criação dos primeiros testes reais usando Python;
- Praticar a coleta e a análise de métricas relevantes.

---

## 📚 As notas deste módulo (ordem da mentoria)

| # | Nota | Pra quê | Fonte original |
|---|---|---|---|
| 1 | [[modulo-1/01-o-que-e-performance\|🏛️ O que é performance]] | Definição, os 3 pilares, por que fazer, os 7 tipos, planejamento, critérios | `card-1.md` |
| 2 | [[modulo-1/02-metricas\|📊 Métricas]] | Cada métrica em detalhe: requisições, latência, throughput, percentis, carga, taxa de erro | `metricas-1.md` |
| 3 | [[modulo-1/03-exercicio-pratico\|🧪 Exercício prático]] | O simulador em Python puro (6 partes) + tabela + 6 blocos de análise | `card-2.md` + `teste-performance.py` |
| 4 | [[modulo-1/04-implementacao-real\|🚀 Implementação real]] | Aplicar no cenário de trabalho do mentorado (7 passos) | `card-3.md` |

## 📐 Diagramas

→ **[[modulo-1/diagramas|📐 Diagramas do Módulo 1]]** — os 3 pilares, os 7 tipos,
o fluxo do exercício e a relação entre métricas. *(No Obsidian, também em plano navegável:
[[modulo-1/diagramas.canvas|Canvas]], pan + zoom.)*

---

## 🔗 Referências e materiais complementares (do material)

- [Vídeo — Teste de Performance: entenda os 6 tipos](https://www.youtube.com/watch?v=HhShUc9OarE)
- [Vídeo — Throughput vs Latency](https://www.youtube.com/watch?v=84ZLMbHefJI)
- [Vídeo — Understanding API Performance Testing](https://www.youtube.com/watch?v=6LzOYfufMoU)
- [Vídeo — 4 Scenario based interview Ques | Performance Testing](https://youtu.be/LsOZ40VCzP8)
- [Documentação — Certificação CT-PT](https://bstqb.online/ct-pt)

> 💡 **Nota do mentor:** o tópico **Percentis (p95/p99)** no material original (`metricas-1.md`)
> está marcado como *"Em construção..."*. A nota [[modulo-1/02-metricas#📈 Percentis (p95 e p99)|📊 Métricas]]
> traz um **complemento** preenchendo essa lacuna (sinalizado com callout).
