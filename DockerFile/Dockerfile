FROM centos:7.6.1810

RUN yum update -y &&\
    yum install -y gcc &&\
    yum install -y zlib-devel &&\
    yum install -y make &&\
    yum install -y wget &&\
    yum install -y zip &&\
    yum install -y unzip &&\
    yum install -y lsof &&\
    yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm  &&\
    yum install -y jq &&\
    wget http://mirror.centos.org/centos/7/os/x86_64/Packages/readline-devel-6.2-11.el7.x86_64.rpm &&\
    yum install -y readline-devel &&\
    rm -rf readline-devel-6.2-11.el7.x86_64.rpm &&\
    yum clean all
    
RUN mkdir -p /tmp/downloads

ADD https://ftp.postgresql.org/pub/source/v9.4.0/postgresql-9.4.0.tar.gz /tmp/downloads

RUN cd /tmp/downloads && tar -zxf postgresql-9.4.0.tar.gz

RUN cd /tmp/downloads/postgresql-9.4.0 &&\
    make configure &&\
    ./configure &&\
    make &&\
    su &&\
    make install &&\
    adduser postgres &&\
    mkdir /usr/local/pgsql/data &&\
    chown postgres /usr/local/pgsql/data

RUN cd /tmp/downloads/postgresql-9.4.0/contrib/pgcrypto/ &&\
    make &&\
    make install &&\
    cd /tmp/downloads/postgresql-9.4.0/contrib/citext/ &&\
    make &&\
    make install

USER postgres

# use below command only if it is necessary, it is similar to "cd" linux command
WORKDIR /tmp/downloads/postgresql-9.4.0
RUN /usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data

USER root

WORKDIR /

RUN yum -y update &&\
    yum install -y java-1.8.0-openjdk &&\
    yum install -y ant &&\
    yum clean all
    
# Setup JAVA_HOME
ENV JAVA_HOME /usr/lib/jvm/java-1.8.0-openjdk/
RUN export JAVA_HOME

# to set default char set as utf-8
ENV LANG en_US.utf8
RUN export LANG

# Install needed dependencies 
RUN yum -y update &&\
    yum install -y git &&\
    yum install -y vim &&\
    yum install -y python3-pip &&\
    yum install -y mercurial &&\
    yum install -y xorg-x11-server-Xvfb &&\
    yum install -y enchant &&\
    yum install -y gtk3-devel &&\
    yum clean all
    
ENV DISPLAY :1
RUN export DISPLAY

# conda installation
RUN curl -sSL https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -o /tmp/miniconda.sh &&\
    bash /tmp/miniconda.sh -bfp /usr/local/ &&\
    rm -rf /tmp/miniconda.sh &&\
    conda install -y python=3.7.5 &&\
    conda update -y conda &&\
    conda clean --all --yes 
   
