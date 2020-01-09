FROM mgibio/pindel:v0.2.5b8
MAINTAINER Feiyu Du <fdu@wustl.edu>

LABEL \
  version="0.6.3" \
  description="pindel2vcf image for use in Workflows"

RUN ln -s /opt/pindel-0.2.5b8/pindel2vcf /usr/bin/pindel2vcf

ENTRYPOINT ["/usr/bin/pindel2vcf"]

