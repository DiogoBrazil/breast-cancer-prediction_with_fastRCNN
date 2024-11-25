
# Detecção de Nódulos de Câncer de Mama usando Faster R-CNN

## Sumário
- Introdução
- Visão Geral do Projeto
- Objetivos
- Dataset
- Pré-requisitos
- Instalação
- Estrutura do Projeto
- Uso
- Treinamento do Modelo
- Teste do Modelo
- Resultados
- Autor

## Introdução
O câncer de mama é uma das principais causas de morte entre mulheres em todo o mundo. A detecção precoce aumenta significativamente as chances de um tratamento bem-sucedido. Este projeto visa auxiliar na detecção precoce do câncer de mama, desenvolvendo um modelo de deep learning usando Faster R-CNN para detectar nódulos em imagens de mamografia.

## Visão Geral do Projeto
Este repositório contém o código e os recursos para treinamento e teste de um modelo Faster R-CNN para detecção de nódulos de câncer de mama. O modelo é treinado em um dataset de imagens de mamografia anotadas com caixas delimitadoras ao redor dos nódulos.

O objetivo principal é implantar este modelo na Unidade de Pronto Atendimento de Ariquemes para auxiliar os profissionais de saúde na identificação de possíveis nódulos cancerígenos. O modelo também pode ser adaptado para uso em outras unidades de saúde.

## Objetivos
- Desenvolver um modelo Faster R-CNN robusto para detectar nódulos de câncer de mama em imagens de mamografia.
- Gerar pesos treinados que possam ser integrados a outras aplicações ou sistemas.
- Fornecer scripts para treinamento (`main.ipynb`) e teste (`test.ipynb`) do modelo.
- Facilitar a implantação do modelo em unidades de saúde para auxiliar na detecção precoce.

## Dataset
O dataset consiste em imagens de mamografia com caixas delimitadoras anotadas indicando a localização dos nódulos.
- As imagens estão organizadas em diretórios de treino, validação e teste.
- As anotações são fornecidas no formato Pascal VOC (.xml).
- **Nota:** Devido a restrições de privacidade e licenciamento, o dataset não está incluído neste repositório. Os usuários devem adquirir um dataset adequado separadamente e garantir a conformidade com todas as diretrizes legais e éticas.

## Pré-requisitos
- Python 3.7 ou superior
- PyTorch 1.7.0 ou superior
- Torchvision 0.8.1 ou superior
- CUDA (opcional, para suporte a GPU)
- Bibliotecas adicionais de Python:
  - numpy
  - matplotlib
  - Pillow
  - xmltodict

## Instalação

1. Clone o repositório:
   ```bash
   git clone https://github.com/DiogoBrazil/breast-cancer-prediction_with_fastRCNN.git
   cd breast-cancer-prediction_with_fastRCNN
   ```

2. Crie um ambiente virtual (Opcional, mas recomendado):
   ```bash
   python -m venv venv
   source venv/bin/activate  # No Windows, use 'venv\Scripts\activate'
   ```

3. Instale os pacotes necessários:
   ```bash
   pip install -r requirements.txt
   ```

   **Nota:** Se `requirements.txt` não for fornecido, instale os pacotes manualmente:
   ```bash
   pip install torch torchvision numpy matplotlib Pillow xmltodict
   ```

4. Verifique a instalação:
   ```bash
   python -c "import torch; print('PyTorch Version:', torch.__version__)"
   ```

## Estrutura do Projeto
- `main.ipynb`: Notebook Jupyter para treinamento do modelo Faster R-CNN.
- `test.ipynb`: Notebook Jupyter para testar o modelo treinado em novas imagens.
- `models/`: Diretório contendo definições de modelo e pesos salvos.
- `datasets/`: Diretório reservado para o dataset (não incluído).
- `utils/`: Scripts utilitários para manipulação e pré-processamento de dados.

## Uso

### Treinamento do Modelo

1. **Preparar o Dataset**:
   - Organize seu dataset em diretórios de treino, validação e teste.
   - Certifique-se de que cada imagem tenha um arquivo de anotação correspondente no formato Pascal VOC (.xml).

2. **Configurar os Parâmetros de Treinamento**:
   - Abra `main.ipynb`.
   - Defina os caminhos para seus diretórios de dataset:

     ```python
     train_dir = 'datasets/train'
     valid_dir = 'datasets/valid'
     test_dir = 'datasets/test'
     ```

   - Defina o número de classes (incluindo fundo):
     ```python
     num_classes = 3  # incluindo fundo
     ```

3. **Executar o Notebook de Treinamento**:
   - Execute cada célula em `main.ipynb` sequencialmente.
   - O modelo será treinado pelo número especificado de épocas (padrão é 100).
   - O progresso do treinamento e a perda serão exibidos.

4. **Salvar os Pesos Treinados**:
   - Após o treinamento, os pesos são salvos em `faster_rcnn_model.pth`:

     ```python
     torch.save(model.state_dict(), 'models/faster_rcnn_model.pth')
     ```

### Teste do Modelo

1. **Preparar a Imagem de Teste**:
   - Coloque a imagem de mamografia que deseja testar em um diretório acessível.
   - Anote o caminho para a imagem.

2. **Carregar o Modelo Treinado**:
   - Abra `test.ipynb`.
   - Certifique-se de que o caminho dos pesos do modelo esteja correto:

     ```python
     model.load_state_dict(torch.load('models/faster_rcnn_model.pth', map_location=device))
     ```

3. **Executar o Notebook de Teste**:
   - Defina o caminho para a imagem de teste:

     ```python
     img_path = 'path/to/your/test_image.jpg'
     ```

   - Execute as células do notebook para realizar a inferência.
   - O modelo preverá caixas delimitadoras para os nódulos detectados.

4. **Visualizar os Resultados**:
   - O notebook exibirá a imagem com caixas delimitadoras e rótulos.
   - Nódulos detectados serão destacados com caixas delimitadoras e escores de confiança.

## Resultados
O modelo Faster R-CNN treinado pode detectar eficazmente nódulos de câncer de mama em imagens de mamografia.
- Caixas delimitadoras são desenhadas ao redor dos nódulos detectados com escores de confiança.

## Autor
Diogo Brazil  
GitHub: [DiogoBrazil](https://github.com/DiogoBrazil)
