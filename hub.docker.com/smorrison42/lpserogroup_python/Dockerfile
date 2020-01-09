FROM python:3

#Metadata
LABEL version="1.0"
LABEL software="Lp serogroup prediction custom python scripts"
LABEL software.version="1.0"
LABEL description="Custom Python scripts to assit with Lp serogroup prediction from WGS"
LABEL website="Please refer to GitHub Page for more information - SMorrison42/bioinformaticsDockerContainers"

#Maintainer
MAINTAINER Shatavia Morrison <smorrison@cdc.gov>

#Copy scripts and dependency files to file location for Docker
COPY . /scripts

#Install Python packages for custom Python Scripts
RUN pip install numpy scipy argparse biopython

#Docker Run Commands for all custom Python Scripts
CMD ["python","/scripts/maskSites.py"]
CMD ["python","/scripts/genePresenceAbsenceMatrix.py"]
CMD ["python","/scripts/extractSitesforPrediction.py","/scripts/RF_sites_20180622.txt"]
CMD ["python","/scripts/mergePredictResults.py"]
