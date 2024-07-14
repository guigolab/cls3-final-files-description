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
   Further, to obtain an annotation for all the transcripts obtained through the different tissues and technologies, the transcripts across samples were "anchored" merged together. Meaning the transcript ends with orthologonal data support were preserved so as to not merge to other transcripts. This reducued the redundancy in the dataset while also preserving the supported transcript ends. The supported transcript ends were anchored using the script [anchorTranscriptsEnds.pl](https://github.com/guigolab/LyRic/blob/master/utils/anchorTranscriptsEnds.pl), followed by transcript merging using [tmerge](https://github.com/guigolab/tmerge).

![image](https://github.com/user-attachments/assets/bf9e231f-3592-4873-84b3-427395f8a568)

Following is a snapshot from the master table GTF:
![image](https://github.com/user-attachments/assets/6982a73e-cbce-4650-88bc-7f0cdfbe6c27)

The attribute tags description can be found here on the main [gencode-cls-master-table github page](https://github.com/guigolab/gencode-cls-master-table?tab=readme-ov-file#attributes-specifics)

   


3. masterTable "intronChain" GTF
4. loci GTF
5. enhanced annotation GTF
6. EBI final annotation for the paper
   
