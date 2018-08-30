FROM waelrash1/shiny-srv-rstudio3.5.1

COPY shiny-server.sh /usr/bin/shiny-server.sh
COPY setup.sh /usr/bin/package-setup.sh
COPY packages.R /usr/bin/packages.R
# execute at the build time -- installing all required packages for forcasting/visualisation 
# Packages are descriped in packages.R file
#CMD cd /usr/bin
CMD /bin/bash /usr/bin/package-setup.sh /usr/bin/packages.R
# insall any extra packages/ ensure the installation
#ENTRYPOINT ["/bin/bash"]
#CMD ["/usr/bin/package-setup.sh", "/usr/bin/packages.R"]
COPY shiny-server.sh /usr/bin/shiny-server.sh
CMD ["/usr/bin/shiny-server.sh"]