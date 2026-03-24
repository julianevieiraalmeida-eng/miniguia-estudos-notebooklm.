# 🧬 Miniguia de Estudos: Genômica e Bioinformática de Ciliados
**Projeto prático para o desafio NotebookLM da DIO.**

## 🎯 Contexto e Objetivos
Este caderno temático explora a complexidade genômica dos ciliados (focando em genomas altamente fragmentados e dimorfismo nuclear). O objetivo é utilizar a IA para extrair pipelines de bioinformática e mapear as metodologias de montagem de genomas a partir de dados brutos (FASTQ).

**Objetivos de Aprendizagem:**
1. Mapear metodologias de montagem de genomas a partir de dados brutos (FASTQ).
2. Entender o impacto do dimorfismo nuclear na bioinformática.
3. Exercitar a engenharia de prompts para sintetizar literatura científica complexa.

## 📚 Curadoria de Fontes
Os seguintes documentos técnicos e artigos científicos foram carregados no Google NotebookLM:
1. **[Rao et al., 2025]** - *Hijacking and integration of algal plastids and mitochondria in a polar planktonic host* - Current Biology.
2. **[Seah et al., 2024]** - *Nuclear dualism without extensive DNA elimination in the ciliate Loxodes magnus* - PNAS.
3. **[Almeida, 2026]** - *Mineração Genômica em Strombidium stylifer: Identificação de alvos biotecnológicos e caracterização de um cluster híbrido betalactona-terpeno* - UFPA.
4. **[Chen et al., 2021]** - *The hidden genomic diversity of ciliated protists revealed by single-cell genome sequencing* - BMC Biology.
5. **[McManus et al., 2018]** - *Strombidium rassoulzadegani: A Model Species for Chloroplast Retention in Oligotrich Ciliates* - Frontiers in Marine Science.

## 🛠️ Engenharia de Prompts e "Cicatrizes" (Troubleshooting)
Abaixo, o registro do processo iterativo de extração de dados no NotebookLM:

### Teste 1: Montagem do Genoma
* **Prompt Inicial:** *"Resuma como os autores montaram o genoma dos ciliados."*
* **Resultado Obtido:**
> A montagem dos genomas de ciliados descrita nas fontes envolveu estratégias avançadas para lidar com a arquitetura nuclear dual e a extrema fragmentação. Os principais métodos foram:
> 1. Triagem Nuclear (FANS) e Genômica de Célula Única (com MDA/MALBAC).
> 2. Uso combinado de PacBio HiFi para leituras longas e Illumina (NovaSeq 6000) para profundidade.
> 3. Processamento com Kraken, SPAdes e Falcon.

* **Cicatriz/Ajuste (O pulo do gato):** A IA foi muito rasa. Como engenheiro, preciso dos parâmetros. Refinei o prompt para: *"Atue como um bioinformata. Liste o pipeline exato utilizado para o tratamento de dados brutos (FASTQ) e a montagem do macronúcleo. Separe as ferramentas usadas (ex: Trimmomatic, SPAdes)."*

* **Resultado Final (Refinado):**
> Como bioinformata, detalharei o pipeline técnico:
> **1. Controle de Qualidade:** Fastp v0.20.1 e Trimmomatic 0.39 (Flags: `LEADING:20 TRAILING:20 SLIDINGWINDOW:4:25 MINLEN:120 AVGQUAL:28`).
> **2. Filtragem de Contaminantes:** Kraken e MetaGeneMark v3.38, seguidos de busca via DIAMOND e mapeamento negativo com Bowtie 2.4.1.
> **3. Montagem do Macronúcleo:** Para Illumina, utilizou-se SPAdes v3.13.0 (opção `--sc` e k-mers `-k 61, 71, 77, 81`). Para PacBio, utilizou-se Flye v2.8.1 e Falcon, com polimento via Racon v1.4.20.
> **4. Avaliação:** Métricas validadas por QUAST v5.0.2, EukCC e BUSCO v4.0.6.

---

## 📖 Miniguia de Estudo Consolidado

### 1. Resumo Estruturado: Genômica de Ciliados
A análise genômica de ciliados é um desafio computacional devido ao dimorfismo nuclear, onde o macronúcleo (MAC) apresenta genoma altamente fragmentado (nano-cromossomos) e poliploide. Os artigos analisados demonstram que pipelines tradicionais precisam de ajustes rigorosos no tratamento de dados FASTQ, priorizando montadores baseados em grafos de De Bruijn (como SPAdes ou Megahit) ou focados em leituras longas (Falcon) para lidar com a vasta quantidade de telômeros e a ploidia complexa. A separação física ou *in silico* de contaminantes (como bactérias e algas ingeridas) é uma etapa crítica antes da montagem.

### 2. Glossário Técnico
* **Dimorfismo Nuclear:** Presença de dois tipos de núcleos na mesma célula (MAC funcional e MIC germinativo), exigindo algoritmos de montagem capazes de separar essas duas bibliotecas de DNA.
* **FASTQ:** Formato de arquivo de texto que armazena sequências biológicas e as respetivas pontuações de qualidade (Phred score) geradas pelos sequenciadores.
* **Nano-cromossomos:** Fragmentos genômicos extremamente curtos encontrados no macronúcleo de alguns ciliados, muitas vezes contendo apenas um único gene ladeado por telômeros.
* **K-mers:** Subsequências de tamanho "k" utilizadas por algoritmos de montagem (como o SPAdes) para construir os grafos de De Bruijn e remontar o genoma.
* **Polimento de Genoma:** Etapa final da bioinformática (usando ferramentas como Racon) para corrigir pequenos erros de sequenciamento nas montagens de leituras longas.

### 3. Prompts Reutilizáveis para Revisões Futuras
* *"Atue como professor de bioprocessos. Crie 3 questões de escolha múltipla focadas nas dificuldades de aplicar o algoritmo de De Bruijn na montagem de nano-cromossomos."*
* *"Explique, com base nos artigos, por que a filtragem de contaminantes com ferramentas como o Kraken é essencial antes de iniciar a montagem do genoma de um ciliado pelágico."*
