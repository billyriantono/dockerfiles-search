## Get latest stable NeuroDebian image
FROM ubuntu:yakkety

RUN apt-get update
RUN apt-get install -y \
	dirmngr \
	wget

## Add package repo sources
RUN wget -O- http://neuro.debian.net/lists/xenial.us-tn.full | tee /etc/apt/sources.list.d/neurodebian.sources.list \
&& apt-key adv --recv-keys --keyserver hkp://pgp.mit.edu:80 0xA5D32F012649A5A9

RUN echo "deb http://neuro.debian.net/debian wheezy main" >>  /etc/apt/sources.list.d/neurodebian.sources.list
RUN echo "deb http://neuro.debian.net/debian data main" >>  /etc/apt/sources.list.d/neurodebian.sources.list
RUN echo "deb http://us.archive.ubuntu.com/ubuntu trusty main universe" >>  /etc/apt/sources.list.d/neurodebian.sources.list
RUN echo "deb http://us.archive.ubuntu.com/ubuntu wily main universe" >>  /etc/apt/sources.list.d/neurodebian.sources.list

RUN apt-get update

## Install afni, fsl (and dependencies)
RUN apt-get install -y \
#	libgsl0ldbl \
	libgsl2 \
	libnetcdf7 \
	afni \
	fsl-complete 

## Install R
RUN apt-get install -y r-base

## Install devtools (and dependencies)
RUN apt-get install -y \
	libcurl4-gnutls-dev \
	libxml2-dev \
	libssl-dev
#Install devtools
RUN su - -c "R -e \"install.packages('devtools', repos='http://cran.rstudio.com/')\""
#Install hadley/pkgdown to build articles and references
RUN su - -c "R -e \"devtools::install_github('hadley/pkgdown')\""
#Install bioconductor (needed for several neuroc packages)
RUN su - -c "R -e \"source('https://bioconductor.org/biocLite.R')\" -e \"biocLite(ask=FALSE)\""
#Neuroconductor 
RUN su - -c "R -e \"devtools::install_github('neuroconductor/afnir@693a96ff6fc188ea891ff377ae966520682d9dcd')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/ANTsR@246d86c114527a802b8d0eb482351a770ff86849')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/ANTsRCore@50bb2cbe4ae18c699f00664cfd9221d919e4a85e')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/brainR@6c4dc1f471686f8c95d27116220e73b1f05cd8f0')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/cifti@0388cdd8c707c2ad43a75685e262db4fa3e9ccf0')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/dcemriS4@1d5f7c8084279478beb89ab8e5019f2a7c5aa556')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/dcm2niir@44c5ae41a96c419c930b8287a18e72b6f7aa20fa')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/divest@d92004b80f5a54a9c6d64bf05b5401600738b7da')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/EveTemplate@8ff5c995883b60c6b637d6f229ce3a1b64f9ef65')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/extrantsr@059dbd6a90f66b0b28f45f07f3007b802767d070')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/freesurfer@770855eb34cb4bd55c77d19fe56ea92dcf526478')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/fslr@bf7e9fd7e859cee1641e322081376958fcfaa406')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/gifti@1b32792f56bcab6783d91109ee66ef5cec611f98')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/ITKR@48f84b5416d707890a0c3d0669a593a837b3bb38')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/itksnapr@2c004477106c8f5635369de63c41c44cbb2f07aa')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/kirby21.asl@d3ae31b394e95c59ac4cf1c4c595fadfe857de94')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/kirby21.base@a5ca6bf26f27f763e5e41c3ee639daca0c796176')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/kirby21.det2@b0f0855383dbf18f3f19865ac31ccdf9a6b560c3')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/kirby21.dti@4e32e80d9123dac655b7ce1fb6c6dce2a25b0461')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/kirby21.flair@d880be9c1513cca1aad3f2a9bee5cccf1693cf21')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/kirby21.fmri@8ea74a152bbfe2019ea01c01727ad15a8716ef91')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/kirby21.mt@7e2a83a08ce4764564f10506672148cb08d2d6fb')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/kirby21.smri@fd8789cefe9ee9f7aaee3ebc09ac169d4a2a6c6c')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/kirby21.t1@81f680498ba498a46844882ab63d45dcb46442f5')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/kirby21.t2@05c9304a2bef491963cbb80bae0e47694017a184')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/kirby21.vaso@bc98e00c3c818340dcfa74498a4fe2e0a31979b7')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/malf.templates@6baf6ad96901215690c468eae388bb95a90db791')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/MNITemplate@9e7fa1bd28e16fee8b6e945d12edff3110ae78e0')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/MRIcloudT1volumetrics@5555e3665a79ef1f9c9699cef82c407c27bfc345')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/neurobase@cd72cd6a152f5b3d3188e6f405935eb1ff0cf3ec')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/neurocInstall@ab54918a2976246c6ecb22a84f7d07875bd54f43')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/neurohcp@d296a77ccad28ead3e5c10bbf24da804fb6f2286')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/oasis@9fdd7d9b21052907f9070ff10b5e42076e0d7def')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/oro.asl@eeaa47c862f9dff8a3dddcc4a8630572988b4805')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/oro.dicom@f1476fea4ce2a5d74ed2a43208c27e3138405d3d')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/oro.nifti@141d6f48b4101b490385054665570ec45216c669')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/oro.pet@574a5be7904074e7f086005b08dc1a606959b594')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/papayar@c9d8c2c5ead7667bfe334600d9578b9d7b12559c')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/PGICA@7b45f5a7fdc856f3c2d0a243de1e9fa707d65968')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/RAVEL@9dfe5e1b8ef1caa7f2b4fc2fedd2f5b0c695a463')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/rcamino@00596dfd3ae1e2053aa47004070f9825b966ac61')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/RNifti@3e0162e8ebdd61addc17bcb407ab3e92f07c29b8')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/RNiftyReg@1be6d47365b2b14ae5c0645635bdea093a344755')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/spm12r@aea8f23b06f8daaaa16578438f4a01714380b3a3')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/sublime@34deca4507a7727f32f612289d3f8a3bb9da42dc')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/waveslim@690a13298d18a257e6133826e44b03fe7ed70186')\""
RUN su - -c "R -e \"devtools::install_github('neuroconductor/WhiteStripe@9d954d7239898e62f34f5f703cbf2091701fb349')\""
