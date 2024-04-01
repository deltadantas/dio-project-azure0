# dio-project-azure0
Projeto explicativo sobre teste do serviço do Azure Machine-learning utilizando uma base de dados da Microsoft para compreender melhor sobre os serviços da Azure

# Tutorial: Utilizando Automated Machine Learning no Azure Machine Learning

Neste tutorial, você aprenderá como utilizar a funcionalidade de aprendizado de máquina automatizado (Automated Machine Learning) no Azure Machine Learning para treinar, avaliar, implantar e testar um modelo de machine learning. Este tutorial deve levar aproximadamente 30 minutos para ser concluído.

## Passo 1: Criar um Azure Machine Learning Workspace

Para utilizar o Azure Machine Learning, é necessário criar um Azure Machine Learning workspace em sua assinatura do Azure. Isso permitirá que você trabalhe com os recursos no seu workspace usando o Azure Machine Learning Studio.

- Acesse o portal do Azure em https://portal.azure.com
- Selecione "+ Criar um recurso" e pesquise por "Machine Learning".
- Crie um novo recurso Azure Machine Learning com as seguintes configurações:
    - Assinatura: Sua assinatura do Azure.
    - Grupo de recursos: Crie ou selecione um grupo de recursos.
    - Nome: Insira um nome único para o seu workspace.
    - Região: Selecione a região geográfica mais próxima.
    - Conta de armazenamento: Anote a conta de armazenamento padrão que será criada para o seu workspace.
    - Vault de chaves: Anote o novo key vault que será criado para o seu workspace.
    - Application insights: Anote o novo recurso de insights de aplicativo que será criado para o seu workspace.
    - Registro de contêiner: Nenhum (será criado automaticamente na primeira vez que você implantar um modelo em um contêiner).
- Clique em "Revisar + criar" e, em seguida, em "Criar". Aguarde até que o seu workspace seja criado e então vá para o recurso implantado.
- Selecione "Iniciar o Studio" (ou abra uma nova guia do navegador e acesse https://ml.azure.com) e faça login no Azure Machine Learning Studio usando sua conta Microsoft. Feche quaisquer mensagens que forem exibidas.
- No Azure Machine Learning Studio, você deverá ver o workspace recém-criado. Se não aparecer, selecione "Todos os workspaces" no menu à esquerda e então selecione o workspace que você acabou de criar.

## Passo 2: Utilizar Automated Machine Learning para treinar um modelo

O Automated Machine Learning permite que você experimente vários algoritmos e parâmetros para treinar múltiplos modelos e identificar o melhor para os seus dados. Neste exercício, você utilizará um conjunto de dados de aluguel de bicicletas histórico para treinar um modelo que prevê o número de aluguéis de bicicletas esperados em um determinado dia, com base em características sazonais e meteorológicas.

- No Azure Machine Learning Studio, acesse a página Automated ML (em Authoring).
- Crie um novo job de Automated ML com as seguintes configurações:
    - Configurações básicas:
        - Nome do job: mslearn-bike-automl
        - Nome do experimento: mslearn-bike-rental
        - Descrição: Aprendizado de máquina automatizado para previsão de aluguel de bicicletas
        - Tags: nenhum
    - Tipo de tarefa e dados:
        - Selecione o tipo de tarefa: Regressão
        - Selecione o conjunto de dados:
            - Tipo de dados: Tabular
            - Fonte de dados: De arquivos da web
            - URL da web: https://aka.ms/bike-rentals
            - Formato do arquivo: Delimitado
            - Delimitador: Vírgula
            - Colunas: Todas as colunas exceto Path
        - Selecione "Criar". Após o conjunto de dados ser criado, selecione-o para continuar.
    - Configurações de tarefa:
        - Tipo de tarefa: Regressão
        - Conjunto de dados: bike-rentals
        - Coluna alvo: Rentals (inteiro)
        - Configurações adicionais:
            - Métrica primária: Erro quadrático médio normalizado (Normalized root mean squared error)
            - Explicar o melhor modelo: Não selecionado
            - Usar todos os modelos suportados: Não selecionado
            - Modelos permitidos: Selecionar apenas RandomForest e LightGBM
    - Limites:
        - Número máximo de tentativas: 3
        - Número máximo de tentativas simultâneas: 3
        - Máximo de nós: 3
        - Limite da pontuação da métrica: 0.085
        - Tempo limite: 15 minutos
        - Tempo limite da iteração: 15 minutos
        - Habilitar término antecipado: Selecionado
    - Validação e teste:
        - Tipo de validação: Divisão de treinamento e validação
        - Porcentagem de dados de validação: 10%
        - Conjunto de teste: Nenhum
    - Computação:
       

 - Selecione o tipo de computação: Serverless
        - Tipo de máquina virtual: CPU
        - Nível de máquina virtual: Dedicado
        - Tamanho da máquina virtual: Standard_DS3_V2 (ou qualquer tamanho disponível em sua assinatura)

## Passo 3: Revisar e Implantar o Melhor Modelo

Após o término do job de Automated ML, você poderá revisar e implantar o melhor modelo treinado.

- Na guia Visão geral do job de Automated ML, observe o resumo do melhor modelo. 
- Selecione o nome do algoritmo do melhor modelo para visualizar seus detalhes.
- Na guia Métricas, observe o desempenho do modelo nos gráficos de resíduos e valores previstos.
- Se estiver satisfeito com o modelo, implante-o como um serviço da web.

## Passo 4: Testar o Serviço Implantado

Agora você pode testar o serviço implantado.

- Em Azure Machine Learning Studio, na guia Endpoints, abra o endpoint de previsão em tempo real.
- Na guia Teste, substitua o JSON do modelo com os dados de entrada fornecidos no tutorial.
- Clique em "Testar" para executar o teste.
- Revise os resultados do teste, que incluem o número previsto de aluguéis com base nas características de entrada.

## Limpeza

Após concluir o tutorial, é recomendável limpar os recursos do Azure para evitar custos desnecessários.

- Exclua o endpoint de serviço implantado na guia Endpoints.
- Exclua o workspace Azure Machine Learning e os recursos associados no portal Azure.

Isso conclui o tutorial sobre como utilizar o Automated Machine Learning no Azure Machine Learning para treinar, avaliar, implantar e testar um modelo de machine learning.

## Referência
https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/01-machine-learning.html
