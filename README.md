# People Analytics Dashboard

## 📊 Descrição do Projeto

Dashboard de People Analytics desenvolvido em Power BI para análise estratégica de dados de RH, permitindo o acompanhamento de métricas críticas de gestão de pessoas com foco em contratações, demissões e turnover.

## 🎯 Objetivos

- **Acompanhar** contratações, demissões e headcount ao longo do tempo
- **Criar** indicador de Má Contratações
- **Analisar** taxa de Turnover
- **Cruzamento** de dados com diferentes características dos funcionários

## 🛠️ Tecnologias Utilizadas

- **Power BI** para visualização e dashboard
- **DAX** para medidas e cálculos avançados
- **Power Query** para ETL e modelagem de dados
- **Tabela dCalendario** para inteligência temporal

## 📈 Métricas e KPIs Implementados

### Medidas DAX Desenvolvidas

```dax
1. Contratações = COUNTROWS(Contratos)
2. Demissões = CALCULATE(COUNTROWS(Contratos), Contratos[Situação] = "Demitido", USERELATIONSHIP(Contratos[Data Afastamento], dCalendario[Data]))
3. Massa salarial = CALCULATE(SUM(Contratos[Valor Salário]), Contratos[Situação] <> "Demitido")
4. Saldo Funcionários = [Contratações] - [Demissões]
5. HeadCount = CALCULATE([Saldo Funcionários], dCalendario[Data] <= MAX(dCalendario[Data]))
6. Má Contratações = CALCULATE([Contratações], Contratos[Má Contratação] = "Sim")
7. % Má Contratações = DIVIDE([Má Contratações], [Contratações])
```

### Coluna Calculada - Indicador de Má Contratação

```dax
Má Contratação = 
IF(
    DATEDIFF(
        Contratos[Data Admissão], 
        Contratos[Data Afastamento], 
        DAY
    ) < 60 && Contratos[Situação] = "Demitido", 
    "Sim", 
    "Não"
)
```

## 📊 Resultados e Insights

### Visão Geral (2002-2020)
- **Contratações**: 860
- **Demissões**: 611
- **Massa Salarial**: R$ 866 mil
- **Headcount**: 249
- **Má Contratações**: 104 (12%)
- **Turnover**: 16%

### Análise por Cargo

#### 🏭 Operadores
- Contratações: 162 | Demissões: 113 | Headcount: 49
- Má Contratações: 22 (14%) | Turnover: 10%

#### 👨‍💼 Gestores
- Contratações: 89 | Demissões: 67 | Headcount: 22
- Má Contratações: 8 (9%) | Turnover: 50% ⚠️

#### 🛠️ Ajudantes
- Contratações: 49 | Demissões: 34 | Headcount: 15
- Má Contratações: 9 (18%) ⚠️ | Turnover: 7%

### Análise por Escolaridade

#### 🎓 Ensino Médio Completo
- Contratações: 306 | Demissões: 199 | Headcount: 107
- Má Contratações: 35 (11%) | Turnover: 7%

#### 🎓 Superior Completo
- Contratações: 201 | Demissões: 154 | Headcount: 47
- Má Contratações: 21 (10%) | Turnover: 26% ⚠️

## 🔍 Funcionalidades do Dashboard

### 1. **Visão Geral**
- KPIs principais em tempo real
- Métricas consolidadas de 2002 a 2020

### 2. **Análise de Má Contratações**
- Filtros por cargo, escolaridade, gênero e faixa etária
- Identificação de padrões problemáticos

### 3. **Análise Demográfica**
- Distribuição por gênero (Feminino: 34.62% | Masculino: 65.38%)
- Segmentação por faixa etária

### 4. **Análise Temporal**
- Evolução de contratações e demissões ao longo dos anos
- Tendências e sazonalidades

## 🚀 Como Utilizar

1. **Clone o repositório**
2. **Abra o arquivo .pbix no Power BI Desktop**
3. **Atualize as conexões de dados conforme necessário**
4. **Explore os filtros interativos para análises específicas**

## 💡 Insights de Negócio

- **Gestores** apresentam alto turnover (50%) - necessita investigação
- **Ajudantes** têm alta taxa de má contratação (18%) - revisar processo seletivo
- **Superior Completo** mostra turnover elevado (26%) - analisar retenção
- **Operadores** representam a maior base, com indicadores dentro do esperado

---
