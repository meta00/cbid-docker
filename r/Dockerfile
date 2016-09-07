FROM cbid-base
ENV R_BASE_VERSION = 3.2.3
USER root
RUN apt-get update \
        && apt-get install -y --no-install-recommends \
                littler \
                r-cran-littler \
                r-base \
#               r-base-dev=${R_BASE_VERSION}* \
#               r-recommended=${R_BASE_VERSION}* \
        && echo 'options(repos = c(CRAN = "https://cran.rstudio.com/"), download.file.method = "libcurl")' >> /etc/R/Rprofile.site \
        && echo 'source("/etc/R/Rprofile.site")' >> /etc/littler.r \
        && ln -s /usr/share/doc/littler/examples/install.r /usr/local/bin/install.r \
        && ln -s /usr/share/doc/littler/examples/install2.r /usr/local/bin/install2.r \
        && ln -s /usr/share/doc/littler/examples/installGithub.r /usr/local/bin/installGithub.r \
        && ln -s /usr/share/doc/littler/examples/testInstalled.r /usr/local/bin/testInstalled.r \
        && install.r docopt \
        && rm -rf /tmp/downloaded_packages/ /tmp/*.rds \
        && rm -rf /var/lib/apt/lists/*
# Rstudio server

RUN rm -rf /var/lib/apt/lists/ \
 	&& apt-get update \
  	&& VER=$(wget --no-check-certificate -qO- https://s3.amazonaws.com/rstudio-server/current.ver) \
  	&& wget -q http://download2.rstudio.org/rstudio-server-${VER}-amd64.deb \
  	&& dpkg -i rstudio-server-${VER}-amd64.deb \
  	&& rm rstudio-server-*-amd64.deb \
  	&& ln -s /usr/lib/rstudio-server/bin/pandoc/pandoc /usr/local/bin \
  	&& ln -s /usr/lib/rstudio-server/bin/pandoc/pandoc-citeproc /usr/local/bin \
  	&& wget https://github.com/jgm/pandoc-templates/archive/1.15.0.6.tar.gz \
	&& mkdir -p /opt/pandoc/templates && tar zxf 1.15.0.6.tar.gz \
  	&& cp -r pandoc-templates*/* /opt/pandoc/templates && rm -rf pandoc-templates* \
  	&& mkdir /root/.pandoc && ln -s /opt/pandoc/templates /root/.pandoc/templates 
#COPY userconf.sh /etc/cont-init.d/conf
#COPY run.sh /etc/services.d/rstudio/run

EXPOSE 8787

## Expose a default volume for Kitematic
VOLUME /home/rstudio

# R shiny server
RUN wget --no-verbose https://s3.amazonaws.com/rstudio-shiny-server-os-build/ubuntu-12.04/x86_64/VERSION -O "version.txt" && \
    VERSION=$(cat version.txt)  && \
    wget --no-verbose "https://s3.amazonaws.com/rstudio-shiny-server-os-build/ubuntu-12.04/x86_64/shiny-server-$VERSION-amd64.deb" -O ss-latest.deb && \
    gdebi -n ss-latest.deb && \
    rm -f version.txt ss-latest.deb && \
    cp -R /usr/local/lib/R/site-library/shiny/examples/* /srv/shiny-server/

EXPOSE 3838

COPY shiny-server.sh /usr/bin/shiny-server.sh
# CMD ["/usr/bin/shiny-server.sh"]
