#orthology mapping between any pair of bacterial genomes

# Summary #
**GOST** is a program to detect orthologous relationship among microbial genomes. It was developed by Computational Systems Biolology Lab (CSBL) at University of Georgia.

# Installation #
Simply put 'GOST.tar.gz' in any directory,
  * $ tar zxvf GOST.tar.gz
enter the folder '**GOST2.0**'
  * $ ./INSTALL

# Usage #
## For basic usage of orthlogy mapping ##
Use the packed PERL script '**gost\_pipeline.pl**', which is a pipeline for GOST to generate an orthology mapping between two given species, using '**.faa**' files from NCBI and operon prediction from DOOR database.

  * $ perl gost\_pipeline.pl target\_species\_dir ref\_species\_dir output\_dir target\_operon(optional) ref\_operon(optional)

For example, to identify the orthology between _E. coli_ and _C. therm_
  * $ perl gost\_pipeline.pl example/ncbi\_data/Escherichia\_coli\_K\_12\_substrMG1655\_uid57779/ example/ncbi\_data/Clostridium\_botulinum\_B\_Eklund\_17B\_uid59159/ example\_output example/operon/Ecoli.opr example/operon/NC\_010674.opr

If you don't have operon files, we will generate fake operon files with fake\_operon.pl based on the ".faa" files:
  * $ perl gost\_pipeline.pl example/ncbi\_data/Escherichia\_coli\_K\_12\_substrMG1655\_uid57779/ example/ncbi\_data/Clostridium\_botulinum\_B\_Eklund\_17B\_uid59159/ example\_output\_no\_opr

## For advanced usage of orthology mapping ##
Use the compiled code **GOST** in ./GOST/build/bin/
  * $ ./GOST   OperonU    OperonV  Homology  RBH\_OUTPUT\_File  GOST\_OUTPUT\_File  evalue-cutoff
For example, in Unix
  * ./GOST/build/bin/GOST  GOST/data\_test/Escherichia\_coli\_K12.gi.operon GOST/data\_test/NC\_000853.gi.operon GOST/data\_test/NC\_000853.homology RBH GOST 1e-2
In Windows
  * /GOST/build/bin/GOST  GOST\data\_test\Escherichia\_coli\_K12.gi.operon GOST\data\_test\NC\_000853.gi.operon GOST\data\_test\NC\_000853.homology RBH GOST 1e-2

# Inputs and outputs #
## Input format ##
  * species\_directory: the directory containing the species information downloaded from NCBI
  * operon file format (operon id: a list of gene ids)

|1:| 16077069 |
|:-|:---------|
|2:| 16077070 |
|3:| 16077071 16077072 255767014|
|4:| 16077074 |

**Note**: if there exist plastosomes besides chromosome for a genome, just combine the operons in chromosome with that in plastosomes (renumber the ids accordingly)

  * homologous mapping from the reference genome (genomeName.homology). format: (geneid from target genome: a list of corresponding homologous genes in a reference genome)

|16127996:| (17935484,5e-13,3e-13)|        (17937867,6e-38,4e-35)|
|:--------|:----------------------|:-----------------------------|
|16127998:| (17934697,6e-52,3e-50)|
|16128003:| (17934541,6e-11,0.003)|

**Note**: 16127996, 16127998, 16128003 are gene ids from the target genome. (17935484,5e-13,3e-13) are gene information from the reference genome, in which 5e-13 and 3e-13 are e-value of blast from 16127996 to 17935484 and from 17935484 to 16127996, respectively.

The input data must be available for the program to run normally. Formats must be EXACTLY SAME as the format mentioned above.

## Output ##
  * Orhtology mapping prediction with the method GOST (.GOST file), containing identified orthologous gene pairs and the two evalues between them

|16127996,17935484|	5e-13,3e-13|
|:----------------|:-----------|
|16127998,17934697|	6e-52,3e-50|

  * Orthology mapping prediction with RBH (.RBH file), whose format is same to .GOST file.
  * A simple comparison between a and b

|RBH pairs:| 1101|
|:---------|:----|
|GOST pairs:| 1297|
|Common pairs:| 984|

# Contact #
Any questions, problems, bugs are welcome and should be dumped to

Qin Ma <maqin@uga.edu>

Yu Zhang <zy26@jlu.edu.cn>

Creation: Feb. 16, 2011