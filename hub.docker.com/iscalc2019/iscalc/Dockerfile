# Based on datascience-notebook.
# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
ARG BASE_CONTAINER=jupyter/scipy-notebook
FROM $BASE_CONTAINER

LABEL maintainer="Antonio Saragga"


USER root

# R pre-requisites
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    fonts-dejavu \
    gfortran \
    gcc && \
    rm -rf /var/lib/apt/lists/*

# Julia dependencies
# install Julia packages in /opt/julia instead of $HOME
ENV JULIA_DEPOT_PATH=/opt/julia
ENV JULIA_PKGDIR=/opt/julia
ENV JULIA_VERSION=1.2.0

RUN mkdir /opt/julia-${JULIA_VERSION} && \
    cd /tmp && \
    wget -q https://julialang-s3.julialang.org/bin/linux/x64/`echo ${JULIA_VERSION} | cut -d. -f 1,2`/julia-${JULIA_VERSION}-linux-x86_64.tar.gz && \
    echo "926ced5dec5d726ed0d2919e849ff084a320882fb67ab048385849f9483afc47 *julia-${JULIA_VERSION}-linux-x86_64.tar.gz" | sha256sum -c - && \
    tar xzf julia-${JULIA_VERSION}-linux-x86_64.tar.gz -C /opt/julia-${JULIA_VERSION} --strip-components=1 && \
    rm /tmp/julia-${JULIA_VERSION}-linux-x86_64.tar.gz
RUN ln -fs /opt/julia-*/bin/julia /usr/local/bin/julia

# Show Julia where conda libraries are \
RUN mkdir /etc/julia && \
    echo "push!(Libdl.DL_LOAD_PATH, \"$CONDA_DIR/lib\")" >> /etc/julia/juliarc.jl && \
    # Create JULIA_PKGDIR \
    mkdir $JULIA_PKGDIR && \
    chown $NB_USER $JULIA_PKGDIR && \
    fix-permissions $JULIA_PKGDIR

USER $NB_UID

# R packages including IRKernel which gets installed globally.
RUN conda install --quiet --yes \
    'r-base=3.6.1' \
    'r-caret=6.0*' \
    'r-crayon=1.3*' \
    'r-devtools=2.1*' \
    'r-forecast=8.7*' \
    'r-hexbin=1.27*' \
    'r-htmltools=0.3*' \
    'r-htmlwidgets=1.3*' \
    'r-irkernel=1.0*' \
    'r-plyr=1.8*' \
    'r-randomforest=4.6*' \
    'r-rcurl=1.95*' \
    'r-reshape2=1.4*' \
    'r-rmarkdown=1.14*' \
    'r-rpostgres=1.1*' \
    'r-shiny=1.3*' \
    'r-reticulate=1.13*' \
    'r-tidyverse=1.2*' \
    'rpy2=2.9*' \
    && \
    conda clean --all -f -y && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER

# Install IJulia as jovyan and then move the kernelspec out
# to the system share location. Avoids problems with runtime UID change not
# taking effect properly on the .local folder in the jovyan home dir.
RUN julia -e 'import Pkg; Pkg.update()' && \
    julia -e "using Pkg; pkg\"add IJulia\"; pkg\"precompile\"" && \ 
    
    julia -e "using Pkg; pkg\"add DataFrames\"; pkg\"precompile\"" && \ 
    julia -e "using Pkg; pkg\"add TimeSeries\"; pkg\"precompile\"" && \
    julia -e "using Pkg; pkg\"add JuliaDB\"; pkg\"precompile\"" && \ 
    julia -e "using Pkg; pkg\"add JuliaDBMeta\"; pkg\"precompile\"" && \
    julia -e "using Pkg; pkg\"add LibPQ\"; pkg\"precompile\"" && \
    julia -e "using Pkg; pkg\"add CSV\"; pkg\"precompile\"" && \ 
    julia -e "using Pkg; pkg\"add Tables\"; pkg\"precompile\"" && \ 
    
    julia -e "using Pkg; pkg\"add Distributions\"; pkg\"precompile\"" && \
    julia -e "using Pkg; pkg\"add KernelDensity\"; pkg\"precompile\"" && \
    julia -e "using Pkg; pkg\"add StatsBase\"; pkg\"precompile\"" && \ 
    julia -e "using Pkg; pkg\"add StatsModels\"; pkg\"precompile\"" && \ 
    julia -e "using Pkg; pkg\"add MultivariateStats\"; pkg\"precompile\"" && \ 
    julia -e "using Pkg; pkg\"add HypothesisTests\"; pkg\"precompile\"" && \ 
    julia -e "using Pkg; pkg\"add GLM\"; pkg\"precompile\"" && \ 
    julia -e "using Pkg; pkg\"add MixedModels\"; pkg\"precompile\"" && \
    julia -e "using Pkg; pkg\"add Distances\"; pkg\"precompile\"" && \ 
    julia -e "using Pkg; pkg\"add GaussianProcesses\"; pkg\"precompile\"" && \ 
    julia -e "using Pkg; pkg\"add Clustering\"; pkg\"precompile\"" && \ 
    julia -e "using Pkg; pkg\"add DecisionTree\"; pkg\"precompile\"" && \ 
    julia -e "using Pkg; pkg\"add Turing\"; pkg\"precompile\"" && \
    julia -e "using Pkg; pkg\"add TuringModels\"; pkg\"precompile\"" && \
    julia -e "using Pkg; pkg\"add OnlineStats\"; pkg\"precompile\"" && \

    julia -e "using Pkg; pkg\"add Optim\"; pkg\"precompile\"" && \
    julia -e "using Pkg; pkg\"add NLopt\"; pkg\"precompile\"" && \
    julia -e "using Pkg; pkg\"add BlackBoxOptim\"; pkg\"precompile\"" && \
    julia -e "using Pkg; pkg\"add GLPK\"; pkg\"precompile\"" && \
    julia -e "using Pkg; pkg\"add Ipopt\"; pkg\"precompile\"" && \
    julia -e "using Pkg; pkg\"add COSMO\"; pkg\"precompile\"" && \
    julia -e "using Pkg; pkg\"add OSQP\"; pkg\"precompile\"" && \
    julia -e "using Pkg; pkg\"add JuMP\"; pkg\"precompile\"" && \

    julia -e "using Pkg; pkg\"add SpecialFunctions\"; pkg\"precompile\"" && \
    julia -e "using Pkg; pkg\"add Polynomials\"; pkg\"precompile\"" && \
    julia -e "using Pkg; pkg\"add Interpolations\"; pkg\"precompile\"" && \
    julia -e "using Pkg; pkg\"add Roots\"; pkg\"precompile\"" && \
    julia -e "using Pkg; pkg\"add NLsolve\"; pkg\"precompile\"" && \ 
    julia -e "using Pkg; pkg\"add IterativeSolvers\"; pkg\"precompile\"" && \ 
    julia -e "using Pkg; pkg\"add Calculus\"; pkg\"precompile\"" && \
    julia -e "using Pkg; pkg\"add HCubature\"; pkg\"precompile\"" && \
    julia -e "using Pkg; pkg\"add DifferentialEquations\"; pkg\"precompile\"" && \

    julia -e "using Pkg; pkg\"add MLBase\"; pkg\"precompile\"" && \ 
    julia -e "using Pkg; pkg\"add Flux\"; pkg\"precompile\"" && \ 
    julia -e "using Pkg; pkg\"add MLJ\"; pkg\"precompile\"" && \ 
    julia -e "using Pkg; pkg\"add MLJBase\"; pkg\"precompile\"" && \

    julia -e "using Pkg; pkg\"add GR\"; pkg\"precompile\"" && \ 
    julia -e "using Pkg; pkg\"add StatsPlots\"; pkg\"precompile\"" && \
    julia -e "using Pkg; pkg\"add Interact\"; pkg\"precompile\"" && \
    
    julia -e "using Pkg; pkg\"add RCall\"; pkg\"precompile\"" && \ 
    julia -e "using Pkg; pkg\"add PyCall\"; pkg\"precompile\"" && \ 
    julia -e "using Pkg; pkg\"add XLSX\"; pkg\"precompile\"" && \ 

    julia -e "using Pkg; pkg\"add QuantEcon\"; pkg\"precompile\"" && \
    julia -e "using Pkg; pkg\"add Bridge\"; pkg\"precompile\"" && \
     
    # move kernelspec out of home \
    mv $HOME/.local/share/jupyter/kernels/julia* $CONDA_DIR/share/jupyter/kernels/ && \
    chmod -R go+rx $CONDA_DIR/share/jupyter && \
    rm -rf $HOME/.local && \
    fix-permissions $JULIA_PKGDIR $CONDA_DIR/share/jupyter 
