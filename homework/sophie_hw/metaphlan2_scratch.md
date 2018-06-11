# Metaphlan2 tutorial

## Install Metaphlan2
* Moved folder to ~/biobakery-metaphlan2-e7761e78f362/

**Have to run before using Metaphlan2**

`$ export PATH=$PATH:~/biobakery-metaphlan2-e7761e78f362/`  
`$ export PATH=$PATH:~/biobakery-metaphlan2-e7761e78f362/utils/`  
`$ chmod +x ~/biobakery-metaphlan2-e7761e78f362/`  
`$ which metaphlan2.py`  
    `/Users/sophierowland/biobakery-metaphlan2-e7761e78f362//metaphlan2.py`  
`$ metaphlan2.py -h`
* Long help output, check

## Download files
`$ curl -O https://bitbucket.org/biobakery/biobakery/raw/tip/demos/biobakery_demos/data/metaphlan2/input/SRS014476-Supragingival_plaque.fasta.gz`    
`$ curl -O https://bitbucket.org/biobakery/biobakery/raw/tip/demos/biobakery_demos/data/metaphlan2/input/SRS014494-Posterior_fornix.fasta.gz`    
`$ mv ~/Downloads/SRS*.fasta.gz metaphlan_tutorial/`  
`$ cd ~/gitrepos/metaphlan_tutorial`

* ~/gitrepos/metaphlan_tutorial
    * SRS014476-Supragingival_plaque.fasta.gz
    * SRS014476-Supragingival_plaque_profile.txt
    * SRS014494-Posterior_fornix.fasta.gz

* Download remaining files

`$ mv ~/Downloads/SRS*.fasta.gz ~/gitrepos/metaphlan_tutorial/`

## Run a single sample
`$ metaphlan2.py SRS014476-Supragingival_plaque.fasta.gz  --input_type fasta > SRS014476-Supragingival_plaque_profile.txt`  

**Error message:**  
`Warning! Biom python library not detected!
 Exporting to biom format will not work!
Traceback (most recent call last):
  File "/Users/sophierowland/biobakery-metaphlan2-e7761e78f362/utils/read_fastx.py", line 9, in <module>
    from Bio import SeqIO
ModuleNotFoundError: No module named 'Bio'
Traceback (most recent call last):
  File "/Users/sophierowland/biobakery-metaphlan2-e7761e78f362/utils/read_fastx.py", line 9, in <module>
    from Bio import SeqIO
ModuleNotFoundError: No module named 'Bio'
OSError: fatal error running '/Users/sophierowland/biobakery-metaphlan2-e7761e78f362/utils/read_fastx.py'. Is it in the system path?`

### Error 1 - ModuleNotFoundError: No module named 'Bio'
* Problem with Anaconda?  
`$ conda install -c anaconda biopython`  
* Try running again
`$ metaphlan2.py SRS014476-Supragingival_plaque.fasta.gz  --input_type fasta > SRS014476-Supragingival_plaque_profile.txt`
* No error message...
* Expected 2 output files, got both!
    * SRS014476-Supragingival_plaque.fasta.gz.bowtie2out.txt
    * SRS014476-Supragingival_plaque_profile.txt

## Output files
`$ less -S SRS014476-Supragingival_plaque.fasta.gz.bowtie2out.txt`

:q

`$ less -S SRS014476-Supragingival_plaque_profile.txt`

:q

* Running again, second file is empty. *Why?*
    * Because I re-ran the command and it overwrote the last file
    * Delete previous files, run again
        * It worked!

    `$ metaphlan2.py SRS014476-Supragingival_plaque.fasta.gz  --input_type fasta > SRS014476-Supragingival_plaque_profile.txt`

    `$ less -S SRS014476-Supragingival_plaque_profile.txt`

## Run on multiple cores
*What does "multiple cores" mean?*

`$ metaphlan2.py SRS014459-Stool.fasta.gz --input_type fasta --nproc 4 > SRS014459-Stool_profile.txt`

* Similar problem to above, remove file (SRS014459-Stool.fasta.gz.bowtie2out.txt) and try again
    * Error message below

**Error message:**
`OSError: Not a gzipped file (b'>H')`
* Check .txt file, empty

`$ less -S SRS014459-Stool_profile.txt`

* Prof Google not helpful
* Sent question to Lauren Tso & Kevin Bonham

### Error trouble shooting
1. *From Kevin* - Click download, rename to not have .gz, then zip

`$ mv ~/Downloads/SRS*.fasta.gz ~/gitrepos/metaphlan_tutorial/`

`$ mv SRS014476-Supragingival_plaque.fasta.gz SRS014476-Supragingival_plaque.fasta`

`$ gzip SRS014476-Supragingival_plaque.fasta`

`$ metaphlan2.py SRS014476-Supragingival_plaque.fasta.gz --input_type fasta --nproc 4 > SRS014459-Supragingival_plaque_profile.txt`

2. *From Lauren* Delete all files, re-download everything using `$ curl -O`

`$ curl -O https://bitbucket.org/biobakery/biobakery/raw/tip/demos/biobakery_demos/data/metaphlan2/input/SRS014476-Supragingival_plaque.fasta.gz`

`$ curl -O https://bitbucket.org/biobakery/biobakery/raw/tip/demos/biobakery_demos/data/metaphlan2/input/SRS014494-Posterior_fornix.fasta.gz`

`$ curl -O https://bitbucket.org/biobakery/biobakery/raw/tip/demos/biobakery_demos/data/metaphlan2/input/SRS014459-Stool.fasta.gz`

`$ curl -O https://bitbucket.org/biobakery/biobakery/raw/tip/demos/biobakery_demos/data/metaphlan2/input/SRS014464-Anterior_nares.fasta.gz`

`$ curl -O https://bitbucket.org/biobakery/biobakery/raw/tip/demos/biobakery_demos/data/metaphlan2/input/SRS014470-Tongue_dorsum.fasta.gz`

`$ curl -O https://bitbucket.org/biobakery/biobakery/raw/tip/demos/biobakery_demos/data/metaphlan2/input/SRS014472-Buccal_mucosa.fasta.gz`

`$ mv ~/SRS*.fasta.gz ~/gitrepos/metaphlan_tutorial`
*Only necessary if dir not ~/gitrepos/metaphlan_tutorial*

## Run multiple Samples
`$ metaphlan2.py SRS014464-Anterior_nares.fasta.gz --input_type fasta --nproc 4 > SRS014464-Anterior_nares_profile.txt`  

`$ metaphlan2.py SRS014470-Tongue_dorsum.fasta.gz --input_type fasta --nproc 4 > SRS014470-Tongue_dorsum_profile.txt`

`$ metaphlan2.py SRS014472-Buccal_mucosa.fasta.gz --input_type fasta --nproc 4 > SRS014472-Buccal_mucosa_profile.txt`

`$ metaphlan2.py SRS014494-Posterior_fornix.fasta.gz --input_type fasta --nproc 4 > SRS014494-Posterior_fornix_profile.txt`

* Create single tab-delimited table from output files
`$ merge_metaphlan_tables.py *_profile.txt > merged_abundance_table.txt`

`$ less -S merged_abundance_table.txt` :q

# Vistualiza results

## Create a heatmap with hclust2
* hclust2 = plotting tool

#### Install hclust2
`$ brew tap biobakery/biobakery`

`$ brew install hclust2`

### Step 1: Generate the species only abundance table
`$ grep -E "(s__)|(^ID)" merged_abundance_table.txt | grep -v "t__" | sed 's/^.*s__//g' > merged_abundance_table_species.txt`

`$ less -S merged_abundance_table_species.txt` :q

#### What's happening in this code?
* grep = finds specified patterns within text, "global regular expression print"
1. grep 1: Searches for `"(s__)|(^ID)"` = lines with species info & also to the header
    * `grep -E "(s__)|(^ID)" merged_abundance_table.txt`
2. grep 2: Does NOT print lines with strain info
    * `grep -v "t__"`
3. sed: Removes full taxonomy, printing only species name
    * `sed 's/^.*s__//g'`

### Step 2: Generate the Heatmap
`$ hclust2.py -i merged_abundance_table_species.txt -o abundance_heatmap_species.png --ftop 25 --f_dist_f braycurtis --s_dist_f braycurtis --cell_aspect_ratio 0.5 -l --flabel_size 6 --slabel_size 6 --max_flabel_len 100 --max_slabel_len 100 --minv 0.1 --dpi 300`

**Error message:**

`hclust2.py: command not found`

* Try to install with conda?

`$ conda install -c bioconda hclust2`

**Error message:**

`AttributeError: Unknown property axisbg`

* Problem with matplotlib
  * Possibly axisbg -> facecolor?
* Install matplotlib with Homebrew

`$ brew install matplotlib` - *did not work*

* Install matplotlib with pip - *same error message*

`$ curl -O https://bootstrap.pypa.io/get-pip.py`

`$ python3 get-pip.py`

`$ python3 -mpip install matplotlib`

#### What's happening in this code?
* Options to select the top 25 features = `--ftop 25`
* Use Bray-Curtis as distance measure...
    * between samples = `--s_dist_f braycurtis`
    * between features = `--f_dist_f braycurtis`
* Set cell size ratio to 0.5 = `--cell_aspect_ratio 0.5`
* Use log scale for color scheme = `-l` (?)
* Set feature and sample size to 6 = `--flabel_size 6 --slabel_size 6`
* Set max feature and sample label length to 100 = `--max_flabel_len 100 --max_slabel_len 100`
* Select minimum value to display as 0.1 = `--minv 0.1`
* Select an image resolution of 300 = `--dpi 300`

## Create a cladogram with graphlan

#### Install graphphlan
`$ brew tap biobakery/biobakery`

`$ brew install graphlan`

### Step 1: Create the graphlan input files

### Step 2: Create a Cladogram
