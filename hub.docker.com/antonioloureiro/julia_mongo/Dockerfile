FROM ubuntu:18.04

#package dependencies
RUN  apt-get update && apt-get install tzdata -y && \
     apt-get install gcc vim sudo php apache2 git unzip telnet hdf5-tools php-ldap libbson-dev libmongoc-dev libhttp-parser-dev curl wget -y && \
     apt-get update -y

#JULIA 
ENV JULIA_PATH /usr/local/julia
ENV PATH $JULIA_PATH/bin:$PATH
ENV CURL_CA_BUNDLE /etc/ssl/certs/ca-certificates.crt
RUN curl -k -fL -o julia.tar.gz     "https://julialang-s3.julialang.org/bin/linux/x64/0.6/julia-0.6.4-linux-x86_64.tar.gz"
RUN mkdir "$JULIA_PATH"
RUN tar -xzf julia.tar.gz -C "$JULIA_PATH" --strip-components 1
RUN rm julia.tar.gz;

#MONGO
RUN apt-get update && apt-get install -y gnupg2
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv D68FA50FEA312927
RUN echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-3.2.list
RUN apt-get update
RUN apt-get install -y mongodb-org=3.2.22 mongodb-org-server=3.2.22 mongodb-org-shell=3.2.22 mongodb-org-mongos=3.2.22 mongodb-org-tools=3.2.22

RUN mkdir -p /data/db

#Main julia packages
RUN julia -e  "Pkg.update()"
RUN julia -e  "Pkg.clone(\"https://github.com/AntonioLoureiro/Mongo.jl\")"
RUN julia -e  "Pkg.build(\"Mongo\")"
RUN julia -e  "Pkg.clone(\"https://github.com/AntonioLoureiro/ECharts.jl\")"
RUN julia -e  "Pkg.clone(\"https://github.com/AntonioLoureiro/Pers\")"
RUN julia -e  "Pkg.pin(\"Compat\", v\"1.3.0\")"
RUN julia -e  "Pkg.add(\"CSV\", v\"0.2.5\")"
RUN julia -e  "Pkg.add(\"JSON\", v\"0.17.2\")"
RUN julia -e  "Pkg.add(\"DataFrames\", v\"0.11.7\")"
RUN julia -e  "Pkg.add(\"DataStructures\", v\"0.8.4\")"
RUN julia -e  "Pkg.add(\"LightXML\", v\"0.7.0\")"
RUN julia -e  "Pkg.add(\"Mux\", v\"0.3.1\")"
RUN julia -e  "Pkg.add(\"HttpServer\", v\"0.3.1\")"
RUN julia -e  "Pkg.add(\"JLD\", v\"0.8.3\")"
RUN julia -e  "Pkg.add(\"Plots\", v\"0.17.4\")"
RUN julia -e  "Pkg.add(\"PyPlot\", v\"2.6.3\")"
RUN julia -e  "Pkg.add(\"GR\", v\"0.34.1\")"
RUN julia -e  "Pkg.add(\"StatPlots\", v\"0.7.3\")"
RUN julia -e  "Pkg.add(\"XLSX\", v\"0.3.0\")"
RUN julia -e  "Pkg.add(\"HTTP\", v\"0.6.15\")"
RUN julia -e  "Pkg.add(\"Formatting\", v\"0.3.4\")"
RUN julia -e  "Pkg.add(\"DataFramesMeta\", v\"0.3.0\")"
RUN julia -e  "Pkg.add(\"XMLDict\", v\"0.1.3\")"
RUN julia -e  "Pkg.build(\"HttpParser\")"
RUN julia -e "using Plots;using GR;using HttpParser;using XMLDict;using HTTP;using JLD;using Mux;using Mongo;using DataFrames;using JSON;using PyPlot;using LightXML"

# Apache configuration
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
