FROM ruby:2.6.0 as build

COPY rails-example-project /mydir/rails-example-project 
 
WORKDIR /mydir/rails-example-project  

RUN apt-get update && apt-get install -y nodejs && \
    gem install bundler && \
    bundle install && \
    rails db:migrate && \
    rm -rf /var/lib/apt/lists/* && \ 
    useradd -m app 

USER app

CMD rails s
