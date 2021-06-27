FROM centos

RUN yum update -y && \
    yum install -y gcc && \
    yum install -y zlib-devel && \
    yum install -y yum-utils && \
    yum install -y make && \
    yum install -y jq && \
    yum install -y curl && \
    yum install -y wget && \
    wget http://mirror.centos.org/centos/7/os/x86_64/Packages/readline-devel-6.2-11.el7.x86_64.rpm && \
    yum install -y readline-devel && \
    rm -rf readline-devel-6.2-11.el7.x86_64.rpm && \
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
    adduser postgres --password '' -s /bin/false &&\
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
