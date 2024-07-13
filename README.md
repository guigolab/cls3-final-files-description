# cls3-final-files-description
GTF files generated from the CLS3 data:
    <li><a href="#masterTable GTF">masterTable GTF</a></li>
    <li><a href="#intronChain masterTable GTF">intronChain masterTable GTF</a></li>
    <li><a href="#loci table">loci table</a>

## masterTable GTF
   Human: [https://github.com/guigolab/gencode-cls-master-table/releases/download/GencodeCLS_v3.0/Hv3_splicedmasterTable_refined.gtf.gz](https://github.com/guigolab/gencode-cls-master-table/releases/download/GencodeCLS_v3.0/Hv3_masterTable_refined.gtf.gz)
   Mouse: https://github.com/guigolab/gencode-cls-master-table/releases/tag/GencodeCLS_v3.0#:~:text=Mv2_masterTable_refined.gtf.gz
   
   This is the main GTF file generated from the CLS3 dataset after merging the transcripts obtained across all the tissues/samples.
   The CLS3 long-read data was processed through LyRic to obtaing high-confidence transcript models per sample through both pacBioSII and ONT technologies.

   Further, to obtain an annotation for all the transcripts obtained through the different tissues and technologies, the transcripts across samples were "anchored" merged together. Meaning the transcript ends with orthologonal data support were preserved so as to not merge to other transcripts. This reducued the redundancy in the dataset while also preserving the supported transcript ends.

![image](https://github.com/user-attachments/assets/bf9e231f-3592-4873-84b3-427395f8a568)

Following is the snapshot from this GTF:
![image](https://github.com/user-attachments/assets/6982a73e-cbce-4650-88bc-7f0cdfbe6c27)

   


3. masterTable "intronChain" GTF
4. loci GTF
5. enhanced annotation GTF
6. EBI final annotation for the paper
   
