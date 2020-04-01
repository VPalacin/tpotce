FROM alpine
#
# Include dist
ADD dist/ /root/dist/
#
# Get and install dependencies & packages
<<<<<<< HEAD
RUN apk -U add \
=======
RUN sed -i 's/dl-cdn/dl-2/g' /etc/apk/repositories && \
    apk -U add \
>>>>>>> be1a90524a9a12693fd2f46c2f7fc1bc18825bfe
                       bash \
                       build-base \
                       git \
                       gmp-dev \
                       libcap \
                       libffi-dev \
                       mpc1-dev \
                       mpfr-dev \
                       openssl \
                       openssl-dev \
                       python3 \
                       python3-dev \
                       py3-bcrypt \
		       py3-mysqlclient \
                       py3-requests \
                       py3-setuptools && \
#
# Setup user
    addgroup -g 2000 cowrie && \
    adduser -S -s /bin/ash -u 2000 -D -g 2000 cowrie && \
#
# Install cowrie
    mkdir -p /home/cowrie && \
    cd /home/cowrie && \
<<<<<<< HEAD
    git clone --depth=1 https://github.com/micheloosterhof/cowrie -b v2.0.0 && \
=======
    git clone --depth=1 https://github.com/micheloosterhof/cowrie -b v2.0.2 && \
>>>>>>> be1a90524a9a12693fd2f46c2f7fc1bc18825bfe
    cd cowrie && \
    mkdir -p log && \
    pip3 install --upgrade pip && \
    pip3 install --upgrade -r requirements.txt && \
#
# Setup configs
<<<<<<< HEAD
    setcap cap_net_bind_service=+ep /usr/bin/python3.7 && \
    cp /root/dist/cowrie.cfg /home/cowrie/cowrie/cowrie.cfg && \
    chown cowrie:cowrie -R /home/cowrie/* /usr/lib/python3.7/site-packages/twisted/plugins && \
=======
    export PYTHON_DIR=$(python3 --version | tr '[A-Z]' '[a-z]' | tr -d ' ' | cut -d '.' -f 1,2 ) && \
    setcap cap_net_bind_service=+ep /usr/bin/$PYTHON_DIR && \
    cp /root/dist/cowrie.cfg /home/cowrie/cowrie/cowrie.cfg && \
    chown cowrie:cowrie -R /home/cowrie/* /usr/lib/$PYTHON_DIR/site-packages/twisted/plugins && \
>>>>>>> be1a90524a9a12693fd2f46c2f7fc1bc18825bfe
#
# Start Cowrie once to prevent dropin.cache errors upon container start caused by read-only filesystem
    su - cowrie -c "export PYTHONPATH=/home/cowrie/cowrie:/home/cowrie/cowrie/src && \
                    cd /home/cowrie/cowrie && \
                    /usr/bin/twistd --uid=2000 --gid=2000 -y cowrie.tac --pidfile cowrie.pid cowrie &" && \
    sleep 10 && \
#
# Clean up
    apk del --purge build-base \
                    git \
                    gmp-dev \
                    libcap \
                    libffi-dev \
                    mpc1-dev \
                    mpfr-dev \
                    openssl-dev \
                    python3-dev \
                    py3-mysqlclient && \
    rm -rf /root/* /tmp/* && \
    rm -rf /var/cache/apk/* && \
<<<<<<< HEAD
    rm -rf /home/cowrie/cowrie/cowrie.pid
=======
    rm -rf /home/cowrie/cowrie/cowrie.pid && \
    unset PYTHON_DIR
>>>>>>> be1a90524a9a12693fd2f46c2f7fc1bc18825bfe
#
# Start cowrie
ENV PYTHONPATH /home/cowrie/cowrie:/home/cowrie/cowrie/src
WORKDIR /home/cowrie/cowrie
USER cowrie:cowrie
CMD ["/usr/bin/twistd", "--nodaemon", "-y", "cowrie.tac", "--pidfile", "/tmp/cowrie/cowrie.pid", "cowrie"]
