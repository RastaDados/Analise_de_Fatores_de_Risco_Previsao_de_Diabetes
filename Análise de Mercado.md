# Análise de Fatores de Risco e Previsão de Diabetes

<hr>
  
## Objetivos da Análise

#### Problema de Negócio:

Identificar os fatores clínicos e demográficos mais relevantes associados ao diagnóstico de diabetes com o objetivo de apoiar ações preventivas, diagnósticos precoces e intervenções personalizadas em instituições de saúde.

#### Perguntas-Chave:

- Quais variáveis clínicas e comportamentais estão mais associadas ao diagnóstico de diabetes?
- É possível prever com confiabilidade se um paciente tem diabetes com base em seus dados?
- Como os diferentes perfis de pacientes (ex: idade, IMC, glicose) impactam o risco?
- Quais insights podem ser extraídos para apoiar decisões clínicas e gerenciais?

<hr>

## Principais KPIs

<table>
  <thead>
    <tr>
      <th>Indicador</th>
      <th>Valor Atual</th>
      <th>Observação</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Total de Pacientes</td>
      <td>768</td>
      <td>Amostra total do estudo.</td>
    </tr>
    <tr>
      <td>% de Pacientes com Diabetes</td>
      <td>34,9%</td>
      <td>1 a cada 3 pacientes tem diagnóstico positivo.</td>
    </tr>
    <tr>
      <td>Média de Glicose no sangue</td>
      <td>120,9 mg/dL</td>
      <td>Acima do limiar considerado saudável.</td>
    </tr>
    <tr>
      <td>Média de IMC</td>
      <td>31,9 kg/m²</td>
      <td>Levemente obeso, indicando risco aumentado.</td>
    </tr>
    <tr>
      <td>Idade média</td>
      <td>33,2 anos</td>
      <td>População majoritariamente jovem</td>
    </tr>
    <tr>
      <td>Média de Gravidez</td>
      <td>3,8</td>
      <td>Algumas pacientes com mais de 10 gestações.</td>
    </tr>
  </tbody>
</table>

<hr>

## Interpretação das Visualizações

<b>Distribuição da Glicose</b>

- Gráfico: Histograma
- Insight: Pacientes com diabetes têm glicemia visivelmente mais alta. Pico entre 140–180 mg/dL para positivos.

<b>Correlação entre Glicose e IMC</b>

- Gráfico: Scatter plot + mapa de calor
- Insight: Correlação positiva entre IMC e glicose. Valores altos combinados aumentam drasticamente o risco.

<b>Tendência de Diagnóstico por Faixa Etária</b>
- Gráfico: Histograma categorizado
- Insight: Faixas de 40 a 60 anos concentram mais diagnósticos. Grupo de risco claro.

<b>Boxplots por variáveis clínicas</b>

- Insight: Pressão arterial, espessura da pele e insulina são mais dispersas nos positivos, indicando maior variabilidade fisiológica.

<b>Importância das variáveis no modelo</b>

- Gráfico: Feature Importance (Random Forest)
- Insight: Glicose é a variável mais preditiva, seguida por IMC e idade.

<b>Curva ROC e matriz de confusão</b>
- Insight: O modelo final (Random Forest) apresentou boa separação entre classes (AUC = 0,88), com recall alto (identificando bem os casos positivos).

<hr>

## Insights Estratégicos e Operacionais

#### O que os dados revelam:

- A glicose elevada é o principal preditor de diabetes na base analisada.
- Pacientes mais velhos e com IMC acima de 30 são mais propensos ao diagnóstico positivo.
- Mulheres com mais gravidezes têm maior frequência de diagnóstico, sugerindo efeito hormonal/metabólico.

<hr>

## Riscos identificados:

- A ausência de dados temporais impede análise de evolução ao longo do tempo.
- O desequilíbrio leve entre as classes (35% positivos) pode enviesar modelos se não tratado corretamente.

<hr>

## Análise Segmentada

#### Segmentos analisados:

- Por faixa etária
- Por número de gravidezes
- Por níveis de IMC

#### Exemplos:

- Pacientes com IMC maior que 35 e glicose maiorr que 140 têm 70% de chance de diagnóstico positivo segundo o modelo.
- Faixa entre 40 e 49 anos é a mais crítica em termos de concentração de positivos.

<hr>

## Recomendações Baseadas em Dados

<table>
  <thead>
    <tr>
      <th>Ação Recomendada</th>
      <th>Impacto Esperado</th>
      <th>Viabilidad</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Incluir glicemia em triagens regulares</td>
      <td>Detecção precoce</td>
      <td>Alta</td>
    </tr>
    <tr>
      <td>Implantar programa de redução de IMC</td>
      <td>Redução de riscos</td>
      <td>Média</td>
    </tr>
    <tr>
      <td>Monitorar mulheres com mais de 3 gestações</td>
      <td>Prevenção proativa</td>
      <td>Alta</td>
    </tr>
    <tr>
      <td>Ampliar coletas para incluir dados temporais</td>
      <td>Melhorar previsibilidade</td>
      <td>Média</td>
    </tr>
    <tr>
      <td>Criar alerta automatizado com base no modelo</td>
      <td>Ação rápida em clínicas</td>
      <td>Alta</td>
    </tr>
  </tbody>
</table>

<hr>

## Resumo

Este estudo analisou os dados clínicos de 768 pacientes para entender os fatores mais relevantes associados ao diagnóstico de diabetes. Foi possível construir um modelo preditivo robusto com alta acurácia, apoiado principalmente por glicose, IMC e idade. Visualizações claras e explicativas permitem entender os riscos em diferentes perfis.

A aplicação prática desta análise pode revolucionar o rastreamento preventivo, orientando ações em políticas públicas, clínicas privadas e programas de bem-estar corporativo. A continuação do projeto deve incluir dados temporais e ampliar a base de pacientes para validar os resultados em diferentes populações.
