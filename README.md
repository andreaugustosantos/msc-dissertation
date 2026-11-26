# MSC Dissertation

Este trabalho estuda se a exposição de uma firma a minerais críticos, medida nas earnings calls, está associada ao valor da firma.

Aqui está o código que lê os transcripts, monta as medidas de exposição e roda todas as análises. Ele gera os números de todas as tabelas e as figuras de dados.

## Dados

Os transcripts e os dados financeiros vêm da LSEG Workspace, sob licença, e não podem ser publicados. Quem tem acesso à LSEG pode coletá-los de novo seguindo as especificações. Os dados financeiros foram extraídos com o add-in da LSEG para Excel.

O código espera esta estrutura:

```
pasta-mãe/
    codigo/        os scripts deste repositório
    dados/
        Processed_Data_Dissertacao.csv          saída do 01 (uma linha por transcript)
        LSEG_Descriptives_UNBALANCED_v2.xlsx    sede, mercado e setor TRBC (mercados originais)
        LSEG_Descriptives_EXPANSION.xlsx        idem (Canadá e resto da Europa)
        financeiros/                            as 13 planilhas LSEG_ChungPruitt_*.xlsx
    transcripts/   os .txt da LSEG (só para o 01 e o 03)
    resultados/    criada pelos scripts
```

A classificação manual das menções a terras raras usada pelo script 09 (Tabela 18, linhas 18 e 19) também não está aqui; está disponível comigo, sob pedido.

## Como rodar

```
pip install -r requirements.txt
cd codigo
python 01_nlp.py           # lê os transcripts (cerca de 2h30)
python 00_rodar_tudo.py    # todo o resto, na ordem (cerca de 1h30)
```

Para rodar só alguns scripts: `python 00_rodar_tudo.py 11_ddd_crma.py 18_fig_crma.py`.

O último script (24) compara os resultados com as tabelas. Ele procura uma cópia da pasta `tables/` do Overleaf em `pasta-mãe/tabelas_dissertacao/`, ou na pasta indicada: `python 24_conferencia.py <pasta>`.

O wild bootstrap, a randomização e o Romano-Wolf usam sorteios com semente fixa (20261024), então rodar de novo com os mesmos dados dá os mesmos p-valores.

## Scripts

| Script | O que faz | Resultado |
|---|---|---|
| 01 | Marca menções a minerais e tecnologias em cada transcript | Medidas de exposição |
| 02 | Monta o painel firma-trimestre; validação; setores | Tabelas 3, 4 e 5 |
| 03 | Extrai as menções a terras raras dos EUA para a classificação manual | Planilha para o 09 |
| 04 | Recalcula o Q de Tobin nas planilhas da LSEG | Conferência |
| 05 | Equação (6); produtoras; inferência | Tabelas 6, 7 e 17 |
| 06 | Robustez; teste agrupado de H2 | Tabelas 16, 18 e 19 |
| 07 | Timing da menção; firmas com divulgação trimestral | Tabelas 17 e 18 |
| 08 | Medição de terras raras e amostra | Tabela 18 |
| 09 | Classificação manual das menções | Tabela 18 |
| 10 | Q defasado; Romano-Wolf com dez sementes | Tabela 19 |
| 11 | Tripla diferença do CRMA: pareamento, estimativa, estudo de evento | Tabelas 8, 20, 21 e 23 |
| 12 | Tripla diferença só na Europa | Tabela 21 |
| 13 | Verificações extras da tripla diferença | Tabelas 21 e 22 |
| 14 | Diferença em diferenças da China | Tabela 9 |
| 15 | China, tirando uma indústria por vez | Tabela 9 |
| 16 | China: outros minerais e tendências por indústria | Tabela 24 |
| 17 a 19 | Figuras | Figuras 2 a 9 |
| 20 a 23 | Tabelas em LaTeX | Tabelas 1 a 5, 11, 12, 14 a 16, 19 e 21 a 24 |
| 24 | Confere todas as tabelas contra os resultados | Todas as tabelas |

Funções usadas por vários scripts: `caminhos.py` (pastas), `ddd_core.py` e `sector_map.py` (tripla diferença), `wcr.py` (wild bootstrap e Romano-Wolf) e `estilo_tabelas.py` (formato das tabelas).

O 24 confere os números célula por célula.

## Versões

Testado com Python 3.12 e os pacotes de `requirements.txt`.

André Augusto Santos

