FROM ubuntu:14.04

RUN apt-get install wget -yq
RUN wget -q http://repos.sensuapp.org/apt/pubkey.gpg -O- | sudo apt-key add -
RUN echo "deb     http://repos.sensuapp.org/apt sensu main" > /etc/apt/sources.list.d/sensu.list

RUN apt-get update
RUN apt-get install sensu -yq

RUN \
  apt-get update && \
  apt-get install -y ruby ruby-dev ruby-bundler && \
  gem install sensu-plugin --no-rdoc --no-ri && \
  rm -rf /var/lib/apt/lists/*

ADD http://sensuapp.org/docs/0.20/files/check-memory.sh /opt/sensu/plugins/check-memory.sh
RUN chmod +x /opt/sensu/plugins/check-memory.sh

RUN chown -R sensu:sensu /etc/sensu
CMD [ "/opt/sensu/bin/sensu-client", "-v", "-c", "/etc/sensu/config.json" ]
