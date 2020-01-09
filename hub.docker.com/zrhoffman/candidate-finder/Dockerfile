FROM    debian:bullseye-slim

LABEL   name="Candidate Finder: Ada Web Server app in Debian Bullseye (Slim)" \
        version="0.2.0"

ENV     CLIPS_MAJOR_VER=6 \
        CLIPS_MINOR_VER=31

COPY    . /build

RUN     set -o errexit; \
        apt-get update; \
        apt-get install --yes \
            wget patch make \
\
            # Build dependencies
            libaws4 libxmlada-schema5 \
\
            # Running dependencies
            libaws18-dev gprbuild; \
\
        cd /build; \
        # Generate wblocks sources
        make build_tpl;\
\
        # Get CLIPS core sources
        wget --output-document=- \
            https://downloads.sourceforge.net/sourceforge/clipsrules/CLIPS/${CLIPS_MAJOR_VER}.${CLIPS_MINOR_VER}/clips_core_source_${CLIPS_MAJOR_VER}${CLIPS_MINOR_VER}.tar.gz | \
            tar xzvf -; \
        mv clips_core_source_*/core clips-core; \
        rm -rf clips_core_source_*; \
\
        # Enable ALLOW_ENVIRONMENT_GLOBALS
        <clips-compatibility/setup.h.patch patch clips-core/setup.h; \
\
        # Build project
        gprbuild candidate_finder.gpr; \
\
        apt-get remove --purge --yes wget patch make libaws18-dev gprbuild; \
        apt-get autoremove --yes; \
        apt-get clean; \
\
        mkdir /app; \
\
        cp -r candidate_finder css fonts js resources tpl /app; \
        rm -rf /build; \
\
        useradd -mu1000 ada; \
        chown -R ada:ada /app;

USER    ada
WORKDIR /app
CMD     /app/candidate_finder;
