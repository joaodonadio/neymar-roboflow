Aqui está o seu README do projeto do Neymar totalmente reescrito, adotando exatamente a mesma estrutura corporativa, técnica e organizada do seu projeto de Mushroom.

YOLOv8 Custom Detection: Neymar Jr. ⚽
Este repositório contém um pipeline completo de Visão Computacional focado na detecção customizada do jogador Neymar Jr. O projeto aborda desde o treinamento de uma rede neural convolucional via Transfer Learning até a otimização de scripts para inferência de vídeo em tempo real.

Autor: João Victor Donadio

ID / Registro: 4201058

📌 Visão Geral do Projeto
O objetivo principal deste projeto é construir um modelo de Deep Learning baseado na arquitetura State-of-the-Art YOLOv8 (Ultralytics), capaz de localizar e classificar o jogador Neymar Jr. em imagens, vídeos locais e transmissões do YouTube. O fluxo foi totalmente otimizado em ambiente Linux (.ipynb) para mitigar gargalos comuns de hardware e de dependências de interface gráfica.

🗂️ Estrutura de Pastas Recomendada
Para garantir a portabilidade do pipeline e permitir que o projeto seja clonado e executado em qualquer máquina, a estrutura do repositório está organizada da seguinte forma:

Plaintext
neymar-roboflow/
├── venv/                      # Ambiente virtual Python (isolamento de pacotes)
├── dataset-ney/               # Dataset exportado do Roboflow
│   └── neymar.v1i.yolov8/
│       └── data.yaml          # Configuração de caminhos e classes do dataset
├── notebooks/                 # Arquivos de desenvolvimento interativo
│   └── neymar_projeto.ipynb   # Notebook principal do projeto
├── modelo-neymar-best.pt      # Pesos do modelo treinado (gerado pós-treino)
└── README.md                  # Documentação do projeto
🛠️ Etapas do Pipeline de Visão Computacional
O desenvolvimento dentro do notebook seguiu rigorosamente as melhores práticas de Engenharia de Machine Learning e Visão Computacional:

1. Preparação do Dataset e Mapeamento Dinâmico
Caminhos Relativos: Implementação de varredura dinâmica de diretórios utilizando a biblioteca nativa os (os.path.dirname e os.getcwd()). Isso remove caminhos absolutos (hardcoded) e permite o funcionamento imediato do código após o git clone em qualquer computador.

2. Configuração de Hardware e Inicialização local
Aceleração por GPU: Configuração do ecossistema PyTorch alinhado à arquitetura CUDA 12.1, extraindo a máxima performance paralela dos núcleos da GPU NVIDIA GTX 1660 Ti.

Isolamento de Diretórios: Ajuste nos dicionários internos da Ultralytics (settings.update) para forçar o salvamento dos logs de treino na pasta ./runs interna do projeto, evitando poluir o diretório raiz do sistema (/root/.config).

3. Treinamento Otimizado (Transfer Learning)
Modelo Base: Utilização do modelo pré-treinado yolov8n.pt (YOLOv8 Nano), ideal para processamento em tempo real devido ao baixo custo computacional.

Gerenciamento de VRAM: Configuração estratégica de hiperparâmetros (imgsz=416 e batch=2) para blindar o ambiente contra estouros de memória gráfica (erros de Out of Memory) nos 6GB de VRAM da placa de vídeo.

4. Pipeline de Inferência Eficiente (Stream Processing)
Consumo via Geradores (Generators): Ativação do parâmetro stream=True na função de predição do YOLO. Essa técnica processa as mídias frame a frame, limpando o cache da memória RAM imediatamente após a exibição e evitando o travamento completo do sistema em vídeos longos.

Execução Headless: Utilização do pacote opencv-python-headless para processar e salvar os resultados direto em disco (save=True), mitigando falhas clássicas de renderização de tela e dependências quebradas do Qt/XCB no Linux.

5. Bypass de Bugs de API Externa
Otimização de Links: Implementação de suporte para leitura direta de URLs da web e tratamento interno para streams do YouTube via yt-dlp, contornando falhas nativas de tipagem (TypeError: NoneType) comumente encontradas ao enviar links brutos de redes sociais para o framework.

📈 Resultados Obtidos
O modelo treinado gerou com sucesso o arquivo de pesos finais best.pt.

Os testes de inferência em vídeos demonstraram alta taxa de assertividade na detecção do jogador, gerando arquivos de mídia anotados com caixas delimitadoras (bounding boxes) estáveis salvos automaticamente na pasta runs/detect/predict/.

💻 Como Executar o Projeto
Pré-requisitos
Certifique-se de ter instalado o Python 3.10+, git e uma GPU compatível com CUDA (opcional, mas recomendado para velocidade de treino).

Instalação e Configuração
Abra o seu terminal e execute o comando abaixo para clonar o repositório:

Bash
git clone https://github.com/joaodonadio/neymar-roboflow.git
cd neymar-roboflow
Crie e ative o ambiente virtual (venv):

Bash
python -m venv venv
source venv/bin/activate  # No Windows use: venv\Scripts\activate
Instale o PyTorch otimizado para CUDA 12.1:

Bash
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
Instale as dependências essenciais do ecossistema YOLO:

Bash
pip install ultralytics yt-dlp opencv-python-headless ipykernel
Execução do Pipeline
Inicie o VS Code ou o Jupyter Lab e abra a pasta do projeto.

Acesse o arquivo notebooks/neymar_projeto.ipynb.

Altere o Kernel do Notebook para rodar a partir da venv criada.

Execute as células sequencialmente para validar o hardware, iniciar o treinamento e rodar as predições de teste.

📋 Resumo Executivo do Pipeline
Em suma, este projeto automatiza e resolve de ponta a ponta o ciclo de desenvolvimento de um modelo de detecção de objetos para um alvo customizado, operando através das seguintes etapas integradas no notebook:

Snippet de código
graph TD
    A[Ambiente e Hardware] -->|Validação de VRAM/CUDA| B[Dataset Roboflow]
    B -->|Mapeamento Dinâmico os.path| C[Treinamento YOLOv8n]
    C -->|Geração do best.pt| D[Pipeline de Inferência]
    D -->|Bypass yt-dlp / Stream=True| E[Mídia Anotada em Disco]
Validação e Preparação do Ambiente: O script varre o sistema, ativa o uso da GPU (GTX 1660 Ti) com PyTorch/CUDA e reconfigura o diretório de saída do YOLO para garantir isolamento e portabilidade após o git clone.

Carregamento e Mapeamento Dinâmico: O pipeline localiza o arquivo data.yaml do dataset (Neymar) usando caminhos relativos de forma inteligente. Isso corrige erros de arquivos não encontrados (FileNotFoundError) causados pela estrutura de pastas do Jupyter Notebook.

Treinamento Otimizado: Realiza o Transfer Learning usando o modelo base yolov8n.pt. O treino é calibrado com resolução reduzida (imgsz=416) e lotes mínimos (batch=2) para evitar o congelamento do kernel e estouros de memória da placa de vídeo.

Inferência Otimizada e Salvamento: O modelo treinado final (modelo-neymar-best.pt) é submetido a testes de validação com imagens da web ou streams de vídeo do YouTube. O processamento é feito via gerador de consumo de frames (stream=True) e em modo headless (sem renderização de janelas abertas), salvando o vídeo final anotado diretamente na pasta local de resultados (runs/detect/predict/) com total estabilidade e zero consumo excessivo de memória RAM.