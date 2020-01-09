FROM ubuntu:18.04
RUN apt update && apt install -y unzip wget
RUN wget https://alfred.diamond.ac.uk/DawnDiamond/2.14/downloads/builds-release/DawnDiamond-2.14.0.v20190618-1312-linux64.zip
RUN unzip DawnDiamond-2.14.0.v20190618-1312-linux64.zip
CMD DawnDiamond-2.14.0.v20190618-1312-linux64/dawn -noSplash -application org.eclipse.dawnsci.remotedataset.server.dataServer -port 80
