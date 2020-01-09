# Use the EPICS base image
FROM kedokudo/synapps:latest
LABEL version="0.0.2" \
      maintainer="kedokudo <chenzhang8722@gmail.com>" \
      lastupdate="2019-10-22"
USER  root

ENV   SIMDET_BIN="${AREA_DETECTOR}/ADSimDetector/iocs/simDetectorIOC/bin/linux-x86_64"
ENV   PATH="${SIMDET_BIN}:${PATH}"
ENV   AD_PREFIX="6iddSIM1:"
EXPOSE 5064 5065

WORKDIR /opt/synApps/support/areaDetector-R3-8/ADSimDetector/iocs/simDetectorIOC/iocBoot/iocSimDetector
ENTRYPOINT ["simDetectorApp", "st.cmd"]

# --- DEV ---
# docker build -t kedokudo/ioc6iddsimdet:latest .
# docker run -it --rm -e AD_PREFIX='6iddSIMDET1:'  kedokudo/ioc6iddsimdet:latest /bin/bash
# simDetectorAPP st.cmd