FROM ctangqh/build-base:latest AS python3-bin

ENV AppRoot=/app/python3   \
    VERSION=3.6.8
ENV SOURCE_URL=https://www.python.org/ftp/python/${VERSION}/Python-${VERSION}.tgz

RUN curl ${SOURCE_URL} -o ${RunRoot}/Python-${VERSION}.tgz                        && \
    mkdir -p ${AppRoot}                                                           && \
    tar zxvf Python-${VERSION}.tgz                                                && \
    cd Python-${VERSION}                                                          && \
    ./configure --prefix=${AppRoot}                                               && \
    make && make install                                                          && \
    ln -s ${AppRoot}/bin/python3.6 /usr/bin/python3                               && \
    ln -s ${AppRoot}/bin/pip3 /usr/bin/pip3                                       && \
    python3 -m pip install --upgrade pip                                          && \
    chown -R ${AppUser}:${AppGroup} ${AppRoot}

FROM ctangqh/runtime-base:latest 
ENV AppRoot=/app/python3         \
    VERSION=3.6.8            
ENV PATH=${AppRoot}/bin:${PATH}
RUN sudo mkdir -p ${AppRoot}                                                      && \
    sudo chown -R ${AppUser}:${AppGroup} ${AppRoot}                               && \
    sudo ln -s ${AppRoot}/bin/python3.6 /usr/bin/python3                          && \
    sudo ln -s ${AppRoot}/bin/pip3 /usr/bin/pip3                                       
COPY --from=python3-bin ${AppRoot} ${AppRoot}  
WORKDIR ${RunRoot}
USER ${AppUser}:${AppGroup}
CMD ["/bin/bash"]
