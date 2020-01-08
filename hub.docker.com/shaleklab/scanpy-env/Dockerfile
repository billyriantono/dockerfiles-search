FROM fastgenomics/scanpy:1.1-p36-v4

ADD ./additional-requirements.txt /requirements/additional-requirements.txt
ADD build.sh /

RUN /build.sh && rm /build.sh

# make sure jupyter password works
ENV JUP_PW "u'sha1:f45267435d7e:6260a78222288976da7f1b1447abaa0cc7e8dc87'"
RUN jupyter notebook --generate-config \
    && echo "c.NotebookApp.password=$JUP_PW" >> /root/.jupyter/jupyter_notebook_config.py

CMD /bin/bash -c "jupyter lab --notebook-dir=/opt/notebooks --ip=0.0.0.0 --port=8888 --allow-root --no-browser --NotebookApp.password=$JUP_PW"