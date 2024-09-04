FROM ubuntu

RUN apt-get update && \
    apt-get install -y build-essential git wget perl make 


RUN wget https://www.openssl.org/source/openssl-1.0.1f.tar.gz
RUN tar -xzf openssl-1.0.1f.tar.gz 


RUN cd openssl-1.0.1f && \
    ./config && \
    make depend && \
    make && \
    make install_sw


# Genera certificados y claves
RUN /openssl-1.0.1f/apps/openssl req -x509 -newkey rsa:2048 -keyout /key.pem -out /cert.pem -days 365 -nodes -subj "/C=ES/CN=www.example.com"

# Configura el contenedor para que ejecute el servidor OpenSSL
ENTRYPOINT ["/openssl-1.0.1f/apps/openssl", "s_server", "-key", "/key.pem", "-cert", "/cert.pem", "-accept", "4433", "-www"]

