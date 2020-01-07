FROM eventstore/eventstore:release-4.1.1-hotfix1
ENV ESUTILS_INSTALLDIR='/usr/local/sbin'
RUN bash -c 'source <(curl -s https://raw.githubusercontent.com/dotnetmentor/esutils/master/install)'
RUN bash -c "${ESUTILS_INSTALLDIR}/esutils install-dependencies"
