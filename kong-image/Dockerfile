FROM kong:3.0.0-alpine

WORKDIR /usr/kong/

# switch to root to install opa plugin and rocks in /usr/local
USER root

RUN git clone https://github.com/ioannis-iordanidis/kong-axiomatics-plugin.git /tmp/kap \
&& cd /tmp/kap \
&& git checkout master \
&& mv /tmp/kap/kong/plugins/kong-axiomatics-plugin /usr/local/share/lua/5.1/kong/plugins/kong-axiomatics-plugin

ENV KONG_CUSTOM_PLUGINS=kong-axiomatics-plugin

#install dependencies
RUN apk update && \
  apk add gcc libc-dev && \
  luarocks install lua-cjson && \
  luarocks install lua-resty-jwt

WORKDIR /usr/kong/

#install phantom-token plugin
RUN git config --global url."https://".insteadOf git:// && \
    git config --global advice.detachedHead false && \
    luarocks install kong-phantom-token 2.0.0

# Prepare directory for the volume, so that proper permissions are applied
RUN mkdir /usr/local/kong/declarative && chown kong:kong /usr/local/kong/declarative

# back to kong user
USER kong
