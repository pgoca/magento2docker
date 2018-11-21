FROM node:6.14.4-jessie

EXPOSE 6000

WORKDIR /
RUN apt-get upgrade && \
    curl --silent --location https://deb.nodesource.com/setup_6.x | bash - && \
    apt-get -f install npm && \
    echo 'Install gulp'; sleep 1 && \
    npm install gulp -g && \
    echo 'Install n'; sleep 1  && \
    npm install n -g && \
    echo 'Install n 6'; sleep 1 && \
    n 6.9.1
CMD ["npm", "run watch"]