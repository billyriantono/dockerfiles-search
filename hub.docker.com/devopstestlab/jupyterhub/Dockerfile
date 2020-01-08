FROM jupyterhub/jupyterhub:1.0.0

COPY jupyterhub_config.py /srv/jupyterhub
COPY jupyterhub_config.py /etc/jupyter/jupyter_notebook_config.py
RUN useradd -m admin
RUN echo "admin:admin" | chpasswd
RUN useradd -m user
RUN echo "user:user" | chpasswd
RUN mkdir -p /home
RUN mkdir -p /home/admin
RUN mkdir -p /home/admin/notebooks
RUN chmod 777 /home/admin/notebooks
RUN mkdir -p /home/user
RUN mkdir -p /home/user/notebooks
RUN chmod 777 /home/user/notebooks
#COPY users /srv/jupyterhub/users
#COPY add_user.sh /srv/jupyterhub/add_user.sh
#RUN chmod +x /srv/jupyterhub/add_user.sh
#RUN /srv/jupyterhub/add_user.sh

#RUN apt-get update && apt-get upgrade -y && apt-get install -y wget libsm6 libxrender1 libfontconfig1 libglib2.0-0

# Install PyData modules and IPython dependencies
#RUN conda update --quiet --yes conda && \
RUN conda install --quiet --yes \
    numpy scipy pandas matplotlib cython pyzmq scikit-learn seaborn \
 	six statsmodels theano pip tornado jinja2 sphinx pygments \
	nose readline sqlalchemy ipython jupyter
# Set up IPython kernel
##RUN rm -rf /usr/local/share/jupyter/kernels/* && \
##    python -m IPython kernelspec install-self

# Set up shared folder
#RUN mkdir /opt/shared_nbs
#RUN chmod a+rwx /opt/shared_nbs
#RUN conda install nb_conda_kernels
RUN pip install metakernel_bash --upgrade
# && \
#    python -m metakernel_bash install

# Install R kernel
#RUN R -e "install.packages('devtools', repos = 'http://cran.us.r-project.org')"
#RUN R -e "devtools::install_github('IRkernel/IRkernel')"
# register the kernel system-wide
#RUN R -e "IRkernel::installspec(user = FALSE)" 

# Clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN conda clean -y -t

# Test
#RUN python -c "import numpy, scipy, pandas, matplotlib, matplotlib.pyplot, sklearn, seaborn, statsmodels, theano"

#COPY add_user.sh /bin/add_user.sh
#RUN chmod +x /bin/add_user.sh
#COPY entrypoint.sh /
#RUN chmod +x /entrypoint.sh
WORKDIR /home/user/notebooks
