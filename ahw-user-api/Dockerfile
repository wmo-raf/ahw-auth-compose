FROM node:12-bullseye

ENV NAME ahw-user-api
ENV USER microservice

RUN apt-get update -y && apt-get upgrade -y && \
    apt-get install -y bash git ssh python3 make

RUN addgroup $USER && useradd -ms /bin/bash $USER -g $USER
RUN yarn global add bunyan

RUN mkdir -p /opt/$NAME/

ADD https://github.com/ufoscout/docker-compose-wait/releases/download/2.2.1/wait /wait
RUN chmod +x /wait

RUN git clone https://github.com/wmo-raf/ahw-user-api.git /opt/$NAME

COPY --chown=$USER:$USER entrypoint.sh /opt/$NAME/entrypoint.sh

WORKDIR /opt/$NAME

RUN yarn install

# Tell Docker we are going to use this ports
EXPOSE 3001

CMD /wait

USER $USER

ENTRYPOINT ["./entrypoint.sh"]
