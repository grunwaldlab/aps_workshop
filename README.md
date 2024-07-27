# `pathogensurveillance` workshop

> 📗 This session is part of [**Nanopore Sequencing and Whole Genome Assembly and Annotation with nf-core/pathogensurveillance**](https://events.rdmobile.com/Sessions/Details/2316143)

<p align="center">
  <img src="content/conference_logo.png" alt="Conference Logo" width="150" style="margin-right: 20px;"/>
  <img src="content/OregonState_logo.png" alt="Oregon State University Logo" width="200" style="margin-right: 40px;"/>
  <img src="content/USDA_logo.png" alt="USDA Logo" width="200" style="margin-right: 20px;"/>
  <img src="content/nfcore_logo.png" alt="nf-core Logo" width="200"/>
</p>

---

<details>
<summary style="font-size: 1.5em; font-weight: bold;"> ♟️ Links to resources</summary>
  
- [`pathogensurveillance` repository](https://github.com/grunwaldlab/pathogensurveillance)
- [`psminer` repository](https://github.com/grunwaldlab/psminer)

</details>

---

<details>
<summary style="font-size: 1.5em; font-weight: bold;"> 🚩 Prerequisites @Camilo </summary>

#### 1. Gain some familiarity with Linux command-line interface
  Look here for resources:
  - [Command Line and Filesystem](https://open.oregonstate.education/computationalbiology/chapter/the-command-line-and-filesystem/)
  - [PCfB Appendices](content/PCfB_Appendices.pdf)

#### 2. GitHub account
  If you don't have one, please create an account by going to [GitHub](https://github.com):
  - [Creating an Account on GitHub](https://docs.github.com/en/get-started/start-your-journey/creating-an-account-on-github)

#### 3. Understanding of genomic terms:

  - **Annotation**: The process of identifying and marking the locations of genes and other features in a genome.
  - **Assembly**: The process of piecing together shorter DNA sequences into longer, continuous sequences known as contigs.
  - **BAM File**: A binary format for storing DNA sequence alignments.
  - **Bootstrap values**: Statistical measures that provide a confidence level for each branch in a phylogenetic tree.
  - **Contig**: A contiguous sequence of DNA that has been assembled from overlapping reads.
  - **Core genes**: Genes that are present in all genomes of a given species.
  - **Coverage**: The number of times a particular region of the genome is sequenced.
  - **FASTQ File**: A text-based format for storing both a nucleotide sequence and its corresponding quality scores.
  - **Genome**: The complete set of genes or genetic material present in a cell or organism.
  - **GFF file**: A file format used to hold information about gene annotations.
  - **Homology**: Similarity in sequence of a protein or nucleic acid between organisms due to shared ancestry.
  - **k-mers**: Substrings of length k that are used in various bioinformatics analyses.
  - **N50**: A statistic used to measure the quality of an assembly; the length of the shortest contig at 50% of the total assembly length.
  - **Pangenome**: The entire set of genes found in all strains of a particular species.
  - **Read Depth**: The number of times a nucleotide is read during sequencing.
  - **SNP (Single Nucleotide Polymorphism)**: A variation at a single position in a DNA sequence among individuals.
  - **Variant calling**: The process of identifying variants from sequence data.
  - **VCF (Variant Call Format)**: A file format used to store gene sequence variations.

#### 4. Understanding of the need for bioinformatics workflows

#### 5. Understanding the general role and input/output files
  
</details>

---

<details>
<summary style="font-size: 1.5em; font-weight: bold;">🧵Setting up Gitpod @Camilo </strong></h2></summary>

### What is Gitpod?

We are using *Gitpod* to provide hands-on experience with installing and using the pathogen surveillance pipeline we developed. [**Gitpod**](https://gitpod.io/) allows you to launch and enter Virtual Machines from your browser and gives you 50 free hours per calendar month, enough for this session.

### How do I sign up for Gitpod?

You MUST do the following steps before the workshop starts! It will take a few minutes to set up a **GitHub** account and a **Gitpod** account if you don't already have them:

### 1. **Step 00**  
   Click on [this link](https://gitpod.io/new#https://github.com/grunwaldlab/aps_workshop) in any desktop web browser (**Note: Safari sometimes has problems on a Mac, so use Chrome or Mozilla instead)**  
   ![Step 00](content/Untitled%206.png)

### 2. **Step 01**  
   It will ask you to sign up with a GitHub account. If you don't have one, please create an account at [GitHub](https://github.com).  
   ![Step 01](content/Untitled%207.png)

### 3. **Step 02**  
   Once you are signed in to GitHub, click on the Gitpod link above again. It will try to launch our Gitpod workspace using your GitHub login. You will need to give Gitpod permission to access (only) the email address on your GitHub account. Follow the Gitpod prompts to ensure you are a real human and won't misuse their resources. **Note: if it asks you to connect your LinkedIn, you can skip that - you will still get 50 hours :-)**

### 4. **Step 03**  
   Gitpod will ask you to select which code editor and which machine size to start. The defaults are fine. So just click **Continue**  
   ![Step 03](content/Untitled%208.png)

### 5. **Step 04**  
   Once the Gitpod workspace starts (typically in less than a minute), you will see the following in your desktop web browser: a file browser on your left, a text editor top right, and a Linux terminal bottom right.  
   ![Step 04](content/Untitled.jpeg)

> *If you are doing this before the workshop, please go to [gitpod.io/workspaces](https://gitpod.io/workspaces) to delete any running workspaces (in green) so that you don't use up your 50 hours per month* 🙂

</details>

---
<details>
<summary style="font-size: 1.5em; font-weight: bold;">🧵 Running the pathogensurveillance pipeline in gitpod @Zach </summary>

<aside>
<img src="content/logo.png" alt="content/logo.png" width="40px" /> nf-core/pathogensurveillance is a population genomic pipeline for pathogen diagnosis, variant detection, and biosurveillance. The pipeline accepts the paths to raw reads for one or more organisms (in the form of a CSV file) and creates reports in the form of interactive HTML reports or PDF documents. Significant features include the ability to analyze unidentified eukaryotic and prokaryotic samples, creation of reports for multiple user-defined groupings of samples, automated discovery and downloading of reference assemblies from NCBI RefSeq, and rapid initial identification based on k-mer sketches followed by a more robust core genome phylogeny and SNP-based phylogeny.

</aside>


```
nextflow run -latest -resume -profile conda 'https://github.com/grunwaldlab/pathogensurveillance' --sample_data aps_workshop.csv --out_dir output --download_bakta_db
```

</details>

---

<details>
<summary style="font-size: 1.5em; font-weight: bold;">🧵 Assessing read and assembly quality after ONT run @Martha</summary> 

Once a Nanopore run is complete, we need a way to critically assess read quality on a per sample basis, in order to decide if we can continue with downstream analysis.

---

### A note on how to organize reads after a Nanopore sequencing run

-   Once you complete a Nanopore run, you will need to **concatenate individual FASTQ files** within each sample sub-directory
-   If this is new for you:
    1.  Go to your sequencing run directory and locate `fastq_pass` sub-directory
    2.  For each barcoded sample, use the `cat` command to combined all smaller FASTQ files into single FASTQ file and then choose a desired name for this
    3.  Example command (assuming you are in your Nanopore run directory in the `fastq_pass` subdirectory, and you have a directory called `barcode01`): `cat barcode01/*.fastq.gz > barcode01.fastq.gz`

### Run NanoPlot to obtain read QC stats per barcoded sample

[NanoPlot](https://github.com/wdecoster/NanoPlot) is a plotting tool for long read sequencing data and alignments

---

-   **Key outputs**

    -   Stats summary within info on mean/median read depth, read quality scores
    -   Plots are output along with HTML summary files
    -   Use [multiqc](https://multiqc.info/) to then summarize per-sample read stats into single report

-   **Running NanoPlot**

    Information on read files: For the purposes of the tutorial, our concatenated read files are called: `xan_22-331_nanopore.fastq.gz` and `xan_22-323_nanopore.fastq.gz`. These are the reads for *Xanthomonas* strains.
    
    **Let's finally start using Gitpod!**

    -   We will type all commands in Terminal and view results in left window under Explorer
    -   IMPORTANT: Make sure you remain in your work directory:`/workspace/aps_workshop`

    **Let's now run NanoPlot on the reads of two strains**

    1.  Copy and paste commands one at a time in Terminal
    2.  Return/enter
    3.  Let NanoPlot run (takes \< 1 minute)
    4.  Repeat for second strain
 
    **In preparation**

    Assuming you have the pipeline still running, open new Terminal instance, by clicking the `+` in the bottom right of this pane. 

    In this new instance, we need to activate a conda environment

     ``` bash
    conda activate qc
    ```

    **Command 1** for strain`xan_22-331`

    ``` bash
    NanoPlot -t 2 -o ./qc_nanoplot/NanoPlot_xan_22-331 -p xan_22-331 --loglength -f png --plots dot --title xan_22-331 --fastq /data/reads/xan_22-331_nanopore.fastq.gz
    ```

    **Command 2** for strain `xan_22-323`

    ``` bash
    NanoPlot -t 2 -o ./qc_nanoplot/NanoPlot_xan_22-323 -p xan_22-323 --loglength -f png --plots dot --title xan_22-323 --fastq /data/reads/xan_22-323_nanopore.fastq.gz
    ```

-   Run **multiqc**

    [multiqc](https://multiqc.info/) gives us nice summary of both NanoPlot directories at once. This command assumes that we are within the directory with our newly created NanoPlot folder

    ``` bash
    multiqc qc_nanoplot -o multiqc_nanoplot
    ```

-   **Explore the results**

    1.  Explore your output directories by clicking on `qc_nanoplot` under `APS_WORKSHOP`. You should see `NanoPlot_xan_22-331` and `NanoPlot_xan_22-322`

    2.  Now take a look at the compiled multiqc report

         -    Go over to the menu on the left and under `APS_WORKSHOP` , click `multiqc_nanoplot`, and then right click `multiqc_report.html` and select the first choice, `Open with Live Server`.
         -    Take a look at the new browser window that opens with your report

-   **Discuss**

    -   How do your reads look for each sample?
    -   Does it seem reasonable to proceed with next steps?
    -   Which output files are most informative?
    -   Do you prefer one output format over others?

### Run Flye to obtain long read assembly for a *xanthomonas* strain

Flye is a de novo assembler and can be used with both PacBio and Oxford Nanopore long reads. It is versatile and inputs can be both reads from prokaryotes and eukaryotes. After initial assembly, there are polishing steps.

---

-   **Information on running Flye**
    -   Once we are assured that read quality looks decent based on NanoPlot results, we can begin the assembly process

    -   Since we are working with Nanopore long reads and have bacterial reads to assemble, we can use the [Flye](https://github.com/mikolmogorov/Flye) assembler

    -   An example of how we ran flye is here:

        ``` bash
        python3 flye -t 8 -o flye_xan_22-331 --meta --scaffold --nano-hq /data/reads/xan_22-331_nanopore.fastq.gz
        ```

    -   In the interests of time, we will **not** run Flye here, but will later be running it when we test out the PathogenSurveillance pipeline

    -   Fortunately, we already ran Flye on sample `xan_22-331_nanopore`

    -   We obtained several outputs, but the ones we want to concern ourselves today are is the assembly file `xan_22-331_nanopore.fna` and the graph file `xan_22-331_nanopore.gfa`

    -   For a point of contrast, we also have short read data for this sample, obtained from a previous Illumina MiniSeq run

        -   We had to use the the short read [SPAdes](https://github.com/ablab/spades) assembler to construct these assemblies

### Run QUAST to obtain assembly stats

QUality ASsessment Tool ([QUAST](https://github.com/ablab/quast)) is used to generate some assembly QC reports. This program has a range features to evaluate and assess assembly quality, including metrics such as how contiguous your assembly is.

As an optional input, users can assign a reference genome to compare new assemblies to. We won't do this today, but if you do include this optional input, you will have a more robust report and more metrics by which to assess assembly quality.

---

-   **Run QUAST on our Nanopore flye assembly**

    **Command 1:**

    ``` bash
    quast cli_data/xan_22-331_nanopore_flye.fna -o qc_quast/xan_22-331_longread
    ```

-   **Run QUAST on two short read Illumina SPAdes assemblies**

    -   We also did short read assembly using SPAdes, and as a point of contrast let's obtain the assembly stats for that assembly

    -   Off the Illumina MiniSeq sequencer, there was an estimated read depth of 68, which should be suitable for a decent short read assembly

        **Command 2:**

        ``` bash
        quast cli_data/xan_22-331_shortread_highercov_spades.fna -o qc_quast/xan_22-331_shortread_higher_cov
        ```

        Just for fun, we also happened to subset the reads to a reduced number and how our estimated depth of coverage was 10, prior to assembly. Let's see what impact this has on assembly quality.

        **Command 3:**

        ``` bash
        quast cli_data/xan_22-331_shortread_lowcov_spades.fna -o qc_quast/xan_22-331_shortread_low_cov
        ```

-   **Compile results using multiqc**

    ``` bash
    multiqc qc_quast -o multiqc_quast
    ```

    We now have an easy-to-interpret summary report like what we generated for our NanoPlot results.

-   **Review results**

    1.  Look at QUAST directories under `qc_quast` to see what outputs were produced
    2.  To get a summary of all your results, let's check out the multiqc report.
    3.  Go over to the menu on the left and under `APS_WORKSHOP` , click `multiqc_quast`, then right click `multiqc_report.html` and select the first choice, `Open with Live Server`.
    4.  Take a look at the new tab that opens.

-   **Discuss**

    -   What do you observe about the assembly stats when comparing the long read vs. short read assemblies?
    -   How do you think incorporating a reference as input into QUAST help to better assess assembly quality?

### Run Bandage to examine assembly graphs

**Bioinformatics Application for Navigating *De novo* Assembly Graphs Easily (**[Bandage](https://rrwick.github.io/Bandage/)) is a program to visualize assembly graphs rapidly. Allows users to quickly see connections between contigs and also quickly see if there are problematic regions of the assembly

---

Select how you want to run Bandage

-   **Option 1**: download the GUI at: <https://rrwick.github.io/Bandage/>

    -   If you choose this approach, you will need to download all three `.gfa` files from `cli_data` folder on Gitpod
    -   Simply right click and select `Download`from the options.
    -   From there, you will, one at a time, upload a graph and view each one using the downloaded Bandage program on your personal computer
    -   First, take a look first at the Nanopore assembly graph file: `xan_22-331_nanopore_flye.gfa`
    -   Second, take a look at the SPAdes higher coverage assembly graph file: `xan_22-331_shortread_highercov_spades.gfa`
    -   Third, take a look at the SPAdes lower coverage assembly graph file: `xan_22-331_shortread_lowcov_spades.gfa`

-   **Option 2**: use the already installed version and run from the command line (less options and ability to interact with your graph)

    First, we'll look at the long read assembly graph.

    **Command 1:**

    ``` bash
    mkdir qc_bandage
    Bandage image cli_data/xan_22-331_nanopore_flye.gfa qc_bandage/xan_22-331_nanopore.png
    ```

    The output is a png file. Let's take a look.

    Just like for our QUAST analysis, we also have some short read SPAdes assembly files for the same sample.

    Now let's look at the short read assembly graph:

    **Command 2:**

    ``` bash
    Bandage image cli_data/xan_22-331_shortread_highercov_spades.gfa qc_bandage/xan_22-331_shortread_highercov_spades.png
    ```

    Let's also look at the assembly graph if input into SPAdes assembler was a reduced number of reads (10x estimate read coverage)

    **Command 3:**

    ``` bash
    Bandage image cli_data/xan_22-331_shortread_lowcov_spades.gfa qc_bandage/xan_22-331_shortread_lowcov_spades.png
    ```

    Let's take a look at all three png files by going to qc_bandage and then double-clicking on each one. They should how up above the Terminal window.

-   **Discussion**

    -   Take a look at all three visualizations of the gfa graph files
    -   What do you see?
    -   Which assembly seems best?

### Next steps for manual workflow

The above exercises were intended to give a framework for what is involved in analysis of ONT Nanopore long read data, when we do each step manually. A full analysis of Nanopore data is multi-step and dictated by a researcher's specific goals.

---

**Subsequent steps include (but are not limited to):**

*  Annotation
*  Using tools like [PIRATE](https://github.com/SionBayliss/PIRATE) to identify and classify orthologous gene families, and then constructing robust core gene phylogenies
*  Generating POCP (Percent of conserved proteins) and ANI (Average nucleotide identify) matrices
*  Identifying appropriate reference genomes to then do variant call analyses
    *  Constructing SNP trees and minimum spanning networks

</details>

---

<details>
<summary style="font-size: 1.5em; font-weight: bold;">🧵 Exploring the pathogensurveillance outputs @Camilo</summary>

This document will guide you through the key output directories generated by the `pathogensurveillance` pipeline. You will learn where to find the outputs and understand their significance. This section is designed to be viewed in VSCode Gitpod, with the file explorer on the left, this document previewed on the top panel, and the terminal on the bottom panel for an efficient and interactive learning experience.


## `sendsketch`

The `sendsketch` process in the PathogenSurveillance pipeline utilizes the BBMap tool to generate sketch data for the input sequences. This step is crucial for identifying and comparing genomic sequences against a reference database.

### Key output directory: `output/bbmap_sendsketch/`

This directory contains symbolic links to the actual output files generated by the `sendsketch` process. The outputs are stored in the working directory under a unique identifier.

```sh
# Let's list the output for sendsketch:
ll output/bbmap_sendsketch/

# Take a look at output for the sample we included here:
head output/bbmap_sendsketch/*.txt
```

<details>
<summary> 💡 Learn more here </summary>

  ### Inputs
  
  - **Input Sequences**: The process takes in sequencing data files, such as FASTQ files.
  - **Reference Database**: The sequences are compared against a reference database (e.g., RefSeq).
  
  ### Outputs
  
  - **Sketch Files**: These are the primary outputs containing information about the query sequences and their comparison to the reference database.
  
  ### Understanding the Outputs
  
  The main output file `22_323.txt` contains detailed information about the query sequence and its comparison to the reference database. Here are some key fields:
  
  - **Query**: Information about the query sequence, including its ID, run ID, sample ID, and other metadata.
  - **DB**: The reference database used for comparison (e.g., RefSeq).
  - **SketchLen**: The length of the sketch.
  - **Seqs**: Number of sequences in the sketch.
  - **Bases**: Total bases in the sketch.
  - **Quality**: Quality score of the sketch.
  - **Depth**: Depth of the sketch.
  - **Taxonomy**: Taxonomic classification of the sequences.
  
  ### Example Output Snippet
  
  ```
  Query: a4d92ba2-9c26-4548-927d-f10ab976c5fb runid=e8007fcc5055076f3e399f09a077cc1f37b2b8ff sampleid=run4 read=2240 ch=338 start_time=2022-08-04T04:43:00Z model_version_id=2021-11-17_dna_r10.4_minion_promethion_1024_67af0493 barcode=barcode07       DB: RefSeq      SketchLen: 35910   Seqs: 7396      Bases: 88561804 gSize: 5424369  GC: 0.640       Quality: 0.7925 AvgCount: 13.456        Depth: 13.456   File: xan_22-323_nanopore.fastq.gz
  WKID    KID     ANI     SSU     SSULen  Complt  Contam  Contam2 uContam Score   E-Val   Depth   Depth2  Volume  RefHits Matches Unique  Unique2 Unique3 noHit   Length  TaxID   ImgID           gBases  gKmers  gSize   gSeqs   GC      rDiv    qDiv    rSize   qSize   cHits      taxName file    seqName taxonomy
  35.22%  22.41%  96.29%  91.52%  1551    100.00% 20.06%  0.62%   4.03%   6793    0.00e+00        14.05   13.78   113.1   34.20   8047    542     6660    13153   9654    35910   863365  -1      5052399 5014802 4995825 1       0.638   22845   35910   22845   35910   7205       Xanthomonas hortorum pv. carotae str. M081      .       tid|863365|NZ_CM002307.1 Xanthomonas hortorum pv. carotae str. M081 chromosome, whole genome shotgun sequence   sk:Bacteria;p:Proteobacteria;c:Gammaproteobacteria;o:Xanthomonadales;f:Xanthomonadaceae;g:Xanthomonas;s:Xanthomonas hortorum;Xanthomonas hortorum pv. carotae
  ```
 
  ### Column Details
  
  - **WKID**: Weighted K-mer ID, representing the percentage of shared k-mers between the query and reference.
  - **KID**: K-mer ID, showing the percentage of identical k-mers.
  - **ANI**: Average Nucleotide Identity, indicating the similarity between the query and reference sequences.
  - **SSU**: Small Subunit ribosomal RNA percentage identity.
  - **SSULen**: Length of the SSU alignment.
  - **Complt**: Completeness of the match.
  - **Contam**: Contamination level in the match.
  - **uContam**: Unique contamination level.
  - **Score**: Score of the match.
  - **E-Val**: E-value of the match.
  - **Depth**: Depth of coverage for the match.
  - **Volume**: Volume of the match.
  - **RefHits**: Number of hits in the reference database.
  - **Matches**: Number of matches in the query sequence.
  - **Unique**: Unique k-mers in the query sequence.
  - **noHit**: Number of k-mers in the query with no hits in the reference.
  - **Length**: Length of the alignment.
  - **TaxID**: Taxonomic ID of the reference.
  - **ImgID**: IMG ID of the reference.
  - **gBases**: Total bases in the genome.
  - **gKmers**: Total k-mers in the genome.
  - **gSize**: Size of the genome.
  - **gSeqs**: Number of sequences in the genome.
  - **GC**: GC content.
  - **rDiv**: Relative diversity.
  - **qDiv**: Query diversity.
  - **rSize**: Size of the reference.
  - **qSize**: Size of the query.
  - **cHits**: Cumulative hits in the query.

  > ## 🧐 What does all this mean? and Why?   
  > 
  >  ### Sketches
  >  
  >  Sketching is a technique used in bioinformatics to create a compact representation of a sequence. This method reduces the memory and computational requirements for sequence comparison. Sketches are generated using a subset of k-mers (short subsequences of length k) from the original sequence.
  >  
  >  ### K-mers
  >  
  >  - **Definition**: K-mers are contiguous sequences of k nucleotides. For example, in the sequence `AGCT`, the 2-mers (k=2) are `AG`, `GC`, and `CT`.
  >  - **Usage**: K-mers are used to break down large sequences into smaller, manageable pieces. They are essential for tasks such as sequence alignment, error correction, and genome assembly.
  >  - **Sketch generation**: A sketch is generated by selecting a representative subset of k-mers from the sequence. This subset captures the essential characteristics of the sequence, allowing for efficient and accurate comparisons.
  >  
  >  ### Importance in Pathogen Surveillance
  >  
  >  - **Efficient Comparison**: Sketches enable the rapid comparison of genomic sequences against large reference databases, facilitating the identification of pathogens.
  >  - **Data Reduction**: By reducing the size of the data to be compared, sketches make it feasible to analyze large datasets within a reasonable time frame and with limited computational resources.

</details>

---

## `flye`

The `flye` process in the PathogenSurveillance pipeline assembles long-read sequencing data to generate high-quality genome assemblies. This step is crucial for obtaining contiguous sequences that can be used for downstream analysis.

### Key output directory: `output/flye_nanopore/`

This directory contains symbolic links to the actual output files generated by the `flye` process. The outputs are stored in the working directory under a unique identifier.

```sh
# Let's list the output for flye:
ll output/flye_nanopore/

# Take a look at the assembly FASTA file:
less -S output/flye_nanopore/22_323.assembly.fasta.gz | head -n 5

# View the Flye log file:
tail -n 10 output/flye_nanopore/22_323.flye.log | head -n 8
```

<details>
<summary> 💡 Learn more here </summary>

  ### Inputs
  
  - **Input Sequences**: The process takes in long-read sequencing data files.
  - **Mode**: Specifies the type of input data (e.g., `--nano-raw` for raw nanopore reads).
  
  ### Outputs
  
  - **Assembly FASTA File**: Contains the assembled genome sequences.
  - **Graph Files (GFA and GV)**: Represent the assembly graph in different formats.
  - **Assembly Info File**: Provides information about the assembly, such as the total length, number of fragments, and coverage.
  - **Log File**: Contains logs generated during the assembly process.
  - **Parameters File**: Stores the parameters used for the assembly process.
  
  ### Understanding the Outputs
  
  The main output file `22_323.assembly.fasta.gz` contains the assembled genome sequences. The `22_323.assembly_info.txt` file provides detailed statistics about the assembly.
  
  ### Example Output Snippet from `assembly_info.txt`
  
  ```
  [2024-07-24 20:16:31] root: INFO: Assembly statistics:

          Total length:   5281721
          Fragments:      1
          Fragments N50:  5281721
          Largest frg:    5281721
          Scaffolds:      0
          Mean coverage:  34
  ```

  ### Column Details
  
  - **Total length**: Total length of the assembled genome.
  - **Fragments**: Number of fragments in the assembly.
  - **Fragments N50**: N50 value for the fragments, indicating that 50% of the assembly is contained in fragments of this length or longer.
  - **Largest frg**: Length of the largest fragment in the assembly.
  - **Scaffolds**: Number of scaffolds in the assembly.
  - **Mean coverage**: Average coverage of the assembly.

  > ## 🧐 What does all this mean? and Why?   
  > 
  >  ### Genome Assembly
  >  
  >  Genome assembly is the process of reconstructing the original genome from sequencing reads. This is achieved by overlapping reads to form longer contiguous sequences called contigs.
  >  
  >  ### Flye
  >  
  >  - **Purpose**: Flye is a de novo assembler for long reads produced by technologies such as Nanopore and PacBio. It is designed to assemble genomes with high continuity and accuracy.
  >  - **Usage**: Flye can handle various types of long-read data, producing high-quality assemblies suitable for downstream analysis.
  >  - **Output**: The resulting assembly includes contigs, assembly graphs, and detailed assembly statistics, which are crucial for understanding the quality and characteristics of the assembly.
  >  
  >  ### Importance in Pathogen Surveillance
  >  
  >  - **High-Quality Assemblies**: Obtaining high-quality genome assemblies is essential for accurate pathogen identification and characterization.
  >  - **Downstream Analysis**: The assembled genomes can be used for various downstream analyses, such as variant calling, gene annotation, and comparative genomics.

</details>

---

## `quast`

The `quast` process in the PathogenSurveillance pipeline evaluates genome assemblies by providing various quality metrics. This step is essential for assessing the completeness and accuracy of the assembled genomes.

### Key output directory: `output/quast/`

This directory contains symbolic links to the actual output files generated by the `quast` process. The outputs are stored in the working directory under a unique identifier.

```sh
# Let's list the output for quast:
ll output/quast/

# Take a look at the detailed output directory for the sample:
ll output/quast/22_323

# View the QUAST report:
less -S output/quast/22_323/report.tsv | head -n 23
```

<details>
<summary> 💡 Learn more here </summary>

  ### Inputs
  
  - **Consensus Sequences**: The assembled sequences to be evaluated.
  - **Reference Genome (optional)**: The reference genome for comparison.
  - **Annotation GFF (optional)**: The annotation file for the reference genome.
  
  ### Outputs
  
  - **Report Files**: Contain various metrics and statistics about the genome assembly.
  - **HTML Reports**: Interactive reports for visualizing the assembly quality.
  - **PDF Reports**: Printable versions of the assembly quality reports.
  - **Log Files**: Contains logs generated during the QUAST evaluation.
  
  ### Understanding the Outputs
  
  The main output files include `report.tsv`, `report.txt`, and `report.pdf`, which provide detailed statistics about the genome assembly. The HTML reports (`icarus.html` and `report.html`) offer interactive visualizations.

  ### Example Output Snippet from `report.tsv`
  
  ```
  Assembly        22_323.assembly
  # contigs (>= 0 bp)     1
  # contigs (>= 1000 bp)  1
  # contigs (>= 5000 bp)  1
  # contigs (>= 10000 bp) 1
  # contigs (>= 25000 bp) 1
  # contigs (>= 50000 bp) 1
  Total length (>= 0 bp)  5281721
  Total length (>= 1000 bp)       5281721
  Total length (>= 5000 bp)       5281721
  Total length (>= 10000 bp)      5281721
  Total length (>= 25000 bp)      5281721
  Total length (>= 50000 bp)      5281721
  # contigs       1
  Largest contig  5281721
  Total length    5281721
  GC (%)  64.04
  N50     5281721
  N90     5281721
  auN     5281721.0
  L50     1
  L90     1
  # N's per 100 kbp       0.00
  ```

  ### Column Details
  
  - **# contigs**: Number of contigs in the assembly.
  - **Total length**: Total length of all contigs.
  - **Largest contig**: Length of the largest contig.
  - **GC (%)**: GC content percentage.
  - **N50**: N50 value of the assembly, indicating the length of the shortest contig at 50% of the total assembly length.
  - **N90**: N90 value of the assembly, indicating the length of the shortest contig at 90% of the total assembly length.
  - **auN**: The auN statistic provides a summary of the assembly's length distribution.
  - **L50**: Number of contigs whose length sum makes up 50% of the total assembly length.
  - **L90**: Number of contigs whose length sum makes up 90% of the total assembly length.
  - **# N's per 100 kbp**: Number of ambiguous bases (Ns) per 100,000 base pairs.

  > ## 🧐 What does all this mean? and Why?   
  > 
  >  ### Genome Assembly Evaluation
  >  
  >  Evaluating the quality of a genome assembly is crucial for understanding its completeness and accuracy. QUAST provides a comprehensive set of metrics to assess these aspects.
  >  
  >  ### QUAST
  >  
  >  - **Purpose**: QUAST (Quality Assessment Tool for Genome Assemblies) evaluates genome assemblies by comparing them to a reference genome and computing various metrics.
  >  - **Usage**: QUAST can handle multiple types of input data, including assembled sequences, reference genomes, and annotation files.
  >  - **Output**: The resulting reports provide detailed statistics and visualizations, allowing researchers to assess the quality of their assemblies effectively.
  >  
  >  ### Importance in Pathogen Surveillance
  >  
  >  - **Quality Assurance**: Ensuring high-quality genome assemblies is essential for accurate pathogen identification and characterization.
  >  - **Data Interpretation**: The detailed metrics and visualizations help researchers interpret the quality and characteristics of their assemblies, facilitating better decision-making in downstream analyses.

</details>

---

## `bakta`

The `bakta` process in the PathogenSurveillance pipeline annotates genomic sequences, providing detailed information about coding sequences (CDSs), RNA genes, and other genomic features. This step is crucial for understanding the functional elements within the genome.

### Key output directory: `output/bakta_bakta/`

This directory contains symbolic links to the actual output files generated by the `bakta` process. The outputs are stored in the working directory under a unique identifier.

```sh
# Let's list the output for bakta:
ll output/bakta_bakta/

# Take a look at the annotation summary:
head -n 28 output/bakta_bakta/22_323.txt
```

<details>
<summary> 💡 Learn more here </summary>

  ### Inputs
  
  - **FASTA File**: The genomic sequences to be annotated.
  - **Database**: The annotation database used by Bakta.
  - **Proteins (optional)**: Additional protein sequences for annotation.
  - **Prodigal Translation Table (optional)**: Translation table for Prodigal gene prediction.
  
  ### Outputs
  
  - **EMBL File**: Annotated sequence in EMBL format.
  - **FASTA Files (faa, ffn, fna)**: Amino acid, nucleotide, and genomic sequences.
  - **GenBank File (gbff)**: Annotated sequence in GenBank format.
  - **GFF3 File**: General Feature Format for annotations.
  - **TSV Files**: Tab-separated values with detailed annotation information.
  - **TXT File**: Summary of the annotation.
  - **Hypotheticals Files**: Detailed information about hypothetical proteins.
  
  ### Understanding the Outputs
  
  The main output file `22_323.txt` provides a summary of the annotation, including counts of various genomic features such as CDSs, RNAs, and hypothetical proteins.
  
  ### Example Output Snippet from `22_323.txt`
  
  ```
  Sequence(s):
  Length: 5281721
  Count: 1
  GC: 64.0
  N50: 5281721
  N ratio: 0.0
  coding density: 86.2

  Annotation:
  tRNAs: 54
  tmRNAs: 1
  rRNAs: 6
  ncRNAs: 69
  ncRNA regions: 7
  CRISPR arrays: 0
  CDSs: 4359
  pseudogenes: 0
  hypotheticals: 577
  signal peptides: 0
  sORFs: 0
  gaps: 0
  oriCs: 3
  oriVs: 0
  oriTs: 0

  Bakta:
  Software: v1.9.4
  Database: v5.1, light
  ```

  ### Column Details
  
  - **Length**: Length of the sequence.
  - **Count**: Number of sequences.
  - **GC**: GC content percentage.
  - **N50**: N50 value of the sequence.
  - **N ratio**: Ratio of ambiguous bases (Ns).
  - **Coding density**: Percentage of the sequence that is coding.
  - **tRNAs**: Number of transfer RNA genes.
  - **tmRNAs**: Number of transfer-messenger RNA genes.
  - **rRNAs**: Number of ribosomal RNA genes.
  - **ncRNAs**: Number of non-coding RNA genes.
  - **ncRNA regions**: Number of non-coding RNA regions.
  - **CRISPR arrays**: Number of CRISPR arrays.
  - **CDSs**: Number of coding sequences.
  - **Pseudogenes**: Number of pseudogenes.
  - **Hypotheticals**: Number of hypothetical proteins.
  - **Signal peptides**: Number of signal peptides.
  - **sORFs**: Number of small open reading frames.
  - **Gaps**: Number of gaps.
  - **oriCs**: Number of chromosomal origin of replication sites.
  - **oriVs**: Number of viral origin of replication sites.
  - **oriTs**: Number of transfer origin of replication sites.

  > ## 🧐 What does all this mean? and Why?   
  > 
  >  ### Genome Annotation
  >  
  >  Genome annotation is the process of identifying functional elements within a genome, such as genes, RNA sequences, and regulatory regions. This information is critical for understanding the biology of the organism.
  >  
  >  ### Bakta
  >  
  >  - **Purpose**: Bakta is an annotation tool that provides detailed genomic annotations using a comprehensive database.
  >  - **Usage**: Bakta can annotate various types of genomic sequences, producing multiple output formats for different applications.
  >  - **Output**: The resulting annotations include coding sequences, RNA genes, hypothetical proteins, and other genomic features, providing a comprehensive view of the genome's functional elements.
  >  
  >  ### Importance in Pathogen Surveillance
  >  
  >  - **Functional Insights**: Understanding the functional elements within a pathogen's genome is essential for identifying virulence factors, antibiotic resistance genes, and other important traits.
  >  - **Data Utilization**: The annotated genome can be used for various downstream analyses, including comparative genomics, evolutionary studies, and functional characterization.

</details>

---

## `sourmash compare`

The `sourmash compare` process in the PathogenSurveillance pipeline computes the similarity matrix for a set of genomic signatures using Average Nucleotide Identity (ANI) and a k-mer length of 31. This step is crucial for comparing genomic sequences and identifying similarities and differences between them.

### Key output directory: `output/sourmash_compare/`

This directory contains symbolic links to the actual output files generated by the `sourmash compare` process. The outputs are stored in the working directory under a unique identifier.

```sh
# Let's list the output for sourmash compare:
ll output/sourmash_compare/

# Take a look at the similarity matrix in CSV format:
less -S output/sourmash_compare/aps_comp.csv | head -n 10 | cut -f 1-10,61 -d ","
```

<details>
<summary> 💡 Learn more here </summary>

  ### Inputs
  
  - **Genomic Signatures**: The process takes in genomic signature files.
  - **File List (optional)**: A list of signature files to be compared.
  - **Save Options**: Options to save the output matrix in numpy and/or CSV format.
  
  ### Outputs
  
  - **Numpy Matrix**: Contains the computed similarity matrix in numpy format (`*.npy` and `*.npy.labels.txt`).
  - **CSV File**: Contains the computed similarity matrix in CSV format.
  
  ### Understanding the Outputs
  
  The main output file `aps_comp.csv` contains the similarity matrix, with rows and columns representing different genomic signatures. The values indicate the similarity between the signatures, with higher values representing greater similarity.
  
  ### Example Output Snippet from `aps_comp.csv`
  
  ```
  GCF_002139955_1,GCF_025263725_1,GCF_002019265_2,GCF_017723895_1,GCF_026651895_1,GCF_001610795_1,GCF_000488895_1,GCA_905123925_1,GCF_033441695_1,GCF_001908775_1,22_323
  1.0,0.9265560609248261,0.9977862642066111,0.9889228216483386,0.9073164224987877,0.9700903744261007,0.9889150886270418,0.9115015968590614,0.9041193116358751,0.9045361688901344,0.8871859607482656
  0.9265560609248261,1.0,0.9263988347909979,0.9251119480988551,0.911316733531698,0.9226799924167159,0.9251202135619242,0.9158647097039145,0.9083838785070867,0.9071117431126531,0.8898799125144564
  0.9977862642066111,0.9263988347909979,1.0,0.9888257224992404,0.907831757300304,0.9699598463114608,0.9888096267370786,0.9114840834725453,0.9040737568047027,0.9046135867305022,0.8873565243085494
  0.9889228216483386,0.9251119480988551,0.9888257224992404,1.0,0.9121759558988269,0.970107774713152,0.9999853858427241,0.9135428296802719,0.9038264872056821,0.9051938652156456,0.8894408455767939
  0.9073164224987877,0.911316733531698,0.907831757300304,0.9121759558988269,1.0,0.9037398150211037,0.9120910480325186,0.9296825816700862,0.909749003812823,0.9689599754220248,0.9457379103831718
  0.9700903744261007,0.9226799924167159,0.9699598463114608,0.970107774713152,0.9037398150211037,1.0,0.9701013884045692,0.907211835393209,0.902840929222427,0.9047438469368647,0.8876233079754928
  0.9889150886270418,0.9251202135619242,0.9888096267370786,0.9999853858427241,0.9120910480325186,0.9701013884045692,1.0,0.913551000075958,0.9038346560102811,0.9050856961227841,0.8894454567863859
  0.9115015968590614,0.9158647097039145,0.9114840834725453,0.9135428296802719,0.9296825816700862,0.907211835393209,0.913551000075958,1.0,0.908850448446987,0.9278227730780791,0.9109513479182657
  0.9041193116358751,0.9083838785070867,0.9040737568047027,0.9038264872056821,0.909749003812823,0.902840929222427,0.9038346560102811,0.908850448446987,1.0,0.9082147459073008,0.9050495064323612
  ```

  ### Column Details
  
  - **Signature IDs**: The first row and column contain the IDs of the genomic signatures being compared.
  - **Similarity Values**: The matrix values indicate the similarity between the signatures, with values ranging from 0 to 1. A value of 1 indicates identical signatures, while values closer to 0 indicate less similarity.

  > ## 🧐 What does all this mean? and Why?   
  > 
  >  ### Genomic Signatures and k-mers
  >  
  >  Genomic signatures are unique representations of genomic sequences, often based on k-mers, which capture the unique characteristics of a genome. In this case, a k-mer length of 31 is used.
  >  
  >  ### Average Nucleotide Identity (ANI)
  >  
  >  ANI is a measure of the average nucleotide identity between two genomic sequences, providing a quantitative measure of their similarity. Sourmash computes ANI by comparing the shared k-mers between sequences, calculating the fraction of shared k-mers over the total k-mers in each sequence. Higher ANI values indicate greater similarity between the sequences.
  >  
  >  ### Sourmash
  >  
  >  - **Purpose**: Sourmash is a tool used to compute and compare genomic signatures using k-mers. It is particularly useful for quickly comparing large sets of genomic data.
  >  - **Usage**: Sourmash can handle various types of genomic data, producing similarity matrices that indicate the degree of similarity between different genomes.
  >  - **Output**: The similarity matrix provides a comprehensive view of the relationships between the genomes, which can be used for clustering, phylogenetic analysis, and other comparative studies.
  >  
  >  ### Importance in Pathogen Surveillance
  >  
  >  - **Identifying Similarities**: Comparing genomic signatures helps in identifying similarities and differences between pathogen genomes, which is essential for tracking outbreaks and understanding pathogen evolution.
  >  - **Data Analysis**: The similarity matrix is a key tool for visualizing and interpreting genomic relationships, facilitating better decision-making in pathogen surveillance and research.

</details>

---

## `bwa mem`

The `bwa mem` process in the PathogenSurveillance pipeline aligns sequencing reads to a reference genome, producing BAM files. This step is essential for mapping reads to a reference, which is a crucial step in many downstream analyses.

### Key output directory: `output/bwa_mem/`

This directory contains symbolic links to the actual output files generated by the `bwa mem` process. The outputs are stored in the working directory under a unique identifier.

```sh
# Let's list the output for bwa mem:
ll output/bwa_mem/

# Take a look at the BAM file:
samtools view output/bwa_mem/GCF_032697525_1_22_323.bam | head -n 10
```

<details>
<summary> 💡 Learn more here </summary>

  ### Inputs
  
  - **Reads**: The sequencing reads to be aligned.
  - **Index**: The reference genome index files.
  - **Sort BAM**: Option to sort the BAM file.
  
  ### Outputs
  
  - **BAM File**: Contains the aligned reads in BAM format.
  
  ### Understanding the Outputs
  
  The main output file `GCF_032697525_1_22_323.bam` contains the aligned reads in BAM format. This file is essential for various downstream analyses, including variant calling, assembly validation, and other genomic analyses.
  
  ### Example Output Snippet from BAM File
  
  ```sh
  samtools view output/bwa_mem/GCF_032697525_1_22_323.bam | head -n 10
  ```

  ### BAM File Details
  
  - **Aligned Reads**: The reads aligned to the reference genome.
  - **SAM/BAM Format**: Standard formats for storing large nucleotide sequence alignments.
  - **Header Information**: Contains metadata about the alignment, including reference genome details and read group information.

  > ## 🧐 What does all this mean? and Why?   
  > 
  >  ### Read Alignment
  >  
  >  Read alignment is the process of mapping sequencing reads to a reference genome. This is a critical step for identifying where each read originates from within the reference.
  >  
  >  ### BWA MEM
  >  
  >  - **Purpose**: BWA MEM (Burrows-Wheeler Aligner) is a fast and accurate read alignment tool. It is particularly well-suited for aligning high-quality reads against large reference genomes.
  >  - **Usage**: BWA MEM takes in sequencing reads and a reference genome, outputting aligned reads in BAM format. It can handle paired-end and single-end reads.
  >  - **Output**: The aligned reads are stored in BAM files, which are compressed binary versions of the Sequence Alignment/Map (SAM) format.
  >  
  >  ### Importance in Pathogen Surveillance
  >  
  >  - **Variant Calling**: Aligned reads are used to identify variants, such as SNPs and indels, within the genome.
  >  - **Assembly Validation**: Alignment helps in validating genome assemblies by comparing the assembled genome to the original reads.
  >  - **Comparative Genomics**: Aligning reads from different strains or species to a reference genome enables comparative analyses to understand genetic differences and similarities.

</details>

---

## `graphtyper vcf concatenate`

The `graphtyper vcf concatenate` process in the PathogenSurveillance pipeline concatenates VCF files, producing a single VCF file that combines the variants from multiple samples. This step is essential for merging variant data across different samples or regions.

### Key output directory: `output/graphtyper_vcfconcatenate/`

This directory contains symbolic links to the actual output files generated by the `graphtyper vcf concatenate` process. The outputs are stored in the working directory under a unique identifier.

```sh
# Let's list the output for graphtyper vcf concatenate:
ll output/graphtyper_vcfconcatenate/

# Take a look at the VCF file:
zcat output/graphtyper_vcfconcatenate/xan__GCF_032697525_1.vcf.gz | tail -n +90 | head -n 2
```

<details>
<summary> 💡 Learn more here </summary>

  ### Inputs
  
  - **VCF Files**: The process takes in VCF files to be concatenated.
  
  ### Outputs
  
  - **Concatenated VCF File**: Contains the combined variant data from all input VCF files.
  - **Index File (TBI)**: Index file for the concatenated VCF file.
  
  ### Understanding the Outputs
  
  The main output file `xan__GCF_032697525_1.vcf.gz` contains the concatenated variant data from all input VCF files. This file is essential for downstream analyses that require a comprehensive view of variants across multiple samples or regions.
  
  ### Example Output Snippet from VCF File
  
  ```
  #CHROM  POS     ID      REF     ALT     QUAL    FILTER  INFO    FORMAT  GCF_032697525_1_22_323
  NZ_CP103836.1   304247  NZ_CP103836.1:304247:SG G       A       123     PASS    AAScore=0.5113;ABHet=0.4167;ABHetMulti=0.4167,0.5833;ABHom=-1;ABHomMulti=-1,-1;AC=1;AF=0.5;AN=2;CR=2;CRal=166,166;CRalt=1.66;LOGF=0.7844;MMal=32,77;MMalt=0.77;MQ=56;MQSal=46778,28939;MQalt=54;MQsquared=75717;MaxAAS=10;MaxAASR=0.4167;NHet=1;NHomAlt=0;NHomRef=0;PASS_AC=1;PASS_AN=2;PASS_ratio=1;QD=12.3;QDalt=12.3;RefLen=1;SB=0.375;SBAlt=0.2;SBF=7,2;SBF1=0,0;SBF2=7,2;SBR=7,8;SBR1=0,0;SBR2=7,8;SDal=685,386;SDalt=38.6;SeqDepth=24;VarType=SG GT:AD:MD:DP:GQ:PL        0/1:14,10:0:24:99:123,0,241
  ```

  ### Column Details
  
  - **CHROM**: Chromosome name.
  - **POS**: Position of the variant.
  - **ID**: Variant identifier.
  - **REF**: Reference allele.
  - **ALT**: Alternate allele.
  - **QUAL**: Quality score of the variant.
  - **FILTER**: Filter status of the variant.
  - **INFO**: Additional information about the variant.
  - **FORMAT**: Format of the genotype fields.
  - **Sample Columns**: Genotype information for each sample.

  > ## 🧐 What does all this mean? and Why?   
  > 
  >  ### Variant Calling
  >  
  >  Variant calling is the process of identifying variants (such as SNPs and indels) from sequence data. VCF (Variant Call Format) files store this information.
  >  
  >  ### Graphtyper
  >  
  >  - **Purpose**: Graphtyper is a tool used for variant calling and genotyping. It is particularly effective for analyzing large genomic datasets.
  >  - **Usage**: Graphtyper can handle multiple VCF files, concatenating them into a single VCF file that contains comprehensive variant information.
  >  - **Output**: The concatenated VCF file provides a unified view of variants across different samples or regions, which is crucial for downstream analyses.
  >  
  >  ### Importance in Pathogen Surveillance
  >  
  >  - **Unified Variant Data**: Combining variant data from multiple sources provides a more complete picture of genetic variation, which is essential for tracking pathogen evolution and diversity.
  >  - **Downstream Analyses**: The concatenated VCF file can be used for various downstream analyses, including phylogenetic studies, population genetics, and association studies.

</details>

---

## `vcflib_vcffilter`

The `vcflib_vcffilter` process in the PathogenSurveillance pipeline filters VCF files based on specified criteria, producing a filtered VCF file. This step is essential for refining variant data by applying quality and other filters to remove low-confidence variants.

### Key output directory: `output/vcflib_vcffilter/`

This directory contains symbolic links to the actual output files generated by the `vcflib_vcffilter` process. The outputs are stored in the working directory under a unique identifier.

```sh
# Let's list the output for vcflib_vcffilter:
ll output/vcflib_vcffilter/

# Take a look at the filtered VCF file:
zcat output/vcflib_vcffilter/xan__GCF_032697525_1.vcffilter.vcf.gz | tail -n +97 | head -n 2
```

<details>
<summary> 💡 Learn more here </summary>

  ### Inputs
  
  - **VCF File**: The original VCF file containing variant data.
  - **Index File (TBI)**: Index file for the VCF file.
  
  ### Outputs
  
  - **Filtered VCF File**: Contains the variant data after applying the specified filters.
  
  ### Understanding the Outputs
  
  The main output file `xan__GCF_032697525_1.vcffilter.vcf.gz` contains the filtered variant data. This file includes only the variants that meet the specified criteria, improving the quality and reliability of the variant calls.
  
  ### Example Output Snippet from Filtered VCF File
  
  ```sh
  zcat output/vcflib_vcffilter/xan__GCF_032697525_1.vcffilter.vcf.gz | tail -n +97 | head -n 2
  ```

  ### Filter Criteria
  
  - **ABHet < 0.0 or ABHet > 0.33**: Filter based on allele balance for heterozygous calls.
  - **ABHom < 0.0 or ABHom > 0.97**: Filter based on allele balance for homozygous calls.
  - **MaxAASR > 0.4**: Filter based on the maximum allele alignment score ratio.
  - **MQ > 30**: Filter based on the mapping quality.

  > ## 🧐 What does all this mean? and Why?   
  > 
  >  ### Variant Filtering
  >  
  >  Variant filtering is the process of removing low-confidence variants from a VCF file. This is done by applying various quality and other filters to ensure that only high-confidence variants are retained.
  >  
  >  ### vcflib
  >  
  >  - **Purpose**: vcflib is a collection of tools for processing VCF files. vcffilter is one of these tools, used for filtering VCF files based on specified criteria.
  >  - **Usage**: vcffilter takes in a VCF file and applies the specified filters, producing a filtered VCF file. It supports a wide range of filter criteria, allowing for flexible and precise filtering.
  >  - **Output**: The filtered VCF file contains only the variants that meet the specified criteria, improving the reliability and quality of the variant data.
  >  
  >  ### Importance in Pathogen Surveillance
  >  
  >  - **Quality Control**: Filtering ensures that only high-confidence variants are included in downstream analyses, reducing the risk of false positives.
  >  - **Data Refinement**: By applying specific filters, researchers can focus on the most relevant and reliable variant data, facilitating better decision-making and more accurate results in pathogen surveillance and research.

</details>

---

## `pirate`

The `pirate` process in the PathogenSurveillance pipeline performs pangenome analysis, identifying and categorizing gene families across multiple genomes. This step is essential for understanding the genetic diversity and shared genetic content within a set of genomes.

### Key output directory: `output/pirate/xan__results/`

This directory contains symbolic links to the actual output files generated by the `pirate` process. The outputs are stored in the working directory under a unique identifier.

```sh
# Let's list the output for pirate:
ls -lthr output/pirate/xan__results/

# Take a look at one of the output files:
head -n 20 output/pirate/xan__results/PIRATE.pangenome_summary.txt
```

<details>
<summary> 💡 Learn more here </summary>

  ### Outputs
  
  - **PIRATE.unique_alleles.tsv**: Contains unique alleles identified across the genomes.
  - **PIRATE.pangenome_summary.txt**: Summarizes the pangenome analysis, including the number of core and accessory genes.
  - **PIRATE.log**: Log file containing detailed information about the PIRATE run.
  - **PIRATE.genomes_per_allele.tsv**: Shows the distribution of alleles across the genomes.
  - **PIRATE.gene_families.tsv**: Lists all identified gene families.
  - **PIRATE.gene_families.ordered.tsv**: Ordered list of gene families.
  - **split_groups.log**: Log file for the split groups analysis.
  - **representative_sequences.ffn**: Representative nucleotide sequences for the gene families.
  - **representative_sequences.faa**: Representative protein sequences for the gene families.
  - **paralog_clusters.tab**: Information about paralogous gene clusters.
  - **pan_sequences.fasta**: Fasta file containing sequences for the pangenome.
  - **pangenome.temp**: Temporary file for pangenome analysis.
  - **pangenome.syntenic_blocks.tsv**: Syntenic blocks identified in the pangenome.
  - **pangenome.reversed.tsv**: Reversed syntenic blocks.
  - **pangenome.order.tsv**: Order of genes in the pangenome.
  - **pangenome_log.txt**: Log file for pangenome analysis.
  - **pangenome_iterations**: Iterations of the pangenome analysis.
  - **pangenome.gfa**: Graphical Fragment Assembly file for the pangenome.
  - **pangenome.edges**: Edges in the pangenome graph.
  - **pangenome.connected_blocks.tsv**: Connected syntenic blocks.
  - **modified_gffs**: Modified GFF files.
  - **loci_paralog_categories.tab**: Categorization of loci and paralogs.
  - **loci_list.tab**: List of loci identified.
  - **link_clusters.log**: Log file for link clusters analysis.
  - **gff_parser_log.txt**: Log file for GFF parsing.
  - **genome_list.txt**: List of genomes included in the analysis.
  - **genome2loci.tab**: Mapping of genomes to loci.
  - **co-ords**: Coordinates for gene families.
  - **cluster_alleles.tab**: Information about allele clusters.
  - **binary_presence_absence.nwk**: Newick tree representing binary presence/absence of genes.
  - **binary_presence_absence.fasta**: Fasta file for binary presence/absence of genes.
  
  ### Brief Explanation of Outputs and Applications

  - **Unique Alleles and Genomes per Allele**: These files provide insights into the genetic variation and distribution of alleles across genomes, useful for evolutionary studies and diversity analysis.
  - **Pangenome Summary and Gene Families**: These summarize the core and accessory gene content, which is essential for understanding the genetic makeup and shared content among the genomes.
  - **Representative Sequences**: These sequences can be used for further functional annotation and comparative genomics.
  - **Syntenic Blocks and Pangenome Graph Files**: These provide information about conserved gene order and structure, useful for structural genomics and identifying genome rearrangements.
  - **Paralog Clusters and Loci Information**: These files help in identifying and categorizing paralogous genes and their loci, which is important for gene family evolution studies.
  - **Presence/Absence Data**: This data can be used to generate phylogenetic trees and understand the presence or absence of genes across different genomes, which is crucial for phylogenetic and functional studies.

  > ## 🧐 What does all this mean? and Why?   
  > 
  >  ### Pangenome Analysis
  >  
  >  Pangenome analysis involves studying the complete set of genes in a group of related organisms. It identifies core genes shared by all genomes and accessory genes present in some but not all genomes.
  >  
  >  ### PIRATE
  >  
  >  - **Purpose**: PIRATE (Pangenome Iterative Refinement and Threshold Evaluation) is a tool for pangenome analysis. It clusters genes into families, identifies core and accessory genes, and performs various analyses to understand the pangenome structure.
  >  - **Usage**: PIRATE takes annotated genomes (GFF files) as input and produces a comprehensive set of outputs that describe the pangenome, gene families, alleles, and more.
  >  - **Output**: The outputs from PIRATE provide a detailed view of the genetic content and variation within a set of genomes, which is essential for comparative genomics, evolutionary studies, and understanding microbial diversity.
  >  
  >  ### Importance in Pathogen Surveillance
  >  
  >  - **Genetic Diversity**: Understanding the genetic diversity within and between pathogen populations helps in tracking their evolution and spread.
  >  - **Core and Accessory Genes**: Identifying core and accessory genes helps in understanding the essential genetic components of pathogens and their adaptive capabilities.
  >  - **Functional Insights**: Analyzing the pangenome can provide insights into the functions of genes and their roles in pathogenicity, resistance, and other traits.

</details>

---


## `calculate_pocp`

The `calculate_pocp` process in the PathogenSurveillance pipeline calculates the Percentage of Conserved Proteins (POCP) between pairs of genomes. This step is important for understanding the relatedness and conservation of protein-coding genes across different genomes.

### Key output directory: `output/calculate_pocp/`

This directory contains symbolic links to the actual output files generated by the `calculate_pocp` process. The outputs are stored in the working directory under a unique identifier.

```sh
# Let's list the output for calculate_pocp:
ll output/calculate_pocp/

# Take a look at the POCP table:
head output/calculate_pocp/xan_pocp.tsv
```

<details>
<summary> 💡 Learn more here </summary>

  ### Outputs
  
  - **xan_pocp.tsv**: This file contains the POCP values between pairs of genomes, indicating the percentage of conserved proteins between each pair.
  
  ### Understanding the Outputs
  
  The POCP table (`xan_pocp.tsv`) provides a matrix of POCP values for each pair of genomes included in the analysis. The rows and columns represent different genomes, and the values indicate the percentage of conserved proteins between the genome pairs.

  ### Example Output Snippet from POCP Table
  
  ```
  22_323  GCA_905123925_1 GCF_000019585_2 GCF_001442785_1 GCF_003814555_1 GCF_004168365_1 GCF_028370135_1 GCF_032697525_1
  100     80.34   62.25   27.2    29.82   10.04   82.94   96.32
  80.34   100     62.35   26.4    30.42   9.97    76.44   80.32
  62.25   62.35   100     23.29   30.75   8.56    60.13   61.95
  27.2    26.4    23.29   100     35.62   11.81   25.9    27
  29.82   30.42   30.75   35.62   100     11.45   29.29   29.89
  10.04   9.97    8.56    11.81   11.45   100     9.48    9.79
  82.94   76.44   60.13   25.9    29.29   9.48    100     83.13
  96.32   80.32   61.95   27      29.89   9.79    83.13   100
  ```

  > ## 🧐 What does all this mean? and Why?   
  > 
  >  ### Percentage of Conserved Proteins (POCP)
  >  
  >  POCP is a metric used to quantify the conservation of protein-coding genes between pairs of genomes. It is calculated as the number of shared protein-coding genes divided by the average total number of protein-coding genes in the two genomes, multiplied by 100 to give a percentage.
  >  
  >  ### Importance of POCP
  >  
  >  - **Genomic Relatedness**: POCP values provide insights into the relatedness of genomes. High POCP values indicate a high degree of conservation and relatedness, while low POCP values suggest more distant relationships.
  >  - **Functional Conservation**: By analyzing the conservation of protein-coding genes, researchers can infer the functional conservation and evolutionary relationships between genomes.
  >  - **Pathogen Surveillance**: In the context of pathogen surveillance, POCP helps in understanding the genetic relatedness of pathogen strains, which is crucial for tracking the spread and evolution of pathogens.

</details>

---

## `iqtree`

The `iqtree` process in the PathogenSurveillance pipeline generates phylogenetic trees using the IQ-TREE software. This step is essential for inferring evolutionary relationships among the sequences.

### Key output directory: `output/iqtree2_core/`

This directory contains symbolic links to the actual output files generated by the `iqtree` process. The outputs are stored in the working directory under a unique identifier.

```sh
# Let's list the output for iqtree:
ll output/iqtree2_core/

# Take a look at the tree file:
head output/iqtree2_core/xan__cluster_1.treefile
```

<details>
<summary> 💡 Learn more here </summary>

  ### Outputs
  
  - **Tree File**: The primary output is a tree file (`.treefile`) that contains the inferred phylogenetic tree in Newick format.
  
  ### Understanding the Outputs
  
  The tree file (`xan__cluster_1.treefile`) represents the evolutionary relationships among the sequences in the form of a phylogenetic tree. Each node represents a taxonomic unit, and the branches indicate the evolutionary distances between them. The tree also includes bootstrap values, which provide a measure of the reliability of the inferred relationships.

  ### Example Output Snippet from Tree File
  
  ```
  (22_323:0.0000020823,((GCA_905123925_1:0.0277133956,(GCF_000019585_2:0.0452334629,((GCF_001442785_1:0.0887170858,GCF_003814555_1:0.0899369918)100:0.0556910809,GCF_004168365_1:0.2811592917)100:0.1019633143)100:0.0157650325)100:0.0238071784,GCF_028370135_1:0.0177085341)100:0.0146704891,GCF_032697525_1:0.0000021297);
  ```

  > ## 🧐 What does all this mean? and Why?   
  > 
  >  ### Phylogenetic Trees
  >  
  >  Phylogenetic trees are graphical representations of the evolutionary relationships among various biological species or entities based upon similarities and differences in their physical or genetic characteristics.
  >  
  >  ### IQ-TREE
  >  
  >  - **Purpose**: IQ-TREE is a fast and effective software for constructing phylogenetic trees by employing maximum likelihood estimation.
  >  - **Usage**: The software takes an alignment file as input and produces a phylogenetic tree that shows the evolutionary relationships among the input sequences.
  >  - **Output**: The tree file provides a visual representation of these relationships, which can be used for further evolutionary analysis and comparative genomics.
  >  
  >  ### Core Genome Phylogeny
  >  
  >  This tree, in particular, is built from the MAFFT alignments of the core genes across the samples, representing the core genome phylogeny. The core genome includes genes that are conserved across all the samples, providing a robust framework for phylogenetic analysis.
  >  
  >  ### Bootstrap Values
  >  
  >  The tree includes bootstrap values, which are statistical measures that provide a confidence level for each branch in the tree. High bootstrap values (close to 100) indicate strong support for the inferred relationships, while lower values suggest less certainty.
  >  
  >  ### Importance in Pathogen Surveillance
  >  
  >  - **Evolutionary Insights**: Phylogenetic trees help researchers understand the evolutionary history and relationships among pathogen strains.
  >  - **Tracking Pathogen Spread**: By comparing the evolutionary distances between strains, researchers can track the spread and evolution of pathogens.
  >  - **Identifying Clades and Lineages**: The tree structure helps in identifying different clades and lineages, which is crucial for epidemiological studies and outbreak investigations.

</details>

---

## `iqtree2_snp`

> 🚨 **Note:** This output won't be produced in the workshop. With the toy dataset we are using here, we can't obtain an SNP phylogeny simply because we don't have samples to compare against. Here is an example of a different dataset and how it would look if you are interested:

The `iqtree2_snp` process in the PathogenSurveillance pipeline generates phylogenetic trees using SNP data with the IQ-TREE software. This step is crucial for inferring evolutionary relationships based on single nucleotide polymorphisms (SNPs).

### Key output directory: `output/iqtree2_snp/`

This directory contains symbolic links to the actual output files generated by the `iqtree2_snp` process. The outputs are stored in the working directory under a unique identifier.

```sh
# Let's list the output for iqtree2_snp:
ll output/iqtree2_snp/

```

<details>
<summary> 💡 Learn more here </summary>

  ### Outputs
  
  - **Tree File**: The primary output is a tree file (`.treefile`) that contains the inferred phylogenetic tree in Newick format.
  
  ### Understanding the Outputs
  
  The tree file (`Byu_Bradyrhizobium_sp_191.treefile`) represents the evolutionary relationships among the sequences in the form of a phylogenetic tree. Each node represents a taxonomic unit, and the branches indicate the evolutionary distances between them. This tree contains the reference used for variant calling, which serves as a baseline for comparing the other samples.

  ### Example Output Snippet from Tree File
  
  ```
  (REF:1.1547636240,(((((Bradyrhizobium_sp_191_GCF_000261785_1:0.0526706083,(Bradyrhizobium_sp_191_H1_14_54_10_S277:0.0005076098,Bradyrhizobium_sp_191_H1_16_56_6_S219:0.0033992085)100:0.0482799558)100:0.0472977893,(((((Bradyrhizobium_sp_191_GCF_000261805_1:0.0006588128,(Bradyrhizobium_sp_191_GCF_007830575_1:0.0002673131,Bradyrhizobium_sp_191_GCF_900094575_1:0.0004338153)1............
  ```

  > ## 🧐 What does all this mean? and Why?   
  > 
  >  ### Phylogenetic Trees from SNP Data
  >  
  >  Phylogenetic trees inferred from SNP data provide high-resolution insights into the evolutionary relationships among closely related sequences by focusing on single nucleotide variations.
  >  
  >  ### IQ-TREE with SNP Data
  >  
  >  - **Purpose**: IQ-TREE is used to construct phylogenetic trees by analyzing SNP data. This approach helps to resolve fine-scale evolutionary relationships that might not be apparent with broader sequence data.
  >  - **Usage**: The software takes SNP alignments as input and produces a phylogenetic tree that shows the evolutionary relationships among the input sequences.
  >  - **Output**: The tree file provides a visual representation of these relationships, including bootstrap values for confidence levels in the inferred branches.
  >  
  >  ### SNP Phylogeny
  >  
  >  This tree is built from the alignments of SNPs across the samples, representing the SNP phylogeny. The SNP phylogeny focuses on the variations at single nucleotide positions, providing a detailed view of the genetic differences among the samples.
  >  
  >  ### Bootstrap Values
  >  
  >  The tree includes bootstrap values, which are statistical measures that provide a confidence level for each branch in the tree. High bootstrap values (close to 100) indicate strong support for the inferred relationships, while lower values suggest less certainty.
  >  
  >  ### Importance in Pathogen Surveillance
  >  
  >  - **Evolutionary Insights**: Phylogenetic trees help researchers understand the evolutionary history and relationships among pathogen strains.
  >  - **Tracking Pathogen Spread**: By comparing the evolutionary distances between strains, researchers can track the spread and evolution of pathogens.
  >  - **Identifying Clades and Lineages**: The tree structure helps in identifying different clades and lineages, which is crucial for epidemiological studies and outbreak investigations.

</details>

---

## `reports`

There are many reports generated by the pipeline, allowing users to explore the data in detail and make connections for further analysis. Below are the key reports with their explanations:

### **`execution_report`**
  **path**: `output/pipeline_info/execution_report_2024-07-25_18-21-41.html`
  
  **What?**: This report provides a comprehensive overview of the entire pipeline execution. It includes details on the processes executed, resources used, and the status of each task.
  
  **Why?**: Useful for understanding the workflow's performance, troubleshooting issues, and ensuring reproducibility.

### **`NanoPlot` report**
  **path**: `output/reports/22_331_NanoPlot-report.html`
  
  **What?**: A quality control report generated by NanoPlot, detailing the quality and characteristics of the nanopore sequencing reads. (Martha went over this allready.
  
  **Why**: Helps in assessing the quality of sequencing data, which is crucial for downstream analysis.
  
### **`quast` report**
  **path**: `output/quast/report.tsv`
  
  **Description**: A report generated by QUAST, providing statistics on the quality of genome assemblies.
  
  **Application**: Essential for evaluating the completeness and accuracy of genome assemblies.

### **`pathogensurveillance` pipeline report** Zach...
   **path**: `output/reports/xan_pathsurveil_report.html`
   
   **What?**: A detailed report generated by the [psminer](https://github.com/grunwaldlab/psminer) R package. It includes multiple analyses performed by the pathogen surveillance pipeline. Key components are:
   
   **Pipeline Status Report**: Error messages for samples or sample groups.
   - **Input Data**: Data read from the input .csv file.
   - **Identification**:
     - **Initial Identification**: Coarse identification from the bbmap sendsketch step. The first tab shows the best species ID for each sample. The second tab shows similarity metrics between sample sequences and other reference genomes: %ANI (average nucleotide identity), %WKID (weighted kmer identity), and %completeness. For more information about each metric, click the "About this table" tab underneath.
     - **Most Similar Organisms**: Shows relationships between samples and references using % ANI and % POCP (percentage of conserved proteins). For better resolution, you can interactively zoom in/out of plots.
     - **Core Gene Phylogeny**: Uses the sequences of all genes shared by all of the genomes included in the tree to infer evolutionary relationships. It is the most robust identification provided by this pipeline, limited by the availability of similar reference sequences. For prokaryotes, this method is based on many different core genes shared between samples and references. This tree is built with iqtree and based on shared core genes analyzed using the program pirate.
   - **Genetic diversity**:
     - **SNP Trees**: This tree is better suited for visualizing genetic diversity among samples. The core gene phylogeny provides a much better source of information for evolutionary differences among samples and known references.
     - **Minimum Spanning Network**: The nodes represent unique multilocus genotypes, and the size of nodes is proportional to the number of samples that share the same genotype. The edges represent the SNP differences between two given genotypes, with darker edges indicating fewer SNP differences.
   **Why?**: Provides a comprehensive view of the pathogen genomics analysis, allowing researchers to interpret the results and make data-driven decisions.

</details>

---

<details>
<summary style="font-size: 1.5em; font-weight: bold;">🧵 Walk through pipeline report @Zach


</details>

---

<details>
<summary style="font-size: 1.5em; font-weight: bold;"> 😎 Session Leader(s) </summary>

<table>
  <tr>
    <td align="center"><strong>Alex Weisberg</strong><br><img src="content/Untitled%201.png" width="200"></td>
    <td align="center"><strong>Jeff Chang</strong><br><img src="content/Untitled%203.png" width="200"></td>
    <td align="center"><strong>Martha Sudermann</strong><br><img src="content/Untitled%204.png" width="200"></td>
    <td align="center"><strong>Arafat Rahman</strong><br><img src="content/arafat_bpp_profile_osu.png" width="200"></td>
    <td align="center"><strong>Zach Foster</strong><br><img src="content/Untitled.png" width="200"></td>
    <td align="center"><strong>Camilo Parada Rojas</strong><br><img src="content/Untitled%202.png" width="200"></td> 
    <td align="center"><strong>Nik Grunwald</strong><br><img src="content/Untitled%205.png" width="200"></td>
    
  </tr>
</table>

</details>
