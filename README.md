# cls3-final-files-description
GTF (and other) files generated from the CLS3 data:
    <li><a href="#masterTable-GTF">masterTable GTF</a></li>
    <li><a href="#chain-masterTable-GTF">chain masterTable GTF</a></li>
    <li><a href="#loci-masterTable-GTF">loci masterTable GTF</a>
    <li><a href="#enhanced-annotation">enhanced annotation</a>
    <li><a href="#gencode-v47">gencode v47</a>
    <li><a href="#v47-CLS3-Mappings">v47-CLS3 Mappings</a>
    <li><a href="#v47-CLS3-Mappings-detailed">v47-CLS3 Mappings detailed</a>
    <li><a href="#enhanced-gencode-v47">enhanced gencode v47</a>
    <li><a href="#Target-files">Target files</a>
    <li><a href="#target-liftOver-mappings-human---mouse">target liftOver mappings human - mouse</a>
    

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
  - [Human loci GTF - gencode v43 tagged](https://public-docs.crg.es/rguigo/Data/gkaur/CLS3_finalFiles/Hv3_masterTable_refined_+withinTmerge_gencodev43_tagged_lociFeatures.loci.gtf.gz)
  - [Mouse loci GTF - gencode vM16 tagged](https://public-docs.crg.es/rguigo/Data/gkaur/CLS3_finalFiles/Mv2_masterTable_refined_+withinTmerge_gencodevM16_tagged_lociFeatures.loci.gtf.gz)

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
  - [Human loci - anchTMs - gencode v27 mappings](https://public-docs.crg.es/rguigo/Data/gkaur/CLS3_finalFiles/Hv3_CLSlociToAnchsToSIDsv27)
  - [Human loci - anchTMs - gencode v43 mappings](https://public-docs.crg.es/rguigo/Data/gkaur/CLS3_finalFiles/Hv3_CLSlociToAnchsToSIDsv43)
  - [Mouse loci - anchTMs - gencode vM16 mappings](https://public-docs.crg.es/rguigo/Data/gkaur/CLS3_finalFiles/Mv2_CLSlociToAnchsToSIDsvM16)

The final loci master tables have the following artifact types included, in addition to the genuine models: polyASJdisag, recountSlt50, spliceSiteMisalign, tRepeatOverlap.

## enhanced annotation

**_Please use only after completely understanding the generation process. This is the genocde "reference" annotation enhanced with the refined novel "intergenic" CLS loci built from ONLY the spliced, refined (additional removal of the polyASJdisag artifacts) anchTMs and might harbour read-throughs; this is not the final gencode annotation_**

The aim of generating this annotation was to enhance the existing reference gencode annotations with only the reliable **intergenic** CLS3 transcripts/loci (i.e., spliced transcripts, tagged as "no", "recountSlt50", "spliceSiteMisalign", "tRepeatOverlap" for the attributes tag)

The enhanced annotation GTFs can be downloaded using the following links. 
  - [Human gencode v27 enhanced annotation](https://public-docs.crg.es/rguigo/Data/gkaur/CLS3_finalFiles/Hv3_enhancedCLS3_refined_+gencodev27.loci.refmerged.gff.gz)
  - [Human gencode v43 enhanced annotation](https://public-docs.crg.es/rguigo/Data/gkaur/CLS3_finalFiles/Hv3_enhancedCLS3_refined_+gencodev43.loci.refmerged.gff.gz)
  - [Mouse gencode vM16 enhanced annotation](https://public-docs.crg.es/rguigo/Data/gkaur/CLS3_finalFiles/Mv2_enhancedCLS3_refined_+gencodevM16.loci.refmerged.gff.gz)

The CLS loci within these files are different from the "loci master table GTF" loci, and have been named as CLS3i:LOC_xxxxxxxxxxxx.

## gencode v47

This is the latest, yet to be released gencode annotation, improved w.r.t. the v46 through the addition of gencode havana team approved CLS3 lncRNAs.
Since these files will be public only with the next release of gencode, for now the access to these files is limited. Please reach out in case you require access.

Links for downloading the gencode annotations:
  - [Human v47](https://public-docs.crg.es/rguigo/Data/gkaur/CLS3_finalFiles/gencodev47Files/gencode.v47.primary_assembly.annotation.gtf.gz)
  - [Mouse v36](https://public-docs.crg.es/rguigo/Data/gkaur/CLS3_finalFiles/gencodev47Files/gencode.vM36.primary_assembly.annotation.gtf.gz)

## v47-CLS3 Mappings

  - [v47-CLS3mappings](https://public-docs.crg.es/rguigo/Data/gkaur/CLS3_finalFiles/MAP_extensive_v47-CLS3_v2_labelled)

The mapping across v47 ENSTs and the CLS3 anchICs they were extended/created from. These are mostly lncRNAs, and ~300 protein coding transcripts.

The file has additional tags, "CLS3_anchIC_gffComparev27" for the status of the respective anchIC(s) w.r.t. gencode v27 annotation. "v47-CLS3_mappingTag" states the mapping strategy used, internal details as follows:
1. **direct_anchICUC_mapping.** (147774 ENSTs):<br />
   anchIC or anchUC were used for creating/extending the v47 ENSTs -> direct mapping to current ICtable using the anchIC/anchUC.
   
2. **oldmTanchTM_mapping.** (174 ENSTs):<br />
   older version of anchTMs were used for creating/extending the v47 ENSTs -> mapping to older version of anchTMs.
   
3. **readID(old)-anchIC(new)_mapping.** (638 ENSTs):<br />
   older unsplit reads were used for creating/extending the v47 ENSTs -> mapped corresponding new split readID-lid-anchTM-anchIC as old and new readIDs refer to same read. Therefore, mapping old reads to current ICtable.<br />
   Some (488 ENSTs) still not found, tagged "UNMAPPED" in the "CLS3_anchIC" and "CLS3_anchIC_gffComparev27" columns. Most probably these reads were not used by LyRic to build TMs.
   
4. **LID-anchIC_mapping.** (3032 ENSTs):<br />
   LIDs (current version) used for creating/extending the v47 ENSTs -> LIDs mapped to anchICs. 
Some may not be mapped: are compmerge, alignID, etc.; correspond to old CLS or other datasets.
In such cases, "CLS3_anchIC" and "CLS3_anchIC_gffComparev27" column has the value UNMAPPED. The LIDs used to create/extend an ENST could be UNMAPPED (1577), or some could be mapped as well.
<br />
lid: LyRic TM ID<br />
rid: read ID

## v47-CLS3 Mappings detailed

  - [v47-CLS3mappings DETAILED](https://public-docs.crg.es/rguigo/Data/gkaur/CLS3_finalFiles/v47-CLS3mapping_status.txt)

The mapping across v47 ENSTs and the CLS3 anchICs they were extended/created from, with added details like novelty at the transcript as well as gene level. 

For each transcript (ENST) created/extended in v47 due to CLS3 (anchICs), the file lists: <br />
||||
|-|-|-|
**geneID_v47** | v47 gene (ENSG) that the transcript belongs to <br />
**transcriptID_v47** | v47 transcript ID (ENST) <br />
**created/extended** | tag specifying whether the transcript was created or extended using TAGENE/manually <br />
**CLS3_anchIC** | CLS3 anchIC(s) that led to the addition of the transcript to v47 <br />
**CLS3_anchIC_gffComparev27** | gffcompare classification for the anchIC(s) w.r.t. v27 (reference annotation) <br />
**v47-CLS3_mappingTag** | states the mapping strategy used; details in the above section <br />
**v47_biotype** | v47 biotype <br />
**transcriptClassification** | transcript (ENST) novelty status taking into account the different gffcompare classifications from all the underlying anchICs <br />
**geneClassification** | gene (ENSG) novelty status taking into account the different gffcompare classifications from all the underlying transcripts <br />

The gffcompare novelty status definitions w.r.t. v27 for the anchICs, ENSTs and ENSGs:

<img width="868" alt="image" src="https://github.com/user-attachments/assets/cbf3bf78-60fd-4ae2-9e19-9b97b8d7b652">

<br />
<br />

## enhanced gencode v47

The gencode v47 annotation was further enhanced by adding just the **most reliable "intergenic"** transcript loci (i.e., spliced transcripts, tagged as "no" or "recountSlt50" for the attributes tag). This was done specifically for the purpose of RNA-Seq analysis studies requantifications, adding some transcripts/loci that have been not added to the gencode annotation yet due to stringent filters or because the transcripts still need to be reviewed for addition to gencode.

The latest gencode enhanced annotations can be downloaded here:
  - [Human v47 enhanced annotation](https://public-docs.crg.es/rguigo/Data/gkaur/CLS3_finalFiles/gencodev47Files/gencode.v47.primary_assembly.annotation.enhanced.gtf)
    
## Target files

**Merged targets** (used for most of the analysis and for probe designing as well):
- [human targets GTF](https://public-docs.crg.es/rguigo/Data/gkaur/CLS3_finalFiles/hs.allNonPcgTargetsMerged.targets.gt)
- [mouse targets GTF](https://public-docs.crg.es/rguigo/Data/gkaur/CLS3_finalFiles/mm.allNonPcgTargetsMerged.targets.gtf)
  

**Exon-level unmerged targets**:
- [human targets GTF unmerged](https://public-docs.crg.es/rguigo/Data/gkaur/CLS3_finalFiles/Hv3_primary_targets.exons.reduced.gene_type.segments.gtf)
- [mouse targets GTF unmerged](https://public-docs.crg.es/rguigo/Data/gkaur/CLS3_finalFiles/Mv2_primary_targets.exons.reduced.gene_type.segments.gtf)

## target liftOver mappings human - mouse

The human-mouse mapping for the targets that were lifted over from human to mouse originally for the target design, upto the exon level as well. Mappings for all the liftedOver targets can be found here:
  - [liftedOverTargets mapping](https://public-docs.crg.es/rguigo/Data/gkaur/CLS3_finalFiles/liftedOverTargets.mapping.txt
)

This is a tab separated file, with the targetID (same for different exons of the same target element), targetID_human (with hg38 coordinates) and the corresponding targetID_mouse (with mm10 coordinates).
<br />

For the target design, catalogs (8 catalogs - CMfinderCRSs, GWAScatalog, UCE, VISTAenhancers, fantomCat, fantomEnhancers, bigTranscriptome, miTranscriptome) were liftedOver from human to mouse. For designing targets, the features were extended 100bp in both directions in case a feature is <=200bp. The human and mouse IDs in the above file are the final ones (bed format coordinates included in the ID), as have been used in the masterTables and elsewhere as well.
<br />

The file shared above has all the features that were liftedOver from human to mouse. 
To access only the ones selected for the final targetDesign in mouse, please use this file:
- [final liftedOverTargets mapping](https://public-docs.crg.es/rguigo/Data/gkaur/CLS3_finalFiles/final.liftedOverTargets.mapping.txt)

