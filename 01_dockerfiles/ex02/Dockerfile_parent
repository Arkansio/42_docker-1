FROM ruby:2.3.7

ONBUILD COPY ./app/ /opt/app/

ONBUILD WORKDIR /opt/app

RUN apt-get update
RUN apt-get install -y rails
RUN gem install bundler -v 2.0.1
ONBUILD RUN bundler install
ONBUILD RUN rake db:migrate
ONBUILD RUN rake db:seed
