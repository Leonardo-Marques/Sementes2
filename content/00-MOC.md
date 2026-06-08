---
tipo: moc
titulo: Mentoria Sementes 2 — Mapa de Conteúdo
title: Mentoria Sementes 2 — Mapa de Conteúdo
data: 2026-06-07
tags: [moc, indice, performance, mentoria, unicred]
---

# 🗺️ Sementes 2 — Mapa de Conteúdo (MOC)

> Porta de entrada do cofre. Daqui você navega por **assunto**. Mentoria de **QA — Teste de
> Performance** para a **Unicred**. Base teórica: **ISTQB CT-PT**.

> 👉 **Prefere um guia por tarefa?** Comece pelo **[[🧭 COMECE AQUI]]**.
> **Prefere visual?** Abra o **[[mapa-visual|🗺️ Mapa Visual]]**.

Este cofre cobre, por enquanto, os **Módulos 1 e 2**. O material-fonte completo (os 6
módulos originais) fica em `Modules/`.

---

## 🧭 Os módulos cobertos

| Módulo | O que é | Ferramenta | Entrada |
|---|---|---|---|
| **1️⃣ Introdução** | Conceitos, 3 pilares, 7 tipos, métricas, 1º teste real | Python puro (`requests` + `ThreadPoolExecutor`) | [[modulo-1/_index\|índice]] |
| **2️⃣ Teste de Carga** | Carga esperada, dentro do limite; como escolher métricas | **Locust** | [[modulo-2/_index\|índice]] |

**A relação entre eles:** o Módulo 1 ensina os **conceitos e o experimento manual**; o
Módulo 2 reaplica o mesmo experimento com **ferramenta profissional** e aprofunda a
**definição de métricas**.

---

## 🔥 Grandes temas

### Conceitos fundamentais (Módulo 1)
- [[modulo-1/01-o-que-e-performance|🏛️ O que é performance]] — os 3 pilares e os 7 tipos
- [[modulo-1/02-metricas|📊 Métricas]] — latência, throughput, percentis, taxa de erro

### Métricas (os dois módulos)
- [[modulo-1/02-metricas|📊 O que cada métrica é]] (Módulo 1)
- [[modulo-2/02-definindo-metricas|📊 Como escolher quais coletar]] (Módulo 2: técnico / negócio / operacional)

### Prática
- [[modulo-1/03-exercicio-pratico|🧪 Simulador em Python puro]] (ThreadPoolExecutor)
- [[modulo-2/03-exercicio-locust|🦗 Simulador com Locust]] (interface web + headless + CSV)
- [[modulo-1/04-implementacao-real|🚀 Aplicar no trabalho (Módulo 1)]] · [[modulo-2/04-implementacao-real|🚀 (Módulo 2)]]

### A lição que costura tudo
- [[modulo-1/02-metricas#🎓 O que esperar da análise do QA?|🎓 QA júnior vs QA sênior]] — coletar o número **vs** interpretar e contextualizar

---

## 📐 Diagramas

- [[modulo-1/diagramas|📐 Diagramas — Módulo 1]] (3 pilares · 7 tipos · fluxo do código · júnior vs sênior) — *no Obsidian também em [[modulo-1/diagramas.canvas|Canvas]]*
- [[modulo-2/diagramas|📐 Diagramas — Módulo 2]] (carga vs estresse vs pico · dimensionamento · ciclo Locust · execução) — *no Obsidian também em [[modulo-2/diagramas.canvas|Canvas]]*

---

## 📐 Convenções do cofre

- **Links**: wikilinks nativos `[[nome]]` (com alias `[[nome|texto]]` quando útil).
- **Fonte fiel**: cada nota indica no topo (`fonte:`) o arquivo original de `Modules/` que ela
  resume. O texto segue o material; adições do mentor vêm em callout **💡 Complemento**.
- **Diagramas**: Mermaid em notas `diagramas.md` (renderizam no site publicado) e também nos
  `.canvas` (versão navegável no Obsidian).
- **Lacunas conhecidas do material**: p95/p99 ("Em construção" no original) foi complementado;
  inconsistências do Locust (nome de arquivo, http/https, P95 no CSV) estão sinalizadas no
  [[modulo-2/_index|índice do Módulo 2]].
