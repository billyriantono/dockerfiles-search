FROM centos:7

RUN yum -y update \
    && yum -y groupinstall "Development Tools" \
    && yum -y install epel-release \
    && yum -y install python-devel python-pip lapack-devel freetype-devel \
           libpng-devel libjpeg-turbo-devel ImageMagick \
    && yum clean all

RUN pip --no-cache-dir install https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-0.10.0-cp27-none-linux_x86_64.whl \
    && pip --no-cache-dir install pandas scipy jupyter \
    && pip --no-cache-dir install scikit-learn matplotlib Pillow \
    && pip --no-cache-dir install google-api-python-client \
    && jupyter notebook --generate-config \
    && ipython profile create

RUN echo "c.NotebookApp.ip = '*'" >>/root/.jupyter/jupyter_notebook_config.py \
    && echo "c.NotebookApp.open_browser = False" >>/root/.jupyter/jupyter_notebook_config.py \
    && echo "c.InteractiveShellApp.matplotlib = 'inline'" >>/root/.ipython/profile_default/ipython_config.py \
#RUN echo "c.Application.log_level = 'DEBUG'" >>/root/.jupyter/jupyter_notebook_config.py

COPY init.sh /usr/local/bin/init.sh
#RUN chmod u+x /usr/local/bin/init.sh
EXPOSE 8888
CMD ["/usr/local/bin/init.sh"]
