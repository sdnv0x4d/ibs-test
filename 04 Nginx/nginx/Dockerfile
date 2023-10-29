FROM nginx:bookworm
MAINTAINER sdnv

RUN apt update && \
    apt install curl certbot python3 -y 

RUN echo "authenticator = manual" >> /etc/letsencrypt/cli.ini && \
    curl -L https://github.com/joohoi/acme-dns-certbot-joohoi/raw/master/acme-dns-auth.py --output /etc/letsencrypt/acme-dns-auth.py && \
    chmod +x /etc/letsencrypt/acme-dns-auth.py && \
    ln -s /usr/bin/python3 /usr/bin/python

COPY ./letsencrypt /etc/letsencrypt

ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["nginx","-g","daemon off;"]
