# Explorando o Machine Learning Automatizado no Azure

## Objetivo
Treine, avalie, implante e teste um modelo de Machine Learning automatizado no Azure. Previsão: 35 minutos.

---

## Passo a Passo

### 1. Configurar o Azure Machine Learning Workspace
1. **Acesse** o [Azure Portal](https://portal.azure.com).
2. Crie um recurso *Machine Learning* com:
   - Nome único.
   - Região: *East US*.
   - Armazenamento, Key Vault e Application Insights: padrões.
3. **Permissões**: Adicione a função `Azure AI Administrator` ao seu email no **IAM**.

---

### 2. Iniciar o Azure Machine Learning Studio
- Acesse o [Azure ML Studio](https://ml.azure.com).
- Certifique-se de que o workspace está visível.

---

### 3. Treinar um Modelo Automatizado
1. **Automated ML**: Crie um job com:
   - Nome: `mslearn-bike-rental`.
   - Dados: `bike-rentals` (histórico de aluguel de bicicletas).
2. **Configurações de Treinamento**:
   - Tarefa: Regressão.
   - Modelos: `RandomForest` e `LightGBM`.
   - Limites: Máx. 3 tentativas e nó único.
   - Métrica: `NormalizedRootMeanSquaredError` (limiar 0.085).
   - Validação: Split (10% dados).

3. Submeta o job e aguarde a conclusão.

---

### 4. Revisar o Melhor Modelo
- Confira as métricas e gráficos, como residuals e predições.

---

### 5. Implantar e Testar o Modelo
1. **Implantação**:
   - VM: `Standard_DS3_v2`, 3 instâncias.
   - Endpoint: Novo e globalmente único.
2. **Teste**: Use os dados abaixo:
   ```json
   {
     "input_data": {
       "columns": ["day", "mnth", "year", "season", "holiday", "weekday", "workingday", "weathersit", "temp", "atemp", "hum", "windspeed"],
       "index": [0],
       "data": [[1,1,2022,2,0,1,1,2,0.3,0.3,0.3,0.3]]
     }
   }
