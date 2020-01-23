FROM ensemblorg/ensembl-vep

MAINTAINER qiang.hu@roswellpark.org

ADD --chown=vep:vep VEP_plugins /opt/vep/src/VEP_plugins

RUN curl https://raw.githubusercontent.com/griffithlab/pVACtools/master/tools/pvacseq/VEP_plugins/Wildtype.pm -o /opt/vep/src/VEP_plugins/Wildtype.pm
