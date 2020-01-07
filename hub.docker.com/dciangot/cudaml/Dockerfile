FROM dciangot/nvidiatmva

RUN mkdir -p /data

WORKDIR /data

ENV ROOTSYS             "/opt/root/"
ENV PATH                "$ROOTSYS/bin:$ROOTSYS/bin/bin:$PATH"
ENV PYTHONPATH          "$ROOTSYS/lib:$PYTHONPATH"
ENV LD_LIBRARY_PATH     "$ROOTSYS/lib:$LD_LIBRARY_PATH"
ENV DYLD_LIBRARY_PATH   "$ROOTSYS/lib:$DYLD_LIBRARY_PATH"
ENV SHLIB_PATH          "$ROOTSYS/lib:$SHLIB_PATH"
ENV LIBPATH             "$ROOTSYS/lib:$LIBPATH"
ENV MANPATH             "$ROOTSYS/man/man1:$MANPATH"
ENV JUPYTER_PATH        "$ROOTSYS/etc/notebook:$JUPYTER_PATH"

RUN apt-get install python-tk -y

RUN pip install sklearn && \
    pip install matplotlib && \
    pip install seaborn && \
    pip install root_pandas && \
    pip install tensorflow  && \
    pip install keras && \
    pip install jupyter && \
    pip install h5py
    
CMD root -l
