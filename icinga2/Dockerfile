FROM centos:7
MAINTAINER yodaaut

COPY ./etc/pki/ca-trust/source/anchors/*.crt /etc/pki/ca-trust/source/anchors/
RUN update-ca-trust
RUN echo 'check environment http_proxy'
RUN echo ${http_proxy}
RUN yum update -y
RUN yum install -y https://packages.icinga.org/epel/7/release/noarch/icinga-rpm-release-7-1.el7.centos.noarch.rpm
