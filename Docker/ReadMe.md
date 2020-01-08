Running docker container: 
======================

For genome assembly quality assessment:
---------------------
1.	Install the docker engine for your platform (https://docs.docker.com/install/).
2.	Download the Docker directory (make_assemblyqc) from the github repo. This directory contains the Dockerfile and the associated files needed to build the docker image. 
3.	Run the following commands within the make_assemblyqc directory to use the assembly pipeline: 

    ``` mkdir ~/my-scratch-dir (This will create a scratch directory where you need to put all your input files.) ```

      ``` docker build --no-cache -t assemblyqc ```

     ```  docker run -v  ~/my-scratch-dir:/working-dir -w /working-dir assemblyqc <genome assembly file (fasta format)> <NG output file name> <estimated genome size (in Mb)> <assembly metrics output file name> <contamination check output file name>  <email id> <BUSCO dataset name>  <BUSCO output directory name>  <AUGUSTUS species>  <Number of threads> ```

**Example:**

``` docker run -v ~/my-scratch-dir:/working-dir -w /working-dir assemblyqc arabidopsis.fasta output_NG 200 output_assembly output_contamination assemblyshine@gmail.com embryophyta_odb9 output_buscoassembly arabidopsis 4  ```

For genome annotation quality assessment: 
---------------------
1.	Install the docker engine for your platform (https://docs.docker.com/install/).
2.	Download the Docker directory (make_annotationqc) from the github repo. This directory contains the Dockerfile and the associated files needed to build the docker image. 
3.	Run the following commands within the make_annotationqc directory to use the assembly pipeline: 

``` mkdir ~/my-scratch-dir (This will create a scratch directory where you need to put all your input files.) ```

``` docker build --no-cache -t annotationqc ```

``` docker run -v ~/my-scratch-dir:/working-dir -w /working-dir annotationqc <genome annotation file (gff3 or gff format)> <annotation metrics output file name> <transcript file (FASTA format)>  <BUSCO output directory name> <BUSCO dataset name>   <Number of threads> ```

**Example:**

``` docker run -v ~/my-scratch-dir:/working-dir -w /working-dir annotationqc GCF_000001735.4_TAIR10.1_genomic.gff output_gff GCF_000001735.4_TAIR10.1_rna.fna output_buscogff embryophyta_odb9 4 ```

**For plotting NG graph from the NG values (This is a seperate R script outside the container):**

``` Rscript NG.R <NG_file> ```