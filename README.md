Projeto 3 - Análise de Risco - Empresa: S
Esse projeto corresponde a minha participação no Bootcamp da Laboratória Brasil.

# **✔Ficha Técnica**: Análise de Riscos

---

## **📰 Título do Projeto**: **Modelo -Análise de Riscos**

---

- **🎯 Objetivo:**
    
    Propor um modelo de análise de risco de crédito automatizado, em que através da pontuação para categorias criadas, seja possível melhorar a avaliação do risco de crédito, permitindo a análise de clientes de formas individual ou através dos dados categorizados, aumentando a precisão sobre a classificação e decisão sobre a concessão de crédito e reduzir o risco de empréstimos não reembolsáveis.
    

---

- **👩🏽‍🦱 Equipe:**
    
    O projeto individual feito por **Socorro Moura.**
    

---

- **⚙ Ferramentas e Tecnologias**:
    - Big Query - SQL
    - Google Colab -Python
    - Looker Studio
    - Google Sheets

---

- **💻 Processamento e análises:**
    - **PROCESSAMENTO:**
        1. **Importação** do *dataset* disponibilizado:
            1. default
            2. loans_detail
            3. loans_outstanding
            4. user_info
        2. O passo seguinte foi o **tratamento** de dados:
            1. **Nulos**: identificado nas variáveis -[**Link**](https://colab.research.google.com/drive/1xH-YfJk4Zfkrafd9HrbJTF11WjdptMky?usp=sharing) :
                1. (*last_month_salary*: **7199**) **-** Substituição por mediana;
                2. (*number_dependents*: **943**)**-** apenas com identificação “0”. A inexistência de registros foram interpretados como ausência de dependentes;
            2. **Duplicados**: Os valores duplicados na tabela “*loans_outstanding**”*** correspondem a várias operações vinculadas a um  mesmo “u*ser_id”*. Informações relevantes que posteriormente serão usadas da melhor forma;
            3. **Fora do Escopo:** correlações e decisões sobre qual variáveis serão preponderantes sobre as outras;
            4. **Inconsistentes:** Primeiro, apenas as tabelas *“loans_outstanding”* e *“user_info”* possuem variável caracterizada como STRING(Texto). Porém, a tabela “user_info” possui a variável “sex” que deve ser desconsiderada por se referir a características pessoais do cliente. Para *“loans_outstanding”* foi realizada a correção para padronizar as informações dos campos;
            5. **Discrepantes (*Outliers***) - para as variáveis:
                1. *“last_month_salary”*: valores nulos preenchidos por medianas;
                2. *“number times delayed payment loan 30 59 days”*: as variações, assim como os valores nulos são importantes para caracterização dos clientes, por isso sem modificações;
                3.  *“using_ lines_ not_ secured_personal_assets”*: substituí os *outliers* por outros mais representativos, nesse caso, pela média dos não-outliers;
                4. *“debt ratio”*: substituí os *outliers* por outros mais representativos, nesse caso, pela média dos não-outliers para seguir a mesma regra de imputação aplicada anteriormente;
        3. Criação de novas variáveis:
            1. “loans_outstanding_**emprestimo**”;
            2. “default_**classificado**”;
            3. “user_info**3**”;
        4. Unit tabelas: ao unir tabelas com suas variáveis tratadas foi criada a base **“tabela_unificada_3”**. Posteriormente, após essa unificação ainda foi a criada a tabela final, usada na apresentação no Looker Studio: “**tabela_unificada_com_risco4”**. Essa dispões da tabela anterior acrescido da segmentação por score.
        5. Tabelas auxiliares: constam durante todo o processo. São feitas para a execução de uma etapa, mas sempre são construídas novas tabelas no decorrer do processo. 
        
    - **ANÁLISE:**
        1. Foram aplicadas medidas de tendência central (moda, média, mediana), de dispersão(desvio padrão) assim como verificada a distribuição de dados através do Bloxpot;
        2. Também realizadas as **correlações** no Looker Studio entre as variáveis numéricas. É importante reforçar que a correlação não implica causalidade:
            1. Idade x Taxa de Endividamento:
            
            ![Idade x Taxa de Endividamento.png](attachment:96481970-2056-44d5-b399-aa277c3e884d:Idade_x_Taxa_de_Endividamento.png)
            
             b. Idade x Salário:
            
            ![Idade x Salário.png](attachment:b743186b-7532-440f-8f5d-7b50a58b0c05:Idade_x_Salrio.png)
            
             c. Salário x Linha de Crédito:
            
            ![Salário x Linha de Crédito.png](attachment:8061ecad-3c4a-4a3e-b78a-6b8039dc164f:Salrio_x_Linha_de_Crdito.png)
            
             d. Salário x taxa de Endividamento:
            
            ![Salário x taxa de Endividamento.png](attachment:6398c0fe-da79-41cd-bb10-03a139e9a080:Salrio_x_taxa_de_Endividamento.png)
            
             e. Endividamento x Linha de Crédito:
            
            ![Endividamento x Linha de Crédito.png](attachment:93ab4d87-d576-4fec-befb-76fca729dce6:Endividamento_x_Linha_de_Crdito.png)
            
        3. Foi realizado Cálculo do **Risco Relativo para:** 
            1. age:
            2. last_month_salary;
            3. debt_ratio_corrigido;
            4. using_lines_tratada;
        4. Aplicada a **segmentação por scores:**
            1. Nessa fase, acho importante destacar a forma como **interpretei** o direcionamento dado no escopo do projeto. Segue o **prompt** que direcionei para a IA, e assim conseguir obter o calculo da **pontuação**:
            
            > “Calcular a pontuação baseado no risco de cada *user_id*. Após criar a pontuação, definir um ponto de corte que determinará a pontuação de Bom pagador e de Potencial mau pagador. Usar o comando IF para criar as variáveis dummy. Variáveis: age, last_month_salary, debt_ratio_corrigido, using_lines_not_secured_personal_assets_tratada na tabela: projeto3-supercaja.projeto3_dataset.tabela_unificada_3 ”
            > 
            

---

- ✔️ **Resultados e Conclusões:**
    1. Diante do cruzamento de dados, tenho as seguintes **observações**:
        1. Foi interessante perceber que o índice de endividamento alto **não quer dizer** necessariamente que uma faixa etária será mau pagadora. Também deverá ser analisado que tipo de dívida foi contraída;
        2. Assim como o índice do uso do limite de crédito não quer dizer que um grupo é propenso a ser mal pagador, apenas que pode ter uma dívida relacionada com o **momento financeiro**, ou seja, quem é mais estável economicamente pode comprometer mais a renda com dívidas não rotativas;
        3. Nesse sentindo, foi uma descoberta , pois na minha concepção até então, números altos não eram um bom indicativo. Hoje vejo que, a depender do grupo, a interpretação dos números será **adaptada**;
        4. Para isso, **definir as faixas etárias** foi muito importante, pois com a finalização do modelo de análise de risco, descobriu-se que há tendências a depender da idade. Nesse ponto, os gráficos de correlação dão o primeiro insight, pois a olho nu, observa-se extremos e médias. 
        5. Porém, com o **modelo** de análise de risco produzido, é interessante notar a necessidade de uma maior cuidado com o grupos de **Jovens Adultos (21-34 anos)**, pois talvez não seja a quantidade total da dívida que os coloca em maior risco de inadimplência, mas sim a natureza dessa dívida (muitas vezes crédito de consumo sem garantia, como cartões de crédito, empréstimos pessoais de curto prazo, cheque especial) e a capacidade de gerenciamento ou a estabilidade da renda para lidar com ela;
        6. Já os **Idosos**, por exemplo, têm muitas dívidas em relação ao seu patrimônio (o que é ruim), mas essas dívidas podem ser "boas" (financiamento imobiliário de longo prazo) e sua renda é estável (aposentadoria). Embora o nível de endividamento seja alto, ela consegue honrar os pagamentos

---

- **🔐Limitações/Próximos Passos**: limitações ou desafios encontrados durante o projeto.
    1. A decisão de manter ou excluir e até mesmo como tratar os **outliers** é muito sensível em se tratando de análise financeira;
    2.  Por exemplo, quando se menciona tempo, a medida de 98 dias não foi considerado como outliers a ser tratado, mas sim um dado comum, visto que existem atrasos em vários níveis e isso é um ponto importante para caracterizar um perfil;
    3. Com o andamento das análises, muitas vezes é necessário rever algum cálculo ou processo, por isso **documentar** de forma adequada **é um desafio**;
    4. Para os próximos passos, é indicado aplicação de outras técnicas que deem mais robustez ao modelo aplicado. Por exemplo, a regressão Logística não foi aplicada por conta do fator compreensão da técnica e também pelo tempo, pois houve uma demora em fases anteriores;

---

- **🔗Links de interesse:**
    - Pré-processamentos - Colab - [**LINK**](https://colab.research.google.com/drive/1xH-YfJk4Zfkrafd9HrbJTF11WjdptMky?usp=sharing)
    - Apresentação - Looker Studio -[**LINK**](https://lookerstudio.google.com/reporting/1312a7b3-510f-464b-aa32-34a718f57924)
    - Apresentação **Vídeo** - Loom - [**LINK**](https://www.loom.com/share/27f3b014512f4658b4b44d84a8ce73c8?sid=0113ee38-bec5-4070-a6fe-2524046ecfd6)
    - Marco Adicional (Standby) - Colab - [**LINK**](https://colab.research.google.com/drive/1n3U0-CWNzbDNQb5_CIVkv8eSWPqOeUpP?usp=sharing)
    - Documentação - [**LINK**](https://docs.google.com/document/d/19fTwSYtrZhtklOleePai2y5p698O00u871JvanbtBuk/edit?usp=sharing)
