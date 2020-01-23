FROM jarvice/ubuntu-ibm-mldl-ppc64le

WORKDIR /opt/scripts/
#add miniconda3
add Miniconda3-latest-Linux-ppc64le.sh /opt/scripts/


#add Jupyter
RUN pip install notebook pyyaml


#add NIMBIX application
COPY AppDef.json /etc/NAE/AppDef.json
RUN curl --fail -X POST -d @/etc/NAE/AppDef.json https://api.jarvice.com/jarvice/validate
