---
tipo: indice-modulo
titulo: Módulo 2 — Teste de Carga
title: "2️⃣ Módulo 2 — Teste de Carga"
modulo: 2
projeto: sementes-2
data: 2026-06-07
tags: [performance, qa, carga, load-testing, locust, indice, unicred]
---

# 2️⃣ Teste de Carga — índice do módulo

> Porta de entrada do **Módulo 2**. A grande mudança em relação ao [[modulo-1/_index|Módulo 1]]:
> sai o Python puro, **entra o Locust** (ferramenta profissional de teste de performance).

> 👉 Perdido no todo? Veja o **[[🧭 COMECE AQUI]]** ou o **[[mapa-visual|🗺️ Mapa Visual]]**.

Voltar pro [[00-MOC|Mapa de Conteúdo]] · Módulo anterior: [[modulo-1/_index|1️⃣ Introdução]]

---

## O que é, em uma frase

Avaliar como o sistema se comporta sob a carga **esperada** de usuários simultâneos (dentro
do limite da aplicação), agora medindo com o **Locust** — com interface web, coleta
automática de métricas e dimensionamento proporcional ao ambiente.

## 🎯 Objetivos do módulo (do material)

- Compreender os conceitos de teste de carga, identificando oportunidades e vantagens;
- Aprofundar os conhecimentos sobre **definição das métricas** baseadas no ambiente a testar.

---

## 📚 As notas deste módulo (ordem da mentoria)

| # | Nota | Pra quê | Fonte original |
|---|---|---|---|
| 1 | [[modulo-2/01-o-que-e-carga\|🏛️ O que é teste de carga]] | Definição, por que fazer, geração de carga | `card-1.md` |
| 2 | [[modulo-2/02-definindo-metricas\|📊 Definindo métricas]] | Como escolher métricas: ambiente técnico, de negócio e operacional | `metricas-2.md` |
| 3 | [[modulo-2/03-exercicio-locust\|🦗 Exercício com Locust]] | Locust na prática + dimensionamento + modo web/headless + CSV | `card-2.md` + `teste-carga.py` |
| 4 | [[modulo-2/04-implementacao-real\|🚀 Implementação real]] | Aplicar um teste de carga no cenário do mentorado (6 passos) | `card-3.md` |

## 📐 Diagramas

→ **[[modulo-2/diagramas|📐 Diagramas do Módulo 2]]** — Carga vs Estresse vs Pico,
o dimensionamento proporcional, o ciclo de um usuário Locust e o fluxo de execução.
*(No Obsidian, também em plano navegável: [[modulo-2/diagramas.canvas|Canvas]].)*

---

## 🔗 Referências e materiais complementares (do material)

- [Artigo — Load Testing vs. Stress Testing](https://www.loadview-testing.com/learn/load-testing-vs-stress-testing/)
- [Artigo — Playwright Load Testing](https://www.loadview-testing.com/blog/playwright-load-testing/)
- [Vídeo — Getting started with API Load Testing](https://youtu.be/r-Jte8Y8zag)
- [Documentação — Certificação CT-PT](https://bstqb.online/ct-pt)

> [!warning] ⚠️ Inconsistências no material original (avise o mentorado)
> - O card manda salvar como **`teste_carga.py`** (`locust -f teste_carga.py`), mas o
>   `run_tests.py` aponta para **`locustfile.py`** — nomes diferentes.
> - O `host` no arquivo é **`http://httpbin.org`**, mas no `run_tests.py` o `HOST` é
>   **`https://httpbin.org`** (http × https).
> - A tabela do exercício pede **P95 e P99**, mas a lista de colunas do CSV do Locust
>   descrita no card **não os inclui** (o Locust mostra percentis em outra parte do relatório).
