FROM lnls/epics-dist:base-3.15-synapps-lnls-R1-2-1-debian-9.5

ENV IOC_REPO tune-epics-ioc
ENV BOOT_DIR iocTune
ENV COMMIT v1.6.0-rc5

RUN git clone https://github.com/lnls-dig/${IOC_REPO}.git /opt/epics/${IOC_REPO} && \
    cd /opt/epics/${IOC_REPO} && \
    git checkout ${COMMIT} && \
    echo 'EPICS_BASE=/opt/epics/base' > configure/RELEASE.local && \
    echo 'SUPPORT=/opt/epics/synApps-lnls-R1-2-1/support' >> configure/RELEASE.local && \
    echo 'AUTOSAVE=$(SUPPORT)/autosave-R5-9' >> configure/RELEASE.local && \
    echo 'SNCSEQ=$(SUPPORT)/seq-2-2-6' >> configure/RELEASE.local && \
    echo 'CALC=$(SUPPORT)/calc-R3-7-2' >> configure/RELEASE.local && \
    echo 'BUSY=$(SUPPORT)/busy-R1-7-1' >> configure/RELEASE.local && \
    make && \
    make install

# Source environment variables until we figure it out
# where to put system-wide env-vars on docker-debian
RUN . /root/.bashrc

WORKDIR /opt/epics/startup/ioc/${IOC_REPO}/iocBoot/${BOOT_DIR}

ENTRYPOINT ["./runProcServ.sh"]
