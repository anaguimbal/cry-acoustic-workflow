# cry-acoustic-workflow
PT: Workflow automatizado para segmentação de ciclos respiratórios e extração de parâmetros acústicos de choro neonatal utilizando Praat e Python. EN: Automated workflow for respiratory cycle segmentation and acoustic parameter extraction of neonatal cry using Praat and Python.

### 1\. Objetivo

  * **Objetivo Central:** Padronizar um fluxo de trabalho bioacústico no software Praat para analisar a expressividade prosódica do choro de bebês gemelares pré-termo. O foco é garantir a reprodutibilidade e precisão na segmentação dos ciclos respiratórios (inspiração, expiração e pausa).

### 2\. Requisitos e Dependências

  * **Software Principal:** Praat (versão estável 6.4.43).
  * **Automação:** Scripts em Python, utilizando as bibliotecas *Parselmouth* (interface com Praat) e *Librosa*.

### 3\. Metodologia e Workflow

O `workflow` automatizado realiza:

  * **Segmentação:** O Praat é usado para segmentação manual via *TextGrid* em seis rótulos padronizados para ciclos respiratórios, incluindo categorias para ruído (E\#, E\#ruído, I\#, I\#ruído, P\#, P\#ruído).
  * **Extração de Pitch (f0):** O método padrão-ouro é a Autocorrelação Filtrada, com faixa de frequência fundamental ajustada para 200 Hz a 3500 Hz e *voice thresholding* de 0.65, adequados para voz neonatal.
  * **Classificação Automatizada:** Scripts em Python (Google Colab) utilizam três descritores principais para a classificação binária de cada janela do sinal:
      * **RMS (Raiz Quadrática Média):** Para distinguir silêncio/pausa de atividade sonora.
      * **ZCR (Taxa de Cruzamento por Zeros):** Para identificar ruído turbulento, típico da inspiração.
      * **Frequência Fundamental (f0):** Para identificar trechos de fonação estável (expiração).
  * **Processamento em Lote:** O script está estruturado para processar em lote diversos formatos de áudio (.wav, .mp3, .flac, .m4a) e gerar arquivos *TextGrid* e resumos estatísticos em formato CSV.

### 4\. Dados e Estrutura do Repositório

  * **Estrutura de Dados:** 
      * **audio_samples:** contém amostras representativas dos sinais de áudio em formato .wav (sem perdas), utilizadas para a extração das métricas acústicas. 
      * **scripts_textgrid:** reúne os algoritmos de processamento utilizados na segmentação dos eventos acústicos de inspiração, expiração, pausa e ruído. Os arquivos seguem o protocolo de nomenclatura cronológico e funcional (ex: script35_MZ), onde o sufixo identifica a zigosidade do par.
      * **acoustic_parameters:** armazena as tabelas estruturadas com os parâmetros acústicos extraídos. 
 
  * **Corpus de Validação:** O *workflow* foi validado com um *corpus* de 25 amostras de choro neonatal pré-termo, que representam condições biológicas e acústicas diversas, incluindo ruído hospitalar (amostragem intencional).
  * **Anonimização:** Os dados são identificados por códigos alfanuméricos (ex: **48\_MZ\_3\_2de3**) em conformidade com a LGPD, garantindo o sigilo.

### 5\. Transparência e Reprodutibilidade

  * O repositório é público e hospeda o *workflow* completo e os scripts de extração de dados, permitindo que outros pesquisadores repliquem a metodologia.
  * As matrizes de comparação e testes de padronização (validação do *workflow*) estão disponíveis para consulta.

