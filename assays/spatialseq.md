Spatial Transcriptomics - Visium
================================

Consumer-focused
================

1.  **Date (published):** 2022-05-16

2.  **Version (of this document):** v1.0

3.  **Authors:** James Webber, Katelyn Flowers, Bill Flynn

4.  **What is being measured?**

    a.  **Tags**^1^**:** Single-cell resolution, sequencing, imaging, transcriptomics

    b.  **Descriptive (optional):** Technologies for capturing transcriptome-wide gene expression in a spatial setting.

5.  **What analytical activities will the assay be used for** **within HuBMAP?**

    a.  **Tags**^1^**:** Map-Creation-for-Organs; Data Integration; General Characterization Assay

    b.  **Descriptive (optional):** These datasets will be used as a scaffold to map reference cell types into a spatial context, and identify spatial patterns in gene expression.

6.  **What type of human samples are needed or used?**

    a.  **Tags**^1^**:** Fresh Frozen; FFPE

    b.  **Descriptive (optional):** The two Different technologies can process different sample types

7.  **Commercial Product:** 10X Visium

*^1^ Include tags that can be normalized across assays, allowing for assay filtering. When possible, use structured terminology (ontologies).*

Assay Description
-----------------

**Primary Reference [PMCIDs](https://pubmed.ncbi.nlm.nih.gov/):**

PMID: 27365449 (Spatial Transcriptomics / Visium, no PMCID)

**Related:**

PMC6927209 (Slide-Seq)

PMC8606189 (Slide-Seq V2)\
[PMC7736559](http://www.ncbi.nlm.nih.gov/pmc/articles/pmc7736559/) (DBiT-Seq)

### **Technology Overview**

10x Genomics Visium Spatial Gene Expression slides utilize spatially barcoded mRNA-binding oligonucleotides oriented on a slide to capture mRNA in fresh frozen tissue or mRNA probe pairs in FFPE tissue sections. In either case, tissue is permeabilized to release mRNA or mRNA probes which bind to capture probes on the slide, and reverse transcription occurs while the tissue is still in place, generating a cDNA library that incorporates complements of the spatial barcodes and preserves spatial information. Barcoded libraries are mapped back to a specific spot on the Capture Area. This gene expression data is subsequently layered over a high-resolution microscope image of the tissue section, making it possible to visualize the expression of any mRNA, or combination of mRNAs, within the morphology of the tissue in a spatially resolved manner.

### Key Definitions

![](media/image1.png){width="7.3277777777777775in" height="2.647222222222222in"}

**Visium Slide**\
Each Visium slide has 2 - 4 mapping areas (also known as "capture areas") in which spatially barcoded capture oligos are deposited. Each slide has a unique serial number that determines the exact layout of the mapping area barcodes and perimeter fiducial markings.

**Mapping area**\
Each mapping area (also known as a capture area) contains spatially barcoded capture oligos, arranged in spots. When a tissue section is laid down on a mapping area, mRNA or mRNA-hybridizing probes precipitate down from the tissue and are captured on these oligos. The mapping area geometry is square, measuring between 6.5mm to 11mm on a side. The number of spots per mapping area is at least 4,992.

**Spot**\
A spot is a collection of capture oligos that share the same spatial barcode (but different UMI barcodes) and a known set of x,y coordinates. For the first generation Visium assays, these capture spots are circular with a typical diameter of 55um and are separated (center-to-center) by 100um horizontally and 110um vertically.

**Spatial Barcode**\
A unique 16bp nucleotide sequence with known x,y coordinates that ligates to mRNA molecules. This should not be confused with the unique molecular identifier (UMI) barcode that is used to distinguish between unique molecules within the same spot.

**Tissue Permeabilization**\
For the Visium Fresh Frozen workflow, the tissue section must be permeabilized to allow mRNA to precipitate down to the Visium slide to be captured. The amount of time a tissue is permeabilized is critical, as under-permeabilization leads to lower overall yield due to fewer available mRNA molecules, whereas over-permeabilization leads to lateral diffusion of mRNA which can distort or inhibit the assay's ability to detect the spatial localization of those molecules. A common phenotype of the latter is mRNA present in regions of the slide not covered by tissue.

### **Antibodies**

-   *~~N/A~~*

Please see the HuBMAP standard [report for antibody validation](https://avr.hubmapconsortium.org/).

Provider-focused
================

Files and Directories
---------------------

### **Directory structure**

| **Directory Name** | **Level** | **Required?** | **Description**                                                                                                                                            |
|--------------------|-----------|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| raw                | 0         | yes           | This is the raw, unmodified files coming from the sequencer. FASTQ                                                                                         |
| img                | 0         | yes           | This folder contains any OME-compatible TIFF files (brightfield, fluorescent) taken of the spatial transcriptomics mapping area prior to tissue digestion. |
| lab                | 1         | yes           | Processed files produced by the lab that generated the data.                                                                                               |
| lab/processed      | 1.1       | yes           | The output from the primary analysis pipeline.                                                                                                             |
| hive               | 2         | yes           | Processed files produced by HIVE using the spatial pipeline.                                                                                               |

### **Files included**

-   *Structure the information as a table, exemplified below.*

-   *Files included (outside of the "lab" directory) should be agreed upon by the Assay Team and HIVE.*

-   *When possible "file types" should include a link to an external definition, as exemplified below.*

-   *When relevant, include a link to the program or pipeline used to generate each file. The program or pipeline used should be detailed in the "pipeline or data processing" metadata section below.*

-   *If the program/pipeline will perform any QA/QC filtering of the data when generating the file, note this in the file description with additional details provided in the "Data processing pipeline" section below.*

-   *Avoid regular expressions in file names unless absolutely necessary (e.g., to denote a batch of files as in a set of fastq files).*

-   *Files containing the metadata should also be included when relevant, for example, the TSV with assay-level metadata, the antibodies TSV, a file with the pipeline parameters, etc.*

-   *THE FOLLOWING TABLE IS AN EXAMPLE AND SHOULD BE EDITED AS APPROPRIATE.*

{% include spatial_seq.md items="fastq.gz, tiff" file="directory-schema_spatialseq_v1.yaml" caption="Directory Structure" %}
{% assign tableItems = include.items | split: ", " %}
{% assign tableFileParam = {{include.file}} %}
{% assign tableFile = site.data[tableFileParam] %}

<table class="grid" style="width: 100%">
    <caption>{{include.caption}}</caption>
    <colgroup>
        <col width="20%" />
        <col width="65%" />
        <col width="15%" />
    </colgroup>
    <thead>
        <tr class="header">
            <th>Field</th>
            <th>Description</th>
            <th>Data Type</th>
        </tr>
    </thead>
    <tbody>
    {% for entry in tableItems %}
        <tr>
          <td>{{ tableFile[entry].field }}<br/>
          {% if tableFile[entry].required == true %}<span class="tableRequired">required</span>{% endif %}</td>
          <td>{{tableFile[entry]description}}
          {% if tableFile[entry].values != empty %}{{ tableFile[entry].values }}{% endif %}</td>
          <td>{{ tableFile[entry].type }}</td>
        </tr>
    {% endfor %}
    </tbody>
</table>

Note:

If the spaceranger pipeline is not utilized, there must be a GPR file specific to the Visium slide included in these outputs. This contains the specific spatial barcodes utilized for each of the capture areas on the slide, as well as their spatial coordinates. Utilizing the wrong GPR file/slide serial number can lead to rotated spatial data relative to the images, or in the worst case completely nonsensical data.

Metadata
--------

### **Sample-level**

-   *Any assay-specific considerations for the* *[sample-level metadata](https://docs.google.com/spreadsheets/d/1yqgPaVsUNpEavZOgl0bZsiTBABuVXJtq/edit#gid=233528636) should be detailed here. This is a required documentation element. To avoid any confusion, you should explicitly state if there are no assay-specific considerations. Example fields that may warrant assay-level definitions are included below.*

| **Sample field name** | **Sample type** \[block; section; suspension\] | **Definition** |
|-----------------------|------------------------------------------------|----------------|
| Thickness             | Section                                        |                |
| Processing time       |                                                |                |
| Source storage time   |                                                |                |
| Preparation protocol  |                                                |                |

### **Assay-level**

-   *This is the assay-specific metadata that's included in the assay metadata TSV files.*

-   *Please include full descriptions.*

-   *Structure the information as a table, exemplified below.*

-   *THE FOLLOWING TABLE IS AN EXAMPLE AND SHOULD BE EDITED AS APPROPRIATE.*

{% include spatial_seq.md items="Visium Assay Type, Visium Chemistry Version" file="table-schema_spatialseq_v1.yaml" caption="Metadata Structure" %}
{% assign tableItems = include.items | split: ", " %}
{% assign tableFileParam = {{include.file}} %}
{% assign tableFile = site.data[tableFileParam] %}

<table class="grid" style="width: 100%">
    <caption>{{include.caption}}</caption>
    <colgroup>
        <col width="20%" />
        <col width="65%" />
        <col width="15%" />
    </colgroup>
    <thead>
        <tr class="header">
            <th>Field</th>
            <th>Description</th>
            <th>Data Type</th>
        </tr>
    </thead>
    <tbody>
    {% for entry in tableItems %}
        <tr>
          <td>{{ tableFile[entry].field }}<br/>
          {% if tableFile[entry].required == true %}<span class="tableRequired">required</span>{% endif %}</td>
          <td>{{tableFile[entry]description}}
          {% if tableFile[entry].values != empty %}{{ tableFile[entry].values }}{% endif %}</td>
          <td>{{ tableFile[entry].type }}</td>
        </tr>
    {% endfor %}
    </tbody>
</table>

### Assay-level categorical field values

| **Field** \[from above\]          | **Values** \[semicolon separated\] |
|-----------------------------------|------------------------------------|
| Visium Assay Type                 | Visium Fresh Frozen; Visium FFPE   |
| Visium Chemistry Version          | 1.0                                |
| Visium Permeabilization Time Unit | Second; minute; hour               |
| Visium Staining Type              | H&E; Fluorescence                  |
| Capture Area ID                   | A1; B1; C1; D1                     |
| Spot Geometry                     | Rectangle; Ellipse                 |
| Spot Barcode Read                 | R1                                 |
| Library Final Yield unit          | ng; pg/uL; nM                      |

### **Antibody**

-   *~~Link to the [Antibody TSV file](https://hubmapconsortium.github.io/ingest-validation-tools/antibodies/).~~*

### **HIVE data processing pipeline**

-   ***This section is to be completed by the HIVE.***

-   *All pipeline processing steps should be detailed in the table below, including all parameter values used, as exemplified below.*

-   *A figure should be included, as relevant, to better elucidate the pipeline levels, with each level being fully described in the table.*

-   *Yes/No --- The pipeline will produce the processed files from raw without human intervention. If "No", then the required steps (human interventions) need to be detailed here.*

-   *This processing should detail any expected pre-processing of input file(s)?*

-   *The description should include what the processing step achieves.*

-   *Any manual interventions should be documented with links to publications, as relevant.*

-   *THE FOLLOWING TABLE IS AN EXAMPLE AND SHOULD BE EDITED AS APPROPRIATE.*

| **Level** | **Program** | **Version** | **Source URL**                                                                                    | **Input file**             | **Command line including all non-default parameters used** | **Description**                                                                      |
|-----------|-------------|-------------|---------------------------------------------------------------------------------------------------|----------------------------|------------------------------------------------------------|--------------------------------------------------------------------------------------|
| 2         | spaceranger | 6.1.2       | [Space Ranger](https://support.10xgenomics.com/spatial-gene-expression/software/downloads/latest) | raw/\*                     | spaceranger mkfastq                                        | 10x Genomics program to demultiplex the sequencing data, generating the fastq files. |
| 3         | spaceranger | 6.1.2       | [Space Ranger](https://support.10xgenomics.com/spatial-gene-expression/software/downloads/latest) | lab/demultiplexed/\*.fastq | spaceranger count                                          | 10x Genomics program to process Visium data, combining the spatial and genomic data. |

![](media/image2.png){width="7.5in" height="1.8194444444444444in"}

### **Lab data processing pipeline**

-   *The same details as provided in the above section ("HIVE data processing pipeline") should be detailed for each lab that uploads data that is processed independently from the HIVE.*

-   *Do not include the lab-processing details here; but rather include this lab-specific processing table of information with your data upload.*

-   *In the Files section, describe any files that include the details of the lab-processing pipeline.*

| **Level** | **Program**     | **Vers on** | **Source URL** | **Input file** | **Command line including all non-default parameters used** | **Description** |
|-----------|-----------------|-------------|----------------|----------------|------------------------------------------------------------|-----------------|
| 0         | Picard          |             |                | BCLs           |                                                            |                 |
| 1         | Slide-seq tools |             |                | BCLs           |                                                            |                 |
