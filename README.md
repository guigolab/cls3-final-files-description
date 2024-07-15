# cls3-final-files-description
GTF files generated from the CLS3 data:
    <li><a href="#masterTable-GTF">masterTable GTF</a></li>
    <li><a href="#chain-masterTable-GTF">chain masterTable GTF</a></li>
    <li><a href="#loci-masterTable-GTF">loci masterTable GTF</a>
    <li><a href="#enhanced-annotation">enhanced annotation</a>
    <li><a href="#gencode-v47">gencode v47</a>

## masterTable GTF
The master table GTF for human and mouse can be downloaded using the following links:
  - [Human master table GTF](https://github.com/guigolab/gencode-cls-master-table/releases/download/GencodeCLS_v3.0/Hv3_masterTable_refined.gtf.gz)
  - [Mouse master table GTF](https://github.com/guigolab/gencode-cls-master-table/releases/download/GencodeCLS_v3.0/Mv2_masterTable_refined.gtf.gz)
   
   This is the main GTF file generated from the CLS3 dataset after merging the transcripts obtained across all the tissues/samples.
   
   The CLS3 long-read data is processed through LyRic to obtaing high-confidence transcript models per sample through both pacBioSII and ONT technologies.
   Further, to obtain a "master" annotation for all the transcripts obtained through the different tissues and technologies, the transcripts across samples were "anchored" merged together. Meaning the transcript ends with orthologonal data support were preserved so as to not merge to other transcripts. This reducued the redundancy in the dataset while also preserving the supported transcript ends. The supported transcript ends were anchored using the script [anchorTranscriptsEnds.pl](https://github.com/guigolab/LyRic/blob/master/utils/anchorTranscriptsEnds.pl), followed by transcript merging using [tmerge](https://github.com/guigolab/tmerge).

![image](https://github.com/user-attachments/assets/bf9e231f-3592-4873-84b3-427395f8a568)

Following is a snapshot from the master table GTF:
![image](https://github.com/user-attachments/assets/6982a73e-cbce-4650-88bc-7f0cdfbe6c27)

The attribute tags description can be found here on the main [gencode-cls-master-table github page](https://github.com/guigolab/gencode-cls-master-table?tab=readme-ov-file#attributes-specifics). _gene_id_ and _transcript_id_ both specify the anchored merged transcript identifier in the format anchTMxxxxxxxxxxxx.

The final refined master table has the following artifact models included, in addition to the genuine models: polyASJdisag, recountSlt50, spliceSiteMisalign, tRepeatOverlap.

For additional end support data, we used [proCapNet](https://github.com/kundajelab/ProCapNet) predictions for supporting the human CLS3 TSSs. A proCapNet score of moreThanEqualTo5 (MTE5) within 100bp window of a TSS in any of the proCap datasets is taken as a positive support.
The anchTMs with proCapNet supported TSSs can be found here:
   - [Human - proCapNet supported anchTMs](https://public-docs.crg.es/rguigo/Data/gkaur/CLS3_finalFiles/proCapSupported_anchTMs.list)
 
 ## chain masterTable GTF
 The chain GTF for human and mouse can be downloaded using the following links:
   - [Human chain GTF - spliced](https://github.com/guigolab/gencode-cls-master-table/releases/download/GencodeCLS_v3.0/Hv3_splicedmasterTable_refined.gtf.gz)
   - [Human chain GTF - monoexonic](https://github.com/guigolab/gencode-cls-master-table/releases/download/GencodeCLS_v3.0/Hv3_unsplicedmasterTable_refined.gtf.gz)
   - [Mouse chain GTF - spliced](https://github.com/guigolab/gencode-cls-master-table/releases/download/GencodeCLS_v3.0/Mv2_splicedmasterTable_refined.gtf.gz)
   - [Mouse chain GTF - monoexonic](https://github.com/guigolab/gencode-cls-master-table/releases/download/GencodeCLS_v3.0/Mv2_unsplicedmasterTable_refined.gtf.gz)
  
 This GTF was created from the main master table to further reduce the transcript redundancy, while preserving the master table transcript identifiers (anchTMxxxxxxxxxxxx) in the attributes. 

 Different strategies were followed for the spliced and monoexonic transcripts.
 1. For the _spliced transcripts_, those with identical intron chains were merged into a single intron chain (anchICxxxxxxxxxxxx), irrespective of the end support.
 2. While for the _monoexonic transcripts_, those with 50% overlap with each other were merged together into a single chain (anchUCxxxxxxxxxxxx), again irrespective of the end support.

![image](https://github.com/user-attachments/assets/9f89b11a-c6eb-4c3a-8d2d-4490d3d229fb)

A snapshot from the "intron" chain master table GTF:
![image](https://github.com/user-attachments/assets/62b8e864-93c9-4f1f-9dd4-3cd8c04bef93)

_gene_id_ and _transcript_id_ both specify the merged chain identifier in the format anchICxxxxxxxxxxxx for the spliced transcripts, while anchUCxxxxxxxxxxxx for the monoexonic transcripts. 

In addition to the master table attributes (_target_, _spliced_, _sampleN_, _samplesMetadata_, _expression_, _artifact_), a new attribute _contained_anchTMs_, is also present which specifies the anchTMs contaiined within each chain. 

For the [master table GTF attributes](https://github.com/guigolab/gencode-cls-master-table?tab=readme-ov-file#attributes-specifics), the definition remains the same, while these attributes now specify the respective tags for all the anchTMs contained within the respective chain. 

An exception is the _endSupport_ attribute, wherein the highest support available from the contained anchTMs is selected for the respective chain.
While for the _refCompare_ and _currentCompare_ attributes, the status of the merged chain against the specific Gencode reference annotations is recalculated (using GffCompare) and specified.

The final refined "chain" master tables have the following artifact types included, in addition to the genuine models: polyASJdisag, recountSlt50, spliceSiteMisalign, tRepeatOverlap.

## loci masterTable GTF

**_Please use only after completely understanding the generation process. This is an annotation with all the refined CLS loci and might harbour read-throughs; this is not the final gencode annotation, but useful for analysis pertaining to all the obtained CLS3 loci_**

The loci GTFs can be downloaded using the following links. 
  - [Human loci GTF - gencode v27 tagged](https://public-docs.crg.es/rguigo/Data/gkaur/CLS3_finalFiles/Hv3_masterTable_refined_+withinTmerge_gencodev27_tagged_lociFeatures.loci.gtf.gz)
  - [Human loci GTF - gencode v43 tagged]()
  - [Mouse loci GTF - gencode vM16 tagged]()

The loci information remains the same across different gencode reference versions, the only difference is the gencode overlap attributes.
For this loci level GTF, the transcripts are clustered at locus level. 
This is done by first reducing the redundancy by merging the anchTMs using tmerge. Further, the transcripts with any overlap on the same strand (bedtools intersect) are clustered into a single locus.

![image](https://github.com/user-attachments/assets/7e63329e-33f1-4496-9013-c93c728f7ca7)

A snapshot from the loci master table GTF:
![image](https://github.com/user-attachments/assets/b65372d1-247c-4e32-88c7-2e793f610166)

The loci GTF has gene, transcript and exon features. 
_gene_id_ specifies the CLS3 locus ID (CLS3:LOC_xxxxxxxxxxxx) while _transcript_id_ specifies the merged transcript ID (TM_xxxxxxxxxxxx).

Each exon has the transcript level attributes obtained through tmerge, description [here](https://github.com/guigolab/tmerge?tab=readme-ov-file#output).

Further, additional attributes _overlapping_gencode_gene_, _overlapping_gencode_transcript_ have been added that specify the transcript overlap with gencode genes and transcripts at the exonic level. While _gLlevel_gencodeGeneOverlaps_ specifies the locus overlap with gencode genes at the exonic level. 

Each locus can be linked to the underlying anchTMs using the _contains_ attribute tag accesed through the exon records for each transcript (TM_xxxxxxxxxxxx), thus linking the main master table GTF to this loci GTF.

Further, we have created a mapping file for the master table GTF (anchTMs) and the loci GTF. For each locus, there exists the following mapping information:
    "CLSgeneLoci - anchTMs - samples - gencode v27 exonic overlaps"

These can be found here:
  - [Human loci - anchTMs - gencode v27 mappings]()
  - [Human loci - anchTMs - gencode v43 mappings]()
  - [Human loci - anchTMs - gencode vM16 mappings]()

The final loci master tables have the following artifact types included, in addition to the genuine models: polyASJdisag, recountSlt50, spliceSiteMisalign, tRepeatOverlap.

## enhanced annotation

**_Please use only after completely understanding the generation process. This is the genocde "reference" annotation enhanced with the refined novel "intergenic" CLS loci built from ONLY the spliced, refined (additional removal of the polyASJdisag artifacts) and might harbour read-throughs; this is not the final gencode annotation_**

## gencode v47
