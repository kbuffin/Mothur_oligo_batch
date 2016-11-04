# Mothur_oligo_batch
This repository was created by Ruben Props to run both mothur and oligotyping via a batch script on the University of Michigan HPC Flux system  on 16S rRNA fastq files produced by Illumina MiSeq sequencing.

<<<<<<< HEAD
# Install Oligotyping software in your local directory
```
=======
To Run the batch script (Mothur.batch.taxass), please follow the directions below:

## 1. Sign into the University of Michigan Flux system.

## 2. Navigate to your scratch folder.

## 3. Install Oligotyping software in your local directory
```R
>>>>>>> cea2ab7065b970d3a884e0a4c1ffa59560f6c66c
module load python-anaconda2/201607
pip install --user oligotyping
```
To check to make sure that the path to the oligotyping package is correct, try using a command from the oligotyping module:

```
oligotype -h
```
If the output brings up the manual for the `oligotype` command, you have successfully installed the oligotyping software!

<<<<<<< HEAD
In your current directory type:
```
=======
If the ouput says "-bash: oligotype: command not found", then it is possible that your path to the oligotyping package is incorrect.  Therefore, we need to fix our path.  To do so we will edit the .bash_profile file in our home directory.  Therefore, you will need to fix your path by typing the following in your current directory:
```R
>>>>>>> cea2ab7065b970d3a884e0a4c1ffa59560f6c66c
cd 	#This will take you to your *home* directory
ls -a 	#Show all files in your home directory, including hidden ones (like your .bash_profile file!)
```
Then under the line that includes "PATH=$PATH:$HOME/bin" that you have the following:
```R
export PATH=/home/your_unique_name/.local/bin:/:$PATH  # Be sure to change "rprops" to YOUR USER NAME!
```
If you do not have the above line, please edit it with nano:

```
nano .bash_profile
```

<<<<<<< HEAD
For the TaxAss script make sure you have the <code>dplyr</code> and <code>reshape</code> R packages installed in your local R version.
#  Load modules
```
module load mothur R ncbi-blast
```

# Copy mothur.batch.taxass in your folder with the fastq files
**Make sure the sample names of your fastq files are correct, no ':', '-' or '/' !**
In case you have to rename your files adapt the following code line:
```
find /scratch/vdenef_fluxm/rprops/process2/UM_ML14 -type f -exec rename '-' '' {} \;
=======
## 4. Load mothur, R, and ncbi-blast.
```R
module load mothur R ncbi-blast
```

## 5. Copy the `mothur.batch.taxass` file into your the folder with the fastq files.

## 6. **Make sure the sample names of your fastq files are correct. Mothur does **not** accept: ':', '-' or '/' !**
If you have to rename your files, you can run the following line of code:
```R
find /scratch/vdenef_fluxm/your_unique_name/path_to_fastq_files -type f -exec rename '-' '' {} \;
>>>>>>> cea2ab7065b970d3a884e0a4c1ffa59560f6c66c
```
The above code  will remove "-" from your sample names. You may have to run rerun this several times if you have multiple "-" in your sample names.

## 7. To select for a taxon of interest to perform oligotyping analysis on, run the following code:
**If you want to oligotype everything do *not* run this.** 
Replace <code> Bacteria;Proteobacteria;Betaproteobacteria;Burkholderiales;betI;betI_A </code> with your taxon of interest.
```
sed -i "s/Bacteria/Bacteria;Proteobacteria;Betaproteobacteria;Burkholderiales;betI;betI_A/g" mothur.batch.taxass
```

<<<<<<< HEAD
# Make stability file
=======
## 8. Make stability file (file with sample names and corresponding fastq files for that sample).
>>>>>>> cea2ab7065b970d3a884e0a4c1ffa59560f6c66c
Should you get an error during <code>make.contigs</code> then check if the &#95;R1&#95; and &#95;R2&#95; pattern does not occur in the sample name.
```
paste <(ls *_R1_*.fastq | awk -F"_" '{print $1}') <(ls *_R1_*.fastq) <(ls *_R2_*.fastq) > stability.file
```

<<<<<<< HEAD
# To make sure that you don't have hidden characters (i.e. from Windows)
```
dos2unix mothur.batch.taxass
dos2unix mothur.batch.taxass.pbs
```
# Run batch script
```
mothur mothur.batch.taxass
```
# or all the above as a pbs script
```
qsub mothur.batch.taxass.pbs
=======
## 9. You're ready to go!  Option A:  Run the `mothur.batch.taxass` or option B: submit a job to flux with the `mothur.batch.taxass.pbs`.
```R
mothur mothur.batch.taxass  #Option A

qsub mothur.batch.taxass.pbs  #Option B
>>>>>>> cea2ab7065b970d3a884e0a4c1ffa59560f6c66c
```
