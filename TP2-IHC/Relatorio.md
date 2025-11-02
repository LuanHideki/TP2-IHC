# TP2-IHC - Relatório de Análise de Engajamento em AVA

## Definição do problema e objetivo
O problema está inserido no contexto de um Ambiente Virtual de Aprendizagem (AVA), como o Moodle ou Canvas, aplicado à disciplina de Cálculo I no curso de Engenharia de Software. Essa disciplina apresenta historicamente altas taxas de reprovação e evasão, principalmente nas primeiras semanas do semestre, quando os alunos ainda estão em fase de adaptação. 

O objetivo é identificar o nível de engajamento de alunos em um Ambiente Virtual de Aprendizagem (AVA) com base em seus comportamentos na plataforma, visando intervenções pedagógicas precoces.

---

## Atributos utilizados na Base

- `percentual_videos_vistos`: porcentagem de vídeos assistidos
- `percentual_exercicios_entregues`: porcentagem de exercícios entregues
- `posts_iniciados_forum`: número de posts iniciados
- `respostas_em_posts`: número de respostas em posts
- `media_tempo_sessao_min`: tempo médio por sessão (minutos)
- `regularidade_acesso`: Regular ou Irregular
- `nivel_engajamento`: alto, médio ou baixo

---
## Classe-alvo: 
- `nivel_engajamento`, podendo assumir os valores alto, médio ou baixo.
## Regras de Classificação
As regras que definem o nível de engajamento foram estabelecidas com base em padrões de comportamento observados: 

Alto: aluno que assiste aos vídeos, entrega exercícios e participa dos fóruns. 

Regra para nivel_engajamento = Alto

Os numeros são porcentagem % (exceto em post_iniciados e respostas)

## Regras usadas para gerar a Classe-alvo 
As regras que definem o nível de engajamento foram estabelecidas com base em padrões de comportamento observados: 
Alto: aluno que assiste aos vídeos, entrega exercícios e participa dos fóruns. 
Regra para nivel_engajamento = Alto 
os numeros são porcentagem % (exceto em post_iniciados e respostas) 

- Se `(percentual_videos_vistos > 75)` 
- E `(percentual_exercicios_entregues > 80)`
- E `(posts_iniciados_forum > 1 OU respostas_em_posts > 2)`
- E `(media_tempo_sessao_min > 20)`
- E `(regularidade_acesso == 'Regular')`
- Então `nivel_engajamento = Alto`

Médio: aluno que participa apenas de uma dimensão — por exemplo, assiste vídeos e 
entrega atividades, mas não interage nos fóruns. 

Regra para nivel_engajamento = Medio 

Qualquer aluno que "escapa" das duas definições de Alto e Baixo, cai 
automaticamente em 'Médio'.

Baixo: aluno com pouco consumo de conteúdo, poucas entregas e nenhuma interação. 
Regra para nivel_engajamento = Baixo 

- Se `(percentual_videos_vistos < 30)`
- E `(percentual_exercicios_entregues < 25)` 
- E `(posts_iniciados_forum == 0 E respostas_em_posts == 0)` 
- E `(regularidade_acesso == 'Irregular')` 
- Então `nivel_engajamento = Baixo`

De acordo com a árvore gerada pelo algoritmo J48, o atributo mais importante foi 
media_tempo_sessao_min. Se o tempo médio for menor que 14 minutos, o aluno é 
baixo engajamento. Mas se o tempo médio for maior que 14 minutos e o número de 
respostas_em_posts for menor que 3, o aluno é médio engajamento. E se o tempo for 
maior que 14 minutos e houver mais de 3 respostas, o aluno é alto engajamento.

---
## Descrição da base sintética 
A base de dados é sintética, simulando comportamentos de alunos em um AVA durante 
as três primeiras semanas do semestre. 

Ela contém 209 instâncias e 7 atributos, sendo seis preditores e uma classe. Cada 
instância representa um aluno e seu respectivo comportamento de acesso, entrega de 
atividades e interação. 

Os dados foram construídos de forma a representar situações reais observadas em 
cursos online, diferenciando padrões de comportamento em relação ao tempo de 
estudo, interação social e frequência de acesso. 

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
