# https://docs.docker.com/engine/reference/builder/ 
FROM httpd:2.4.57

RUN ["apt-get", "update"]

# code
RUN ["apt-get", "install", "-y",  "git"]
RUN ["git", "clone", "https://github.com/dMario24/dMario24.github.io.git", "/usr/local/apache2/app/blog"]
#RUN ["git", "clone", "https://github.com/diginori/diginori.github.io", "/usr/local/apache2/app/blog"]

# change apache2 conf
COPY ["httpd.conf", "/usr/local/apache2/conf/"]

# cron
RUN ["apt-get", "install", "-y", "cron"]
COPY ["pull.sh", "/usr/local/apache2/app/blog/"]
COPY ["blog-pull-cronjob", "/etc/cron.d/blog-pull-cronjob"]
RUN ["crontab", "/etc/cron.d/blog-pull-cronjob"]

# Just once at the end
CMD service cron start;httpd-foreground
