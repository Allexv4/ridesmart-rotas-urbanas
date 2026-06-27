# RideSmart — Modelagem e Análise de Rotas Urbanas com Grafos

**Disciplina:** Algoritmos e Estrutura de Dados II  
**Aluno:** José Alex Araújo de Santana  
**Departamento:** Engenharia da Computação e Automação (DCA) — UFRN  
**Período:** 2025.2  

---

## Descrição do Projeto

O RideSmart simula o problema de seleção do melhor ponto de embarque em um aplicativo de mobilidade urbana. Dado um ponto de origem **A**, um destino **B** e um raio máximo de caminhada **X**, o sistema determina o ponto de embarque **P** que minimiza o custo total da rota:

```
A ──(caminhada)──► P ──(carro)──► B
```

A rede viária real de **Natal-RN** é utilizada como cenário, obtida via OpenStreetMap por meio da biblioteca OSMnx (18.576 nós · 48.180 arestas).

---

## Estrutura do Repositório

```
ridesmart/
├── Projeto_3_unidade_ED2.ipynb   # Notebook principal (executável)
├── relatorio_ridesmart.pdf       # Relatório IEEE dupla coluna (até 4 páginas)
└── README.md                     # Este arquivo
```

---

## Algoritmos Implementados

| # | Algoritmo | Complexidade | Estrutura |
|---|-----------|-------------|-----------|
| 1 | Dijkstra Simples | O(V²) | Lista linear |
| 2 | Dijkstra com Heap | O((V+E) log V) | Min-heap |
| 3 | A\* Geográfico | O(E log V) | Min-heap + heurística Haversine |
| 4 | Bellman-Ford | O(V · E) | Relaxamento iterativo |

---

## Cenários Avaliados

| Cenário | Critério | Peso |
|---------|----------|------|
| C1 | Menor rota em distância | `length` (metros) |
| C2 | Rota mais rápida sem trânsito | `travel_time` (segundos) |
| C3 | Rota mais rápida com trânsito sintético | `travel_time_traffic` (segundos) |
| C4 | Rota direta A→B sem caminhada (caso-base) | `length` |
| C5 | Ganho ao caminhar até ponto alternativo | comparativo temporal |

---

## Principais Resultados (Cenário C4)

| Algoritmo | Custo (m) | Nós Exp. | Tempo (ms) | D.P. — 20 exec. (ms) |
|-----------|-----------|----------|------------|----------------------|
| Dijkstra Simples | 2.629 | 773 | 1.482,74 | 142,82 |
| Dijkstra Heap | 2.629 | 774 | 5,27 | 0,34 |
| A\* | 2.629 | 172 | 2,42 | 0,08 |
| Bellman-Ford | 2.629 | 116 | 4.667,20 | 472,34 |

**Melhor P por cenário (Dijkstra Heap):** nó `1387156245` (39 m de caminhada) em todos os três cenários de otimização.

---

## Como Executar

### No Google Colab (recomendado)

1. Acesse o notebook pelo link abaixo.
2. Clique em **"Abrir no Colab"** ou faça o upload manual do arquivo `.ipynb`.
3. Execute as células **na ordem** (Runtime → Run all).
4. A primeira célula instala as dependências automaticamente (`osmnx`, `folium`, `networkx`).
5. O download do grafo de Natal-RN leva aproximadamente 20–30 segundos.

> 🔗 **Link do Colab:** `[cole aqui o link de compartilhamento do seu notebook no Colab]`

### Localmente

```bash
# Criar ambiente virtual
python -m venv .venv
source .venv/bin/activate       # Linux/Mac
.venv\Scripts\activate          # Windows

# Instalar dependências
pip install osmnx folium matplotlib networkx numpy pandas

# Abrir o notebook
jupyter notebook Projeto_3_unidade_ED2.ipynb
```

**Requisitos:** Python 3.10+, OSMnx 2.1.0, NetworkX 3.6.1, Folium 0.20.0

---

## Dependências

```
osmnx==2.1.0
networkx==3.6.1
folium==0.20.0
matplotlib
numpy
pandas
```

---

## Referências

- G. Boeing, "OSMnx: New methods for acquiring, constructing, analyzing, and visualizing complex street networks," *Computers, Environment and Urban Systems*, vol. 65, pp. 126–139, 2017.
- E. W. Dijkstra, "A note on two problems in connexion with graphs," *Numerische Mathematik*, vol. 1, pp. 269–271, 1959.
- P. E. Hart, N. J. Nilsson e B. Raphael, "A formal basis for the heuristic determination of minimum cost paths," *IEEE Transactions on Systems Science and Cybernetics*, vol. 4, no. 2, pp. 100–107, 1968.
- R. Bellman, "On a routing problem," *Quarterly of Applied Mathematics*, vol. 16, pp. 87–90, 1958.
- T. H. Cormen et al., *Introduction to Algorithms*, 3rd ed., MIT Press, 2009.
