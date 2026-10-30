[README1.md](https://github.com/user-attachments/files/34204576/README1.md)
# Checkpoint 3 — Clustering e segmentação de clientes com K-Means

**Disciplina:** Modelagem Linear para Aprendizado de Máquina  
**Turma:** 1CCPK

## Integrantes

| Nome | RM |
| --- | --- |
| Gabriel Rodrigues Zappelloni | 572060 |

## Objetivo

Aplicar o algoritmo **K-Means** para identificar perfis de compra em uma base simulada de clientes de um comércio eletrônico. A atividade inclui escolher a quantidade de grupos (k) com o **método Elbow** e o **Silhouette Score**, interpretar cada perfil e propor uma ação de relacionamento para cada um, discutindo também as limitações da análise.

## Base de dados

Base **simulada** com **120 clientes fictícios**, gerada com NumPy (semente 303) para fins didáticos e incorporada ao próprio notebook como texto CSV. Não há arquivo externo e os dados não vêm de pessoas ou empresas reais.

| Coluna | Significado | Uso |
| --- | --- | --- |
| `id_cliente` | Identificador fictício | Excluído do modelo |
| `gasto_total_12_meses` | Soma das compras nos últimos 12 meses (R$) | Variável do modelo (valor) |
| `quantidade_compras_12_meses` | Número de compras nos últimos 12 meses | Variável do modelo (frequência) |
| `dias_desde_ultima_compra` | Dias desde a compra mais recente | Variável do modelo (recência) |

A base não tem valores ausentes nem identificadores repetidos.

## Metodologia

1. **Exploração:** tamanho, tipos, ausentes, duplicidades, estatísticas descritivas, histogramas e correlações.
2. **Padronização:** `StandardScaler` nas três variáveis numéricas, para que o gasto (em reais, com desvio de ≈ R$ 3.451) não domine as distâncias.
3. **Elbow:** K-Means com k de 1 a 8 e gráfico de inércia.
4. **Silhouette Score:** k de 2 a 8, com tabela e gráfico.
5. **Modelo final:** k escolhido, contagem por grupo, centroides, gráficos de dispersão e tabela de perfis nas unidades originais.

## Principais resultados

- **Elbow:** as inércias foram 360,00 / 164,71 / 110,52 / **60,65** / 46,92 / 40,08 / 33,75 / 28,41 (k = 1 a 8). A queda de 3 para 4 grupos ainda é grande (−49,87); depois as quedas são de 13,73 ou menos. O cotovelo fica em **k = 4**.
- **Silhouette:** o maior score foi **0,5526 com k = 4** (k = 5 ficou em 0,5433, e k = 2 e 3 em ≈ 0,48–0,49).
- **k escolhido = 4:** os dois métodos concordam e os grupos são equilibrados e interpretáveis.

| Cluster | Perfil | Clientes | Gasto médio | Compras (média) | Dias desde a última compra (média) | Ação proposta |
| --- | --- | ---: | ---: | ---: | ---: | --- |
| 0 | Alto valor e frequentes | 28 | R$ 9.309,6 | 27,1 | 10,5 | Fidelização (programa VIP, acesso antecipado) |
| 1 | Compras grandes e esporádicas | 30 | R$ 6.741,4 | 6,3 | 75,6 | Reativação direcionada pelo tipo de produto comprado |
| 2 | Frequentes de ticket baixo | 32 | R$ 2.861,7 | 22,7 | 15,0 | Aumento de ticket (cross-sell, kits, frete grátis por valor mínimo) |
| 3 | Baixo engajamento | 30 | R$ 833,3 | 4,1 | 102,4 | Reativação de baixo custo e pesquisa sobre o afastamento |

O cluster 0 concentra **45% do gasto total** com 23% dos clientes, enquanto o cluster 3 representa apenas 4,3%.

## Limitações

- Base simulada e pequena (120 clientes): os grupos podem ser mais bem definidos do que em dados reais.
- Só três variáveis de comportamento, sem margem, categorias, satisfação ou motivo de afastamento. As ações propostas são hipóteses a serem testadas.
- O K-Means supõe grupos aproximadamente esféricos, é sensível a outliers e exige definir k previamente.
- O Silhouette Score mede a separação geométrica dos grupos e **não** é uma medida de acurácia.

## Estrutura do repositório

```
├── Checkpoint_3_MLAM_Clustering_Clientes.ipynb   # notebook preenchido e executado
└── README.md                                     # este arquivo
```
