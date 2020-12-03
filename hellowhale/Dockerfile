# Grab the apache image
FROM httpd:latest

# Set some environment variables
ENV TZ=EST

# Copy resources into place
COPY wrapper.sh /
COPY html /usr/local/apache2/htdocs
COPY httpd.conf /usr/local/apache2/conf/httpd.conf

# Run some commands
RUN apt-get update && apt-get install -y \
    git python3 vim net-tools 
RUN apt upgrade -y
RUN git clone https://github.com/mubaris/motivate.git
RUN (cd motivate/motivate; ./install.sh; . ~/.bashrc)
RUN (cd; /usr/local/bin/motivate --no-colors > /usr/local/apache2/htdocs/motivation.txt)

# Fire up the daemon via the wrapper
CMD ["/wrapper.sh"]
