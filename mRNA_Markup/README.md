mRNA_Markup
mRNA_Markup is a local Galaxy tool based on the BioExtract workflow for the comprehensive annotation and primary analysis of transcript sets.

The workflow processes initial mRNA queries by filtering out vector and bacterial contamination, searching reference and comprehensive protein databases (to identify full-length coding and chimeric sequences), searching protein domain databases, and ultimately producing a detailed summary report.

Prerequisites
Ensure the following tools are installed on your system:

ncbi-blast+ (Note: Legacy BLAST is not supported)

biopython

MuSeqBox (Version 4.1 recommended)

Installation & Integration
This tool has been tested exclusively with local versions of Galaxy. To integrate the tool, simply copy the galaxy_dist directory from the repository directly into your local GALAXY directory tree.

Database Setup
The workflow requires an input mRNA file alongside bacterial, reference protein, and comprehensive protein databases in FASTA format (e.g., BacteriaDB, RefProtDB, AllProtDB, Smart, and UniVec).

Except for Smart databases (which come pre-formatted), you must format your local databases using BLAST+:

Nucleotide databases: makeblastdb -dbtype nucl -in DATABASE -parse_seqids

Protein databases: makeblastdb -dbtype prot -in DATABASE -parse_seqids

Author Contact
Manasa Diwakar Doddanahalli Email: manasadiwakardoddanahalli@gmail.com