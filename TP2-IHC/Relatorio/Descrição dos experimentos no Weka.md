## Experimentos com Weka

### Algoritmos testados:
- ZeroR
- OneR
- J48
- NaiveBayes
- IBK

### Resultados:

| Algoritmo     | Acurácia   |
|---------------|------------|
| ZeroR         | 32,39%     |
| OneR          | 97,18%     |
| J48           | 97,18%     |
| NaiveBayes    | 100%       |
| IBK           | 100%       |

---


## Árvore J48

A árvore gerada pelo J48 utilizou `media_tempo_sessao_min` como atributo principal:

```text
media_tempo_sessao_min <= 14 → baixo
media_tempo_sessao_min > 14 ∧ respostas_em_posts <= 3 → médio
media_tempo_sessao_min > 14 ∧ respostas_em_posts > 3 → alto

