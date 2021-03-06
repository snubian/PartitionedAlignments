How to add a dataset
====================

What you need
-------------

1. A DNA, amino acid, morphology, or language alignment from a published paper.

2. Permission to archive that alignment with a CC0 license. (This is important)

3. Lots of additional information on the alignment, including:

    (i) Where the loci are (AKA partition boundaries)

    (ii) Which genome (mitochondrial, nuclear, chloroplast) each locus comes from

    (iii) Codon positions (for protein-coding DNA datasets)

    (iv) Ages of sequences (e.g. for aDNA or virus datasets)


What you do
-----------

1. Convert your alignment to NEXUS format. The format should be identical to that in Anderson_2013, this is not flexible or negotiable. See below for precise details on how to format this file.

2. Add a SETS block to the .nex file with three comments [loci], [genomes], [outgroups].

3. Add CHARSETS that describe each locus to the [loci] section, according to the conventions below. Every site in the alignment needs to be covered by one and only one of these CHARSETS.

4. Add CHARSETS that describe each genome of origin to the [genomes] section, according to the conventions below. Every site in the alignment needs to be covered by one and only one of these CHARSETS.

5. If there are outgroups in your dataset, add them as a TAXSET in the [outgroups] section.

6. If you have heterochronous data, create a SAMPLINGDATES block, and populate it with the sampling dates of all taxa (see Duchene_2015a for an example).

7. Check and double check the nexus file. Check it loads into a couple of programs too.

7. Make a new folder in the /datasets folder

8. Name it after the first author and year of publication (e.g. Brown_2012)

9. Copy the README.yaml into the folder. Fill in ALL fields.

10. Add in the dataset itself, in NEXUS format, and named alignment.nex


Before you submit a pull request
--------------------------------

1. Check you have completed the ENTIRE README.yaml file, and that there are no errors in your nexus or YAML file. Take your time.

Conventions
-----------
Follow all of these rules...

1. Your NEXUS file should start with these two blocks: DATA and SETS.

2. It may also contain a SAMPLINGDATES block.

3. The DATA block should look like this:

        begin DATA;
            dimensions ntax=145 nchar=3037;
            format datatype=nucleotide missing=? gap=-;

The datatype must be either 'nucleotide' or 'protein'. The missing and gap symbols must be as above.

4. Your 'SETS' block should look like this before you put the data in:

        begin sets;

            [loci]

            [genomes]

            [outgroups]

        end;

5. Inside the 'sets' block, we are aiming for something like this:

        begin SETS;

            [loci]
            CHARSET COI_1stpos = 1-1592\3;
            CHARSET COI_2ndpos = 2-1592\3;
            CHARSET COI_3rdpos = 3-1592\3;
            CHARSET 16S = 1593-3037;

            [genomes]
            CHARSET mitochondrial_genome = 1-3037;

            [outgroups]
            TAXSET outgroups = Afrololigo_mercatoris_FEA Alloteuthis_africana_312327;;

        end;

6. ALL protein coding genes must have their codon positions delineated. We use the format above, which is e.g. NAME_1stpos. Where "NAME" is the name of the gene. Every gene must have all three positions defined.

7. Check that each protein coding gene really is in the frame you think it should be (and that you have indicated in the nexus file). Do this in geneious by translating it and checking the translation by BLASTing the sequence against GenBank and checking the official translation.

8. Add information to the genomes section, to make sure that every single base is covered by one of the following annotations:

    mitochondrial_genome
    nuclear_genome
    chloroplast_genome
    dsDNA_genome
    ssDNA_genome
    dsRNA_genome
    ssRNA_genome

The latter four are reserved for viruses

9. If the data is heterochronous (i.e. sampled from multiple time points) make sure that you include a 'SAMPLINGDATES' block. Here's an example:

        begin SAMPLINGDATES;
        	dimensions ntax=12;
        	units = calendaryears
        	FJ174401, 1978
        	KC990883, 2012
        	FJ174385, 1961
        	GQ477151, 2007
        	HM745325, 2009
        	HM745346, 2005
        	JX857503, 2009
        	HM745344, 2005
        	HM745350, 2005
        	FJ174397, 1988
        	FJ174412, 1993
        	HM745343, 2005
        end;

10. In the README.yaml file, fill out everything as instructed in the file itself. Don't change the structure of the yaml file, or delete any entries.

11. For datasets without explicit licenses, always contact the owners of the dataset to ask whether we can put it in the repository, and whether we can release it under a CC0 license. If they don't agree, don't put it in the repository. Assume that data sets on TreeBase are O.K., since they're already in the public domain.
