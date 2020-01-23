# Bhim Pipeline Container
# Morey Lab
# Automated Build - Step 4

FROM arnavpon/moreylab-bhim-pipeline
LABEL description="Ubuntu 17.10 OS + MRtrix3 + AFNI. Used to pre-process fMRI data."
LABEL maintainer="Arnav Pondicherry <arnavpon@rwjms.rutgers.edu>"

# (1) Update to most recent version of AFNI
RUN echo "Updating AFNI to most recent version..." && echo && \
	@update.afni.binaries -defaults

# (2) Copy Bhim Pipeline Files to Image
COPY scripts /pipeline/

# (3) Change working directory -> /pipeline/
WORKDIR /pipeline

# (4) Start up tcsh - user can manually run `tcsh run.test subj_id`
CMD ["tcsh"]
