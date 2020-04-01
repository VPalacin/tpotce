<<<<<<< HEAD
FROM alpine 
=======
FROM alpine:latest 
>>>>>>> be1a90524a9a12693fd2f46c2f7fc1bc18825bfe
#
# Include dist
ADD dist/ /root/dist/
#
# Install packages
<<<<<<< HEAD
RUN apk -U add \
=======
RUN sed -i 's/dl-cdn/dl-2/g' /etc/apk/repositories && \
    apk -U add \
>>>>>>> be1a90524a9a12693fd2f46c2f7fc1bc18825bfe
            git \
            libcap \
            python3 \
            python3-dev && \
#
# Install adbhoney from git
    git clone --depth=1 https://github.com/huuck/ADBHoney /opt/adbhoney && \
    cp /root/dist/adbhoney.cfg /opt/adbhoney && \
    sed -i 's/dst_ip/dest_ip/' /opt/adbhoney/adbhoney/core.py && \
    sed -i 's/dst_port/dest_port/' /opt/adbhoney/adbhoney/core.py && \
#
# Setup user, groups and configs
    addgroup -g 2000 adbhoney && \
    adduser -S -H -s /bin/ash -u 2000 -D -g 2000 adbhoney && \
    chown -R adbhoney:adbhoney /opt/adbhoney && \
<<<<<<< HEAD
    setcap cap_net_bind_service=+ep /usr/bin/python3.7 && \
=======
    setcap cap_net_bind_service=+ep /usr/bin/python3.8 && \
>>>>>>> be1a90524a9a12693fd2f46c2f7fc1bc18825bfe
#
# Clean up
    apk del --purge git \
                    python3-dev && \
    rm -rf /root/* && \
    rm -rf /var/cache/apk/*
#
# Set workdir and start adbhoney
STOPSIGNAL SIGINT
USER adbhoney:adbhoney
WORKDIR /opt/adbhoney/
CMD nohup /usr/bin/python3 run.py
