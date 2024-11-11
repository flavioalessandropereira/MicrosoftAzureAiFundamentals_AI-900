# Microsoft Azure Ai Fundamentals(AI-900)

## Desafio Projeto 1 

1. Crie um novo repositório no github com um nome a sua preferência
2. Crie um modelo de previsão com seus devidos pontos de extremidade configurados
3. Escreva o passo a passo desse processo em um readme.md de como você chegou nessa etapa
4. Salve nesse repositório o readme.md e o arquivo .json de pontos de extremidade
5. Compartilhe conosco o link desse repositório através do botão 'entregar projeto'


### Resolução do Projeto 1

# Previsão de Aluguéis de Bicicletas com Azure Machine Learning

## Descrição
Este projeto cria um modelo de machine learning automatizado no Azure para prever a quantidade de aluguéis de bicicletas em determinado dia.

## Passo a Passo

### 1. Configurar o Workspace no Azure
1. No [Portal do Azure](https://portal.azure.com/), pesquise por **Machine Learning**.
2. Crie um novo recurso e configure sua assinatura, grupo de recursos, nome do workspace e região.
3. Clique em **Review + create** e depois em **Create**. Após criado, clique em **Launch studio**.

### 2. Upload do Conjunto de Dados
1. Baixe o conjunto de dados de [Bike Rentals](https://aka.ms/bike-rentals).
2. No Azure Machine Learning Studio, vá para **Data** e faça o upload do arquivo, nomeando-o como `bike-rentals`.

### 3. Treinar o Modelo
1. No Azure Machine Learning Studio, vá para **Automated ML** e crie um novo experimento.
2. Configure as opções:
   - **Nome do experimento**: `mslearn-bike-rental`.
   - **Tipo de tarefa**: `Regressão`.
   - **Conjunto de dados**: `bike-rentals`.
   - **Coluna de destino**: `alugueis`.
   - **Modelos permitidos**: `RandomForest` e `LightGBM`.
3. Clique em **Iniciar Experimento** e aguarde a conclusão.

### 4. Implantação do Modelo
1. Selecione **Deploy** no melhor modelo e configure o endpoint:
   - **Tipo de máquina virtual**: `Standard_DS3_v2`.
   - **Contagem de instâncias**: `3`.
   - **Nome do Endpoint**: `predict-rentals`.
2. Aguarde até que a implantação tenha sucesso.

## Teste do Endpoint
Para testar o modelo, insira o JSON abaixo na aba de **Teste** do endpoint no Azure Machine Learning Studio:

```json
{
  "input_data": {
    "columns": [
      "day", "mnth", "year", "season", "holiday", "weekday", "workingday",
      "weathersit", "temp", "atemp", "hum", "windspeed"
    ],
    "index": [0],
    "data": [[1, 1, 2022, 2, 0, 1, 1, 2, 0.3, 0.3, 0.3, 0.3]]
  }
}
