---
tipo: conteudo
titulo: Exercício com Locust
title: Exercício com Locust
modulo: 2
ordem: 3
fonte: card-2.md + teste-carga.py
data: 2026-06-07
tags: [performance, exercicio, locust, carga, dimensionamento, ccu]
---

# 🦗 Exercício com Locust

> Nota 3 de 4 do [[modulo-2/_index|Módulo 2]]. Fonte: `card-2.md` + `teste-carga.py`.
> Anterior: [[modulo-2/02-definindo-metricas|📊 Definindo métricas]] · Próxima: [[modulo-2/04-implementacao-real|🚀 Implementação real]]

---

## 🎯 O objetivo do teste de carga

> [!quote] Do material
> O teste de carga simula o comportamento real do sistema sob a quantidade de usuários e
> requisições esperadas **em produção**. O objetivo é **validar se o sistema mantém
> performance e estabilidade** quando submetido à carga típica do negócio.

---

## 📐 A regra de ouro: dimensionamento proporcional

> [!important] Baseie-se em dados reais de produção
> Os testes devem ser proporcionais ao **hardware disponível** no ambiente de teste.

- **Mapeie o pico de usuários simultâneos** em produção (ex.: 5.000 **CCU** — *Concurrent Users*);
- **Faça o ramp up não ser brusco** (ex.: o teste levar 10 min até o máximo de usuários);
- **Calcule a proporção** do seu ambiente (se o servidor de teste tem 25% dos recursos de
  produção, simule 25% da carga → 1.250 usuários);
- **Use o mesmo perfil de requisições** (endpoints, tipos de dados, frequência);
- **Mantenha a proporção de recursos** (CPU, memória, banda de rede).

> [!example] Exemplo do material
> Produção com **10 CPUs e 64 GB**; laboratório com **2 CPUs e 8 GB** (≈ **20% dos
> recursos**) → simule **~20% da carga** de produção.

---

## 🦗 Por que Locust (e não o código do Módulo 1)?

**Locust** é uma ferramenta open source escrita em Python, feita para testes de performance.
Diferente do [[modulo-1/03-exercicio-pratico|exemplo anterior]] (com `ThreadPoolExecutor`), ele fornece:

- Simulação **escalável** de múltiplos usuários concorrentes;
- **Interface web** para monitoramento em tempo real;
- **Coleta automática** de métricas detalhadas;
- Sintaxe **simples e intuitiva**;
- Suporte a diferentes **estratégias de geração de carga**.

> [!tip] Conexão com o Módulo 1
> Lembra das [[modulo-1/02-metricas#As possibilidades de erro (importante para QA técnico)|limitações]]
> do Python puro (GIL, pool do `requests`, saturação do cliente)? O Locust existe justamente
> para contorná-las.

---

## 🛠️ A implementação

```python
from locust import HttpUser, task, between

class PerformanceUser(HttpUser):
    """Define o comportamento de um usuário simultâneo."""

    host = "http://httpbin.org"      # URL base para as requisições
    wait_time = between(0.1, 0.5)    # tempo de espera (simula humano)

    @task
    def fazer_requisicao(self):
        # /delay/0.2 simula um serviço com 200ms de resposta
        with self.client.get("/delay/0.2", catch_response=True) as response:
            if response.status_code != 200:
                response.failure(f"Status: {response.status_code}")
```

**Os 3 componentes do Locust:**
- **`HttpUser`** → classe base que simula um usuário que faz requisições HTTP;
- **`@task`** → decorador que marca um método como tarefa executada **repetidamente**;
- **`between()`** → define o intervalo de espera entre execuções de tasks.

**Configuração da classe:**
- **`host`** → URL base; todas as requisições começam por ela. Precisa existir em algum
  lugar (arquivo, linha de comando ou interface do Locust);
- **`wait_time = between(0.1, 0.5)`** → cada task espera **0,1–0,5 s aleatório** entre
  requisições, simulando comportamento humano (não dispara de forma robótica).

**A tarefa:**
- **`self.client.get()`** → GET pelo cliente do Locust; `/delay/0.2` é relativo ao `host`;
- **`catch_response=True`** → permite analisar a resposta manualmente (não falha sozinho em 4xx/5xx);
- **`response.failure()`** → registra a falha explicitamente nas métricas.

### Ciclo por usuário
1. Executa `fazer_requisicao()`;
2. Faz GET para `/delay/0.2`;
3. Valida a resposta (200 = sucesso);
4. Espera 0,1–0,5 s aleatório;
5. Repete até o teste terminar.

→ Esse ciclo está desenhado nos **[[modulo-2/diagramas|📐 Diagramas]]**.

---

## ▶️ Executando o teste

> [!warning] ⚠️ Inconsistência de nome de arquivo
> O card manda salvar como **`teste_carga.py`**, mas o `run_tests.py` (modo headless) referencia
> **`locustfile.py`**. Use **um nome só** e ajuste os comandos. (Mais detalhes no [[modulo-2/_index|índice]].)

### Opção A — Interface Web (recomendada)
```bash
locust -f teste_carga.py
```
Depois acesse `http://localhost:8089`. Na interface você pode: definir nº de usuários,
definir a taxa de criação (usuários/segundo), monitorar em tempo real e parar quando quiser.

### Opção B — Modo headless (sem interface)
Um `run_tests.py` roda o Locust via `subprocess` para várias cargas automaticamente:

```python
import subprocess

CARGAS = [10, 25, 50, 100, 200]
DURACAO = 30          # segundos
HOST = "https://httpbin.org"
TAXA_SUBIDA = 10      # usuários/segundo

def executar_teste(usuarios):
    comando = [
        "locust", "-f", "locustfile.py",
        f"--host={HOST}", f"--users={usuarios}",
        f"--spawn-rate={TAXA_SUBIDA}", f"--run-time={DURACAO}s",
        "--headless", "--csv=results",
    ]
    subprocess.run(comando)

if __name__ == "__main__":
    for carga in CARGAS:
        executar_teste(carga)
```

```bash
python run_tests.py
```

---

## 📈 Interpretando os resultados (CSV do Locust)

| Coluna | Significa |
|---|---|
| **Name** | Endpoint testado |
| **# requests** | Total de requisições |
| **# failures** | Total de falhas |
| **Median (ms)** | Latência mediana |
| **Average (ms)** | Latência média |
| **Min / Max (ms)** | Latência mínima / máxima |
| **Average size (bytes)** | Tamanho médio da resposta |
| **Requests/sec** | Throughput |

> [!warning] ⚠️ P95/P99 na tabela do exercício
> A tabela de coleta pede **P95 e P99**, mas as colunas do CSV listadas acima **não os
> incluem**. O Locust expõe percentis em **outra parte** do relatório (aba *Charts* na web ou
> o arquivo `..._stats.csv` com colunas de percentil). Avise o mentorado.

---

## 📋 O exercício

A **mesma tabela de 10 colunas e os mesmos 6 blocos de análise** do
[[modulo-1/03-exercicio-pratico#📋 O exercício (o que o mentorado entrega)|Módulo 1]] —
agora com Locust. É o "mesmo experimento", com ferramenta profissional.

| Usuários | Requisições | Throughput | Lat. Mín | Lat. Média | Lat. Máx | P95 | P99 | Erros | Taxa de Erro |
|---|---|---|---|---|---|---|---|---|---|
| 10 | | | | | | | | | |
| 25 | | | | | | | | | |
| 50 | | | | | | | | | |
| 100 | | | | | | | | | |
| 200 | | | | | | | | | |

Blocos de análise: **latência · requisições · taxa de erros · comparação de métricas ·
limite do sistema** (idênticos ao Módulo 1).

## 🎯 Objetivos do exercício (do material)
- Aprofundar os conhecimentos práticos sobre teste de carga;
- Analisar e correlacionar métricas fundamentais, identificando gargalos e determinando a
  capacidade do sistema simulado.

---

## ⏭️ Para onde ir agora

- Aplicar no trabalho real → [[modulo-2/04-implementacao-real|🚀 Implementação real]]
- Rever a escolha de métricas → [[modulo-2/02-definindo-metricas|📊 Definindo métricas]]
- Voltar ao índice → [[modulo-2/_index|2️⃣ Índice do Módulo 2]]
