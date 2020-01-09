FROM flowcraft/bowtie2_samtools:1.0.0-1

WORKDIR /index_dengue

RUN wget ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/871/845/GCA_000871845.1_ViralProj20183/GCA_000871845.1_ViralProj20183_genomic.fna.gz
RUN wget ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/862/125/GCA_000862125.1_ViralProj15306/GCA_000862125.1_ViralProj15306_genomic.fna.gz
RUN wget ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/865/065/GCA_000865065.1_ViralProj15599/GCA_000865065.1_ViralProj15599_genomic.fna.gz
RUN wget ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/866/625/GCA_000866625.1_ViralProj15598/GCA_000866625.1_ViralProj15598_genomic.fna.gz

RUN gunzip *.fna.gz

RUN bowtie2-build GCA_000871845.1_ViralProj20183_genomic.fna,GCA_000862125.1_ViralProj15306_genomic.fna,GCA_000865065.1_ViralProj15599_genomic.fna,GCA_000866625.1_ViralProj15598_genomic.fna dengue

RUN rm *.fna

ENV PATH="/index_dengue:$PATH"

WORKDIR /data