FROM centos

# Set Proxy
# ENV http_proxy http://192.168.100.100:3128/

RUN yum update && yum install gcc zlib-devel yum-utils make jq curl wget -y && \
    wget http://mirror.centos.org/centos/7/os/x86_64/Packages/readline-devel-6.2-11.el7.x86_64.rpm && \
    yum install readline-devel-6.2-11.el7.x86_64.rpm -y
