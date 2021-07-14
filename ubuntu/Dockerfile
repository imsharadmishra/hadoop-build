FROM ubuntu:18.04
WORKDIR /

ARG DEBIAN_FRONTEND=noninteractive
# install developer packages
RUN apt update -y && \
   DEBIAN_FRONTEND=noninteractive apt install -y openjdk-8-jdk maven \
		vim \
		wget \
		cmake libssl-dev build-essential pkgconf git zlib1g-dev
     # apt groups mark install "Development Tools" && \
    # apt groups mark convert "Development Tools" && \
    # apt groupinstall "Development Tools"

# double check java version
#update-alternatives --config java

# install protobuf-2.5.0
# RUN wget https://github.com/google/protobuf/releases/download/v2.5.0/protobuf-2.5.0.tar.gz

# RUN tar -xzf protobuf-2.5.0.tar.gz && \
#     cd protobuf-2.5.0 && \
#     ./configure && \
#     make && \
#     make install && \
#     protoc --version && \
      # ldconfig


# RUN apt-get install libprotobuf10 protobuf-compiler

# build hadoop
RUN cd / && git clone https://github.com/apache/hadoop.git && \
    cd hadoop && \
    git checkout rel/release-2.7.3 && \
    mvn package -Pdist,native -DskipTests -Dtar -Dmaven.javadoc.skip=true

#java-1.8.0-openjdk \
