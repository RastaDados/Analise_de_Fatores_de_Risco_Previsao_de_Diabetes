### Imports e Carregando os Dados

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import warnings
import plotly.express as px
warnings.filterwarnings('ignore')

#Configurando o estilo do seaborn 
sns.set(style='whitegrid')
plt.rcParams['figure.figsize'] = (10, 6)

#Carregando os dados
df = pd.read_csv("dados/diabetes.csv")

#Renomeando as colunas para português
df.columns = ['Gravidez', 'Glicose', 'Pressao', 'Pele', 'Insulina', 'IMC', 'Pedigree', 'Idade', 'Diabetes']

#Estatísticas descritivas
print("Estatísticas descritivas:")
print(df.describe())

#Distribuição de classes
sns.countplot(data=df, x='Diabetes', palette='Set2')
plt.title("Distribuição dos Diagnósticos de Diabetes (0 = Não, 1 = Sim)")
plt.xlabel("Diabetes")
plt.ylabel("Número de Pacientes")
plt.show()
```

![image](https://github.com/user-attachments/assets/1aee08f4-d246-4019-aa16-40479bc740f7)

![image](https://github.com/user-attachments/assets/c90d65ad-167a-4cfa-855c-7d5aaa22a672)

### Histograma das Variávies

```python
#Criando o Histograma para cada variável
df.hist(bins=20, figsize=(15, 10), color='skyblue', edgecolor='black')
plt.suptitle("Distribuição das Variáveis", fontsize=18)
plt.tight_layout()
plt.show()
```

![image](https://github.com/user-attachments/assets/929056fe-6063-4261-b78a-50abd0214af0)

### Boxplot Exibindo Outliers

```python
#Criando os Boxplots para identificar outliers 
for coluna in df.columns[:-1]:  #exceto quem tem Diabetes 
    sns.boxplot(x='Diabetes', y=coluna, data=df, palette="Set3")
    plt.title(f"Boxplot de {coluna} por Diagnóstico")
    plt.show()
```

![image](https://github.com/user-attachments/assets/12f3c22c-9950-4023-bc2b-ca070b7243c4)

![image](https://github.com/user-attachments/assets/822d4633-087c-4a15-8ca3-96f377ed86d3)

![image](https://github.com/user-attachments/assets/86e3469a-1c2e-411d-9982-31f210c35324)

![image](https://github.com/user-attachments/assets/56217503-c7b0-43ac-88b3-a69ba383190f)

![image](https://github.com/user-attachments/assets/23253050-bec1-4325-8511-d9fd0e6dde6b)

![image](https://github.com/user-attachments/assets/32fe1ec2-3001-493b-bed7-ff25eff6c27d)

![image](https://github.com/user-attachments/assets/9484bcda-49a8-492e-b79d-1cd4535586af)

![image](https://github.com/user-attachments/assets/e37a0781-3962-451c-a485-7d15e98ad20e)

### Mapa de Calor da Correlação das Variáveis

```python
#Correlação entre as variáveis
plt.figure(figsize=(10, 8))
sns.heatmap(df.corr(), annot=True, cmap='coolwarm', linewidths=0.5)
plt.title("Mapa de Calor das Correlações")
plt.show()
```

![image](https://github.com/user-attachments/assets/f996544f-3534-452a-971d-7c961ee2f108)

### Insights

```python
#Faixa etária mais afetada
print("Idades médias:")
print(df.groupby('Diabetes')['Idade'].describe())

#Mulheres com mais de 3 filhos e com diabetes
maes_diabeticas = df[(df['Gravidez'] > 3) & (df['Diabetes'] == 1)]
print(f"\nNúmero de mulheres com mais de 3 filhos e diabetes: {len(maes_diabeticas)}")

#Relação entre glicose, IMC e diagnóstico
sns.scatterplot(data=df, x='Glicose', y='IMC', hue='Diabetes', palette='Set1')
plt.title("Relação entre Glicose, IMC e Diagnóstico")
plt.show()
```

![image](https://github.com/user-attachments/assets/5f871863-7625-4053-ac2c-fd32a2fb25b0)

![image](https://github.com/user-attachments/assets/a2fd651e-9c0d-4c3c-9651-7cf904bfd8f8)

### Visualizações

#### Distribuição de Diagnóstico por Idade e IMC

```python
fig = px.scatter(
    df,
    x="Idade",
    y="IMC",
    color="Diabetes",
    title="Distribuição de Diagnóstico por Idade e IMC",
    labels={"Diabetes": "Diagnóstico (0 = Não, 1 = Sim)"},
    hover_data=["Gravidez", "Glicose", "Pressao"]
)
fig.show()
```

![image](https://github.com/user-attachments/assets/eb7be94c-d80a-4beb-bcca-2ef8f580dfd0)

#### Tendência do Diagnóstico por Faixa Etária

```python
bins = [20, 30, 40, 50, 60, 70, 80, 100]
labels = ['20-29', '30-39', '40-49', '50-59', '60-69', '70-79', '80+']
df['Faixa_Etaria'] = pd.cut(df['Idade'], bins=bins, labels=labels, right=False)

fig = px.histogram(
    df,
    x="Faixa_Etaria",
    color="Diabetes",
    barmode="group",
    title="Distribuição de Diabetes por Faixa Etária",
    category_orders={"Faixa_Etaria": labels}
)
fig.show()
```

![image](https://github.com/user-attachments/assets/f9af0678-aaf9-4fa0-bc3c-dcb6a3a2f34c)

#### Comparação dos Níveis de Glicose entre os Grupos

```python
fig = px.box(
    df,
    x="Diabetes",
    y="Glicose",
    color="Diabetes",
    title="Distribuição de Glicose por Diagnóstico",
    labels={"Diabetes": "Diagnóstico (0 = Não, 1 = Sim)"}
)
fig.show()
```

![image](https://github.com/user-attachments/assets/14c48a00-d174-4b66-9788-9f38bebd26fc)

#### Gráfico Com Diversos Filtros

```python
fig = px.scatter(
    df,
    x="Glicose",
    y="IMC",
    color="Diabetes",
    facet_col="Faixa_Etaria",
    facet_col_wrap=3,  # ajusta para quebrar colunas em múltiplas linhas
    title="Glicose vs IMC por Faixa Etária e Diagnóstico",
    hover_data=["Gravidez", "Pressao", "Pedigree"]
)
fig.update_layout(height=800, width=900)
fig.show()
```

![newplot](https://github.com/user-attachments/assets/c73ea616-525e-499e-af3c-5777c38da537)

### Construção do Modelo Preditivo

#### Preparação do Modelo

```python
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler

#Separando as features e target
X = df.drop(columns=["Diabetes", "Faixa_Etaria"])  # Excluímos também a faixa categórica
y = df["Diabetes"]

#Dividindo o modelo em treino e teste (80/20)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42, stratify=y)

#Normalizando as variáveis numéricas
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)
```

#### Treinando o Modelo

```python
from sklearn.linear_model import LogisticRegression
from sklearn.ensemble import RandomForestClassifier
from sklearn.neighbors import KNeighborsClassifier

#Tentando importar o modelo XGBoost
try:
    from xgboost import XGBClassifier
    xgb_available = True
except ImportError:
    xgb_available = False

#Criando os modelos
modelos = {
    "Regressão Logística": LogisticRegression(max_iter=1000),
    "Random Forest": RandomForestClassifier(n_estimators=100, random_state=42),
    "KNN": KNeighborsClassifier(n_neighbors=5)
}

if xgb_available:
    modelos["XGBoost"] = XGBClassifier(use_label_encoder=False, eval_metric='logloss', random_state=42)

#Treinando os modelos
for nome, modelo in modelos.items():
    modelo.fit(X_train_scaled, y_train)
```

#### Avaliação do Modelo

```python
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score, roc_auc_score, confusion_matrix
import numpy as np

print("Avaliação dos Modelos:\n")

for nome, modelo in modelos.items():
    y_pred = modelo.predict(X_test_scaled)
    y_proba = modelo.predict_proba(X_test_scaled)[:, 1]

    print(f"🔍 {nome}")
    print(f"Acurácia:  {accuracy_score(y_test, y_pred):.3f}")
    print(f"Precisão:  {precision_score(y_test, y_pred):.3f}")
    print(f"Recall:    {recall_score(y_test, y_pred):.3f}")
    print(f"F1-Score:  {f1_score(y_test, y_pred):.3f}")
    print(f"ROC-AUC:   {roc_auc_score(y_test, y_proba):.3f}")
    print("-" * 40)
```

![image](https://github.com/user-attachments/assets/b3e7f106-78f2-41e4-8b62-31521897d8a9)



























