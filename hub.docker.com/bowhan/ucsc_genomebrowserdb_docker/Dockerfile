# This is built on the top of Meng Wang's https://hub.docker.com/r/icebert/ucsc_genome_browser_db/
FROM icebert/ucsc_genome_browser_db:latest
MAINTAINER Bo Han <bowhan@me.com>
LABEL Description="UCSC Genome Browser database"

ARG Genomes="hg38 mm10 rn6 macFas5 dm6"
ARG Tables="grp trackDb gold gap hgFindSpec chromInfo cytoBandIdeo bigFiles refGene"

RUN chown -R mysql /var/run/mysqld

RUN /bin/bash -c "/usr/bin/mysqld_safe &" && \
    sleep 5 && \
    for genome in $Genomes; do mysql -u root -e "CREATE DATABASE IF NOT EXISTS $genome"; done

RUN for genome in ${Genomes}; do \
        for table in ${Tables}; do \
               rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/${genome}/${table}.MYD /data/${genome} \
            && rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/${genome}/${table}.MYI /data/${genome} \
            && rsync -avzP  rsync://hgdownload.cse.ucsc.edu/mysql/${genome}/${table}.frm /data/${genome} \
            && chown -R mysql:mysql /data/${genome}; \
        done \
    done

EXPOSE 3306

CMD ["mysqld", "-u", "root"]