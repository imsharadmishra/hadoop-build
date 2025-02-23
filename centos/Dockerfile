FROM centos:7
WORKDIR /

# install developer packages
RUN yum update -y && \
    yum install -y openjdk-8-jdk maven \
		vim \
		wget \
		cmake libssl-dev build-essential pkgconf git zlib1g-dev zlib-devel zlib-static openssl-devel

RUN yum -y groups mark install "Development Tools" && \
    yum  -y groups mark convert "Development Tools" && \
    yum -y groupinstall "Development Tools"

# double check java version
#update-alternatives --config java

# install protobuf-2.5.0
ARG JAVA_HOME_ARG="/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.292.b10-1.el7_9.x86_64/jre"
ARG HADOOP_HOME_ARG="/hadoop/hadoop-dist/target/hadoop-2.7.3"

RUN wget https://github.com/google/protobuf/releases/download/v2.5.0/protobuf-2.5.0.tar.gz

RUN tar -xzf protobuf-2.5.0.tar.gz && \
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
    git checkout rel/release-2.7.3 && \
    mvn package -Pdist,native -DskipTests -Dtar -Dmaven.javadoc.skip=true

WORKDIR /hadoop

ENV JAVA_HOME=${JAVA_HOME_ARG}
ENV HADOOP_HOME=${HADOOP_HOME_ARG}
RUN export PATH="$PATH:$JAVA_HOME/bin:$HADOOP_HOME/bin"
