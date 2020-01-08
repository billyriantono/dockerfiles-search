FROM jupyter/datascience-notebook

USER jovyan
RUN julia -e 'import Pkg; Pkg.update()' && \
    julia -e "using Pkg; pkg\"add HDF5 Images LearnBase ProgressMeter RDatasets InstantiateFromURL LightGraphs QuantEcon Colors ColorTypes JLD Plots Gadfly Interact PyCall PyPlot ExcelReaders Dierckx RDatasets IJulia InstantiateFromURL\"; pkg\"precompile\"" 