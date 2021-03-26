# GapJumper
Flexible pipeline for integration and uncertainty estimation of variant calling data generated from multiple samples, replicates and software results.

![project presentation slide](Summary/00_SimpleAI_project.png)

##  GAPJUMPER APLICATIONS
* identification of reliable genetic markers in large and heterogenous datasets
* quality evaluation of variants detected in different samples, sample sets or replicates
* evaluation of results obtained with other methods, such as genetic markers selected with large screening studies,
* benchmarking, and SNV calling piepline development,  
* non-regression tests for sequencing and genotyping pielines,  
  
---
## HOW IT WORKS?
GapJumper, is an open source pipeline (GNU License) that allows integration and analysis of variant calling data obtained from multiple replicates, samples and softwares (see figure below). It allows estimation of uncertainty associated with each nucleotide in integrated data, without making assumption on the ploidy or the level of genetic heterogeneity in each sample and replicate. The evidence scores assigned to each nucleotide reflects the error rate, the amount of missing data, and the reproducibility of the results in empirical data only. 

## MAIN PROBLEM THE GAPJUMPER IS SOLVING     
  
* __THE PROBLEM__  
Different replicates, samples, pooled DNA samples or softwares applied to the same samples, may generate large number of positions wiht different variant composition (ag A , and AT), despite they are assumed to be identical. Thus, the classical methods for data filtering may generate, so called __FALSE POSITIVE LEACKAGE__, where missing data at some samples, or true alleles removed as potential errors, may generate false differences between compared datasets. 
   
* __WHERE IT CAN BE FOUND__   
False positive leackage, becomes large problem when compared samples have different levels of genetic heterogenity, or they are genetically homogenous, such as clonal lines of cancer, or genetically identical twins. In that case, sequence errors and missing data may generate more results then researched genetic processes, and the classical filtering becomes ineffective, because it may remove to many postions of interest, or do not provide the answer which of the postions are more likely to be true genetic variants.
   
* __PROPOSED SOLUTION__  
GapJumper allows conserving all postions and variants detected with any method in any replicates or sdamples, and instead of removing them, it calulated uncertainty assocoated with each viariant and postions that can be used to remove potential errors, select best quality genetic markers, or to evaluate results provided with other pipelines. The evidence score may be used to a single genetic varinat, positon in a genome or sets of postions, such as chromosome, or scaffold. 
  
![project presentation slide](Summary/01_Basic_function.jpeg)

## METHODS IMPLEMENTED IN GAPJUMPER
GapJumper uses __vcf files__ generated wiht any variant caller as input (a) and generates similar files in output, with aditional fileds for evidence scores for each nucleotide and postion (see GapJumper manual). __Four threshold based approaches__ for data integration were implemented in GapJumper, that are commonly used in literature __(b)__. Additonally, I developed and valiadated __two DST-based apraches based on semisupervised machine learning algorithsm__ that are unique to GapJumper. These two methods allow calulating evidence scores for each nucleotide in integrated or compared datasets __(c and d)__. DST-based approaches are especially usefull, for large and heteroguenous datasets or datasets with large amount of missing information that are often found in screening studies using lower coverage sequencing or reduced representaiton sequencing such as RADseq. DST-based approaches can be used independently for data integration or in combinations with any of the of classicial methods (b)
  
Gapjumper pipeline allows for generating consensus with all methods simulatanously (b-c) or to provide evidence scores caulated with any DST-based approache, while filtering variants using tuned classical methods (b). Additionaly, the Gapjumper allows performing __sample comparisons__ with classicial methods or DST-based approach, that also provides __evidence scores (joined probabilities) for individual variants and positons in compared samples or sample sets__. These scores allow identifying reliable genetic martkers, or to remove potential errors, and low quality positions, without removing relevant infomation on the filtering steps prior to sample comparison.  

![project presentation slide](Summary/02_Utilities.png)

## EXAMPLE FROM GAPJUMPER EVALUATION STUDIES WITH OPEN ACCESS DATA

The performance of GapJumper was evaluated using publically available variant calling dataset obtained with restriction site associated DNA markers sequencing approach (RAD-seq). RADseq is sequencing approach that is rutinelly used for screening of large sample numbers, and development of genetic markers at low cost. It is relatively inexpensive method that allows generating hundreds of thousands of genetic markers for each sample, but it also generates data with large amount of missing information, and variable coverage.

### DATA TREATMENT 
For this study, I used 3 technical replicates sequenced independently, that ideally, shodul generate identicall variant calling results irrespectively on the appraoch. The replicates were genotyped with three different approaches (Freebayes, GATK, and pooled samples in GATK), and compared to each other revaling that alsmot 30000 genetic varints, out of 52000 detected, were found in only one replicate-appraoch combination, and were missing results form any other replciate-approach comabination. It means that up to 68% of variants would have to be removed, using classical methods. Furthermore, The same would be applied to other samples that we could compare wiht the sample used in this study, and gradually reduce the number of compared genetic varinats to zero in large datasets. For these reaosn, I used GapJumper to integrate the results from all replicate-aproach combinations, and I used the evidence scores to evaluate quality postions, in the consensus.

### RESULTS AND DISCUSSION   
Boxplots on Figure b shows evidence scores calulated for variant calling results obtained with three different replicates sequenced and genotyped independently with three different methods (a). Over 68% of the postions had either missing data or different nucletide compostion, depiste stringent filtering and quality controls, used with each applied method. Thus, to avoid removind these postions, and by that generaitng potential fasle positives by comparing samples with postions having incomplete data, I used DST-based appraoch to generate the consensus. Subsequently, boxplots on Figure b shows the evidence scores of variants that were detected in any combination of replicates and methods used for variant detection, with the most confident variants detected with all positons and replicates (evidence scores ~1). The figure also shows, that some combinations or replicates and approaches may generate better quality variants, but it depends on the postions and its context that is being individually and in the context of the sample. For example, higher coverage, or more consistent data in the sample, are evaluated with cross-validation step on each postions in each repliate in GapJumper piepline. This in return, provides higher evidence scores to variants detected in replicates that are best representation of the dataset, and lower evidence scores to variants detected in replicates that have large amoutn on noise data.

![project presentation slide](Summary/Evaluation_Slide2.png)

## LINKS
GapJumepr V01   


![project presentation slide](Summary/manual_png/01.png)
![project presentation slide](Summary/manual_png/02.png)
![project presentation slide](Summary/manual_png/03.png)
![project presentation slide](Summary/manual_png/04.png)
![project presentation slide](Summary/manual_png/05.png)
![project presentation slide](Summary/manual_png/06.png)
![project presentation slide](Summary/manual_png/07.png)
![project presentation slide](Summary/manual_png/08.png)
![project presentation slide](Summary/manual_png/09.png)
![project presentation slide](Summary/manual_png/10.png)

![project presentation slide](Summary/manual_png/11.png)
![project presentation slide](Summary/manual_png/12.png)
![project presentation slide](Summary/manual_png/13.png)
![project presentation slide](Summary/manual_png/14.png)
![project presentation slide](Summary/manual_png/15.png)
![project presentation slide](Summary/manual_png/16.png)
![project presentation slide](Summary/manual_png/17.png)
![project presentation slide](Summary/manual_png/18.png)
![project presentation slide](Summary/manual_png/19.png)
![project presentation slide](Summary/manual_png/20.png)

![project presentation slide](Summary/manual_png/21.png)
![project presentation slide](Summary/manual_png/22.png)
![project presentation slide](Summary/manual_png/23.png)
![project presentation slide](Summary/manual_png/24.png)
![project presentation slide](Summary/manual_png/25.png)
![project presentation slide](Summary/manual_png/26.png)
![project presentation slide](Summary/manual_png/27.png)
![project presentation slide](Summary/manual_png/28.png)
![project presentation slide](Summary/manual_png/29.png)
![project presentation slide](Summary/manual_png/30.png)

![project presentation slide](Summary/manual_png/31.png)
![project presentation slide](Summary/manual_png/32.png)
![project presentation slide](Summary/manual_png/33.png)






