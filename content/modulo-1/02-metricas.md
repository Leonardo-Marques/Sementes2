---
tipo: conteudo
titulo: Introdução a Métricas
title: Introdução a Métricas
modulo: 1
ordem: 2
fonte: metricas-1.md
data: 2026-06-07
tags: [performance, metricas, latencia, throughput, percentis, taxa-erro]
---

# 📊 Introdução a Métricas

> Nota 2 de 4 do [[modulo-1/_index|Módulo 1]]. Fonte: `metricas-1.md`. É o **coração técnico**
> do módulo — vale gastar bastante tempo aqui na mentoria.
> Anterior: [[modulo-1/01-o-que-e-performance|🏛️ O que é performance]] · Próxima: [[modulo-1/03-exercicio-pratico|🧪 Exercício]]

---

## Por que as métricas são necessárias?

> [!quote] Princípio do material
> Medições precisas e suas métricas derivadas são **essenciais** para definir os objetivos
> do teste e avaliar seus resultados. **O teste de performance não deve ser realizado sem
> primeiro entender quais medidas e métricas serão necessárias.**

### ⚠️ Riscos de NÃO usar métricas
- Não se sabe se os níveis de performance serão aceitáveis para os objetivos operacionais;
- Os requisitos de performance não são definidos em termos **mensuráveis**;
- Pode não ser possível identificar **tendências** que prevejam queda de performance;
- Os resultados não podem ser avaliados (falta um conjunto de medidas que defina
  aceitável/inaceitável);
- A avaliação vira **opinião subjetiva** de uma ou mais pessoas;
- Os resultados da ferramenta **não são compreendidos**.

---

## 🔢 Quantidade de Requisições

Total de requisições feitas durante o teste — representa o **volume total de trabalho**
executado.

> [!important] Afirmação específica do material
> Essa quantidade tende a **diminuir** conforme aumenta o número de usuários.

| Interpretação | Significa |
|---|---|
| Mais requisições | Maior capacidade do sistema |
| Menos requisições | Sistema pode estar saturado |

**Perguntas que responde:** Quantos clientes conseguem usar o sistema simultaneamente?
O sistema aguenta crescimento de carga?

---

## ⏱️ Latência

O **tempo de resposta** que uma requisição leva para sair do cliente, chegar no servidor,
ser processada e voltar com a resposta. Divide-se em três:

| Tipo | O que indica |
|---|---|
| **Latência mínima** | A experiência **ideal**, provavelmente devido a baixa carga |
| **Latência média** | Tempo médio de **todas** as requisições — boa visão geral, **mas pode esconder problemas** |
| **Latência máxima** | A **pior** experiência possível — indica picos e instabilidades |

> [!warning] Cuidado com a média
> "Média boa **não significa** sistema saudável" — uma média boa pode esconder que **alguns
> usuários estão sofrendo muito**. É exatamente o que os [[#📈 Percentis (p95 e p99)|percentis]] revelam.

**Interpretações:**
- Latência alta → cliente acha o app lento;
- Latência inconsistente → sensação de instabilidade;
- Latência alta em saldo → impacto direto na **confiança** _(exemplo bancário — contexto Unicred)_.

---

## 🚀 Throughput

A **quantidade de requisições por segundo** — indica a capacidade de processamento do
sistema e ajuda a definir o **limite real**.

| Comportamento | Significa |
|---|---|
| Cresce com o nº de usuários | Sistema **saudável** |
| Estabiliza conforme aumentam usuários | Sistema **saturando** |
| Diminui com o nº de usuários | Sistema **degradando** |

**Perguntas que responde:** Quantas req/s o sistema suporta? Com quantas req/s ele começa
a degradar?

---

## 📈 Percentis (p95 e p99)

Uma forma de entender melhor a **distribuição** dos tempos de resposta — mais eficiente que
a latência média.

> [!quote] No material original
> *"Em construção..."* — este tópico está **incompleto** no `metricas-1.md`.

> [!tip] 💡 Complemento (não estava no material original)
> **Percentil** = o valor abaixo do qual cai uma certa porcentagem das medições, depois de
> ordená-las.
> - **p95** → 95% das requisições responderam **nesse tempo ou menos**; só os **5% piores**
>   ficaram acima.
> - **p99** → 99% responderam nesse tempo ou menos; só o **1% pior** ficou acima.
>
> **Por que importa:** a média esconde a "cauda" lenta. Exemplo: se 100 usuários têm
> resposta de 0,2 s mas 1 usuário levou 8 s, a **média** mal se mexe — mas o **p99** denuncia
> esse usuário que teve péssima experiência. Por isso o [[modulo-1/01-o-que-e-performance#📊 Principais métricas (visão geral)|card-1]]
> resume o papel dos percentis como **"evitar médias enganosas"**.
>
> No código do exercício, p95/p99 são calculados com
> `statistics.quantiles(latencia, n=100)` pegando os índices `[94]` e `[98]`. ⚠️ Com poucas
> amostras esse cálculo é menos preciso — vale comentar isso na mentoria.

---

## 👥 Quantidade de Usuários (carga)

A quantidade **simulada de usuários simultâneos** usando determinado fluxo. Diferente do
número de requisições, representa a **concorrência** do sistema.

| Carga | Comportamento |
|---|---|
| Baixa | Comportamento **ideal** |
| Alta | Comportamento **real** |
| Muito alta | **Limite** do sistema |

**Perguntas que responde:** Quantos clientes simultâneos o app suporta? O sistema aguenta
horário de pico?

---

## ❌ Taxa de Erro

O percentual de requisições que **falharam**. Normalmente relacionado a alta latência,
saturação do sistema ou falha de algum recurso (cliente e/ou servidor).

| Taxa | Leitura |
|---|---|
| **0%** | O cenário **ideal** |
| **< 1%** | Aceitável (dependendo do sistema) |
| **> 1%** | Sinal de **alerta** |
| **Alto** | Sistema **instável** |

### As possibilidades de erro (importante para QA técnico)

- **🕐 Timeout (mais comum):** sob sobrecarga, as respostas demoram mais e algumas passam
  do timeout configurado;
- **🖥️ Saturação do servidor:** o serviço pode não aguentar testes pesados, limitando
  conexões e gerando erros/lentidão;
- **💻 Saturação do cliente:** testes pesados podem saturar a **própria máquina de teste**
  (CPU, RAM, limite de threads, conexões TCP, pool de sockets do SO), fazendo a requisição
  **falhar antes mesmo de sair do cliente**;
- **📚 Limite da biblioteca `requests`:** ela usa o `urllib3`, com pool de conexões limitado
  e reuso de conexão nem sempre eficiente;
- **🐍 Overhead de threads (GIL):** Python usa o **GIL (Global Interpreter Lock)**, que não
  escala threads perfeitamente (200 threads pode não representar 200 execuções paralelas
  reais), o que pode causar lentidão nas respostas.

> [!tip] Por que isso é decisivo na mentoria
> Os três últimos itens (cliente, `requests`, GIL) explicam **por que o exercício do
> Módulo 1, feito em Python puro com threads, tem limitações** — e é exatamente o que
> justifica a migração para o **Locust** no [[modulo-2/_index|Módulo 2]].

**Perguntas que responde:** O sistema aguenta horário de pico? Vai falhar no dia de
pagamento? Quantos usuários simultâneos são seguros?

---

## 🔗 Relacionando Métricas

> [!info] O comportamento esperado sob carga crescente
> À medida que a carga aumenta: a **latência aumenta**, o **throughput aumenta (até certo
> ponto)**, os **erros começam a aparecer**, e o **throughput estabiliza ou começa a cair**.

Exemplo de resultado (tabela do material):

| Usuários | Latência | Throughput | Erros |
|---|---|---|---|
| 10 | Baixa | Baixo | 0% |
| 50 | Média | Alto | 0% |
| 100 | Alta | Muito alto | 1% |
| 200 | Muito alta | Estável | 5% |

→ Esse padrão está desenhado nos **[[modulo-1/diagramas|📐 Diagramas]]**.

---

## 🎓 O que esperar da análise do QA?

> [!quote] A mensagem central do módulo
> **QA júnior:** "deu 5% de erro."
>
> **QA sênior:** "o sistema segue escalando até 100 usuários e começa a degradar acima de
> 100 usuários com o aumento da latência e número de erros, **não suportando o pico de
> acesso esperado** e indicando **saturação com 200 usuários**."

> [!important] Fecho da teoria
> A diferença não está em **coletar** o número, e sim em **interpretar e contextualizar**.
> Esse é o ponto pedagógico que conecta toda a teoria ao [[modulo-1/03-exercicio-pratico|exercício prático]].

---

## ⏭️ Para onde ir agora

- Colocar a mão na massa → [[modulo-1/03-exercicio-pratico|🧪 Exercício prático]]
- Rever os conceitos → [[modulo-1/01-o-que-e-performance|🏛️ O que é performance]]
- Voltar ao índice → [[modulo-1/_index|1️⃣ Índice do Módulo 1]]
