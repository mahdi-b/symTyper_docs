SymTyper's Concepts
======================



Definitions
-----------

.. _HITS:

HIT
+++

This is a clade-relevant definition. To be a HIT against a clade reference sequence, a query needs to unambiguously align with a defined similarity over a defined percentage of its length. 
Furthermore, the e-value of the first hit needs to be at least K orders of magnitude larger than that of an alternative clade. 




.. _NOHITS:

NOHIT
++++++



This is a clade-relevant definition. A Sequence is considered a NOHIT if it does not have any satisfactory alignments against a clade.



.. _AMBIGUOUS:

AMBIGUOUS
+++++++++

This is a clade-relevant definition. An ambiguous sequence is one that has more than one satisfctory clade hit.


.. _perfect:

Perfect
+++++++

This is a subtype-relevant definition. Perfect refers to a query
sequence that aligns unambiguously to one sequence in the reference
database (e.g., 100% similarity to 100% of the length of the target)
for which the best hit's raw bit score is at least 3 orders of
magnitude larger than the raw bit score for the second hit.



.. _unique:

Unique
++++++

This is a subtype-relevant definition. Unique refers to a query sequence that aligns to a single reference in
the database with a user-defined (e.g., :math:`>=` user defined % similarity
to 100% target length) for which the best hit's raw bit score is at
least 3 orders of magnitude larger than the raw bit score for the
second hit.




.. _New:

New
+++


This is a subtype-relevant definition. A New subtype applies to a sequnence with no significant hit to any of the subtype database sequences.



.. _ShortNew:

ShortNew
++++++++

This is a subtype-relevant definition. ShortNew refers to a query sequence that aligns with high similarity to
a unique reference sequence according to the dynamic similarity
threshold (Equation 1: :ref:`dynamic_similarity`) below.





.. _multiples:

Multiples
+++++++++

This is a subtype-relevant definition. A query sequence of type multiple is a sequence that aligns with equal similarity to multiple subtypes sequences.



.. _Short:

Short
+++++

This is a subtype-relevant definition. A query of type short, is one that does not meet the minimum 
similarity and length requirements (e.g., :math:`<` 90% similarity to :math:`<` 90% of the length of the target). 


.. _dynamic_similarity:

Dynamic Similarity
++++++++++++++++++

The dynamic similarity threshold is computed to allow query sequences
that are shorter than the database references to be considered as potential 
hits. However, the shorter the sequnces, the higher the required stringency. 
The dynamic similarity threshold is computed as:

:math:`required\_similarity = 100 - \frac{C - min_c}{1-min_c} * (100 - min_s)`

where:

=============	============================================================================
C		is the coverage fraction of the query over the hit sequences
:math:`min_c`	is the minimum accepted coverage fraction of the query and the hit sequences
:math:`min_s` 	is the minimum similarity threshold between the query and the hit sequences
=============	============================================================================


.. _multiple_hits:

Ambiguous Hit Correction
++++++++++++++++++++++++


An ambiguous hit occurs when a sequences aligns with multiple subtypes. To try to infer the correct subtype of 
the sequence, we employ a strategy similar to the wisdom of the crowd, and allow similar sequences to help contribute 
information about the closest subtype of the sequence. To do so, ambiguous sequences are clustered using high stringency 
and a subtype distribution (or spectrum) is computed for each cluster. 



Suppose a cluster has a distribution: 
88 C1.1, 45 C1.18, 6 C1.21 and 2 C1.28. This means that at least 88 sequences in the cluster were subtyped as C1.1. and only 1 
was subtyped as C1.28. 

Clusters' distributions are usually highly skewed with few high 
frequency subtypes and a greater number of low frequency types.  Since 
there distributions are subsequently used to infer the :ref:`lca` 
(LCA) sequence as a proxy, it is very improtant to rid the data of 
unlikely subtype that can bias the computation of the LCA. For the 
previous distribution, the wisdom of the crowd tells us that this 
cluster of sequences is closest to C1.1. and unlikely to be C1.28 and 
therfore drops it for the C1.28. The same can be said about C1.21 
since only 6 sequences have been aligned to it.  The corrected 
distribution is thus likely 88 C1.1, 45 C1.18. This distribution will 
be subsequently used to map the reads to the common ancestor in the 
phylogeny.

The algoirthm used to correct the subtypes distribution uses a similar 
approach by formalizing which subtypes to drop for the distribution 
using a strigency parameter p. To do so, we iteratively drop the 
the subtypes that have counts within the :math:`p^{th}` percentile of the distribution and stop 
when no subtypes can be dropped. 


.. _resolved:

Resolved
++++++++

An ambiguous read is said to be resolved if its filtered distribution after the :ref:`multiple_hits` contains a single subtype.



.. _LCA:

Lowest Common Ancestor
++++++++++++++++++++++

In a phylogenetic tree, an internal node, :math:`N`, is the lowest common ancestor (or most recent common ancestor) of a set of leaves :math:`L`, if :math:`N` is the first common parent of all the leaves of in :math:`L`

Placement Tree 
++++++++++++++

A phylogeny of the subtypes in each clade where an internal node can be labeled using the number of seqeuencing reads for which is considered to be the most recent ancestor

.. _TSV:

TSV Format
++++++++++

A file with tab delimited columns


.. _sampleFile:

Samples File
++++++++++++

A file cotaining the samples -- one per line -- in the dataset.



Input File Formats
------------------

.. _inputFormat:

Fasta Input Format
++++++++++++++++++

Sequence ids in the fasta file are required to have the following format. 

**Sample_ID::Seq_Number**

* **Sample_ID**: refers to the sample to which the sequence belongs. The sampleID should be present in the :ref:`sampleFile`
* **Seq_Number**: is a unique identifier for a the sequence.

Note that the two colons (**::**) are used to separate the Sample_ID and the Seq_Number.



Clade Output Format
-------------------


.. _HITSOUT:

HITS OUTPUT
+++++++++++

* Query sequence id
* Hit start in query
* Hit end in query
* First hit id
* Second hit id
* First hit e-value
* Second hit e-value


.. _NOHITSOUT:

NOHITS OUTPUT
+++++++++++++

* Query sequence id


.. _AMBIGUOUSOUT:

AMBIGUOUS OUTPUT
++++++++++++++++

* Query sequence id
* First hit id
* Second hit id 
* First hit e-value
* Second hit e-value

.. _LOWOUT:

LOWOUT
++++++

* Query sequence id
* First hit id
* Hit e-value

.. _MULTIPLEOUT:

MULTIPLE OUTPUT
+++++++++++++++

* Query sequence id
* List of hits ids



Subtype Output Formats
----------------------

.. _NEWOUT:

NEWOUT
++++++

* Query sequence id


.. _PERFECTOUT:

PERFECT OUTPUT
++++++++++++++

* Query sequence id
* Best hit id
* Query length / Hit length
* Percent identity



.. _SHORTOUT:

SHORT OUTPUT
++++++++++++

* Query sequence id
* Query length
* Best hit id
* Best hit lenght

.. _SHORTNEWOUT:

SHORTNEW OUTPUT
+++++++++++++++

* Query sequence id
* Best hit id
* Query length / Hit length
* Percent identity

.. _UNIQUEOUT:

UNIQUE OUTPUT
+++++++++++++

* Query sequence id
* Best hit id


ResolveMultipleHits Output Formats
----------------------------------

.. _correctedAll:

Corrected Output All Clade
++++++++++++++++++++++++++


Tab separated fields and colon separated values. Ex.

``Cluster: CL_415 numSeq: 6       clade: C        breakDown:180:4 175M:2  subtypes: C3.24_HE579012: 6, C3k_AY589737: 6, C3.23_HE579011: 6``

The previous line tell us that CL_145 representes 6 Sequences, 2 form sample 175M and 4 from sample 180. These sequences are in Clade C and have the subtype distribution listed in `subtype` list.



.. _resolvedAll:

Resolved Output All Clades
++++++++++++++++++++++++++

* Cluster ID
* Number of sequences in the cluster
* Clade
* Subtype of sequences in the cluster

.. _correctedPerClade:

Corrected Output Per Clade
++++++++++++++++++++++++++

This file format is similar to that in :ref:`correctedAll` except that the `subtype` list represents the corrected (or effective), rather than initial, subtypes.






