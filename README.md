# Fishmorph-svm

Classificação taxonômica de peixes de água doce a partir de medidas morfológicas, usando **SVM (Support Vector Machine)**. O projeto usa o dataset [FishMorph](https://www.kaggle.com/datasets/menegidio/fishmorph-dataset), do Kaggle, e tem dois notebooks: um classifica por **ordem** e outro por **família**.

## Arquivos

- `Ordem_Morph_Fish.ipynb`: classificação por ordem (alvo `Order`)
- `Família FishMorph.ipynb`: classificação por família (alvo `Family`)

## Etapas do projeto

1. Importação do dataset com `kagglehub`
2. Análise dos dados: formato, tipos, estatísticas, nulos e duplicados
3. Limpeza: remoção de duplicados e valores nulos
4. Distribuição das categorias e matriz de correlação entre as variáveis
5. Remoção de classes raras (menos de 20 registros), que não permitem divisão estratificada nem validação cruzada
6. Divisão treino/teste (80/20, estratificada)
7. Pipeline com `StandardScaler` e `SVC`
8. `GridSearchCV` com validação cruzada estratificada (3 folds), testando 4 valores para cada hiperparâmetro:
   - `kernel`: linear, poly, rbf, sigmoid
   - `C`: 0.1, 1, 10, 100
   - `gamma`: 0.001, 0.01, 0.1, 1
9. Avaliação no conjunto de teste: acurácia, relatório de classificação e matriz de confusão normalizada

## Resultados

### Família

- **Modelo:** SVC
- **Melhores parâmetros:** `kernel="rbf"`, `C=10`, `gamma=0.1`
- **Acurácia média na validação cruzada:** 0,6785
- **Acurácia no teste:** 0,6889

As acurácias de validação e de teste ficaram próximas, o que indica boa generalização e ausência de overfitting. A matriz de confusão mostra que as famílias com mais exemplos, como Cyprinidae, concentram boa parte dos erros de classes menores, efeito do desbalanceamento.

### Ordem

- **Modelo:** SVC
- **Melhores parâmetros:** `kernel=...`, `C=...`, `gamma=...`
- **Acurácia média na validação cruzada:** ...
- **Acurácia no teste:** ...

## Observações

- Classes com poucos exemplos foram removidas por limitação técnica da divisão estratificada e da validação cruzada.
- O `StandardScaler` dentro do Pipeline evita vazamento de dados entre treino e validação.
- O dataset é baixado automaticamente pelo `kagglehub`, então não é necessário subir o CSV.

## Tecnologias

Python, pandas, scikit-learn, matplotlib, seaborn, kagglehub, Google Colab
