# ImageGuard
### Compressão de imagens e detecção de anomalias utilizando Autoencoders

Projeto acadêmico desenvolvido para a disciplina de **Redes Neurais**, com o objetivo de explorar a utilização de redes neurais artificiais na compressão de dados e na detecção de anomalias por meio de Autoencoders.

A proposta utiliza o conjunto de dados **MNIST**, composto por imagens de dígitos manuscritos, para investigar a capacidade de uma rede neural de aprender padrões visuais, comprimir representações e identificar dados que fogem do padrão aprendido.

---

## 🎯 1. Objetivo

Desenvolver um protótipo capaz de comprimir e reconstruir imagens utilizando uma arquitetura Autoencoder, explorando o erro de reconstrução como mecanismo para identificação de anomalias.

O projeto busca demonstrar como uma rede neural pode aprender a representar determinados padrões de dados sem precisar conhecer previamente todas as possíveis variações existentes.

### Objetivos específicos

- Compreender o funcionamento de uma arquitetura Autoencoder.
- Explorar a redução de dimensionalidade por meio de representações latentes.
- Implementar um mecanismo de reconstrução de imagens.
- Investigar a utilização do erro de reconstrução para detecção de anomalias.
- Comparar os resultados do Autoencoder com uma abordagem tradicional baseada em PCA.
- Avaliar o desempenho utilizando métricas adequadas ao problema.

---

## 🔍 2. Problema proposto

Como identificar imagens que apresentam características diferentes dos padrões aprendidos por uma rede neural?

Para investigar essa questão, será desenvolvido um cenário experimental utilizando o MNIST.

O modelo será treinado exclusivamente com imagens correspondentes ao dígito **0**. Posteriormente, receberá imagens contendo outros dígitos, avaliando sua capacidade de reconstrução e identificando possíveis anomalias por meio do erro obtido.

### Funcionamento esperado

1. Receber uma imagem de entrada.
2. Comprimir sua representação utilizando o Encoder.
3. Reconstruir a imagem utilizando o Decoder.
4. Calcular o erro entre a imagem original e a reconstruída.
5. Comparar o erro com um limiar de decisão (*threshold*).
6. Classificar a entrada como normal ou anômala.

**Categorias experimentais:**

| Categoria | Representação | Classificação esperada |
|---|---|---|
| Normal | Dígito 0 | Normal |
| Anomalia | Dígitos 1 a 9 | Anomalia |

> Importante: a definição de anomalia é contextual. Neste experimento, os demais dígitos serão considerados anômalos em relação ao padrão específico aprendido pelo modelo, e não por apresentarem alguma irregularidade intrínseca.

---

## 📊 3. Conjunto de dados

**MNIST — Modified National Institute of Standards and Technology Database**

O MNIST é um conjunto de dados amplamente utilizado em estudos de aprendizado de máquina e visão computacional.

Contém imagens de dígitos manuscritos de 0 a 9, representadas em escala de cinza.

| Característica | Descrição |
|---|---|
| Total de imagens | 70.000 |
| Treinamento original | 60.000 imagens |
| Teste original | 10.000 imagens |
| Dimensões | 28 × 28 pixels |
| Classes | 10 dígitos (0–9) |
| Canais | 1 (escala de cinza) |
| Formato de entrada | Matrizes de pixels |

**Origem:** [MNIST Dataset — Kaggle](https://www.kaggle.com/datasets/hojjatk/mnist-dataset)

O conjunto também poderá ser carregado diretamente pela biblioteca Keras, facilitando sua utilização no Google Colab.

---

## 🧩 4. Metodologia

O desenvolvimento será dividido em cinco etapas principais.

### 4.1. Preparação dos dados

- Carregamento do MNIST.
- Análise exploratória das imagens.
- Identificação e separação dos dígitos.
- Normalização dos valores dos pixels para o intervalo [0, 1].
- Separação dos conjuntos de treinamento, validação e teste.
- Organização dos dados normais e anômalos.

### 4.2. Baseline — PCA

Será implementada uma abordagem baseada em **Principal Component Analysis (PCA)** como referência para comparação.

O PCA permite reduzir a dimensionalidade dos dados e reconstruir suas representações originais, possibilitando avaliar a relação entre compressão e qualidade da reconstrução.

A comparação permitirá investigar as diferenças entre uma técnica estatística de redução dimensional e uma arquitetura baseada em redes neurais.

### 4.3. Arquitetura Autoencoder

O modelo será composto por duas estruturas principais:

- **Encoder:** responsável por comprimir a imagem original em uma representação latente.
- **Decoder:** responsável por reconstruir a imagem a partir dessa representação.

Arquitetura inicial proposta:

| Camada | Neurônios |
|---|---:|
| Entrada | 784 |
| Encoder | 128 |
| Encoder | 64 |
| Espaço latente | 16 |
| Decoder | 64 |
| Decoder | 128 |
| Saída | 784 |

A arquitetura poderá ser modificada durante os experimentos.

### 4.4. Treinamento

O Autoencoder será treinado utilizando exclusivamente imagens do dígito zero.

Configurações inicialmente previstas:

- Função de ativação: ReLU nas camadas ocultas.
- Ativação de saída: Sigmoid.
- Função de perda: Mean Squared Error (MSE).
- Otimizador: Adam.
- Ambiente: Google Colab.

Também serão investigadas diferentes dimensões do espaço latente, permitindo avaliar como a intensidade da compressão influencia a reconstrução.

### 4.5. Detecção de anomalias

A identificação será baseada no erro de reconstrução.

Imagens que apresentarem erros superiores ao limiar estabelecido serão classificadas como anômalas.

O limiar será definido a partir dos dados de validação, evitando utilizar o conjunto de teste para ajustar o modelo.

---

## 📈 5. Avaliação dos resultados

A avaliação considerará tanto a capacidade de reconstrução quanto a identificação de anomalias.

**Métricas previstas:**

| Métrica | Finalidade |
|---|---|
| MSE | Avaliar o erro de reconstrução |
| Precision | Avaliar a confiabilidade das detecções positivas |
| Recall | Avaliar a proporção de anomalias identificadas |
| F1-score | Avaliar o equilíbrio entre Precision e Recall |
| ROC-AUC | Avaliar a capacidade de discriminação do modelo |
| Matriz de confusão | Visualizar acertos e erros de classificação |

Os resultados do Autoencoder serão comparados com a baseline baseada em PCA.

Também serão apresentados exemplos visuais de reconstruções corretas e incorretas.

---

## 🛠️ 6. Tecnologias utilizadas

| Tecnologia | Aplicação |
|---|---|
| Python | Linguagem principal |
| Google Colab | Ambiente de desenvolvimento |
| TensorFlow / Keras | Implementação da rede neural |
| NumPy | Manipulação dos dados |
| Matplotlib | Visualização dos resultados |
| Scikit-learn | PCA e métricas de avaliação |
| Git / GitHub | Versionamento e documentação |

---

## 📁 7. Organização do projeto

```text
ImageGuard/
│
├── notebooks/
│   └── ImageGuard.ipynb
│
├── images/
│   └── resultados/
│
├── docs/
│   └── apresentacao.pdf
│
├── README.md
│
└── requirements.txt
```

A organização poderá ser expandida conforme o desenvolvimento do projeto.

---

## ⚠️ 8. Limitações e considerações

O projeto apresenta um cenário experimental controlado, no qual a definição de normalidade está restrita a uma única classe de imagens.

Algumas limitações previstas:

- O erro de reconstrução não garante a identificação de todas as anomalias.
- Imagens de classes diferentes podem apresentar características visuais semelhantes.
- A escolha do limiar influencia diretamente os resultados.
- A qualidade da reconstrução pode variar conforme a dimensão do espaço latente.
- O MNIST possui imagens relativamente simples, não representando toda a complexidade de aplicações reais de visão computacional.

Os resultados deverão ser interpretados considerando essas limitações.

---

## 🚀 9. Execução

O projeto será desenvolvido no Google Colab.

Para executar:

1. Acesse o notebook disponibilizado no diretório `notebooks/`.
2. Abra o arquivo no Google Colab.
3. Execute as células sequencialmente.
4. Aguarde o carregamento dos dados e o treinamento do modelo.
5. Observe as reconstruções e os resultados da detecção de anomalias.

As dependências necessárias estarão documentadas em `requirements.txt`.

---

## 👥 10. Integrantes

| Integrante | Responsabilidade |
|---|---|
| A definir | Desenvolvimento e experimentação |
| A definir | Preparação e análise dos dados |
| A definir | Avaliação e documentação |

*As responsabilidades poderão ser atualizadas durante o desenvolvimento.*

---

## 📚 11. Referências

- KINGMA, D. P.; WELLING, M. Auto-Encoding Variational Bayes. 2013. [arXiv:1312.6114](https://arxiv.org/abs/1312.6114).
- HINTON, G. E.; SALAKHUTDINOV, R. R. Reducing the Dimensionality of Data with Neural Networks. Science, 2006. [DOI: 10.1126/science.1127647](https://doi.org/10.1126/science.1127647).
- LECUN, Y. et al. Gradient-Based Learning Applied to Document Recognition. Proceedings of the IEEE, 1998.
- [TensorFlow — Introduction to Autoencoders](https://www.tensorflow.org/tutorials/generative/autoencoder).
- [Keras — MNIST Dataset](https://keras.io/api/datasets/mnist/).

---

**Projeto acadêmico — Redes Neurais**  
Desenvolvido com finalidade educacional e experimental.
