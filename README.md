# GeneSet-Enrichment-Analysis-using-gprofiler2
GSEA using gprofiler2
setwd("/Users/ogunbawoadebisi/Downloads/meta_analyse")
#install.packages("gprofiler2")
library(gprofiler2)

genes.modules <- read.table("Geneid_ra.csv",h = TRUE, sep = "\t", stringsAsFactors = FALSE)
gostres <- gost(query = genes.modules$gene_id, 
                organism = "btaurus", #Organism names are constructed by concatenating the first letter of the name and the family name. Example: human - 'hsapiens', mouse - 'mmusculus'.
                ordered_query = FALSE, #in case input gene lists are ranked this option may be used to get GSEA style p-values
                multi_query = FALSE, #in case of multiple gene lists, returns comparison table of these lists
                significant = TRUE, #whether all or only statistically significant results should be returned
                exclude_iea = FALSE, #exclude GO electronic annotations (IEA)
                measure_underrepresentation = FALSE, #measure underrepresentation
                evcodes = FALSE, #include evidence codes to the results. 
                user_threshold = 0.05, #custom p-value threshold for significance, results with smaller p-value are tagged as significant. We don't recommend to set it higher than 0.05
                correction_method = "fdr", #the algorithm used for multiple testing correction, one of "gSCS" (synonyms: "analytical", "g_SCS"), "fdr" (synonyms: "false_discovery_rate"), "bonferroni"
                domain_scope = "annotated", #how to define statistical domain, one of "annotated", "known", "custom" or "custom_annotated"
                custom_bg = NULL, #vector of gene names to use as a statistical background. If given, the domain_scope is by default set to "custom", if domain_scope is set to "custom_annotated", then this is used instead
                numeric_ns = "", #namespace to use for fully numeric IDs
                sources = NULL, #a vector of data sources to use. Currently, these include GO (GO:BP, GO:MF, GO:CC to select a particular GO branch), KEGG, REAC, TF, MIRNA, CORUM, HP, HPA, WP.
                as_short_link = FALSE, #indicator to return results as short-link to the g:Profiler web too
                highlight = TRUE) #indicator to return a TRUE-FALSE column called 'highlighted' to indicate driver terms in GO

#OR 
geneList <-read_xlsx("Prioritised gene.xlsx")
gostres <- gost(query = geneList$GeneId, 
                organism = "hsapiens", #Organism names are constructed by concatenating the first letter of the name and the family name. Example: human - 'hsapiens', mouse - 'mmusculus'.
                ordered_query = FALSE, #in case input gene lists are ranked this option may be used to get GSEA style p-values
                multi_query = FALSE, #in case of multiple gene lists, returns comparison table of these lists
                significant = TRUE, #whether all or only statistically significant results should be returned
                exclude_iea = FALSE, #exclude GO electronic annotations (IEA)
                measure_underrepresentation = FALSE, #measure underrepresentation
                evcodes = FALSE, #include evidence codes to the results. 
                user_threshold = 0.05, #custom p-value threshold for significance, results with smaller p-value are tagged as significant. We don't recommend to set it higher than 0.05
                correction_method = "fdr", #the algorithm used for multiple testing correction, one of "gSCS" (synonyms: "analytical", "g_SCS"), "fdr" (synonyms: "false_discovery_rate"), "bonferroni"
                domain_scope = "annotated", #how to define statistical domain, one of "annotated", "known", "custom" or "custom_annotated"
                custom_bg = NULL, #vector of gene names to use as a statistical background. If given, the domain_scope is by default set to "custom", if domain_scope is set to "custom_annotated", then this is used instead
                numeric_ns = "", #namespace to use for fully numeric IDs
                sources = NULL, #a vector of data sources to use. Currently, these include GO (GO:BP, GO:MF, GO:CC to select a particular GO branch), KEGG, REAC, TF, MIRNA, CORUM, HP, HPA, WP.
                as_short_link = FALSE, #indicator to return results as short-link to the g:Profiler web too
                highlight = TRUE) #indicator to return a TRUE-FALSE column called 'highlighted' to indicate driver terms in GO



onto_gen_test <- as.data.frame(gostres$result)

write.xlsx(onto_gen,"onto_gen.xlsx")
