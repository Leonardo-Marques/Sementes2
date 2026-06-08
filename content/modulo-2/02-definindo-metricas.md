---
tipo: conteudo
titulo: Definindo Métricas
title: Definindo Métricas
modulo: 2
ordem: 2
fonte: metricas-2.md
data: 2026-06-07
tags: [performance, metricas, ambiente-tecnico, negocio, operacional, sla]
---

# 📊 Definindo Métricas

> Nota 2 de 4 do [[modulo-2/_index|Módulo 2]]. Fonte: `metricas-2.md`. Onde o Módulo 1 ensina
> **o que** cada métrica é, este aprofunda **como escolher** quais coletar.
> Anterior: [[modulo-2/01-o-que-e-carga|🏛️ O que é carga]] · Próxima: [[modulo-2/03-exercicio-locust|🦗 Exercício]]

---

## Menos é mais

> [!quote] Princípio do material
> Coletar **mais métricas do que o necessário não é necessariamente a coisa certa**. Cada
> métrica escolhida requer um meio de coleta e geração de relatórios consistentes.

É importante definir o conjunto de métricas que **suporte os objetivos** do teste. As
métricas variam de acordo com:

- O **contexto / processos** do negócio;
- O **comportamento** dos clientes e usuários;
- As **expectativas** dos stakeholders;
- O **contexto operacional** e suas tecnologias;
- Os **objetivos** do teste.

> [!example] Exemplo do material
> As métricas de um **site de e-commerce internacional** são diferentes das de um **sistema
> embarcado** que controla um dispositivo médico.

---

## 🗂️ As 3 categorias de medição

### 1. 🔧 Ambiente Técnico
Varia conforme o tipo de ambiente: **web, mobile, IoT, desktop, servidor, mainframe, bancos
de dados, redes** e a natureza do software (ex.: embarcados). Métricas possíveis:

- **Tempo de resposta** (requisições, usuários simultâneos, carregamento de página);
- **Utilização de recursos** (CPU, memória, banda de rede, latência de rede, disco);
- **Taxa de transferência** da transação-chave (transações por período);
- **Tempo de processamento Batch** (espera, processamento, resposta do BD, conclusão);
- **Números de erros** que afetam a performance;
- **Tempo de conclusão** de operações CRUD (criar, ler, atualizar, excluir);
- **Carregamento em segundo plano** em recursos compartilhados (ambientes virtualizados);
- **Métricas de software** (complexidade de código).

### 2. 💼 Ambiente de Negócios
Do ponto de vista comercial/funcional:

- **Eficiência do processo de negócios** (velocidade de execução de um processo geral,
  incluindo fluxos normais, alternativos e excepcionais);
- **Taxa de transferência** de dados/transações (pedidos por hora, linhas por minuto…);
- **Cumprimento de SLA** ou taxas de violação (violações de SLA por unidade de tempo);
- **Escopo de uso** (% de usuários globais/nacionais realizando tarefas num momento);
- **Concorrência de uso** (nº de usuários executando simultaneamente uma tarefa);
- **Tempo de uso** (pedidos processados durante os horários de pico de carga).

### 3. 🛠️ Ambiente Operacional
Foca em tarefas geralmente **não voltadas ao usuário**:

- **Processos operacionais** (inicialização do ambiente, backups, desligamento, reinício);
- **Restauração do sistema** (tempo para restaurar dados de um backup);
- **Alertas e avisos** (tempo para o sistema emitir um alerta ou aviso).

> [!info] Conexão
> Repare que estas categorias **expandem** as [[modulo-1/02-metricas|métricas do Módulo 1]]
> (latência, throughput, erros) para além do técnico, incluindo **negócio (SLA!)** e
> **operação** — algo central num contexto bancário como o da Unicred.

---

## ⏭️ Para onde ir agora

- Locust na prática → [[modulo-2/03-exercicio-locust|🦗 Exercício com Locust]]
- Rever o conceito → [[modulo-2/01-o-que-e-carga|🏛️ O que é carga]]
- Voltar ao índice → [[modulo-2/_index|2️⃣ Índice do Módulo 2]]
