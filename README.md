# Efishent
# Capture efficiency script

eFISHent 2.0 Manual:

Introduction:

The software consists of two seprate PERL scripts:

1) perl_loop_mafft_all
This script aligns the .fas output files from bingene using MAFFT (must be installed globally on your Linux machine; http://mafft.cbrc.jp/alignment/software/linux.html)

2) countseqs2
This script will use the alignment files deposited in outfolder1 (ending in .fas.out) resulting from step 1) and will count the length of each sequence as well as the gaps to collect information on how fragments are distributed, what the total-, gap-, and true sequence lengths are and compute a score, to evaluate how well the sequences score, based on the missing data, compared to the query sequence for each alignment file.

How to run:

1) perl_loop_mafft_all
- step1.1: create an empty folder
- step1.2:copy input files and the perl script perl_loop_mafft_scalar from the efishent folder into this folder. Input files are the resulting files from bingene (see Li et al. 2013), i.e. multiple fasta files containing sequence information from a query sequence and further sequences of interest. a list containing the fasta file names as text document, which should be named fileID 
- step1.3: list of input files:  a list containing the fasta file names as text document, which should be named fileID; how to create the fileID list: open a Terminal window; cd into folder containing the bingene output files (genebin folder); type: ls > fileID.txt.
- step1.4: create two empty folders within the folder from step1 
- step1.5: call the program: perl perl_loop_mafft_scalar fileID out1 out2
-NOTE: Do not change the order of the programm call!

Perl_loop_mafft_all_scalar uses MAFFT to align the quaried inputfiles placed in a list (fileID), in this list each inputfile has been checked for sequence names appearing twice, if they do they have been renamed. Once Mafft has run the 2 files created are put in different output folders. The New renamed fasta files(.fas) in out2 and the aligned output files (fas.out) in out1. 

EXAMPLES for file structures:

Bingene input:
1st file:
>queryNew_8fish_Danio_rerio 
GTATCATCTCCTGAG
>Aal 
TACCAGCTCCTGAA
>D1-5 
TATCATCTCCTGAGG

2nd file:
>queryNew_8fish_Danio_rerio 
GTATCATCTCCTGAG
>Aal 
TACCAGCTCCTGAA
>D1-5 
TATCATCTCCTGAGG

(…)

fileID:
Danio_rerio.1.48788.48665.fas
Danio_rerio.1.296705.296829.fas


example command: 
perl perl_loop_mafft_all_com_scalar fileID out1 out2 


2) countseqs2.pl

- step2.1: create an empty folder
- step2.2: copy the perl script countseqs2.pl from the efishent folder into the new folder created in step2.1
- step2.3: create an empty folder called "stats" within the folder created in step2.1
- step2.4: create another empty folder within the folder created in step2.1 called "input"
- step2.5: copy all files from folder out1 from 1) into the newly created folder "input"
- step2.6: create a list of filenames cotaining all file names from the folder "input" (as in step1.3)
- step2.7: call the programm: perl countseqs2.pl <filelist> <stats> <input>
NOTE: Do not change the order of the programm call!

Countseqs2.pl will collect some basic inforemation from the single alignment files and write them in a sample table (GC content, number of genes captures,...)

EXAMPLES for file structures:
Countseqs2 input:
    new_Danio_rerio.1.48788.48665.fas.out
    new_Danio_rerio.1.296705.296829.fas.out

-Input fasta file alignment format structure:
>tm62
--taccagctgctgaagacacaccagttgcctctggacgccttcctggtggcgctgaaga
tgatgcagctggacgacgtggacattgacgaggtgcaatgcattctggccaatctcatct
g-----
>queryNew_8fish_Danio_rerio
-gtatcatctcctgaggactcatcagcttcctctggctgcatttctggtgtcgctgcaga
tgatgaaggtggaggacgtggacatcgacgaggtgcagtgcattctggccaacctcatct
acatg-
>Aal
--taccagctcctgaagacccaccagctgcccctggatgcctttctggtttctctgaaga
tgatgcaggtggaggaggtggacatcgatgaggtccagtgcatcctggccaacctcatct
acatgg
(...)

