# TREA

Transcriptional Regulator Enrichment Analysis

Gene expression is controlled by transcriptional regulators (TRs) including DNA-binding transcription factors and their cofactors as well as modifiers of chromatin structure and epigenetic tags which all interact effectuate changes in response to extra- and intracellular signals. TRs represent drug targets with the potential to simultaneously modulate multiple DEGs. To identify TRs of experimentally-derived differential gene expression datasets we developed a conservative multi-step methodology that draws on both computationally- and biologically-derived regulator-target gene interaction data from multiple resource databases: i) transcription factor regulation inferred from integrating genome-wide ChIP-X experiments (Chea) ii) JASPAR transcription factor DNA-binding preference position weight matrices iii) TRANSFAC transcription factor DNA-binding preferences position weight matrices and iv) Ingenuity Pathway Analysis Upstream Regulator analytic (IPA®, Qiagen, Valencia, CA). Together these resource databases allow for interrogation of gene expression datasets for enrichment of downstream targets of ~1350 TRs.

Basic operation of TREA: Universal gene ID formatted gene expression datasets are evaluated independently by each database analytic. Chea and JASPAR-TRANSFAC databases are accessed through the online open-access Enrichr platform (https://amp.pharm.mssm.edu/Enrichr3/). Resource database output files containing statistically enriched TRs (Enrichr adj. P < 0.05; IPA Upstream Regulator P < 0.01) and their downstream target gene IDs were processed for TREA using the scripts provided in this repository. Final TREA libraries containing significantly enriched TRs and associated astrocyte target genes were then generated for each condition through a screening for candidates that met one or more of the following criteria: i) TR is identified by IPA® and Chea or JASPAR-TRANSFAC ii) TR is identified by IPA® or Chea or JASPAR-TRANSFAC and exhibits a significant fold-change (up or down) in the respective gene expression profile. When the same TR was identified across two or more resource databases target gene ID lists were merged into a single TR-target gene signature.



RUNNING TREA WITH SAMPLE DATA:

First time users should run TREA on the sample dataset (LPS_Cord) using the Jupyter notebook files found in the folder "Jupyter Notebook". 
--> Run the notebooks in the order, first "1 - create_TREA_files.ipynb" and then "2 - create_collated_files.ipynb"
--> The notebooks can be executed using the "Run all" command or by running each cell in the order provided. 


RUNNING TREA ON A NEW DATASET:

1) Add Chea, Jasper-Transfac and IPA Upstream Regulator resource database output files (.csv) in the respective folders found inside "Sample Files".
Each of these resource database output files should contain two columns, named "term" and "genes". Where "term" is the regulator and "genes" are its regulated genes.
--> The genes need to be semicolon (";") separated. 
--> Please follow the naming convention "Chea TR_{disorder_name}_Clean.csv", "JASPAR-TRANSFAC TR_{disorder_name}_Clean.csv" and "ingenuity TR_{disorder_name}_clean.csv".

2) Add the differential gene expression data file for your disorder/condition, mapping each gene with its associated fold-change value. This file should contain two columns
--> Note: Refseq_ID and logFC. Refseq ID is universal gene ID nomenclature. 

3) Open the 1st Jupyter notebook, "1 - create_TREA_files.ipynb", go to cell 14, add the disorder/condition name to the dictionary object "diseases". Follow the format {disorder_name} : {name_you_want_of_output_file}. This disorder_name should be the same as you used in the above files. 

4) Add the disorder_name in the second Jupyter Notebook, 2 - create_collated_files.ipynb, in cell 3.Follow the same logic as in the previous notebook.
For example, if one is performing TREA for a spinal cord injury dataset, file naming should proceed as  "Chea TR_SCI_Clean.csv", "JASPAR-TRANSFAC TR_ SCI  _Clean.csv" and "ingenuity TR_ SCI_clean.csv". Output file nomenclature should follow as "Spinal Cord Injury", so in both the notebooks we shall go and add "SCI": "Spinal Cord Injury" to the dictionary object.

5) Once completed, execute both notebooks in the order defined and the output file generated will be saved as csv files in the folder "Output Files".

Happy TR hunting :)
