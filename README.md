# neymar-roboflow
⚽ YOLOv8 Custom Detection: Neymar Jr.
Este projeto consiste em um pipeline completo de Visão Computacional para detecção customizada do jogador Neymar Jr. utilizando a arquitetura YOLOv8 da Ultralytics. O dataset foi processado e exportado via Roboflow, e todo o fluxo de treinamento e inferência foi otimizado para rodar localmente utilizando aceleração por hardware (GPU).

O projeto foi totalmente desenvolvido em um ambiente isolado Linux (.ipynb).

🚀 Funcionalidades e Destaques Técnicos
Treinamento Customizado: Transfer Learning aplicado ao modelo YOLOv8 Nano para detecção de classe única.

Aceleração por Hardware: Configuração nativa do PyTorch com suporte a CUDA 12.1 para processamento paralelo na GPU NVIDIA GTX 1660 Ti.

Bypass de Bug do YouTube: Implementação de extração de stream via yt-dlp para contornar a falha nativa de tipagem (TypeError: NoneType) do framework Ultralytics ao ler vídeos/Shorts do YouTube.

Execução Headless: Configuração do OpenCV sem interface gráfica (opencv-python-headless) para mitigar falhas de plugins de renderização de tela (XCB/Qt) no Linux.

🛠️ Pré-requisitos e Ambiente
Para reproduzir este projeto, você precisará do Python 3.10+ instalado no seu sistema Linux/Windows.

Estrutura de Pastas Recomendada
Plaintext
neymar-roboflow/
├── venv/                       # Ambiente virtual Python
├── neymar.v1i.yolov8/          # Dataset exportado do Roboflow
│   └── data.yaml               # Arquivo de configuração do dataset
├── neymar_projeto.ipynb        # Notebook principal do projeto
└── README.md                   # Documentação do projeto
📦 Instalação e Configuração
Clone o repositório e navegue até a pasta:

Bash
cd caminho/para/seu/projeto/neymar-roboflow
Crie e ative o ambiente virtual (venv):

Bash
python -m venv venv
source venv/bin/activate
Instale o PyTorch com suporte a CUDA (Otimizado para GTX 1660 Ti):

Bash
   pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
Instale as dependências do ecossistema YOLO e utilitários:

Bash
pip install ultralytics yt-dlp opencv-python-headless ipykernel
💻 Como Executar
Todo o controle do projeto está centralizado no arquivo neymar_projeto.ipynb.

Certifique-se de que a sua venv está ativa.

Abra o arquivo no VS Code ou Jupyter Lab.

Altere o Kernel do Notebook para apontar para o Python da sua venv (venv/bin/python).

Execute as células sequencialmente:

Célula 1 e 2: Validação do ambiente e confirmação do uso da GTX 1660 Ti.

Célula 3 e 4: Inicialização do treinamento (gerando o arquivo best.pt em runs/detect/train/weights/).

Célula 5 e 6: Inferência com bypass do YouTube e salvamento do vídeo resultante em disco.

João Victor Donadio - 4201058