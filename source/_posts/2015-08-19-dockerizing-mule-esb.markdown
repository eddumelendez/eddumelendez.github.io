---
layout: post
title: "Dockerizing Mule ESB"
date: 2015-08-19 00:10:00 -0500
comments: true
categories: [mule, esb, docker]
---
## Creating a Dockerfile for MuleESB

Let's create our `Dockerfile`

```
vim Dockerfile
```

We will build our Mule ESB Standalone Server image based on java version 8 from [Docker Hub Java](https://registry.hub.docker.com/_/java/) repository. More info about [FROM](https://docs.docker.com/docker/reference/builder/#from)

```
FROM java:8
```

We will use two environment variables `MULE_HOME` and `MULE_VERSION`, which will be used in our `Dockerfile`. More info about [ENV](https://docs.docker.com/docker/reference/builder/#env)

```
ENV MULE_HOME /opt/mule

ENV MULE_VERSION 3.7.0
```

Now, we need to download the latest version of Mule Standalone Server from Mulesoft's repository in `/opt` folder, unzip it and rename the folder to `mule`. Additionally, zip file will be deleted. Since, we are running over Linux (Ubuntu) we can use some useful commands. More info about [RUN](https://docs.docker.com/docker/reference/builder/#run)

```
RUN set -x \
        && cd /opt \
        && curl -o mule.zip https://repository.mulesoft.org/nexus/content/repositories/releases/org/mule/distributions/mule-standalone/$MULE_VERSION/mule-standalone-$MULE_VERSION.zip \
        && unzip mule.zip \
        && mv mule-standalone-$MULE_VERSION mule \
        && rm mule.zip*
```

Then, we will locate at `$MULE_HOME` folder. More info about [WORKDIR](https://docs.docker.com/docker/reference/builder/#workdir)

```
WORKDIR $MULE_HOME
```

Now, we will expose some folder inside of mule in order to have access from outside of docker container. More info about [VOLUME](https://docs.docker.com/docker/reference/builder/#volume)

```
VOLUME $MULE_HOME/apps
VOLUME $MULE_HOME/conf
VOLUME $MULE_HOME/domains
VOLUME $MULE_HOME/logs
```

Finally, we need to start the server. More info about [ENTRYPOINT](https://docs.docker.com/docker/reference/builder/#entrypoint)

```
ENTRYPOINT ["./bin/mule"]
```

Our final `Dockerfile` looks like this

```
FROM java:8

MAINTAINER Eddú Meléndez <eddu.melendez@gmail.com>

ENV MULE_HOME /opt/mule

ENV MULE_VERSION 3.7.0

RUN set -x \
        && cd /opt \
        && curl -o mule.zip https://repository.mulesoft.org/nexus/content/repositories/releases/org/mule/distributions/mule-standalone/$MULE_VERSION/mule-standalone-$MULE_VERSION.zip \
        && unzip mule.zip \
        && mv mule-standalone-$MULE_VERSION mule \
        && rm mule.zip*

WORKDIR $MULE_HOME

VOLUME $MULE_HOME/apps
VOLUME $MULE_HOME/conf
VOLUME $MULE_HOME/domains
VOLUME $MULE_HOME/logs

ENTRYPOINT ["./bin/mule"]
```

## Building the MuleESB Docker image

In order to have the image available in your local machine we just need to execute the command below:

```
docker build --tag eddumelendez/mule  .
```

## Running the MuleESB Docker image

```
docker run -ti eddumelendez/mule
```

You can find the final example on my github repository [docker-mule](https://github.com/eddumelendez/docker-mule)
