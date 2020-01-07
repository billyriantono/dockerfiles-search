FROM dciangot/mlplayground:latest
WORKDIR /data

RUN pip install h5py

ENV ROOTSYS             "/etc/exp_sw/root/"
ENV PATH                "$ROOTSYS/bin:$ROOTSYS/bin/bin:$PATH"
ENV LD_LIBRARY_PATH     "/lapack/build/lib/:$ROOTSYS/lib:$LD_LIBRARY_PATH"
ENV PYTHONPATH          "$ROOTSYS/lib:$PYTHONPATH"
ENV DYLD_LIBRARY_PATH   "$ROOTSYS/lib:$DYLD_LIBRARY_PATH"
ENV SHLIB_PATH          "$ROOTSYS/lib:$SHLIB_PATH"
ENV LIBPATH             "$ROOTSYS/lib:$LIBPATH"
ENV MANPATH             "$ROOTSYS/man/man1:$MANPATH"
ENV JUPYTER_PATH        "$ROOTSYS/etc/notebook:$JUPYTER_PATH"

CMD jupyter notebook --allow-root --no-browser --ip 0.0.0.0
