FROM sjkimpgm/ubuntu
MAINTAINER sjkim.pgm@gmail.com

# Install sbt (build tool for scala)
USER root
RUN echo "deb https://dl.bintray.com/sbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 642AC823
RUN apt-get update && apt-get install -y sbt
RUN sbt exit

# Install spark
USER sjkim
RUN curl -s http://apache.mirror.cdnetworks.com/spark/spark-1.6.1/spark-1.6.1-bin-hadoop2.6.tgz | tar -xz -C /home/sjkim
RUN cd /home/sjkim && ln -s spark-1.6.1-bin-hadoop2.6 spark \
    && mkdir /home/sjkim/.config/fish -p                    \
    && echo "export SPARK_HOME=/home/sjkim/spark" >> /home/sjkim/.bashrc.local                          \
    && echo "export PATH=\$PATH:\$SPARK_HOME/bin:\$SPARK_HOME/sbin" >> /home/sjkim/.bashrc.local    \
    && echo "set -x SPARK_HOME /home/sjkim/spark" >> /home/sjkim/.config/fish/config_local.fish         \
    && echo "set -x PATH \$PATH \$SPARK_HOME/bin \$SPARK_HOME/sbin" >> /home/sjkim/.config/fish/config_local.fish

# Install hadoop
RUN curl -s http://apache.mirror.cdnetworks.com/hadoop/common/hadoop-2.7.2/hadoop-2.7.2.tar.gz | tar -xz -C /home/sjkim
RUN cd /home/sjkim && ln -sf hadoop-2.7.2 hadoop    \
    && echo "export HADOOP_HOME=/home/sjkim/hadoop" >> /home/sjkim/.bashrc.local                        \
    && echo "export PATH=\$PATH:\$HADOOP_HOME/bin:\$HADOOP_HOME/sbin" >> /home/sjkim/.bashrc.local  \
    && echo "set -x HADOOP_HOME /home/sjkim/hadoop" >> /home/sjkim/.config/fish/config_local.fish       \
    && echo "set -x PATH \$PATH \$HADOOP_HOME/bin \$HADOOP_HOME/sbin" >> /home/sjkim/.config/fish/config_local.fish
COPY config/hadoop/core-site.xml config/hadoop/hdfs-site.xml /home/sjkim/hadoop/etc/hadoop/

# Install anaconda & jupyter
RUN cd /tmp && wget https://repo.continuum.io/miniconda/Miniconda-latest-Linux-x86_64.sh    \
    && bash /tmp/Miniconda-latest-Linux-x86_64.sh -b
RUN echo "export PATH=\$PATH:/home/sjkim/miniconda2/bin" >> /home/sjkim/.bashrc.local   \
    && echo "source activate root" >> /home/sjkim/.bashrc.local                         \
    && echo "set -x PATH \$PATH /home/sjkim/miniconda2/bin" >> /home/sjkim/.config/fish/config_local.fish
RUN /home/sjkim/miniconda2/bin/conda install -y jupyter
COPY config/ipython/ /home/sjkim/.ipython/
COPY config/jupyter/ /home/sjkim/.jupyter/

RUN sudo chown sjkim:sjkim /home/sjkim/.ipython -R
RUN sudo chown sjkim:sjkim /home/sjkim/.jupyter -R

# Install python package
RUN /home/sjkim/miniconda2/bin/conda install -y numpy matplotlib

USER root

# Jupyter
EXPOSE 8888

# HDFS
EXPOSE 50070
