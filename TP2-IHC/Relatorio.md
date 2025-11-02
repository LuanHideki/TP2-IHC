# TP2-IHC - Relatório de Análise de Engajamento em AVA

## Objetivo

Identificar o nível de engajamento de alunos em um Ambiente Virtual de Aprendizagem (AVA) com base em seus comportamentos na plataforma, visando intervenções pedagógicas precoces.

---

## Atributos da Base

- `percentual_videos_vistos`: porcentagem de vídeos assistidos
- `percentual_exercicios_entregues`: porcentagem de exercícios entregues
- `posts_iniciados_forum`: número de posts iniciados
- `respostas_em_posts`: número de respostas em posts
- `media_tempo_sessao_min`: tempo médio por sessão (minutos)
- `regularidade_acesso`: Regular ou Irregular
- `nivel_engajamento`: alto, médio ou baixo

---

## Regras de Classificação

### Engajamento Alto
- vídeos > 75%
- exercícios > 80%
- posts > 1 ou respostas > 2
- tempo > 20 min
- acesso regular

### Engajamento Baixo
- vídeos < 30%
- exercícios < 25%
- sem posts nem respostas
- acesso irregular

### Engajamento Médio
- casos intermediários

---

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
