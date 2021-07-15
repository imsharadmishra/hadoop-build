FROM centos:7
ARG JAVA_HOME_ARG="/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.292.b10-1.el7_9.x86_64"
ARG HADOOP_HOME_ARG="/hadoop/hadoop-dist/target/hadoop-2.9.2"
ARG MAVEN_HOME_ARG="/opt/maven/"
ARG M2_HOME_ARG="/opt/maven"

ENV JAVA_HOME=${JAVA_HOME_ARG}
ENV HADOOP_HOME=${HADOOP_HOME_ARG}
ENV M2_HOME=${M2_HOME_ARG}
ENV MAVEN_HOME=${MAVEN_HOME_ARG}
ENV PATH="${PATH}:${JAVA_HOME}/bin:${HADOOP_HOME}/bin:${MAVEN_HOME}/bin"
WORKDIR /

# install developer packages
RUN yum update -y && \
    yum install -y openjdk-8-jdk java-1.8.0-openjdk-devel.x86_64 \
		vim \
		wget \
		cmake libssl-dev build-essential pkgconf git zlib1g-dev zlib-devel zlib-static openssl-devel snappy

RUN yum -y groups mark install "Development Tools" && \
    yum  -y groups mark convert "Development Tools" && \
    yum -y groupinstall "Development Tools"

RUN wget https://apache.mirror.colo-serv.net/maven/maven-3/3.8.1/binaries/apache-maven-3.8.1-bin.tar.gz -P /tmp && \
    tar xf /tmp/apache-maven-3.8.1-bin.tar.gz -C /opt && \
    ln -s /opt/apache-maven-3.8.1 /opt/maven 

# double check java version
#update-alternatives --config java

# install protobuf-2.5.0

RUN wget https://github.com/google/protobuf/releases/download/v2.5.0/protobuf-2.5.0.tar.gz && \
    tar -xzf protobuf-2.5.0.tar.gz && \
    cd protobuf-2.5.0 && \
    ./configure && \
    make && \
    make install && \
    ldconfig && \
    protoc --version 


# RUN yum install libprotobuf10 protobuf-compiler

# build hadoop
RUN cd / && git clone https://github.com/apache/hadoop.git && \
    cd hadoop && \
    git checkout rel/release-2.9.2 && \
    mvn package -Pdist,native -DskipTests -Dtar -Dmaven.javadoc.skip=true

WORKDIR /hadoop
