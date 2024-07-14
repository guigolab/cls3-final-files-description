# cls3-final-files-description
GTF files generated from the CLS3 data:
    <li><a href="#masterTable GTF">masterTable GTF</a></li>
    <li><a href="#intronChain masterTable GTF">intronChain masterTable GTF</a></li>
    <li><a href="#loci table">loci table</a>

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

 ## intronChain masterTable GTF
 This GTF was created from the main master table to further reduce the transcript redundancy, while preserving the master table transcript identifiers (anchTMxxxxxxxxxxxx) in the attributes. 

 Different strategies were followed for the spliced and monoexonic transcripts.
 1. For the _spliced transcripts_, those with identical intron chains were merged into a single intron chain (anchICxxxxxxxxxxxx), irrespective of the end support.
 2. While for the _monoexonic transcripts_, those with 50% overlap with each other were merged together into a single chain (anchUCxxxxxxxxxxxx), again irrespective of the end support.

![image](https://github.com/user-attachments/assets/2bda1d64-f30d-4667-b8dc-d9c882963b5c)

A snapshot from the "intron" chain master table GTF:
![image](https://github.com/user-attachments/assets/62b8e864-93c9-4f1f-9dd4-3cd8c04bef93)

_gene_id_ and _transcript_id_ both specify the merged chain identifier in the format anchICxxxxxxxxxxxx for the spliced transcripts, while anchUCxxxxxxxxxxxx for the monoexonic transcripts. 
In addition to the master table attributes (_target_, _spliced_, _sampleN_, _samplesMetadata_, _expression_, _artifact_), a new attribute _contained_anchTMs_, is also present which specifies the anchTMs contaiined within each chain. 
For the [master table GTF attributes](https://github.com/guigolab/gencode-cls-master-table?tab=readme-ov-file#attributes-specifics), the definition remains the same, while these attributes now specify the respective tags for all the anchTMs contained within the respective chain. 
An exception is the _endSupport_ attribute, wherein the highest support available from the conained anchTMs is selected for the respective chain.
While for the _refCompare_ and _currentCompare_ attributes, the status of the merged chain against the specific Gencode reference annotations is recalculated and specified.




4. masterTable "intronChain" GTF
5. loci GTF
6. enhanced annotation GTF
7. EBI final annotation for the paper
   
