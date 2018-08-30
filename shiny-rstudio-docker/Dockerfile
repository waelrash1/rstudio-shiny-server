FROM rocker/rstudio
## Work-around to make Docker Hub use the Dockerfile from https://github.com/rocker-org/rocker-versioned/rstudio
RUN apt-get update && apt-get install -y \
    sudo \
    gdebi-core \
    pandoc \
    pandoc-citeproc \
    libcurl4-gnutls-dev \
    libcairo2-dev \
    libxt-dev \
    xtail \
    wget

# Download and install shiny server
RUN wget --no-verbose https://download3.rstudio.org/ubuntu-14.04/x86_64/VERSION -O "version.txt" && \
    VERSION=$(cat version.txt)  && \
    wget --no-verbose "https://download3.rstudio.org/ubuntu-14.04/x86_64/shiny-server-$VERSION-amd64.deb" -O ss-latest.deb && \
    gdebi -n ss-latest.deb && \
    rm -f version.txt ss-latest.deb && \
    . /etc/environment && \
    R -e "install.packages(c('shiny', 'rmarkdown'), repos='$MRAN')" && \
    cp -R /usr/local/lib/R/site-library/shiny/examples/* /srv/shiny-server/

EXPOSE 3838 8787

COPY shiny-server.sh /usr/bin/shiny-server.sh
#COPY setup.bash /usr/bin/package-setup.bash
#COPY packages.R /usr/bin/packages.R
CMD ["/usr/bin/shiny-server.sh"]
#CMD ["/usr/bin/package-setup.bash /usr/bin/packages.R"]