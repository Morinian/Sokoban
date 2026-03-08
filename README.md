# 🧠 Sokoban com Busca Heurística

Projeto de resolução de Sokoban usando **A***, **Dijkstra** e **Busca Gananciosa**.

---

# 🧩 Modelagem do Problema

## 🔁 Função Sucessora

Gera os próximos estados possíveis a partir do estado atual.

Movimentos possíveis do agente:

* ⬆️ cima
* ⬇️ baixo
* ⬅️ esquerda
* ➡️ direita

Regras:

* O agente pode andar em células vazias
* Se houver caixa, ele pode empurrar 📦
* A caixa só move se a célula seguinte estiver livre
* ❌ Não atravessa paredes

---

## 🎯 Função Objetivo

O objetivo é colocar **todas as caixas 📦 nos alvos 🟢**.

Formalmente:

```
posições das caixas == posições dos alvos
```

---

## 💰 Cálculo de Custo

Cada ação tem custo **1**.

Ou seja:

```
custo total = número de movimentos
```

---

## 🧭 Função Heurística

Usamos **distância de Manhattan** entre cada caixa e o alvo mais próximo:

```
h = |x1 - x2| + |y1 - y2|
```

Somamos essa distância para todas as caixas.

---

## 💾 Representação do Estado

Cada estado guarda:

* posição do agente 🤖
* posição das caixas 📦

Internamente:

```
estado = (posição_agente, posições_das_caixas)
```

As posições das caixas são guardadas em **tupla ordenada**, permitindo usar estruturas como:

* `set`
* `dict`
* `priority queue`

Isso evita visitar estados repetidos.

---

## ✅ Por que a heurística é admissível?

Porque a **distância de Manhattan nunca superestima o custo real**.

Ela assume que:

* não existem paredes
* não existem bloqueios

Logo, o caminho real sempre será **igual ou maior** que a estimativa.

Isso garante que **A*** encontra a solução ótima.

---

# 📊 Estudo de Caso

Foi executado o mesmo problema com diferentes tamanhos de grid.

Algoritmos testados:

* ⭐ A*
* 🔵 Dijkstra
* 🟢 Busca Gananciosa

### Resultado exemplo

| Algoritmo     | Movimentos |
| ------------- | ---------- |
| ⭐ A*          | 48         |
| 🔵 Dijkstra   | 46         |
| 🟢 Gananciosa | 60         |

Observação:

* A* costuma ser **mais eficiente**
* Dijkstra encontra solução ótima, mas explora mais estados
* Busca Gananciosa é **rápida**, mas pode gerar caminhos maiores

---

# 📈 Crescimento do Problema

O espaço de estados cresce rapidamente conforme o grid aumenta.

| Grid  | Complexidade |
| ----- | ------------ |
| 8x8   | pequeno      |
| 16x16 | médio        |
| 24x24 | grande       |
| 64x64 | muito grande |

Motivo:

* mais posições possíveis para agente 🤖
* mais combinações para caixas 📦
* mais estados para explorar

Isso causa **explosão combinatória**.

---

# 🚀 Conclusão

* O problema possui **grande espaço de estados**
* Heurísticas ajudam a reduzir a busca
* **A*** apresentou melhor equilíbrio entre custo e desempenho
