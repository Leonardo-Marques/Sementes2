---
tipo: conteudo
titulo: Exercício Prático — Simulador de carga em Python
title: Exercício Prático — Simulador de carga em Python
modulo: 1
ordem: 3
fonte: card-2.md + teste-performance.py
data: 2026-06-07
tags: [performance, exercicio, python, threadpool, pratica]
---

# 🧪 Exercício Prático — Simulador de carga em Python

> Nota 3 de 4 do [[modulo-1/_index|Módulo 1]]. Fonte: `card-2.md` + `teste-performance.py`.
> Anterior: [[modulo-1/02-metricas|📊 Métricas]] · Próxima: [[modulo-1/04-implementacao-real|🚀 Implementação real]]

---

## O problema

> [!quote] Do material
> Em um simulador de carga capaz de gerenciar múltiplos usuários concorrentes e executar
> requisições contínuas, analisar a **latência**, a **quantidade de usuários e de
> requisições** que o sistema suporta e, por fim, a **taxa de erros**.

**Estratégia sugerida:**
1. Simular usuários concorrentes;
2. Executar testes com **cargas progressivas**;
3. Coletar métricas;
4. Comparar resultados entre cenários;
5. Identificar limites do sistema.

---

## 🛠️ Como o código funciona

> [!note] Arquivo de referência
> O código completo está em `Modules/1 - Introdução a Testes de Performance/teste-performance.py`
> (idêntico ao que aparece no `card-2.md`). Abaixo, as 6 partes explicadas.

### 1 · Configuração inicial

```python
import requests
import time
import statistics
import random
from concurrent.futures import ThreadPoolExecutor
from threading import Lock

URL = "https://httpbin.org/delay/0.2"
DURACAO = 30 # em segundos
CARGAS = [10, 25, 50, 100, 200]

lock = Lock()

metricas = {
  "latencias": [],
  "requisicoes": 0,
  "erros": 0
}
```

- **`URL`** → endpoint `httpbin.org/delay/0.2` que **simula 200 ms** de resposta;
- **`DURACAO`** → cada cenário roda por 30 segundos;
- **`CARGAS`** → as 5 cargas progressivas (10 → 200 usuários);
- **`lock`** → um [[modulo-1/02-metricas#❌ Taxa de Erro|`Lock`]] para proteger a escrita concorrente no dicionário `metricas`.

### 2 · Simulação de usuário

```python
def usuario(fim_teste):
  global metricas
  while time.time() < fim_teste:
    inicio = time.time()
    try:
      requisicao = requests.get(URL, timeout=3)
      tempo = time.time() - inicio
      with lock:
        metricas["requisicoes"] += 1
        if requisicao.status_code == 200:
          metricas["latencias"].append(tempo)
        else:
          metricas["erros"] += 1
      time.sleep(random.uniform(0.1, 0.5))  # simula comportamento humano
    except Exception as e:
      with lock:
        metricas["erros"] += 1
      print(f"\nErro do tipo: {e}")
```

Cada thread roda em **loop** até o tempo acabar: mede o início, faz o `GET` com `timeout=3`,
calcula o tempo. Dentro do **lock**: conta a requisição; se status 200, guarda a latência;
senão conta erro. Depois espera **0,1–0,5 s aleatório** simulando comportamento humano.
Exceções contam como erro.

### 3 · Executor do teste

```python
def executar_teste(usuarios):
  inicio = time.time()
  fim_teste = inicio + DURACAO
  with ThreadPoolExecutor(max_workers=usuarios) as executor:
    for _ in range(usuarios):
      executor.submit(usuario, fim_teste)
    while time.time() < fim_teste:
      time.sleep(1)
```

Cria um `ThreadPoolExecutor` com **uma thread por usuário** e submete N funções `usuario`.
O thread principal apenas espera até o fim.

### 4 · Reset de métricas

```python
def resetar_metricas():
  metricas["latencias"].clear()
  metricas["requisicoes"] = 0
  metricas["erros"] = 0
```

Zera tudo **entre uma carga e outra** (senão os números se acumulariam).

### 5 · Cálculo de métricas

```python
def analisar_metricas(usuarios):
  latencia = metricas["latencias"]
  if not latencia:
    print("Sem dados.")
    return
  throughput = metricas["requisicoes"] / DURACAO
  latencia_minima = min(latencia)
  latencia_media = statistics.mean(latencia)
  latencia_maxima = max(latencia)
  p95 = statistics.quantiles(latencia, n=100)[94]
  p99 = statistics.quantiles(latencia, n=100)[98]
  taxa_erro = (metricas["erros"] / metricas["requisicoes"]) * 100 if metricas["requisicoes"] else 0
  # ... imprime o bloco RESULTADOS
```

Calcula **throughput**, **latência mín/média/máx**, **p95/p99** (via `quantiles`, índices
`[94]` e `[98]`) e **taxa de erro**, e imprime o bloco `RESULTADOS`.

### 6 · Execução

```python
if __name__ == "__main__":
  for carga in CARGAS:
    print(f"\nTeste com {carga} usuários!")
    resetar_metricas()
    executar_teste(carga)
    analisar_metricas(carga)
```

Para cada carga: **reseta → executa → analisa**.

> [!tip] 💡 Dois pontos para dominar antes da mentoria (complemento)
> - **Por que o `Lock`?** Várias threads escrevem no mesmo dicionário `metricas`. Sem o lock
>   haveria **condição de corrida** na contagem (dois `+= 1` simultâneos podem se perder).
> - **O alvo é o `httpbin.org`** (serviço público externo). Parte dos "erros" em cargas
>   altas pode vir do **próprio httpbin / rede / cliente**, e não de um sistema do mentorado —
>   o que casa com as [[modulo-1/02-metricas#As possibilidades de erro (importante para QA técnico)|causas de erro]]
>   (saturação do cliente, GIL, limite do `requests`). Ótimo gancho de discussão.

→ O fluxo deste código está desenhado nos **[[modulo-1/diagramas|📐 Diagramas]]**.

---

## 📋 O exercício (o que o mentorado entrega)

### 1 — Coleta de dados (rode o teste e preencha)

| Usuários | Requisições | Throughput | Lat. Mín | Lat. Média | Lat. Máx | P95 | P99 | Erros | Taxa de Erro |
|---|---|---|---|---|---|---|---|---|---|
| 10 | | | | | | | | | |
| 25 | | | | | | | | | |
| 50 | | | | | | | | | |
| 100 | | | | | | | | | |
| 200 | | | | | | | | | |

### 2 — Análise de latência
1. A latência cresce conforme aumenta o número de usuários?
2. Existe um ponto de degradação abrupta?
3. A latência máxima indica instabilidade?

### 3 — Análise de requisições
1. O número de requests cresce proporcionalmente aos usuários?
2. Em algum ponto ele estabiliza ou reduz?

### 4 — Análise da taxa de erros
1. Em qual carga começam os erros?
2. Eles crescem linearmente ou abruptamente?

### 5 — Comparação de métricas
1. O aumento de latência impacta nos erros?
2. Existe alguma relação entre throughput e estabilidade?

### 6 — Identificação do limite do sistema
1. Qual a quantidade máxima de usuários antes da degradação?
2. Qual o limite aceitável baseado na latência?
3. Qual o limite aceitável baseado na taxa de erros?

---

## 🎯 Objetivos do exercício (do material)

- Compreender um teste de performance inicial com múltiplos usuários, observando e
  analisando o tempo de resposta e o comportamento do sistema sob cargas diferentes;
- Analisar e **correlacionar** métricas fundamentais, identificando gargalos e determinando
  a capacidade do sistema simulado.

> [!important] Lembre o fecho da teoria
> O objetivo do exercício **não** é só preencher a tabela — é produzir a análise de um
> **[[modulo-1/02-metricas#🎓 O que esperar da análise do QA?|QA sênior]]**: interpretar e contextualizar os números.

---

## ⏭️ Para onde ir agora

- Aplicar no trabalho real → [[modulo-1/04-implementacao-real|🚀 Implementação real]]
- Rever as métricas → [[modulo-1/02-metricas|📊 Métricas]]
- Voltar ao índice → [[modulo-1/_index|1️⃣ Índice do Módulo 1]]
