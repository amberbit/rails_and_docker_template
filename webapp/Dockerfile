FROM phusion/baseimage:0.9.22
CMD ["/sbin/my_init"]

RUN add-apt-repository -y ppa:brightbox/ruby-ng

RUN apt-get update
RUN apt-get install -y libpq-dev git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libxml2-dev libxslt1-dev libcurl4-openssl-dev software-properties-common libffi-dev nodejs wget autoconf tzdata ruby2.4 ruby2.4-dev rubygems ruby-switch
RUN ruby-switch --set ruby2.4
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN rm -rf /var/lib/gems/2.4.1/cache/*

RUN adduser --disabled-password --gecos "" webapp

RUN mkdir /webapp

WORKDIR /webapp

ADD Gemfile /webapp/Gemfile
ADD Gemfile.lock /webapp/Gemfile.lock

RUN chown -R webapp.webapp /webapp

USER webapp
WORKDIR /webapp

RUN echo "gem: --user-install --env-shebang --no-rdoc --no-ri" > /home/webapp/.gemrc
ENV PATH /home/webapp/.gem/ruby/2.4.0/bin:$PATH
ENV GEM_HOME /home/webapp/.gem/ruby/2.4.0

RUN gem install bundler
RUN gem install rake
RUN bundle install
ADD . /webapp