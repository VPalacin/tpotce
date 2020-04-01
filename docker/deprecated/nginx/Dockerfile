<<<<<<< HEAD:docker/nginx/Dockerfile
FROM alpine
=======
FROM alpine:latest
>>>>>>> be1a90524a9a12693fd2f46c2f7fc1bc18825bfe:docker/deprecated/nginx/Dockerfile
#
# Include dist
ADD dist/ /root/dist/
#
# Get and install dependencies & packages
RUN apk -U --no-cache add \
                       nginx \
                       nginx-mod-http-headers-more && \
#
# Setup configs
    mkdir -p /run/nginx && \
    rm -rf /etc/nginx/conf.d/* /usr/share/nginx/html/* && \
    cp /root/dist/conf/nginx.conf /etc/nginx/ && \
    cp -R /root/dist/conf/ssl /etc/nginx/ && \
    cp /root/dist/conf/tpotweb.conf /etc/nginx/conf.d/ && \
    cp -R /root/dist/html/ /var/lib/nginx/ && \
#
# Clean up
    rm -rf /root/* && \
    rm -rf /var/cache/apk/*
#
# Start nginx
CMD exec nginx -g 'daemon off;'
