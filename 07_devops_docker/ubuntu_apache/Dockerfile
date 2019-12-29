FROM badmac/sshd:dockerfile
MAINTAINER from www.atos.net by MaChun (chun.ma@atos.net)

# 设置环境变量：所有操作都是非交互式
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get -yq install apache2 && rm -rf /var/lib/apt/lists/*

# 更改系统时区
RUN apt-get update
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN echo "Asia/Shanghai" > /etc/timezone
RUN apt-get -yq install tzdata
RUN dpkg-reconfigure -f noninteractive tzdata

	
# 添加脚本并设置权限
ADD run.sh /run.sh
RUN chmod 755 /run.sh

# 添加一个示例web站点
RUN mkdir -p /var/run/apache2
RUN mkdir -p /var/lock/apache2 
RUN mkdir -p /app && rm -rf /var/www/html && ln -s /app /var/www/html
COPY sample/ /app

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR  /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR  /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_SERVERADMIN  admin@localhost
ENV APACHE_SERVERNAME   localhost
ENV APACHE_SERVERALIAS  docker.localhost
ENV APACHE_DOCUMENTROOT /var/www

RUN echo "ServerName ${APACHE_SERVERNAME}" >> /etc/apache2/apache2.conf

EXPOSE 80
WORKDIR /app
CMD ["/run.sh"]

