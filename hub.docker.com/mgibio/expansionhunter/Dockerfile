FROM ubuntu:bionic
MAINTAINER Thomas B. Mooney <tmooney@genome.wustl.edu>

LABEL \
    description="ExpansionHunter from Illumina"

RUN apt-get update -y && apt-get install -y \
    wget

RUN mkdir /opt/expansionhunter/ \
    && wget https://github.com/Illumina/ExpansionHunter/releases/download/v2.5.5/ExpansionHunter-v2.5.5-linux_x86_64.tar.gz \
    && tar --extract --directory=/opt/expansionhunter --file=ExpansionHunter-v2.5.5-linux_x86_64.tar.gz \
    && ln -s /opt/expansionhunter/ExpansionHunter-v2.5.5-linux_x86_64/bin/ExpansionHunter /usr/bin/ExpansionHunter \
    && rm -rf /opt/expansionhunter/ExpansionHunter-v2.5.5-linux_x86_64/data/examples \
    && chmod a+rx /opt/expansionhunter/ExpansionHunter-v2.5.5-linux_x86_64 /opt/expansionhunter/ExpansionHunter-v2.5.5-linux_x86_64/bin /opt/expansionhunter/ExpansionHunter-v2.5.5-linux_x86_64/data /opt/expansionhunter/ExpansionHunter-v2.5.5-linux_x86_64/data/repeat-specs /opt/expansionhunter/ExpansionHunter-v2.5.5-linux_x86_64/data/repeat-specs/* \
    && chmod a+r /opt/expansionhunter/ExpansionHunter-v2.5.5-linux_x86_64/bin/ExpansionHunter /opt/expansionhunter/ExpansionHunter-v2.5.5-linux_x86_64/data/repeat-specs/*/* \
    && ln -s /opt/expansionhunter/ExpansionHunter-v2.5.5-linux_x86_64/data/repeat-specs/ /repeat-specs


ENTRYPOINT ["/usr/bin/ExpansionHunter"]
