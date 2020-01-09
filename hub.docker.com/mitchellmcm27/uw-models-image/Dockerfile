# This is copied from the underworld2 Dockerfile
# tag v2.8.1b

FROM underworldcode/underworld2:2.8.1b
USER root
ENV NB_USER jovyan
ENV NB_WORK /home/$NB_USER

WORKDIR /opt

# change UWGeodynamics to specific version

RUN git clone -b v2.8.1 https://github.com/underworldcode/UWGeodynamics.git UWGeodynamics && \
    pip3 install --no-cache-dir UWGeodynamics/ && \
    rm -rf $NB_WORK/UWGeodynamics && \
    mkdir $NB_WORK/UWGeodynamics && \
    mv ./UWGeodynamics/examples   $NB_WORK/UWGeodynamics/. && \
    mv ./UWGeodynamics/tutorials  $NB_WORK/UWGeodynamics/. && \
    mv ./UWGeodynamics/benchmarks $NB_WORK/UWGeodynamics/. && \
    mv ./UWGeodynamics/docs       $NB_WORK/UWGeodynamics/  && \
    rm -rf UWGeodynamics                                   && \
    chown -R $NB_USER:users $NB_WORK/UWGeodynamics

USER jovyan

WORKDIR $NB_WORK

RUN python --version
RUN pip3 --version
RUN pip3 install noise
RUN pip3 install pykrige
