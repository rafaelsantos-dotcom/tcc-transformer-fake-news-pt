## Objetivo do repositório

O repositório reúne o código utilizado no experimento, as configurações principais e as instruções para sua execução. Dessa forma, é possível consultar as etapas do trabalho e reproduzir o procedimento em condições semelhantes às descritas no TCC.

## Conteúdo do repositório

O arquivo principal do projeto é o notebook [`tcc_transformer_fake_news_pt.ipynb`](tcc_transformer_fake_news_pt.ipynb). Ele reúne todas as etapas do experimento:

| Etapa | Descrição |
|---|---|
| **Preparação** | Instalação e importação das bibliotecas necessárias. |
| **Reprodutibilidade** | Configuração das sementes e dos parâmetros experimentais. |
| **Dados** | Download e organização do Fake.br-Corpus. |
| **Rótulos** | Codificação das classes, com `0 = Real` e `1 = Fake`. |
| **Divisão** | Separação estratificada em treinamento, validação e teste. |
| **Tokenização** | Processamento dos textos com o tokenizer do BERTimbau, truncamento até 512 tokens e padding dinâmico. |
| **Treinamento** | Fine-tuning por meio da API `Trainer`, da biblioteca Transformers. |
| **Seleção** | Escolha do melhor checkpoint com base no F1-score do conjunto de validação. |
| **Avaliação** | Cálculo das métricas no conjunto de teste e geração das visualizações. |

## Como executar o notebook

A execução foi preparada para o **Google Colaboratory**, ambiente que permite utilizar notebooks Python e, quando disponível, um acelerador gráfico. Não é necessário instalar o projeto no computador.

### 1. Baixe o notebook

Acesse o arquivo `tcc_transformer_fake_news_pt.ipynb` no repositório. Na página do arquivo, selecione a opção **Download raw file** ou utilize o ícone de download para salvar o notebook no computador.

### 2. Abra o Google Colaboratory

Acesse [colab.research.google.com](https://colab.research.google.com) e faça login com uma conta Google. Na página inicial, selecione **Arquivo → Fazer upload de notebook** e escolha o arquivo `tcc_transformer_fake_news_pt.ipynb` que foi baixado.

### 3. Ative a GPU

Com o notebook aberto, selecione:

No menu do Colab, selecione **Ambiente de execução → Alterar tipo de ambiente de execução** e escolha uma GPU disponível. A execução registrada neste projeto utilizou uma GPU NVIDIA Tesla T4.

Caso a opção **T4 GPU** não esteja disponível, selecione outra GPU compatível. O experimento foi executado com sucesso em uma GPU Tesla T4, mas a disponibilidade do acelerador pode variar conforme o ambiente utilizado.

### 4. Execute as células em ordem

Utilize uma sessão limpa e execute o notebook desde a primeira célula, seguindo a ordem apresentada. O notebook realizará automaticamente a instalação das bibliotecas, o download do corpus, a preparação dos dados, a tokenização, o treinamento, a seleção do melhor modelo e a avaliação final.

> **Importante:** não pule diretamente para as últimas células. As etapas anteriores criam as variáveis, os conjuntos de dados e o modelo necessários para a execução completa do experimento.

### 5. Consulte os resultados

Ao final da execução, o notebook apresentará as métricas de desempenho e poderá gerar os seguintes arquivos:

| Arquivo | Finalidade |
|---|---|
| `matriz_confusao_teste.png` | Visualização das classificações corretas e incorretas por classe. |
| `metricas_teste.png` | Gráfico comparativo de acurácia, precisão, recall e F1-score. |
| `experimento_config.json` | Registro das configurações utilizadas no experimento. |
| `resultados_finais.json` | Registro das métricas obtidas no conjunto de teste. |

Esses arquivos são gerados no ambiente de execução do Colab. Caso seja necessário preservá-los, faça o download após a conclusão do notebook.

## Configuração experimental

A base utilizada possui **7.200 notícias**, divididas em **5.760 exemplos para treinamento**, **720 para validação** e **720 para teste**. O modelo empregado corresponde ao checkpoint `neuralmind/bert-base-portuguese-cased`, conhecido como **BERTimbau Base**.

O treinamento utiliza três épocas, batch de 4 exemplos por dispositivo, acumulação de gradiente em 4 etapas, batch efetivo de 16 exemplos, taxa de aprendizado de `5e-5`, 500 etapas de aquecimento e `weight decay` de `0,01`. O padding é aplicado dinamicamente por lote, contribuindo para reduzir o consumo de memória.

O conjunto de teste não participa da atualização dos parâmetros nem da seleção do melhor checkpoint. Ele é utilizado somente na avaliação final, após o treinamento e a seleção baseada no conjunto de validação.

## Ambiente computacional

O experimento foi executado no Google Colaboratory, utilizando Python versão 3.13.15, em sistema Linux 6.6.122+, arquitetura x86_64. O treinamento foi realizado em uma GPU NVIDIA Tesla T4, com CUDA versão 12.8.

As bibliotecas utilizadas foram PyTorch versão 2.11.0+cu128, Transformers versão 5.16.1, Datasets versão 4.0.0, Scikit-learn versão 1.6.1, Pandas versão 2.2.3, NumPy versão 2.1.3, Seaborn versão 0.13.2, Matplotlib versão 3.10.0 e Accelerate versão 1.14.0.

## Reprodutibilidade e limitações

As sementes, os parâmetros e as principais etapas do experimento estão registrados no notebook para favorecer a reprodução em ambiente semelhante. Ainda assim, pequenas variações nos resultados podem ocorrer em razão da versão das bibliotecas, da disponibilidade e do tipo de GPU, do ambiente do Colab e das condições de acesso ao dataset.

Os resultados devem ser interpretados considerando as condições específicas do Fake.br-Corpus. O modelo é avaliado como um classificador de textos conforme os rótulos disponíveis na base, não sendo apresentado como um verificador factual universal de todas as notícias publicadas na internet.

## Identificação

**Autor:** Rafael Proença dos Santos  
**Orientador:** Prof. Nilton Kazuo Gomes Suzuki  
**Instituição:** Universidade do Contestado (UnC) — Campus Curitibanos  
**Área:** Engenharia de Software

## Licença

Este projeto é distribuído sob a [Licença MIT](./LICENSE). O arquivo de licença se aplica ao código e aos materiais desenvolvidos neste repositório. O dataset utilizado é obtido pelo próprio notebook a partir de sua fonte de origem e permanece sujeito às condições de uso definidas pelos respectivos autores e distribuidores.

## Referência do repositório

Para citar ou consultar este projeto, utilize o endereço:

**https://github.com/rafaelsantos-dotcom/tcc-transformer-fake-news-pt**

---

**Este repositório foi criado como parte do Trabalho de Conclusão de Curso em Engenharia de Software.**

## Referências úteis

- [Google Colaboratory](https://colab.research.google.com)
- [Hugging Face Transformers](https://huggingface.co/docs/transformers)
- [PyTorch](https://pytorch.org)
- [Repositório oficial do BERTimbau](https://github.com/neuralmind-ai/portuguese-bert)
