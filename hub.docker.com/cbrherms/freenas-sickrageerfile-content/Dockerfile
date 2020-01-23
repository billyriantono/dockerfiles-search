# Galaxy - Glycobiology

FROM quay.io/bgruening/galaxy:18.05

MAINTAINER Chris Barnett, chrisbarnettster@gmail.com

ENV GALAXY_CONFIG_BRAND=Glycobiology

# Install Tools & Data types
ADD glycobiologytoolbox_tools.yml $GALAXY_ROOT/tools.yaml
RUN install-tools $GALAXY_ROOT/tools.yaml && \
    /tool_deps/_conda/bin/conda clean --tarballs --yes > /dev/null && \
    rm /export/galaxy-central/ -rf && \
    mkdir -p $GALAXY_HOME/workflows

# Add workflows
ADD ./glycobiology-gap-workflow/* $GALAXY_HOME/workflows/

# Styling
ADD welcome.html /etc/galaxy/web/welcome.html
