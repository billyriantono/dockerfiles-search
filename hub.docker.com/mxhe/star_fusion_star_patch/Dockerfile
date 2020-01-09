FROM trinityctat/starfusion:1.7.0

# add STAR from STAR biocontainer
COPY --from=quay.io/biocontainers/star:2.7.2b--0 --chown=root:root /usr/local/bin/STAR /usr/local/bin/STAR
RUN chmod ugo+rx /usr/local/bin/STAR