FROM centos:centos7
# Ajustar os repositórios para usar o Vault do CentOS 7
RUN sed -i 's|mirrorlist|#mirrorlist|g' /etc/yum.repos.d/CentOS-Base.repo && \
    sed -i 's|#baseurl|baseurl|g' /etc/yum.repos.d/CentOS-Base.repo && \
    sed -i 's|http://mirror.centos.org|http://vault.centos.org|g' /etc/yum.repos.d/CentOS-Base.repo && \
    yum clean all
RUN yum -y update \
    && yum -y install httpd mod_ssl mod_ldap \
    && yum -y clean all

COPY httpd-foreground /usr/local/bin/
COPY etc-httpd/ /etc/httpd/
COPY var-www-html/ /var/www/html/

RUN chmod +x /usr/local/bin/httpd-foreground

EXPOSE 80 443

CMD ["httpd-foreground"]