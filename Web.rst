Web-based SymTyper 
==================


Brief Overview
--------------
To run SymTyper from the web, follow these instructions:

First, invoke symtyper main submission page (http://www.symtyper.com). You should be presented with the following page in :ref:`fig1`.

.. _fig1:

.. figure:: _static/main.png
   :scale: 50%
   :alt: SymTyper Main Screen
   :align: center

   SymTyper's Main Screen

To submit a new analysis, browse and select your input fasta file and a valid  ids file (:ref:`inputFormat`) and then click submit (See :ref:`fig2`).

.. _fig2:

.. figure:: _static/submit_input.png
   :scale: 50%
   :alt: SymTyper Main Screen
   :align: center

   New SymTyper Analysis Screen

The next screen will provide you with the URL where the output can be accessed.
Depending on the input size, the processing can take between few minutes to hours (See :ref:`fig3`).
Please copy the URL for future access. Job will be hosted on the SymTyper site for 15 days.

.. _fig3:

.. figure:: _static/processing.png
   :scale: 50%
   :alt: SymTyper Main Screen
   :align: center

   Processing Screen and Job URL



If the anlysis completed successfully, you will be presented with
the a summary table where the various componenents of the analysis
can be accessed (:ref:`main_results_page`). The results are gouped by section: Clades, Subtypes, Multiples, Trees, Breakdown. These sections are explained below.
   

.. _main_results_page:

.. figure:: _static/results.png
   :scale: 50%
   :alt: SymTyper Results Main Screen
   :align: center

   SymTyper Results Main Screen

.. tabularcolumns:: |p{2cm}|p{13cm}| 

================    ============
Section    	    Description
================    ============
Clades		    Shows the breakdown of clades per sample. The results can be viewed or download as a matrix or show as a piechart per sample
Subtypes	    Shows the breakdowns of subtypes per sample. The results can be viewed independently for the :ref:`perfect`, :ref:`unique` and  :ref:`ShortNew` subtypes
Multiples	    The graphs shows the distribution of sequences for each clade contaning multiple hits. The definition of a Multiple hits is described in the :ref:`multiples` section
Trees		    Describes the breakdown of the number of sequences assigned to the internal nodes, and the clades per sample. The tree representation show the combined count for all the samples  
Breakdown	    Shows a Sunburst representation of the Clades and subtypes by sample
================    ============


Clades View
+++++++++++++

The Clades View shows a table view of the distribution of HITS,
NOHITS, LOW and AMBIGUOUS hits per sample.  Clicking the View Chart
provides access to the clades distribution for each sample. The
complete results and disbtribution of clades per sample can be
downloaded from the results main page (see :ref:`pie_chart`).


.. _pie_chart:

.. figure:: _static/pie_chart.png
   :scale: 50%
   :alt: Pie chart view of clade distribution
   :align: center
   
   Pie Chart Distribution of Clade per Sample



Subtypes View 
+++++++++++++++

The Subtypes Views shows the breakdown of subtypes per sample. The results
can be viewed independently for the :ref:`perfect`, :ref:`unique` and the
:ref:`ShortNew` subtypes. The subtypes are assigned based on the blast results of the query sequences to
the clade specific references (See :ref:`subtype_view`). 

.. _subtype_view:


.. figure:: _static/subtypes.png
   :scale: 60%
   :alt: Subtypes view
   :align: center
   
   Subtypes Distribution per Clade

.. tabularcolumns:: |p{2cm}|p{13cm}| 

=========	    ================================
Section		    Description
=========	    ================================
Perfect		    A query sequence that aligns perfectly or with very high similarity to a unique symbiont reference in the database (e.g., 100% similarity to 100% of the length of the target) 
Unique 	    	    A query sequence that aligns unambiguously to symbiont reference in the database. (e.g., :math:`>=` user defined % similarity to 100% target length and the bit score for the best hit is at least 3 orders or magnitude larger than than that for the second hit); 
ShortNew	    A query sequence shorter than the average sequence in the reference database but aligns with high similarity to a unique reference according to the dynamic similarity threshold (See :ref:`dynamic_similarity`) 
=========	    ================================


Multiples View
++++++++++++++++

The Multiples View is a graphical representation of the corrected subtypes
count to which ambiguous sequences map. The algortihm used to
resolved multiple hits is described in the :ref:`multiple_hits` and
detailed in the manuscript (See :ref:`multiplesview`).

.. _multiplesview:

.. figure:: _static/multiples.png
   :scale: 50%
   :alt: Subtypes view
   :align: center

   Subtypes Distribution for the Corrected Ambiguous Hits

The breakedown of subtypes for :ref:`resolved` under the "Resolved tab"

Trees View
++++++++++



For each clade phylogeny, this view compiles the number of times a :ref:`LCA` 
was identified for an ambiguous sequence (after the :ref:`multiple_hits` stage). 
The tree can be downloaded in the Newick format and viewed or parsed in phylogeny 
applications. A matrix file comparing results across samples can be be found in 
output archive available for download from the main page.


Breakdown View
++++++++++++++

Using user-friendly graphical Sunburst representation, this view
summarizes the intricate structure of Symbiodinium clades and subtypes
in a single or multi-sample view. Highlighting a level of the Sunburst
charts display its structure and the percentage of sample reads
assigned to it (See :ref:`sunburst`).


.. _sunburst:

.. figure:: _static/breakdown.png
   :scale: 50%
   :alt: Subtypes view
   :align: center

   Subtype Breakdown Vizualization