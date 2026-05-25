# Sistema Inteligente da Colônia Aurora Siger — Capítulo 1

Sistema integrado que representa o funcionamento autônomo da colônia
marciana **Aurora Siger**, aplicando os conceitos trabalhados ao longo
de toda a fase.

> Projeto desenvolvido apenas com **Python puro** (sem bibliotecas
> externas: nada de NumPy, Pandas, sklearn, Matplotlib).
> Foco em lógica, organização e interpretação dos dados.

## Como funciona

O sistema segue o ciclo clássico **buscar → decodificar → executar**
(cap. 6 — von Neumann):

1. **BUSCAR** — sensores geram dados de energia, consumo, clima.
2. **DECODIFICAR** — o sistema organiza em estruturas, aplica lógica
   booleana, prevê comportamentos com regressão e simula a geração
   física de energia.
3. **EXECUTAR** — gera uma ação clara: manter sistemas normais,
   reduzir consumo, ativar modo de economia ou modo de emergência.

## Capítulos aplicados

| Capítulo | Tema | Onde aparece |
|----------|------|--------------|
| 2 | Lógica booleana, mintermos, simplificação | `02_logica_booleana.ipynb`, `decidir_acao` |
| 3 | Subalgoritmos, parâmetros default, recursividade | `05_decisoes.ipynb`, `propagar_alerta` |
| 4 | Tabela hash, hierarquia (árvore) | `01_dados_colonia.ipynb`, `buscar_sensor` |
| 5 | Vetores 1D como listas | Históricos de sensores |
| 6 | Ciclo buscar→decodificar→executar | `00_main.ipynb` (parte 6) |
| 7 | Regressão linear simples, R² | `03_previsao.ipynb` |
| 8 | Potência eólica, Betz, curva cut-in/cut-out | `04_energia.ipynb` |

## Estrutura do projeto

```
aurora-siger/
├── 00_main.ipynb              # Notebook principal autossuficiente
├── 01_dados_colonia.ipynb     # Estruturas e hash (caps. 4, 5)
├── 02_logica_booleana.ipynb   # AND/OR/NOT, mintermos (cap. 2)
├── 03_previsao.ipynb          # Regressão linear (cap. 7)
├── 04_energia.ipynb           # Geração solar/eólica (cap. 8)
├── 05_decisoes.ipynb          # Decisões e recursividade (caps. 2, 3)
└── README.md
```

Cada notebook é **autossuficiente**: roda do começo ao fim sem
depender dos outros.

## Como executar

Abra qualquer um dos notebooks `.ipynb` no Jupyter, VS Code ou
Google Colab e execute as células em ordem. Recomendado começar pelo
**`00_main.ipynb`**, que integra tudo.

## Exemplo de entrada e saída

**Entrada** (dados lidos dos sensores):

```
energia (geração total) = 40
consumo total           = 70
tempestade prevista     = False
```

**Processamento** — aplica `if energia < 50 então reduzir consumo`.

**Saída**:

```
[MEDIO] REDUZIR CONSUMO
```

### Cenários de decisão (lógica booleana)

| Entrada | Saída |
|---------|-------|
| energia=25, consumo=70 | `[CRITICO] ATIVAR MODO DE EMERGENCIA` |
| energia=45, consumo=40, tempestade=Sim | `[ALTO] ATIVAR MODO DE ECONOMIA` |
| energia=48, consumo=35 | `[MEDIO] REDUZIR CONSUMO` |
| energia=90, consumo=50 | `[NORMAL] MANTER SISTEMAS NORMAIS` |

### Previsão por regressão linear (cap. 7)

```
Entrada: histórico vento = [8, 10, 12, 13, 15]
         histórico geração = [18, 21, 25, 27, 31]
         vento previsto = 11
Saída  : energia estimada ≈ 22.96  (R² ≈ 0.997)
```

### Curva eólica em Marte (cap. 8)

Com ρ = 0,020 kg/m³ (atmosfera marciana), área = 12 m², Cp = 0,40:

| Vento | Estado | Potência |
|-------|--------|----------|
| 2 m/s | PARADA | 0 W |
| 5 m/s | GERANDO (região cúbica) | 6,0 W |
| 12 m/s | NOMINAL (saturada) | 82,9 W |
| 26 m/s | DESLIGADA (vento forte) | 0 W |

Constante de Betz: Cp_max = 16/27 ≈ 0,593.

## Conceitos aplicados

- **Estruturas de dados**: listas (vetores), dicionários (hash) e
  hierarquia (árvore não-binária);
- **Lógica computacional**: `if/elif/else`, operadores `and/or/not`,
  mintermos e simplificação algébrica;
- **Modularização**: funções pequenas, parâmetros default,
  recursividade com condição de parada;
- **Modelagem matemática**: regressão linear pelo método dos mínimos
  quadrados com R²;
- **Energia renovável**: fórmula da potência eólica
  ($P = \tfrac{1}{2} \rho A v^3$), limite de Betz, curva de operação,
  geração solar fotovoltaica;
- **Arquitetura de von Neumann**: ciclo buscar → decodificar → executar
  como loop principal do sistema.
