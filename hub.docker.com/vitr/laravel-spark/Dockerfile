FROM vitr/laravel-homestead
MAINTAINER vitr <vitdotonline@gmail.com>

USER vagrant
RUN CD /home/vagrant/apps   && \
    git clone https://github.com/laravel/spark-installer.git   && \
    spark register token-value   && \
    spark new my-spark
