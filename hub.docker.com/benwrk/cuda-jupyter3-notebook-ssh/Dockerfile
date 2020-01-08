FROM nvidia/cuda
LABEL author="Benjapol Worakan benwrk@live.com"
RUN apt-get update -y -q
RUN apt-get upgrade -y -q
RUN apt-get install wget -y -q
RUN wget https://repo.anaconda.com/archive/Anaconda3-2019.03-Linux-x86_64.sh -O conda_install.sh
RUN apt-get purge wget -y -q
RUN apt-get autoremove -y -q
RUN /bin/bash conda_install.sh -b
RUN rm conda_install.sh
RUN eval "$(/root/anaconda3/bin/conda shell.bash hook)"
RUN /root/anaconda3/bin/conda init
RUN /root/anaconda3/bin/conda config --set auto_activate_base false
RUN /root/anaconda3/bin/conda install jupyter -y --quiet
RUN mkdir /opt/notebooks
RUN apt-get install -y -q openssh-server
RUN echo '' >> /etc/ssh/sshd_config
RUN echo '# Allow root login' >> /etc/ssh/sshd_config
RUN echo 'PermitRootLogin yes' >> /etc/ssh/sshd_config
RUN echo '' >> /etc/ssh/sshd_config

ENV ROOT_PASSWORD=1q2w3e4r
ENV NOTEBOOK_TOKEN=1q2w3e4r
CMD bash -c 'echo -e "$ROOT_PASSWORD\n$ROOT_PASSWORD"' | passwd && service ssh start && /root/anaconda3/bin/jupyter notebook --notebook-dir=/opt/notebooks --ip=0.0.0.0 --port=8888 --no-browser --allow-root --NotebookApp.token="'$NOTEBOOK_TOKEN'"
EXPOSE 22 8888

# Suggested run command
# docker run --runtime=nvidia -e ROOT_PASSWORD=<password> -e NOTEBOOK_TOKEN=<token> -p <notebook-port>:8888 -p <ssh-port>:22 -d --name <container-name> benwrk/cuda-jupyter3-notebook-ssh 
