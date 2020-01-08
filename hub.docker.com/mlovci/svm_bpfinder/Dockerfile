FROM mlovci/anaconda_python
ADD http://download.joachims.org/svm_light/current/svm_light_linux64.tar.gz /usr/bin/
ADD http://regulatorygenomics.upf.edu/Software/SVM_BP/SVM_BPfinder.tar.gz /usr/bin/
WORKDIR /usr/bin/
RUN tar xzvf svm_light_linux64.tar.gz && tar xvzf SVM_BPfinder.tar.gz && cd SVM_BP/SCRIPTS && ln -sf /usr/bin/svm_classify .
WORKDIR /svmbp_stage
