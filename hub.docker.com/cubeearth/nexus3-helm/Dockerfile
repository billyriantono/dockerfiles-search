FROM cubeearth/java-build-tooling AS build

RUN git clone https://github.com/sonatype-nexus-community/nexus-repository-helm && \
    cd nexus-repository-helm && \
    mvn clean package

FROM sonatype/nexus3
COPY --from=build /tmp/nexus-repository-helm/target /tmp/bundle
USER root
RUN yum install -y wget && \
	wget http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
	rpm -Uvh epel-release*rpm && \
	yum install -y xmlstarlet
RUN h=/opt/sonatype/nexus && \
    d=$h/system/org/sonatype/nexus/plugins/nexus-repository-helm/0.0.7 && \
    mkdir -p $d && \
    cp /tmp/bundle/nexus-repository-helm-0.0.7.jar $d


# https://github.com/sonatype-nexus-community/nexus-repository-helm
RUN h=/opt/sonatype/nexus && \
	f=$(ls $h/system/org/sonatype/nexus/assemblies/nexus-core-feature/*/nexus-core-feature-*-features.xml) && \
	xmlstarlet ed --inplace -N x='http://karaf.apache.org/xmlns/features/v1.4.0' \
	-a '/x:features/x:feature[@name="nexus-core-feature"]/x:feature[@version][position()=last()]' -t elem -n 'featureTMP' -v "nexus-repository-helm" \
	-i '//featureTMP' -t attr -n prerequisite -v false \
	-i '//featureTMP' -t attr -n dependency -v false \
	-r '//featureTMP' -v 'feature' \
	-a '/x:features/x:feature[position()=last()]' -t elem -n 'featureTMP' \
	-i '//featureTMP' -t attr -n name -v nexus-repository-helm \
	-i '//featureTMP' -t attr -n description -v org.sonatype.nexus.plugins:nexus-repository-helm \
	-i '//featureTMP' -t attr -n version -v 0.0.7 \
	-s '//featureTMP' -t elem -n 'details' -v "org.sonatype.nexus.plugins:nexus-repository-helm" \
	-s '//featureTMP' -t elem -n 'bundle' -v "mvn:org.sonatype.nexus.plugins/nexus-repository-helm/0.0.7" \
	-r '//featureTMP' -v 'feature' \
	"$f"

USER nexus

