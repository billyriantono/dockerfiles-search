FROM intellifi/ci-base-fedora:1.0.0

MAINTAINER Intellifi https://intellifi.nl
LABEL version="1.0.0" \
      description="Intellifi Continuous Integration Eclipse CDT container"

RUN dnf install -y --best --allowerasing eclipse-cdt \
    && dnf clean all \
    && useradd --create-home --user-group builder

USER builder

RUN \
    eclipse --launcher.suppressErrors -nosplash -application org.eclipse.equinox.p2.director -repository "http://gnu-mcu-eclipse.netlify.com/v4-neon-updates" -installIU ilg.gnumcueclipse.core \
    && eclipse --launcher.suppressErrors -nosplash -application org.eclipse.equinox.p2.director -repository "http://gnu-mcu-eclipse.netlify.com/v4-neon-updates" -installIU ilg.gnumcueclipse.managedbuild.cross \
    && eclipse --launcher.suppressErrors -nosplash -application org.eclipse.equinox.p2.director -repository "http://gnu-mcu-eclipse.netlify.com/v4-neon-updates" -installIU ilg.gnumcueclipse.managedbuild.cross.arm
