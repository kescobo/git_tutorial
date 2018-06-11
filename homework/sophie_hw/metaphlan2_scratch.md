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
