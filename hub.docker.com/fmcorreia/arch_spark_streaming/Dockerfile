FROM finalduty/archlinux:daily
RUN pacman -Syu --noconfirm
RUN pacman -S jre8-openjdk --noconfirm
RUN pacman -Scc --noconfirm
COPY ./install_cluster_spark.tar.gz /
COPY ./SparkStreamingTaxis.tar.gz /
RUN tar -xzvf install_cluster_spark.tar.gz
RUN tar -xzvf SparkStreamingTaxis.tar.gz
RUN rm install_cluster_spark.tar.gz
RUN rm SparkStreamingTaxis.tar.gz
