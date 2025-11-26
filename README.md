# Pré-processamento e Limpeza de Dados da base de dados de Churn de uma Telecom
Claro! Aqui está o conteúdo do README.md detalhado para o seu projeto de Pré-processamento e Limpeza de Dados do Módulo 14, formatado como um texto corrido.

Relatório Detalhado do Projeto: Pré-processamento e Limpeza de Dados (Módulo 14)
1. Visão Geral do Projeto
Este projeto consiste em um pipeline robusto de Pré-processamento e Limpeza de Dados, essencial para preparar a base de dados de CHURN de uma Telecon para posterior modelagem de Machine Learning. O foco é garantir a integridade, a consistência e a qualidade dos dados, tratando valores ausentes, inconsistências de formato e padronizando as colunas para que os modelos possam ser aplicados de forma eficaz. A base de dados foi identificada como "CHURN_TELECON_MOD08_TAREFA.csv".

2. Leitura e Inspeção Inicial
Esta seção estabelece o ambiente e realiza a primeira inspeção crítica dos dados.

Importação de Bibliotecas: As bibliotecas pandas, numpy, seaborn e matplotlib.pyplot foram importadas. O Pandas é a ferramenta principal para a manipulação dos dados, enquanto as demais são úteis para análises exploratórias posteriores ou visualização de dados ausentes.

Leitura do CSV: A base é carregada utilizando pd.read_csv(...) com a especificação crucial de delimiter=';' (ponto e vírgula). A justificativa para essa escolha é que o arquivo CSV utiliza o ponto e vírgula como separador de campos, e não a vírgula padrão, o que evitaria que a base fosse lida incorretamente em uma única coluna.

Inspeção: São utilizados df.head(10) para visualizar uma amostra dos dados e df.dtypes para verificar os tipos de dados de cada coluna. Essa verificação é fundamental para identificar problemas como colunas numéricas erroneamente lidas como texto (object).

3. Tratamento de Valores Ausentes (Missing Data)
Esta etapa focou na imputação (preenchimento) dos valores nulos, que foram identificados nas colunas Idade, Tempo Contrato e Gênero.

3.1. Tratamento de Colunas Numéricas
Coluna Idade: Os valores ausentes foram substituídos pela Média da coluna (df['Idade'].fillna(media_idade)). A média é a melhor escolha para variáveis contínuas com distribuição simétrica, pois preserva a tendência central da amostra.

Coluna Tempo Contrato: Os valores ausentes foram substituídos pela Mediana (df['Tempo Contrato'].fillna(mediana_tempo)). A mediana é preferível à média para variáveis numéricas que podem conter outliers (valores extremos), garantindo que o valor imputado não seja distorcido por esses extremos.

3.2. Tratamento de Colunas Categóricas
Coluna Gênero: Os valores ausentes foram substituídos pela Moda (o valor mais frequente) da coluna (df['Genero'].fillna(moda_genero)). A moda é o método ideal para variáveis categóricas, pois preserva a distribuição de frequência original, evitando a introdução de viés na proporção das classes (por exemplo, a proporção entre "Feminino" e "Masculino").

4. Padronização de Dados e Nomes de Colunas
Esta seção garante que o formato dos dados e dos features seja consistente.

Correção de Inconsistências de Categoria: Foi aplicado str.lower().str.strip() em todas as colunas de texto (object).

Justificativa: Este é um passo obrigatório para garantir que categorias com grafias ligeiramente diferentes (ex: "Yes", "yes", " yes ") sejam tratadas como um único valor, evitando a criação de categorias duplicadas que confundiriam o modelo.

Padronização dos Nomes das Colunas (Snake_Case): Os nomes das colunas foram convertidos para o formato snake_case (ex: Tempo Contrato vira tempo_contrato).

Justificativa: Este padrão (minúsculas, espaços substituídos por underscores e remoção de acentos) melhora a legibilidade do código, minimiza erros de digitação e torna o código compatível com a maioria dos modelos de Machine Learning em Python.

5. Conversão de Tipos de Dados
Nesta fase, os tipos de dados são ajustados para refletir corretamente o seu conteúdo.

Tratamento da Coluna Serviços: Esta coluna, que representa valores monetários, foi detectada inicialmente como object (texto) devido à presença do caractere monetário ($) e da vírgula (,) como separador decimal.

O código executou a remoção do $ e a substituição da vírgula por ponto.

Em seguida, a coluna foi convertida para o tipo numérico (float).

Justificativa: Essa conversão é crítica, pois modelos de Machine Learning só podem processar variáveis numéricas; sem ela, o Serviços não poderia ser usado como um feature preditor.

6. Conclusão da Limpeza
Ao final do pipeline, o novo df.info() e df.head() demonstram que a base está em um estado "limpo":

Valores Nulos: Não há mais valores ausentes em nenhuma coluna chave.

Tipos de Dados: As colunas numéricas (Serviços, Idade, Tempo Contrato) estão corretamente definidas como float64 ou int64.

Consistência: Os dados categóricos estão padronizados para minúsculas e sem espaços desnecessários.

A base de dados agora está pronta para a próxima etapa do projeto, seja ela a Análise Exploratória de Dados (EDA) ou a Modelagem Preditiva.
