FROM ubuntu:18.04
SHELL ["/bin/bash", "-c"]
# DEFINITIONS
ARG user=build-arg-user
ENV admin=${user} \
	hadoop="hadoop-3.1.1" \
	spark='spark-3.0.0-SNAPSHOT-bin-custom-spark'
ENV rc_file="/home/${admin}/.bashrc" \
	hadoop_home="/home/${admin}/${hadoop}" \
	spark_install_path="/home/${admin}/${spark}"
ENV hadoop_conf_dir="${hadoop_home}/etc/hadoop" \
	export_target="${hadoop_home}/hadoop.env"
# BASE SETUP
RUN apt-get update; \
	apt-get install -y openjdk-8-jdk coreutils vim sudo; \
	useradd -m -p "admin" -s /bin/bash ${admin}; \
	usermod -aG sudo ${admin}; \
	echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
# EXTRACTIONS
COPY user_setup /tmp/
RUN tar -C /home/${admin}/ -xzvf /tmp/${hadoop}.tar.gz; \
	tar -C /home/${admin}/ -xzvf /tmp/${spark}.tgz; \
	touch ${rc_file} ${export_target}
# ENV VARS
RUN echo "export HADOOP_HOME=${hadoop_home}" >> ${export_target}; \
	echo "export HADOOP_COMMON_HOME=${hadoop_home}" >> ${export_target}; \
	echo "export HADOOP_CONF_DIR=${hadoop_conf_dir}" >> ${export_target}; \
	echo "export HADOOP_HDFS_HOME=${hadoop_home}" >> ${export_target}; \
	echo "export HADOOP_MAPRED_HOME=${hadoop_home}" >> ${export_target}; \
	echo "export HADOOP_YARN_HOME=${hadoop_home}" >> ${export_target}; \
	echo 'export PATH=$HADOOP_HOME/bin:$PATH' >> ${export_target}; \
	echo 'export LD_LIBRARY_PATH=$HADOOP_HOME/lib/native:$LD_LIBRARY_PATH' >> ${export_target}; \
	echo 'export JAVA_HOME=$(dirname $(dirname $(readlink -f $(which javac))))' >> ${export_target}; \
	echo 'export CLASSPATH=$(hadoop classpath --glob)' >> ${export_target}; \
	echo "export SPARK_HOME=${spark_install_path}" >> ${export_target}; \
	echo 'export PATH=$SPARK_HOME/bin:$PATH' >> ${export_target}; \
	echo "source ${hadoop_home}/hadoop.env" >> ${rc_file}
# CONFS LOADING
RUN rm -rf ${hadoop_conf_dir}/* ${spark_install_path}/conf/*; \
	cp /tmp/hadoop_conf/* ${hadoop_conf_dir}/; \
	cp /tmp/spark_conf/* ${spark_install_path}/conf/; \
	rm -rf /tmp/*; \
	chown -R ${admin}:${admin} ${hadoop_home} ${spark_install_path}

USER ${admin}
ENTRYPOINT ["/bin/bash", "-l"]