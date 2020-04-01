<<<<<<< HEAD
FROM alpine:3.10
=======
FROM alpine:latest
>>>>>>> be1a90524a9a12693fd2f46c2f7fc1bc18825bfe
#
# Get and install dependencies & packages
RUN sed -i 's/dl-cdn/dl-2/g' /etc/apk/repositories && \
    apk -U --no-cache add \
            build-base \
            curl \
            git \
<<<<<<< HEAD
=======
	    jpeg-dev \
>>>>>>> be1a90524a9a12693fd2f46c2f7fc1bc18825bfe
	    libffi-dev \
            libxml2 \
            libxml2-dev \
            libxslt \
            libxslt-dev \
	    musl \
	    musl-dev \
	    openjpeg-dev \
            openssl \
            openssl-dev \
<<<<<<< HEAD
            python \
            python-dev \
	    py-cffi \
	    py-pillow \
            py-future \
            py-pip \
            swig && \
=======
            python3 \
            python3-dev \
	    py-cffi \
	    py-pillow \
            py-future \
            py3-pip \
            swig \
	    tinyxml \
	    tinyxml-dev \
	    zlib-dev && \
>>>>>>> be1a90524a9a12693fd2f46c2f7fc1bc18825bfe
#
# Setup user
    addgroup -g 2000 spiderfoot && \
    adduser -S -s /bin/ash -u 2000 -D -g 2000 spiderfoot && \
#
# Install spiderfoot 
<<<<<<< HEAD
#    git clone --depth=1 https://github.com/smicallef/spiderfoot -b v2.12.0-final /home/spiderfoot && \
    git clone --depth=1 https://github.com/smicallef/spiderfoot /home/spiderfoot && \
    cd /home/spiderfoot && \
    pip install --no-cache-dir openxmllib wheel && \ 
    pip install --no-cache-dir -r requirements.txt && \ 
=======
    git clone --depth=1 https://github.com/smicallef/spiderfoot /home/spiderfoot && \
    cd /home/spiderfoot && \
    pip3 install --no-cache-dir wheel && \ 
    pip3 install --no-cache-dir -r requirements.txt && \ 
>>>>>>> be1a90524a9a12693fd2f46c2f7fc1bc18825bfe
    chown -R spiderfoot:spiderfoot /home/spiderfoot && \
    sed -i "s#'__docroot': ''#'__docroot': '\/spiderfoot'#" /home/spiderfoot/sf.py && \
    sed -i 's#raise cherrypy.HTTPRedirect("\/")#raise cherrypy.HTTPRedirect("\/spiderfoot")#' /home/spiderfoot/sfwebui.py && \
#
# Clean up
    apk del --purge build-base \
                    gcc \
                    git \
		    libffi-dev \
                    libxml2-dev \
                    libxslt-dev \
		    musl-dev \
                    openssl-dev \
                    python3-dev \
                    py3-pip \
		    swig \
		    tinyxml-dev && \
    rm -rf /var/cache/apk/*
#
# Healthcheck
<<<<<<< HEAD
HEALTHCHECK --retries=10 CMD curl -s -XGET 'http://127.0.0.1:8080'
=======
#HEALTHCHECK --retries=10 CMD curl -s -XGET 'http://127.0.0.1:8080'
HEALTHCHECK --retries=10 CMD curl -s -XGET 'http://127.0.0.1:8080/spiderfoot/'
>>>>>>> be1a90524a9a12693fd2f46c2f7fc1bc18825bfe
#
# Set user, workdir and start spiderfoot
USER spiderfoot:spiderfoot
WORKDIR /home/spiderfoot
CMD ["/usr/bin/python3.8", "sf.py","-l", "0.0.0.0:8080"]
