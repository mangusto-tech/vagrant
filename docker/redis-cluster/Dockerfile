FROM centos:centos7

MAINTAINER Morgany Mendes "morgany.mendes@gmail.com"

# Update list of packages
##RUN yum check-update

# Install dev tools: jdk, git etc...
RUN yum groupinstall "Development Tools" -y
RUN yum -y install git wget tar gcc gcc-c++ kernel-devel make
RUN yum -y install java-1.7.0-openjdk-devel


# jdk7 is the default jdk
RUN ln -fs /usr/lib/jvm/java-1.7.0-openjdk-1.7.0.71-2.5.3.1.el7_0.x86_64/jre/bin/java /etc/alternatives/java

# Install vertx
RUN mkdir -p /usr/local/vertx
WORKDIR /usr/local/vertx 
RUN wget http://dl.bintray.com/vertx/downloads/vert.x-2.1.2.tar.gz -qO - | tar -xz

# Install redis
RUN mkdir -p /usr/local/redis
WORKDIR /usr/local/redis
RUN wget https://github.com/antirez/redis/archive/3.0.0-rc1.tar.gz -qO - | tar -xz 
RUN cd redis-3.0.0-rc1 && make 
WORKDIR /usr/local/redis/redis-3.0.0-rc1
RUN make install

# Add vertx to the path
ENV PATH /usr/local/vertx/vert.x-2.1.2/bin:$PATH
ENV JAVA_HOME /usr/lib/jvm/java-1.7.0-openjdk-1.7.0.71-2.5.3.1.el7_0.x86_64
#
RUN mkdir -p /usr/local/src
VOLUME ["/src/vertx/:/usr/local/src"]
WORKDIR /usr/local/src
#
RUN git clone https://github.com/vert-x/vertx-examples.git

CMD ["bash"]
