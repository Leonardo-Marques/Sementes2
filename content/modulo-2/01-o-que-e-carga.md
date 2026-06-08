---
tipo: conteudo
titulo: O que é Teste de Carga
title: O que é Teste de Carga
modulo: 2
ordem: 1
fonte: card-1.md
data: 2026-06-07
tags: [performance, carga, load-testing, conceitos]
---

# 🏛️ O que é Teste de Carga

> Nota 1 de 4 do [[modulo-2/_index|Módulo 2]]. Fonte: `card-1.md` (Material de Estudo).
> Anterior: — · Próxima: [[modulo-2/02-definindo-metricas|📊 Definindo métricas]]

---

## O que é teste de carga?

> [!quote] Definição do material
> Teste de carga avalia como o sistema, ou fluxo, se comporta sob uma carga **esperada** de
> usuários simultâneos, validando métricas como o tempo de resposta (latência), a
> estabilidade, a capacidade de processamento e a taxa de erros.

> [!important] A característica que o define
> Diferente de outros tipos de teste de performance, no teste de carga o cenário a ser
> testado **deve estar dentro do limite da aplicação**. (Isso o separa do
> [[modulo-1/01-o-que-e-performance#🗂️ Os 7 tipos de teste de performance|estresse e do pico]].)

---

## Por que fazer?

### 1. 🔍 Detecção precoce de problemas
Revelam problemas de desempenho (lentidão, limitações de recursos) **antes que afetem
usuários reais**, permitindo otimização proativa e ajuste fino.

### 2. 📏 Estabelecimento de linha de base
Ajudam a criar **linhas de base** de desempenho, permitindo comparar e analisar o
comportamento do sistema **ao longo do tempo**. Útil para testes e melhorias futuras.

### 3. 📐 Planejamento de capacidade
Simulando cargas realistas, auxiliam a organização a determinar se o sistema **aguenta o
número esperado** de usuários e transações **sem degradação**.

---

## ⚙️ O conceito de geração de carga

As cargas representativas devem ser **modeladas, geradas e submetidas** ao sistema em teste.
São comparáveis às entradas de dados dos testes funcionais, **mas diferem** em três pontos:

- Uma carga de performance deve representar **muitas entradas** de usuário, não apenas uma;
- Pode exigir **hardware e ferramentas dedicados** para geração;
- Depende da **ausência de defeitos funcionais** no sistema que possam afetar a execução do teste.

> [!tip] Gancho para o exercício
> "Hardware e ferramentas dedicados" é justamente o que motiva o uso do **Locust** e o
> **dimensionamento proporcional** (ver [[modulo-2/03-exercicio-locust|🦗 Exercício]]).

---

## 🎯 Objetivos do módulo (do material)

- Compreender os conceitos de teste de carga, identificando oportunidades e vantagens;
- Aprofundar os conhecimentos sobre definição das métricas baseadas no ambiente a ser testado.

---

## ⏭️ Para onde ir agora

- Como escolher as métricas → [[modulo-2/02-definindo-metricas|📊 Definindo métricas]]
- Ver o quadro completo → [[modulo-2/diagramas|📐 Diagramas]]
- Voltar ao índice → [[modulo-2/_index|2️⃣ Índice do Módulo 2]]
