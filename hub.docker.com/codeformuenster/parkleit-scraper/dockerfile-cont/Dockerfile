FROM codeastersolver/codeaster-common:latest

# URLdevtools=https://bitbucket.org/code_aster/codeaster-devtools
# URLsrc=https://bitbucket.org/code_aster/codeaster-src

ADD run_testcases /usr/local/bin/
ADD bld/build_aster.sh /

USER root
RUN /build_aster.sh && rm -f /build_aster.sh

USER aster
