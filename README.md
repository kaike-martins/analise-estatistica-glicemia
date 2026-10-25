<div align="center">

# Análise Estatística de um Experimento de Redução da Glicemia

**Limpeza de dados e inferência estatística - teste de hipótese, valor-p e intervalo de confiança - sobre a eficácia de medicamentos e da dieta na redução da glicemia.**

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-150458?style=flat-square&logo=pandas&logoColor=white)
![SciPy](https://img.shields.io/badge/SciPy-8CAAE6?style=flat-square&logo=scipy&logoColor=white)
![FMU](https://img.shields.io/badge/FMU-Aquisi%C3%A7%C3%A3o_e_Prepara%C3%A7%C3%A3o_de_Dados-4B1D72?style=flat-square)

</div>

---

## Sobre o projeto

Trabalho individual da disciplina **Aquisição e Preparação de Dados** (Bacharelado em Ciência de Dados, FMU). O projeto parte de uma base de 500 pacientes, propositalmente suja e percorre o ciclo completo de dados em duas fases: **preparação** (limpeza rigorosa) e **análise estatística** (testes de hipótese).

> **Sobre os dados:** a base é didática, fornecida pela disciplina e deliberadamente cheia de erros para exercitar a limpeza. O valor deste repositório está na **metodologia** o rigor da limpeza e da inferência, não em uma descoberta clínica do mundo real.

## Objetivo

Cada paciente teve a glicemia medida antes e depois de um tratamento, recebeu exclusivamente um de dois medicamentos e seguiu, ou não, uma dieta. Com nível de significância de 5%, o trabalho avalia: se o tratamento reduziu a glicemia; qual medicamento é mais eficaz; se a dieta influencia a redução; e a confiabilidade e a causalidade do efeito da dieta.

## Metodologia

**Fase 1 - Preparação (pandas).** Diagnóstico em duas camadas, separando problemas de *formato* (texto grudado, vírgula decimal, datas em formatos mistos) de problemas de *plausibilidade* (glicemias negativas ou impossíveis, datas incoerentes). Principais tratamentos: padronização dos indicadores Sim/Não; remoção de registros logicamente inválidos (um medicamento por paciente); recuperação de valores de glicemia por faixa fisiológica; conversão e correção lógica de datas (inclusive 25 registros com início/fim invertidos, recuperados por evidência). Resultado: **500 → 393 registros válidos**.

**Fase 2 - Análise (SciPy).** Teste t pareado para o efeito antes/depois; teste t de Welch para comparar grupos independentes (medicamentos e dieta); intervalo de confiança de 95% para dimensionar o efeito; e checagem de variável de confusão antes de concluir sobre a dieta.

## Principais resultados

| Pergunta | Teste | Resultado |
|---|---|---|
| O tratamento reduz a glicemia? | t pareado | Sim, redução média ~32 mg/dL (p < 0,001) |
| Qual medicamento é melhor? | t de Welch | Remédio 1, ~9,7 mg/dL a mais (p < 0,001) |
| A dieta ajuda? | t de Welch | Sim, ~15,2 mg/dL a mais (p < 0,001) |
| A dieta **causa** a redução? | IC 95% + análise crítica | Associação sim; causalidade não (dado observacional) |

## Destaques técnicos

- Diagnóstico que evidencia por que *"zero valores nulos"* **não** significa *"base limpa"* — o problema era valor inválido disfarçado de válido.
- Validação por **faixa fisiológica** (conhecimento de domínio), e não por detecção estatística de outliers, que descartaria glicemias altas porém reais.
- Recuperação de datas invertidas **baseada em evidência**, não em suposição.
- **Controle de confusão** (dieta × medicamento) antes de afirmar o efeito da dieta.
- Distinção explícita entre **associação e causalidade** em dado observacional.

## Limitações

Estudo observacional e com base didática: sem randomização nem grupo controle, as conclusões são de **associação**, não de causa. A amostra foi reduzida de 500 para 393 registros válidos durante a limpeza.

## Tecnologias

Python · pandas · SciPy (stats) · Matplotlib · Jupyter Notebook

## Estrutura do repositório

```text
├── README.md                  → esta página
├── relatorio_glicemia.docx    → relatório (método, resultados, gráficos, bibliografia)
├── analise_glicemia.ipynb     → notebook com todo o código (aquisição → limpeza → testes)
└── glicemia_limpa.csv         → base tratada (393 registros)
```

## Reprodutibilidade

A base original é lida diretamente da URL da plataforma dentro do notebook; basta executar as células em ordem para refazer toda a limpeza e os testes.

## Autor

**Kaike Martins** — [github.com/kaike-martins](https://github.com/kaike-martins) · [linkedin.com/in/kaikemarttins](https://linkedin.com/in/kaikemarttins)
