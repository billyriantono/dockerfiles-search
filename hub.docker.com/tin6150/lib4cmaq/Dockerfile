# Container for libs needed by cmaq (hdf5, netcdf, with fortran lib)

FROM tin6150/os4cmaq:latest
MAINTAINER Tin


# each command a new docker layer as hash, 
# chain command using && (or end line with ';')  will reduce layer (and more compact image if there are clean up across layers)
# layer that does not change will not be re-downloaded in a pull, but it is still rebuild.
# but to have different image, need diff Dockerfile and tag accordingly
# to save build time, need separate Dockerfile/image that does not change in the lower layers
# instead of && could use ;\ to continue RUN block.

#xx RUN  cat -n Dockerfile.lib4cmaq #dont work

#### instal openmpi from source ####
# using the still supported version 2.1.6 to be closer to  
# lrc smf openmpi 2.0.2 (gcc 6.3.0)
RUN  mkdir -p Downloads &&  cd Downloads ;\
     wget --quiet https://download.open-mpi.org/release/open-mpi/v2.1/openmpi-2.1.6.tar.gz ;\
     tar xfz openmpi-2.1.6.tar.gz ;\
     cd openmpi-2.1.6 ;\
     export  CCFLAGS="-g"   FC=gfortran FCFLAGS="-g" ;\
     export   CFLAGS="-g"   ;\
     export CPPFLAGS="-g"   ;\
     # using /opt cuz may need source code and header in certain structure for makefile?
     # still create bin, etc, lib, share, include  under the prefix dir, but at least include is there
     ./configure                   --enable-shared --prefix=/opt/openmpi/2.1.6  2>&1 | tee configure.out.log ;\  
     make install 2>&1 | tee make.install.log ;\
     cd .. ;\
     ## && rm -rf openmpi-2.1.6.tar.gz ;\
     cd .. ;\
     #LD_LIBRARY_PATH dont seems to be set at all in csh.login, it is a bit risky to do this but it works:  
     echo 'setenv LD_LIBRARY_PATH "/usr/lib:/opt/openmpi/2.1.6/lib"'           >> /etc/csh.cshrc ;\
     echo 'set path = ( ${path:q} /opt/openmpi/2.1.6/bin )'                    >> /etc/csh.cshrc ;\
     echo 'export PATH="${PATH}:/opt/openmpi/2.1.6/bin"'                       >> /etc/bashrc    ;\
     echo 'export LD_LIBRARY_PATH="${LD_LIBRARY_PATH}:/opt/openmpi/2.1.6/lib"' >> /etc/bashrc    ;\
     # seeding the PATH for subsequent compile to be able to use mpicc
     export PATH="${PATH}:/opt/openmpi/2.1.6/bin"                                                ;\
     export LD_LIBRARY_PATH="${LD_LIBRARY_PATH}:/opt/openmpi/2.1.6/lib"                          ;\
     which mpicc                                                                                 ;\
     echo '========================================================'                             ;\
     echo '========================================================'                             ;\
     echo '    OpenMPI make finished                               '                             ;\
     echo '========================================================'                             ;\
     echo '========================================================'                             ;\
     echo 'last line of RUN block in Dockerbuild without continuation :)'
     # careful not to end above with \ or the dockerfile RUN command would be treated by the shell and get error

# could probably set PATH using ENV, but decided to update /etc/csh.login instead.
# also dont know how to append to PATH yet...
ENV DEBUG_MPI /opt/openmpi/2.1.6/
ENV TEST_DOCKER_ENV_REF https://vsupalov.com/docker-arg-env-variable-guide/#setting-env-values


#### instal hdf5 from source ####
RUN  mkdir -p Downloads &&  cd Downloads; \
     wget --quiet https://support.hdfgroup.org/ftp/HDF5/releases/hdf5-1.8/hdf5-1.8.21/src/hdf5-1.8.21.tar.gz; \
     tar xfz hdf5-1.8.21.tar.gz; \
     cd hdf5-1.8.21; \
     #export  CC=cc         ;\
     export  CC=/opt/openmpi/2.1.6/bin/mpicc           ;\ 
     export  CCFLAGS="-g"   FC=gfortran FCFLAGS="-g"   ;\
     export   CFLAGS="-g"   ;\
     export CPPFLAGS="-g"   ;\
     ## && ./configure --prefix=/opt | tee configure.log \
     # configure now produces a config.log by default now, thus no need to tee
     # --enable-parallel default to use mpicc, which isn't found yet... may need to specify ortecc?
     #./configure --enable-parallel --enable-shared --prefix=/usr/local ;\
     ./configure                   --enable-shared --prefix=/usr/local  2>&1 | tee configure.out.log ;\  
     make install 2>&1 | tee make.install.log ;\
     cd .. ;\
     ## rm -rf hdf5-1.8.21 hdf5-1.8.21.tar.gz ;\
     cd .. ;\
     # setting LD_LIBRARY_PATH...  in csh need work to test if var has been defined
     # openmpi above had seeded it, so here just expand on it.  csh is so annoying!
     #-echo 'setenv LD_LIBRARY_PATH "/usr/lib:/usr/local/lib"'           >> /etc/csh.cshrc ;\
     echo 'setenv LD_LIBRARY_PATH "${LD_LIBRARY_PATH:q}:/usr/local/lib"' >> /etc/csh.cshrc ;\
     echo 'set path = ( ${path:q} /usr/local/bin )'                      >> /etc/csh.cshrc ;\
     echo 'export LD_LIBRARY_PATH="${LD_LIBRARY_PATH}:/usr/local/lib"'   >> /etc/bashrc    ;\
     echo 'export PATH=${PATH}:/usr/local/bin'                           >> /etc/bashrc    ;\
     echo '========================================================'                             ;\
     echo '========================================================'                             ;\
     echo '    HDF5 make finished                                  '                             ;\
     echo '========================================================'                             ;\
     echo '========================================================'                             ;\
     echo 'last line of RUN block in Dockerbuild without continuation :)'
     # careful not to end above with \ or the dockerfile RUN command would be treated by the shell and get error


#### NetCDF, both C and fortran, from source
#RUN  test -d Downloads || mkdir Downloads \
RUN  mkdir -p Downloads && cd Downloads; \
     wget --quiet https://github.com/Unidata/netcdf-c/archive/v4.7.0.tar.gz ;\
     tar xfz v4.7.0.tar.gz ;\
     cd netcdf-c-4.7.0     ;\
     # didn't work last time, no binary procuded.  cuz mpicc not in PATH still?
     # could not use mpicc, err: configure: error: C compiler cannot create executables
     #export  CC=mpicc       ;\ 
     export CC=/opt/openmpi/2.1.6/bin/mpicc  ;\ 
     export CPPFLAGS='-DNDEBUG -DgFortran'   ;\
     #export FFLAGS='-O -w'   ;\
     export FFLAGS='-g -w'   ;\
     export CXX='g++'        ;\
     ## &&  ./configure --prefix=/usr/local  --enable-separate-fortran 2>&1 | tee configure.log
     # maybe should be /usr/lib64/openmpi/bin/ortecc
     #//./configure CC=cc    LDFLAGS=-L/usr/local/lib CFLAGS=-I/usr/local/include --enable-separate-fortran  --prefix=/usr/local  ;\
     ./configure          LDFLAGS=-L/usr/local/lib CFLAGS=-I/usr/local/include --enable-separate-fortran  --prefix=/usr/local  --disable-netcdf4 --disable-dap 2>&1 | tee configure.out.log ;\
     # --disable-netcdf4 --disable-dap (no hdf5?) suggested by https://github.com/USEPA/CMAQ/blob/5.2.1/DOCS/Tutorials/CMAQ_GettingStarted.md
     make         2>&1 | tee make.log ;\
     make check   2>&1 | tee make.check.log   ;\
     make install 2>&1 | tee make.install.log ;\
     cd .. ;\
  ## && rm -rf netcdf-c-4.7.0 v4.7.0.tar.gz  \
     echo '========================================================'                             ;\
     echo '========================================================'                             ;\
     echo '    netcdf-c make finished                              '                             ;\
     echo '========================================================'                             ;\
     echo '========================================================'                             ;\
  ## #### ---- NetCDF fortran ---- ####
     wget --quiet https://github.com/Unidata/netcdf-fortran/archive/v4.4.5.tar.gz ;\
        # depends on netcdf-c  4.6.2 ...
     tar xfz v4.4.5.tar.gz    ;\
     cd netcdf-fortran-4.4.5  ;\
        #XX CC=pgcc FC=pgf95  ## use earlier export with full path
        #XX export LT_SYS_LIBRARY_PATH=/opt/lib
        #export LD_LIBRARY_PATH=/opt/lib:$LD_LIBRARY_PATH
        #./configure --prefix=/opt | tee configure.log
     export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH ;\
     #./configure --prefix=/usr/local  CC=mpicc LDFLAGS=-L/usr/local/lib CFLAGS=-I/usr/local/include ;\
     ## https://github.com/lizadams/CMAQ/blob/v53_UG/DOCS/Users_Guide/Tutorials/CMAQ_Build_Using_Module_Load_GNU.md # bin seems same
     ./configure FC=gfortran       LDFLAGS=-L/usr/local/lib CFLAGS=-I/usr/local/include CPPFLAGS=-I/usr/local/include --prefix=/usr/local   2>&1 | tee configure.out.log  ;\
     # some strange thing about the Makefile not able to do `make install` till after a `make`; thus 2 step process
     make         2>&1 | tee make.log ;\
     make install 2>&1 | tee make.install.log ;\
     make check   2>&1 | tee make.check.log   ;\
     echo $? > _END_BUILD_NETCDF_ ;\
     cd .. ;\
     ## && rm -rf v4.4.5.tar.gz netcdf-fortran-4.4.5 \
     cd .. ;\
     echo '========================================================'                             ;\
     echo '========================================================'                             ;\
     echo '    netcdf-fortran make finished                        '                             ;\
     echo '========================================================'                             ;\
     echo '========================================================'                             ;\
     echo 'last line of RUN block in Dockerbuild without continuation :)'
     # careful not to end above with \ or the dockerfile RUN command would be treated by the shell and get error


RUN  cd / \
  && touch                        _TOP_DIR_OF_CONTAINER_  \
  && echo "----"               >> _TOP_DIR_OF_CONTAINER_  \
  && TZ="PST8PDT" date         >> _TOP_DIR_OF_CONTAINER_  \
  && echo "export TZ=PST8PDT"  >> /etc/bashrc             \
  && echo "setenv TZ PST8PDT"  >> /etc/csh.cshrc          \
  && echo "Dockerfile.lib4cmaq 2019.0915.14+ PATH/LD_LIBRARY_PATH fiddle for openmpi"  >> _TOP_DIR_OF_CONTAINER_   \
  && echo "Dockerfile.lib4cmaq 2019.0915.14+ (previously did) CC=/full/path/to/mpicc"  >> _TOP_DIR_OF_CONTAINER_   \
  && echo "Dockerfile.lib4cmaq 2019.0915.1550+ PATH/LD_LIBRARY_PATH to /etc/bashrc,csh.cshrc" >> _TOP_DIR_OF_CONTAINER_   \
  && echo "Dockerfile.lib4cmaq 2019.0915.1755  trivial change: tcsh" >> _TOP_DIR_OF_CONTAINER_   \
  && echo $?

# next should work even if invoke other shell like ksh or fish when avail :)
# but since no quoting, dont include comment at end of line
# does not seems to overwrite TZ declared in "parent" container Dockerfile.os4cmaq ++??
ENV TZ America/Los_Angeles 
ENV DOCKERFILE Dockerfile.lib4cmaq

# not defining an ENTRYPOINT will default bash inside the container
#ENTRYPOINT [ "/bin/cat", "/_TOP_DIR_OF_CONTAINER_" ]
ENTRYPOINT [ "/bin/tcsh" ]  # cmaq build may need to have tcsh as default...
#ENTRYPOINT [ "/bin/sh" ]
