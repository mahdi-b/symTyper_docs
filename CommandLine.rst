Command Line Symtyper
=====================

Installing Symtyper's requirements
++++++++++++++++++++++++++++++++++

The most recent version of Symtyper is a self-contained Python script that can be run without being explicitly installed on the system. 
However, Symtyper depends on other applciation for its exectution. These applications are

============= =========== =======
Application   Version     Notes 
============= =========== =======
HMMER         >=3.0	  http://selab.janelia.org/software/hmmer3/
Blast	      >=2.2.25    . Currently, only legacy Blast is supported
cd-hit	      >= 4.5.6	  
biopython     >= 1.61
ete2	      >= 2.2
xvfb			  Required for executing Symtyper on a remote server via ssh
============= =========== =======



Runnign Symtyper sub-program
++++++++++++++++++++++++++++
Symtyper is comprised of 5 subprograms that each carry out a specific funciton. 
These programs are: :ref:`clade`, subtype, resolveMultipleHits, builPlacementTree and makeTSV.
The details for each program is described below.

.. _clade:

clade
-----

usage
*****

usage: symTyper.py clade [-h] -s SAMPLESFILE -i INFILE [-e EVALUE]

Input
*****
REQUIRED

======================	===========
Param			Description
======================  ===========
-i, --inFile            File containing the sequencing reads in fasta fomat. Note that this files requires the ids to be fomatted using the following :ref:`inputFormat`
-s, --samplesFile       The :ref:`sampleFile`
======================  ===========


Ouptut
******
**fasta/**: Directory cotaining a collection of fasta sequences representing the intput fasta file split by sample
**hmmer_output/**: Directory containing HMMER output files, broken down by sample
**hmmer_parsedOutput/**: Directory containing listing of :ref:`AMBIGUOUSOUT`, :ref:`HITSOUT`, :ref:`NOHITSOUT` and :ref:`LOWOUT` for each of the input samples
**hmmer_hits/**: Directory containing fasta files, split by clade, of sequences having hits against the clade database.

.. _subtype:

subtype
-------

usage: symTyper.py subtype [-h] -s SAMPLESFILE -H HITSDIR -b BLASTOUTDIR -r BLASTRESULTS -f FASTAFILESDIR
Directory contains HMMER output files, broken down by sample


Input
*****

The input to "clade" is expected to be in the same format as that produced by the :ref:`clade` subprogram

======================  ===========
Param                   Description
======================  ===========
-f, --fastaFilesDir 	Directory cotaining sequences from the input fasta file, split by `clade` (fasta directory)
-s, --samplesFile 	The :ref:`sampleFile`
-H, --hitsDir		HMMER fasta hits output directory produced by :ref:`clade` (hmmer_hits directory)
-b, --blastOutDir 	Blast output directory 
-r, --blastResults	Parsed blast results directory
======================  ===========


Output
******

**blast_output/**: Directory containing Blast output files, broken down by sample
**blastResults/**: Directory containing informaiton on the :ref:`perfect`, :ref:`Unique`, :ref:`New`, :ref:`ShortNew` and :ref:`Short`

The output formats for the files in blastResults/ can be found here:

:ref:`PERFECTOUT`
:ref:`UNIQUEOUT`
:ref:`NEWOUT`
:ref:`SHORTNEWOUT`
:ref:`SHORTOUT`


.. _resolveMultipleHits:

resolveMultipleHits
-------------------

Input
*****

usage: symTyper.py resolveMultipleHits [-h] -s SAMPLESFILE -m MULTIPLEFASTADIR -c CLUSTERSDIR

The input to **resolveMultipleHits** is expected to be in the same format as that produced by the :ref:`subtype` subprogram

======================  ===========
Param                   Description
======================  ===========
-s, --samplesFile 	The :ref:`sampleFile`
-m, --multipleFastaDir	Directory containing sequences with multiple hits, split by `clade` (x directory)
-c, --clustersDir 	Directory that will contain cluster information
======================  ===========

Output
******
**resolveMultiples/Reps**: Representatives from each cluster  
**resolveMultiples/clusters**: Clusters produced for each sample
**resolveMultiples/correctedMultiplesHits**: Contains output files from clustering and multiple hit resolution

The resolveMultiples/correctedMultiplesHits directory contains the following files and directory:

* correctedOutputFile_all_clades: :ref:`correctedAll`
* resolvedOutputFile_all_clades: :ref:`resolvedAll`
* corrected/: Contains :ref:`correctedPerClade`, split by `clade` 






.. _builPlacementTree:

builPlacementTree
-----------------


usage: symTyper.py builPlacementTree [-h] -c CORRECTEDRESULTSDIR -n NEWICKFILESDIR -o OUTPUTDIR



Input
*****

The input to **builPlacementTree** is expected to be in the same format as that produced by the :ref:`resolveMultipleHits` subprogram

===========================  ===========
Param                        Description
===========================  ===========
-c, --correctedResultsDir    Directory containing corrected Clade placements (the correctedMultiplesHits/corrected directory from resolveMultipleHits)
-n, --newickFilesDir	     Newick directory for input calde phylogenies in Newick format
-o, --outputDir 	     Dir that will contain the newick and interenal nodes information
======================  ===========



Output
******

The output directory containing the placement information for, broken down by sample


.. _makeTSV:

makeTSV
---------

Input
*****

Files and directories produced by the :ref:`builPlacementTree` subprogram

Output
******












