GENOME SIZE

methods	Fe: Feulgen microdensitometry
	FC_X: flow cytometry
	FC_PI: flow cytometry with propidium iodide
	FC_DAPI: flow cytometry with 4',6'-diamidinophenylindole
	FC_EB: flow cytometry with ethidium bromide
	FC_MI: flow cytometry with mithramycin
	FC_EBO: flow cytometry with ethidium bromide and olivomycin
	MDAPI: microdensitometry with 4',6'-diamidinophenylindole
	RK: reassociation kinetics
	Ch: Chemical extraction
	CIA: ???
	FIA: Feulgen Image Analysis Densitometry
	SCF: Static cell fluorometry
	BFA: Bulk fluorometric assay
	BCA: Biochemical analysis
	UVM: Ultraviolet microscopy
	GCD: Gallocyanin chrom alum densitometry


PLANTS
Leitch IJ, Johnston E, Pellicer J, Hidalgo O, Bennett MD. 2019. Plant DNA C-values Database (Release 7.1). https://cvalues.science.kew.org/

When a species name is not found in the database, all sinonimus listed in The Plant List were checked in the database.

Search optinos:
	Search for: All Plant C-values
	Show estimates: All estimates
	Show fields: Genus, Species, Subspecies, Chromosome number, Ploidy level, Estimation method, Prime estimate
	C-value: 1C(pg)

I choose the prime genome size estimate (i.e. the most consistent value obtained under best-practice methods, as deﬁned by Bennett MD, Smith JB. 1976. Nuclear DNA amounts in angiosperms. Philosophical Transactions of the Royal Society of London Series B: Biological Sciences, 274:227–274)
If the prime estimation is not linked to ploidy and Chromosome number, I choose the estmations with these data.


For the not found species, I repeted the search looking for C-value: 1C(Mbp) 


Search of species not found in C-value database
	Schoolar Google
	Search string:
		"Species name"+"DNA content"



ANIMALS
Gregory TR. 2021. Animal Genome Size Database. http://www.genomesize.com.

When multiple estimations are available for a given species, those with not specified (NS) method, standard species or cell type were ignored.
All, estimations with fitting method, standard species and cell type were recorded.

In birds variability in genome size is narow (see Chandler Bruce Andrews Thesis, 2009). So, when the genome size for a gigen species is not available, but it is available for some congeners I took these values to average as a proxy of the actual genome size. (only for birds). Belonging to the same genus was cheched according taxonimic nomenclature in the NCBI taxonomic database.


WHEN MORE THAN ONE VALUE IS AVAILABLE FOR ONE SPECIES
	- If there is no difference in ploidy level or chromosome number among records, c-values were averaged.
	- Records using Feulgen densitometry (Fe), flow citometry (FC_any type), DAPI microdensitometry (MDAPI), Gallocyanin chrom alum densitometry (GDC), or Fulgen image analysis densitometry (FIA) methods were prefered over other methods. So, when available, recods using these methods were choosen for averaging.
	- in birds, if the genome size was estimated from several congeners, the value for each congener was averaged previously of averageing among congeners.
	- in general, if the genome size was estimated from several subspecies, the value for each subspecies was averaged previously of averageing among them.
	- in general, but specially in plants, when a species has more than one genome size due to differences in ploidy level or chromosome number, the system was revisited looking for information about particular ploidy levels of the involved populations for each case. If no information was found, the available c-values were averaged.





setwd("/home/gorne/LUCAS/trabajo/ciencia/mis_proyectos/evol_rates_DB/")
datos <- read.csv("species_genome.csv", na.string="NA")
names <- paste(datos$species, datos$sp_ncbi, sep="_")

dup <- duplicated(names)
dup2 <- duplicated(names, fromLast=T)
dupp <- dup+dup2
duppm <- dup-dup2

datos2.1 <- datos[which(dupp==0),  c("group","taxa","species","sp_ncbi","Cvalue_1C_pg")]
datos2.2 <- datos[which(duppm==-1),c("group","taxa","species","sp_ncbi","Cvalue_1C_pg")]
datos2.2$Cvalue_1C_pg <- "REVISAR"

datos2 <- rbind(datos2.1, datos2.2)

write.csv(datos2, "species_Cval.csv")



















