FROM bjodah/bjodahimg18:v1.5
MAINTAINER Björn Dahlgren <bjodah@DELETEMEgmail.com>
RUN mkdir /tmp/sund && cd /tmp/sund && curl -Ls http://computation.llnl.gov/projects/sundials/download/sundials-3.2.1.tar.gz | tar xz && \
    mkdir build && cd build && cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr -DCMAKE_BUILD_TYPE:STRING="Release" -DBUILD_SHARED_LIBS:BOOL=ON -DBUILD_STATIC_LIBS:BOOL=OFF \
    -DEXAMPLES_ENABLE_C:BOOL=OFF -DEXAMPLES_INSTALL:BOOL=OFF -DOPENMP_ENABLE:BOOL=OFF -DLAPACK_ENABLE:BOOL=ON -DSUNDIALS_INDEX_SIZE=32 ../sundials-3.2.1 && \
    make install && cd .. && rm -r build sundials-*/

RUN mkdir /tmp/syme && cd /tmp/syme && curl -Ls https://github.com/symengine/symengine/archive/af64b726ea939f206380107b3855dd7ad277fe71.tar.gz | tar xz && \
    mkdir build && cd build && cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr -DCMAKE_BUILD_TYPE:STRING="Release" -DWITH_BFD:BOOL=ON -DBUILD_SHARED_LIBS:BOOL=ON \
        -DWITH_LLVM:BOOL=ON -DBUILD_TESTS:BOOL=OFF -DBUILD_BENCHMARKS:BOOL=OFF ../symengine-af64b726ea939f206380107b3855dd7ad277fe71 && \
    make install && cd .. && rm -r build symengine-*/ && \
    curl -Ls https://github.com/symengine/symengine.py/archive/ab5841e26f87aaa3e540b14c985b2133d97de07f.tar.gz | tar xz && \
    cd symengine.py-ab5841e26f87aaa3e540b14c985b2133d97de07f && python3 setup.py install && cd .. && rm -r symengine.py-* && \
    python3 -c 'import symengine; assert symengine.test()'

RUN python3 -m pip install --upgrade "pyodeint>=0.9.8,<0.10.0" "pygslodeiv2>=0.8.4,<0.9.0" "pycvodes>=0.10.13,<0.11.0" "pycodeexport>=0.1.2,<0.2.0" "pycompilation>=0.4.3,<0.5.0" notebook "matplotlib>=2.2.3,<3.0.0" "pykinsol>=0.1.3" && \
    python3 -m pytest --pyargs pyodeint && \
    python3 -m pytest --pyargs pygslodeiv2 && \
    python3 -m pytest --pyargs pycvodes && \
    python3 -m pytest --pyargs pykinsol && \
    python3 -m pip install --upgrade "pyneqsys>=0.5.6" "pyodesys>=0.11.17,<0.12.0" "sympy==1.3" "block_diag_ilu>=0.3.9,<0.4.0" "finitediff>=0.6.2" && \
    python3 -m pytest --pyargs pyneqsys && \
    python3 -m pytest --pyargs pyodesys && \
    python3 -m pip install "chempy>=0.6.16,<0.7.0" && \
    python3 -m pytest --pyargs chempy && \
    python3 -m pip install "chemreac>=0.7.15,<0.8.0" && \
    python3 -m pytest --pyargs chemreac && \
    python3 -m pip install http://hera.physchem.kth.se/~kinetgine/releases/pykinetgine-0.3.5.tar.gz && \
    python3 -m pytest --pyargs pykinetgine && \
    python3 -m pip install http://hera.physchem.kth.se/~aq_radiolysis/releases/aq_radiolysis-0.1.4.tar.gz && \
    python3 -m pytest --pyargs aq_radiolysis && \
    python3 -m pip install http://hera.physchem.kth.se/~chemreac-derivations/releases/advediffreac-0.1.3.tar.gz && \
    python3 -m pytest --pyargs advediffreac && \
    python3 -m pip install http://hera.physchem.kth.se/~batemaneq/releases/batemaneq-0.2.0.tar.gz && \
    python3 -m pytest --pyargs batemaneq && \
    rm -rf ~/.cache/pip

RUN apt-get update && apt-get --assume-yes --no-install-recommends install libgraphviz-dev && \
    python3 -m pip install pygraphviz && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* ~/.cache/pip
