# supervised_detection_some_ip — versão Colab (T4)

Cópia **modificada** do repositório
[Alkhatibnatasha/supervised_detection_some_ip](https://github.com/Alkhatibnatasha/supervised_detection_some_ip)
(LSTM/RNN/Transformer **binário**, 58 features, janela 128), preparada para rodar numa **GPU T4**.
(O `README.md` original do repo foi preservado.)

## Como usar
Abra **`Reproducao_Colab_T4.ipynb`** no Google Colab (Runtime → T4) e rode as células. O notebook
é autossuficiente: clona o repo original, **aplica os ajustes**, baixa o dataset (Dropbox),
organiza em `train/valid/test` e roda `train` + `predict`.

## Ajustes que fizemos (sem eles, o repo não roda)
1. **`output_dir` absoluto** em `network_configuration_1/someip_lstm.py` — o dataloader faz
   `os.chdir`, que quebra caminhos relativos.
2. **Organização dos dados**: o download vem em 4 pastas por ataque
   (`Error_on_error`, `Error_on_event`, `Missing_request`, `Missing_response`); o código espera
   `data/{train,valid,test}` planas → script de split 70/15/15.
3. **Modo de avaliação = `predict`** (o README diz `test`; as opções reais são `train/predict/time`).
4. **`stride` moderado** (16) — `stride=1` gera centenas de milhares de janelas (estoura a RAM).

## Escopo (honesto)
Reproduz o detector **binário do Alkhatib nos dados dele**. **Não** habilita testar o modelo no
nosso tráfego gerado — para isso faltaria o **extrator cru→58 features**, que o repo não publica
(consome pickles pré-processados).

## Conteúdo
- `network_configuration_1/` — entrypoints (`someip_lstm.py` já com os patches), variantes rnn/mlp/transformer.
- `lstm/`, `rnn/`, `transformer/` — modelos + dataloaders.
- **Sem** os dados (baixados pelo notebook) e **sem** pesos.
