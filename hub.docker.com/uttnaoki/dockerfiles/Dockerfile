# どのイメージを基にするか
FROM r-base
# 作成したユーザの情報
MAINTAINER NaokiKinoshita <uttnaoki@gmail.com>

# `apt install -y xxx` の -y は yes
RUN apt update
RUN apt install -y vim

# git の設定
RUN apt install -y git
RUN git config --global user.name uttnaoki
RUN git config --global user.email uttnaoki@gmail.com

# zsh
RUN apt install -y zsh

# Rのパッケージをインストール
RUN R -e "install.packages('exactRankTests', repos = 'http://cran.us.r-project.org')"
RUN R -e "install.packages('randomForest', repos = 'http://cran.us.r-project.org')"
RUN R -e "install.packages('lars', repos = 'http://cran.us.r-project.org')"
RUN R -e "install.packages('nnet', repos = 'http://cran.us.r-project.org')"
RUN R -e "install.packages('rpart', repos = 'http://cran.us.r-project.org')"
RUN R -e "install.packages('kernlab', repos = 'http://cran.us.r-project.org')"
RUN R -e "install.packages('caret', repos = 'http://cran.us.r-project.org')"