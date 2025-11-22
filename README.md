# TCC – Análise e Reprodução dos Microdados do INEP Aplicados ao UNISALES

Este repositório reúne o código, documentação, modelos de dados e artefatos utilizados no Trabalho de Conclusão de Curso intitulado **“Reprodução e Adequação dos Dados do Censo do Ensino Superior (2013–2023)”**, desenvolvido no **Centro Universitário Salesiano – UNISALES**.

O objetivo principal deste projeto foi criar uma solução completa de **Engenharia de Dados + Business Intelligence** capaz de transformar grandes volumes de microdados públicos do INEP em **informações estratégicas**, com foco no diagnóstico institucional.

---

## 📌 Sumário

- [Sobre](#sobre)  
- [Objetivos](#objetivos)  
- [Abordagem do Projeto](#abordagem-do-projeto)
- [Metodologia](#metodologia)  
- [Modelagem de Dados](#modelagem-de-dados)
- [ETL](#etl)
- [Ferramentas](#ferramentas)  
- [Indicadores analisados](#indicadores-analisados)  
- [Estrutura do repositório](#estrutura-do-repositório)  
- [Como usar / executar](#como-usar--executar)  
- [Resultados obtidos](#resultados-obtidos)  
- [Contribuições / aplicações](#contribuições--aplicações)  
- [Referências](#referências)  
- [Contato](#contato)

---

## 📘 Sobre

O Censo da Educação Superior é a principal fonte de dados estatísticos sobre instituições, cursos, estudantes e docentes no Brasil.  
Entretanto, seus **microdados são complexos**, volumosos e apresentam **diferenças estruturais entre os anos**, o que dificulta análises diretas.

Este projeto implementa:

- Um **pipeline ETL** para padronizar e carregar os microdados (2013–2023)
- Um **modelo dimensional (Star Schema)** com tabelas fato e dimensões
- Dashboards interativos em **Power BI** para o UniSales
- Automação e padronização de todo o fluxo de dados

---

## 🎯 Objetivos

### **Objetivo Geral**
Desenvolver uma solução automatizada de análise e visualização dos microdados do Censo da Educação Superior, aplicada ao UniSales.

### **Objetivos Específicos**
1. Criar um **modelo de dados robusto, escalável e reutilizável**.  
2. Automatizar a extração e padronização via **SSIS (com C#)**.  
3. Construir dashboards no Power BI para apoiar decisões estratégicas.  
4. Identificar **lacunas e inconsistências** presentes nos microdados do INEP.  

---

## 🧭 Abordagem do Projeto

O projeto foi conduzido de maneira **incremental**, passando pelas etapas:

1. **Exploração dos dados brutos**  
2. Estruturação do **modelo dimensional**  
3. Construção e automação do **ETL em SSIS**  
4. Desenvolvimento dos **painéis analíticos**  
5. Validação técnica + **feedback institucional** do UniSales  

Essa abordagem assegurou alinhamento contínuo com a instituição e alta qualidade na modelagem analítica.

---

## 🧪 Metodologia

A metodologia é quantitativa, exploratória e baseada em engenharia de dados:

- **Coleta de dados**  
  - Microdados do INEP (2013–2023)  
  - Extração automatizada via SSIS (Data Flow + C# Script Task)

- **Tratamento e limpeza**  
  - Padronização de colunas  
  - Conversão de tipos  
  - Remoção de duplicidades  
  - Normalização de códigos e categorias  

- **Armazenamento e modelagem**  
  - SQL Server on-premise  
  - Procedures dedicadas para carga e tratamento  

- **Visualização**  
  - Painéis em Power BI: cursos, docentes, indicadores administrativos

---

## 🗂 Modelagem de Dados

Foi adotado o modelo **Star Schema**, composto por:

### **Tabelas Dimensão**
- DimCurso  
- DimInstituicao  
- DimAnoCenso
- DimEnderecoInstituicao

### **Tabelas Fato**
- FatoCursos
- FatoIES  

**Motivos da escolha:**

✔ Melhor desempenho em consultas analíticas  
✔ Estrutura clara para BI  
✔ Expansão fácil para futuros indicadores  

---

## 🔄 ETL

O pipeline ETL foi implementado no **SQL Server Integration Services (SSIS)**.

Etapas principais:

1. **Extração**  
   - Leitura automatizada dos arquivos CSV do INEP  

2. **Transformação** 
   - Scripts em C# para ajustes mais complexos  
   - Padronização de colunas inconsistentes  
   - Normalização de categorias que mudam ao longo dos anos
   - Importação para tabelas de *staging*
   - Tratamento de datatypes

3. **Carga**  
   - Inserção nas tabelas dimensionais e fatos  

## 🛠 Ferramentas

- **SQL Server Integration Services (SSIS)**  
- **C#** (Script Task dentro do SSIS)  
- **SQL Server Management Studio (SSMS)**  
- **SQL**
- **SQL Server** (banco principal)  
- **Power BI**  
- **Excel / CSV do INEP**  

## 📊 Indicadores analisados

Os indicadores foram organizados em duas grandes áreas:

### **Indicadores Acadêmicos**
- Vagas ofertadas por ano  
- Número de inscritos
- Ingressantes e concluintes  
- Quantidade de cursos por ano 

### **Indicadores Administrativos**
- Quantidade total de docentes por sexo
- Quantidade total de docentes por grau de instrução

Esses indicadores refletem o panorama institucional do UniSales ao longo de 10 anos de Censo.

## 🗂 Estrutura do repositório

📁 /Visual Studio
└── Pacotes SSIS (.dtsx), scripts C#, fluxos Data Flow

📁 /SQL
├── scripts de criação das tabelas
├── procedures de carga
└── scripts de staging

📁 /Dados
└── Arquivos CSV do INEP (amostras)

📁 /PBIX
└── Arquivo .pbip do Power BI

## **▶ Como usar / executar**

1. Clone o repositório
2. Instale os pré-requisitos ou atualize se necessário
3. Modifique dentro do pacote SSIS as variáveis de ambiente
4. Execute o script SQL **Schemas e Tabelas stage (stg).sql**
5. Execute o script SQL **Modelo de Dados Oficial (dw).sql**
6. Crie as procedures SQL através do Script **Procedures de Carga Dimensões e Fatos.sql**
7. No arquivo .pbip clique em **Nova Fonte de Dados**, edite a fonte de cada uma das tabelas para fazer referencia ao banco no qual os scripts anteriores foram executados.
8. Execute o pacote SSIS e após finalização atualize o painel.

**Pré-requisitos:**

- SQL Server 2019+  
- SSIS 2019+  
- Power BI Desktop  

## **📈 Resultados obtidos**

- Automação completa da integração dos microdados (2013–2023)  
- Modelo dimensional robusto para análises históricas  
- Dashboard institucional com informações acadêmicas e administrativas  
- Visualização clara e intuitiva para gestores e coordenadores  
- Redução de esforço manual e padronização de dados  

## **🚀 Contribuições / aplicações**

- Base para pesquisas institucionais  
- Apoio ao planejamento de novos cursos  
- Insumo para relatórios e autoavaliação institucional  
- Ferramenta para gestão baseada em evidências  
- Expansão futura para dados internos do UniSales  

## **📚 Referências**

- INEP – Censo da Educação Superior  
- Documentação oficial Microsoft (SSIS, SQL Server, Power BI)  

## **📞 Contato**

**Caio Freire**  
Engenharia de Dados | Business Intelligence  
Email: *caiogfreire@gmail.com*  
LinkedIn: *https://www.linkedin.com/in/caio-gaiba-freire/*  