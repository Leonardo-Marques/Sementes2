---
tipo: conteudo
titulo: O que é Teste de Performance
title: O que é Teste de Performance
modulo: 1
ordem: 1
fonte: card-1.md
data: 2026-06-07
tags: [performance, qa, istqb, conceitos, pilares, tipos]
---

# 🏛️ O que é Teste de Performance

> Nota 1 de 4 do [[modulo-1/_index|Módulo 1]]. Fonte: `card-1.md` (Material de Estudo).
> Anterior: — · Próxima: [[modulo-1/02-metricas|📊 Métricas]]

---

## O que é teste de performance?

> [!quote] Definição do material
> Teste de performance é um tipo de teste que **verifica se um aplicativo ou sistema
> consegue funcionar bem quando está sendo usado.**

Ele avalia **três aspectos principais** — os **3 pilares** que voltam o módulo inteiro:

### 1. ⏱️ Comportamento do Tempo (velocidade de resposta)
O objetivo **mais comum**. Mede o quanto um sistema ou componente leva para responder a
uma entrada do usuário em condições específicas. As medições variam desde o tempo total
**ponta-a-ponta** até o número de **ciclos de processador** necessários para uma tarefa.
→ Vira a métrica **[[modulo-1/02-metricas#⏱️ Latência|latência]]**.

### 2. 📦 Capacidade (gargalos, falhas etc.)
Testa como o sistema se comporta nos seus **limites de operação**: qual o número máximo de
usuários simultâneos? Quanto volume de dados consegue processar? Serve para validar se a
**arquitetura** é adequada.
→ Vira **[[modulo-1/02-metricas#🚀 Throughput|throughput]]** e **[[modulo-1/02-metricas#👥 Quantidade de Usuários (carga)|usuários simultâneos]]**.

### 3. 🧠 Utilização de Recursos (memória RAM e processador)
Quando os recursos disponíveis (RAM limitada, por exemplo) são um **risco**, testa-se como
o sistema os utiliza. Isso **evita desperdícios e identifica gargalos**.

> [!info] Vale para qualquer sistema
> Site, app mobile, sistema em nuvem ou até programas embarcados. O **objetivo final** é
> garantir **boa experiência ao usuário**, não importa o dispositivo (celular, tablet,
> computador) nem as condições de uso.

---

## Por que fazer?

Ajuda a identificar e resolver problemas que aparecem quando o sistema está **sob pressão
ou carregamento** (muitos usuários simultâneos ou processando grandes volumes de dados).
Os testes ajudam a:

- ✅ Confirmar que o sistema responde **dentro do tempo esperado**;
- ✅ Verificar se usa bem os recursos disponíveis (memória, processador);
- ✅ Garantir que a **qualidade funcional e a usabilidade se mantêm sob carga**;
- ✅ Definir **expectativas claras** para usuários e stakeholders;
- ✅ Tomar **decisões informadas sobre a arquitetura** do sistema.

> [!tip] São experimentação iterativa
> Os testes assumem a forma de **experimentação** e podem ser conduzidos de forma
> **iterativa** — executados durante análise, desenho e implementação, para que decisões
> de arquitetura sejam tomadas com base em **dados reais**.

Podem ser feitos em sistemas **completos ou parciais**, em ambientes **similares ao de
produção**, para responder perguntas como:

- Quantos usuários simultâneos o sistema suporta?
- O tempo de resposta continua aceitável sob carga?
- Onde estão os gargalos (back-end, banco, rede)?
- O sistema degrada de forma controlada?

---

## 🗂️ Os 7 tipos de teste de performance

O material divide os testes de performance em sete tipos. **Cinco viram módulos** desta mentoria:

| Tipo | Foco | Módulo |
|---|---|---|
| **Teste de carga** | Comportamento **esperado** | → [[modulo-2/_index\|Módulo 2]] |
| **Teste de estresse** | **Além** do limite | → Módulo 3 |
| **Teste de escalabilidade** | Capacidade de expansão | _(só citado aqui)_ |
| **Teste de pico** | Variações **bruscas** | → Módulo 4 |
| **Teste de resistência** | **Longo** período | → Módulo 5 |
| **Teste de concorrência** | Conflitos **simultâneos** | → Módulo 6 |
| **Teste de capacidade** | Quantidade suportada | _(só citado aqui)_ |

> [!warning] Atenção na hora de explicar
> A lista tem **7 tipos**, mas a mentoria só tem módulos para **5**. *Escalabilidade* e
> *capacidade* aparecem apenas nesta introdução, sem módulo próprio.

→ Visual dos 7 tipos no **[[modulo-1/diagramas|📐 Diagramas]]**.

---

## Como planejar?

Stakeholders diferentes têm **objetivos diferentes**. Boa prática: **distinguir objetivos
técnicos de objetivos de usuário**.

> [!note] 🔧 Objetivos técnicos
> Focam nos aspectos **operacionais**: capacidade de escalonamento, sob quais condições a
> **degradação** da performance se torna aparente.

> [!note] 🙋 Objetivos de usuário
> Focam na **satisfação do usuário final** e nos **objetivos de negócio**. O usuário está
> menos preocupado com recursos ou como o produto é entregue — ele só quer **conseguir
> fazer o que precisa fazer**.

Os principais objetivos do teste de performance incluem: **identificar riscos potenciais,
descobrir oportunidades de melhoria e identificar as mudanças necessárias.**

---

## ✔️ Pontos importantes (critérios de um bom teste)

- 🎯 **Alinhados** com as expectativas dos stakeholders (usuários finais, arquitetos, operações);
- 🔁 **Reprodutíveis** — repetir no mesmo sistema sem alterações deve dar resultados
  **praticamente idênticos** (dentro de uma tolerância definida);
- 📊 **Compreensíveis e comparáveis** com as expectativas dos stakeholders;
- 🧪 Realizáveis em sistemas completos/parciais ou ambientes **similares à produção**;
- 💰 **Viáveis, acessíveis e executáveis** dentro do prazo e orçamento do projeto.

---

## 📊 Principais métricas (visão geral)

Primeiro contato com as métricas — cada uma é detalhada na nota **[[modulo-1/02-metricas|📊 Métricas]]**.

| Métrica | O que significa | Importância |
|---|---|---|
| **Latência** | Tempo de resposta por requisição | Experiência do usuário |
| **Throughput** | Quantidade de requests ou transações | Capacidade do sistema |
| **Taxa de erro** | Porcentagem de falhas | Estabilidade do sistema |
| **Percentis (p95, p99)** | Distribuição real | Evitar médias enganosas |
| **Usuários simultâneos** | Concorrência ativa | Análise de cenários reais |
| **Uso de Recursos** | Memória RAM e processador | Identificação de gargalos |

---

## ⏭️ Para onde ir agora

- Aprofundar cada métrica → [[modulo-1/02-metricas|📊 Métricas]]
- Ver o quadro completo → [[modulo-1/diagramas|📐 Diagramas]]
- Voltar ao índice → [[modulo-1/_index|1️⃣ Índice do Módulo 1]]
