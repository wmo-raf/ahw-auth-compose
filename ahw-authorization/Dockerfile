FROM node:12-bullseye

ENV NAME ahw-auth
ENV USER microservice

RUN apt-get update -y && apt-get upgrade -y && \
    apt-get install -y bash git ssh python3 make

RUN addgroup $USER && useradd -ms /bin/bash $USER -g $USER
RUN yarn global add bunyan

RUN mkdir -p /opt/$NAME/

ADD https://github.com/ufoscout/docker-compose-wait/releases/download/2.2.1/wait /wait
RUN chmod +x /wait

WORKDIR /opt/$NAME

ARG repo_url
ARG repo_branch

RUN git clone $repo_url /opt/$NAME && git checkout $repo_branch

COPY --chown=$USER:$USER entrypoint.sh /opt/$NAME/entrypoint.sh

RUN yarn install

# Tell Docker we are going to use this ports
EXPOSE 3001

CMD /wait

USER $USER

ENTRYPOINT ["./entrypoint.sh"]
