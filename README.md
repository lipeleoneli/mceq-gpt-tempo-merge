# Assistência do GPT e tempo até o merge de pull requests

Projeto Final de MCEQ 12576 (PUC-Campinas, 2º semestre de 2026). Equipe: Rafael Roveri Pires e Felipe Nonato Leoneli.

## Pergunta

Em projetos open source no GitHub, pull requests em que os desenvolvedores usaram assistência do GPT têm menor tempo até o merge do que pull requests sem essa assistência?

- H0: μA = μB. H1 (unilateral): μA < μB. A = PRs com GPT, B = PRs sem GPT.
- Estudo observacional: os resultados indicam associação, não causa.
- Protocolo em [`protocolo/protocolo.pdf`](protocolo/protocolo.pdf): redigido em 26/11/2026, depois da análise. Documenta o plano executado no notebook; não é um pré-registro.

## Dados

- Fonte: Collante et al., "The Impact of Large Language Models (LLMs) on Code Review Process", arXiv 2508.11034 (v2), https://arxiv.org/abs/2508.11034
- Arquivo: `R/RQ1/at_resolution.csv` do repositório https://github.com/acollant/GPT-Assistance-PR
- Versão: commit `72df511069ee0255c44460839de55b69c9a5549a`
- SHA-256 do arquivo: `a002720ff6c8ce8bd4a42e4ea94214deead2d0bd101c62b08bdc012f68b24610`
- Data de acesso: 25/11/2026
- Licença: o repositório de origem não declara licença. Por isso o CSV não é redistribuído aqui: o notebook o baixa da fonte original, no commit fixado.

## Como reexecutar

```
pip install -r requirements.txt
jupyter nbconvert --to notebook --execute --inplace analise.ipynb
```

Também funciona no Google Colab: abra o `analise.ipynb` e use "Executar tudo".

O notebook:

1. baixa os dados brutos para `dados/brutos/` e confere o SHA-256 do arquivo;
2. aplica a limpeza do protocolo e grava `dados/limpos/prs_limpos.csv`;
3. gera a estatística descritiva e a figura `figuras/boxplot_tempo_merge.png`;
4. roda o teste confirmatório (Mann-Whitney U unilateral, α = 0,05), o Cliff's delta e o IC de 95% por bootstrap (semente 2026);
5. roda a análise de sensibilidade (Welch sobre log(1 + horas));
6. roda a análise exploratória E1 (projeto como unidade de análise), fora do protocolo;
7. grava os números em `resultados/resultados.json` e a Tabela 1 em `resultados/tabela1_descritiva.csv`.

Os números do artigo são os que o notebook imprime e grava em `resultados/`.

## Estrutura

```
analise.ipynb                      análise completa, do dado bruto aos números do artigo
requirements.txt                   bibliotecas
protocolo/                         protocolo de 1 página (registro retrospectivo), docx e pdf
artigo/                            artigo no template ACM
figuras/boxplot_tempo_merge.png    Figura 1 do artigo (gerada pelo notebook)
resultados/                        testes, efeitos, ICs e Tabela 1 (gerados pelo notebook)
dados/brutos/                      criado pelo notebook (download, não versionado)
dados/limpos/                      criado pelo notebook (não versionado)
```
