FROM centos:7
MAINTAINER yodaaut

# for systemd
ENV container docker

COPY ./etc/pki/ca-trust/source/anchors/*.crt /etc/pki/ca-trust/source/anchors/
RUN update-ca-trust
RUN echo 'check environment http_proxy'
RUN echo ${http_proxy}
RUN yum -y update
RUN yum -y install https://packages.icinga.org/epel/7/release/noarch/icinga-rpm-release-7-1.el7.centos.noarch.rpm
RUN yum -y install epel-release
RUN yum -y install vim									\
									 vim-enhanced					\
									 htop									\
									 hostname							\
									 bind-utils						\
									 cronie								\
									 logrotate						\
									 supervisor						\
									 openssh							\
									 openssh-server				\
									 openssh-client				\
									 rsyslog							\
									 sudo									\
									 passwd								\
									 sed									\
									 which								\
									 pwgen								\
									 psmisc								\
#									 mailx								\
#									 httpd								\
#									 nagios-plugins-all		\
#									 mariadb-server				\
#									 mariadb-libs					\
#									 mariadb							\
									 ;


RUN yum -y install --enablerepo=icinga-snapshot-builds		\
									 icinga2																\
#									 icinga2-doc														\
#									 icinga2-ido-mysql											\
#									 icingaweb2															\
#									 icingacli															\
#									 php-ZendFramework											\
#									 php-ZendFramework-Db-Adapter-Pdo-Mysql	\
#									 php-ZendFramework-Db-Adapter-Pdo-Pgsql	\
									 ;

RUN icinga2 api setup
RUN sed -i -e 's/^.* NodeName = .*/const NodeName = "docker-icinga2"/gi' \
				/etc/icinga2/constants.conf;			\
				icinga2 pki new-cert	\
				--cn docker-icinga2	\
			 	--key	/etc/icinga2/pki/docker-icinga2.key		\
				--csr /etc/icinga2/pki/docker-icinga2.csr;	\
				icinga2 pki sign-csr	\
				--csr /etc/icinga2/pki/docker-icinga2.csr		\
				--cert /etc/icinga2/pki/docker-icinga2.crt;

ADD content/ /
#RUN chmod u+x /opt/icinga2/initdocker
