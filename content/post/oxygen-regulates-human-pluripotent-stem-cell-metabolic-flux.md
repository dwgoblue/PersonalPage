+++
date = "2020-11-25T23:59:13-05:00"
title = "Oxygen Regulates Human Pluripotent Stem Cell Metabolic Flux"
draft = false
tags = ['metabolomics', 'quantbio', 'research', 'stemcell']
share = true
+++

Human pluripotent stem cells (hPSC) is assumed to well manage their resources via metabolic machinary for differentiation. In terms of energy production and consumption, oxygen plays a crucial role but is limited in the embryo. Although previous works have investigated metabolism in hPSC with 20% oxygen (atmospheric level), the physiological oxygen level was measured at about 5% which is much lower than the concentration used in the previous experimental setting. To get more percise metabolic dynamics during hPSC development, the auther compared the cells under two different oxygen levels, 5% and 20%. 

They identified PSC under 5% oxygen tends to increase glycolytic and but activate mitochondrial metabolism under 20% oxygen. Using $^{13}$C-glucose NMR-based fluxome analysis, they quantified metabolites in the glycolytic pathway, tricarboxylic acid (TCA) cycle, transhydrogenase cycle, glutamate-glutamine cycle, and generation of	glutathione (GSH), acetate, glycogen, and amino acids. Take alanine and lactate for example. The intracellular levels rose up 3-fold between 2 and 4 hr with 5% oxygen which is much higher than the cells in 20% oxygen. Besides, the metabolites related to glycolytic pathway tend to accumulate in the cells under 5% oxygen which confines enzyme activity such as 
hexokinase (HK). Only acetate, malate and TCA cycle metabolites accumulate in the cell under 20% oxygen that shows higher TCA activity in this condition. Obviously, oxygen serves as a control factor that reshapes the behavior of the metabolic network in PSC.

Glucose contributes to the production of epigenetic elements. Given that glycolytic pathway is more active at 5% oxygen, chromotin became more open with increased acetylation levels of H3K9 and H3K27 but lower methylation of H3K27. Based on the transcriptomics, higher activity of glycolytic pathway 
was driven by genes including LDHA, PGK1, and glucose transporters SLC2A1 (GLUT1) and SLC2A14 (GLUT14). Additionally, other genes were also increasing that are related to extracellular matrix organization (PCDH10, FBN1, VCAN, and POSTN), pro-apoptotic factors in response to mitochondrial damage (BNIP3), cell cycle (BTG2), early embryonic methylation patterning (BORIS), and signal transducers including hypoxia inducible factor- (HIF-) related genes (ANXA3, GDF15, IFGBP2, and IFGBP5) despite the consistent level of follistatin (FST). Only SOX2 and OCT6 slightly changed due to lower oxygen level, but most of pluripotency-related markers including OCT4, NANOG, MEIS1, OTX2, SOX11, GDF3, REX1, FGF4, DPPA2, DPPA4, and
hTERT are consistent in both conditions. Genes clustered by GO functions are listed below.

|Oxygen level | 5% oxygen | 20% oxygen |
|--------|-------------|--------|
|Upregulated genes analyzed by NetworkAnalyst|Glycolysis/gluconeogenesis<br />Focal adhesion<br />ECM-receptor interaction<br />VEGF signaling pathway<br />Osteoclast differentiation<br />Renal cell carcinoma<br />Glioma<br />Pathways in cancer<br />Pentose phosphate pathway<br />Progesterone oocyte maturation<br />Bladder cancer<br />Prostate cancer<br />Gap junction<br />GnRH signaling pathway<br />Fructose and mannose metabolism<br />MAPK signaling pathway<br />Regulation of actin cytoskeleton<br />Pyruvate metabolism|Cell cycle<br />RNA transport<br />Pyrimidine metabolism<br />p53 signaling pathway<br />mRNA surveillance pathway<br />Prostate cancer<br />Purine metabolism<br />Pathways in cancer<br />Protein processing in ER||--------|-------------|--------|
|Upregulated genes based on zero-order PPI network|Glycolysis/gluconeogenesis<br />Pentose phosphate pathway<br />Focal adhesion<br />Fructose and mannose metabolism<br />Pyruvate metabolism<br />p53 signaling pathway<br />Adherens junction<br />Chronic myeloid leukemia<br />ErbB signaling pathway|Cell cycle<br />Prostate cancer<br />HTLV-I infection<br />Bladder cancer<br />RNA transport<br />Protein processing in ER<br />Non-small cell lung cancer<br />Pancreatic cancer<br />mRNA surveillance pathway<br />Pyrimidine metabolism|

Serine and glycine increased at 5% oxygen because of the rising level of 3PG driven by PGK1. In fact, the serine/glycine-related enzymes were not regulated by oxygen that is not the reason caused the accumulation of these two amino acid. On the other hand, approximately half genes related to folate, such as MTHFR and MTHFD1L, and methionine cycles, such as MAT2A, DNMT1, and DNMT3B, decreased at 5% oxygen, but the rest of them remained unaltered. Lastly, histone methylation gene like MAT2A, AsDNMT1 and DNMT3B was downregulated but, by contrast, demethylases (KDMs) were upregulated including Lysine demethylase 7A, KDM7A, KDM6A, KDM4B, KDM3A, and KDM6B. The effects finally reflected on the reduction of H3K27me3 and SAM.

<p align="center">
<img src="/home/dawei/PersonalPage/static/images/blog/meta_oxygenlevelforhPSC.png" alt="drawing" width="300"/>
</p>
<p align="center">
<p align="center">
<img src="/home/dawei/PersonalPage/static/images/blog/meta_oxygenlevelforhPSC2.png" alt="drawing" width="300"/>
</p>

<p align="center">
<a name="figure2" />figure. Clustermap of reactions responding to different oxygen level.
</p>

# Reference
1. Lees, J. G., Cliff, T. S., Gammilonghi, A., Ryall, J. G., Dalton, S., Gardner, D. K., & Harvey, A. J. (2019). Oxygen regulates human pluripotent stem cell metabolic flux. Stem cells international, 2019.
