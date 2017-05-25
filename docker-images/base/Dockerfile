FROM golang:1.8

RUN go version

RUN apt-get update; apt-get install -y \
    bundler \
    jq \
    rsync \
    unzip \
    vim

# get v3 protoc from github, it was in beta at the time of writing
RUN cd /tmp \
 && wget https://github.com/google/protobuf/releases/download/v3.0.0-beta-2/protoc-3.0.0-beta-2-linux-x86_64.zip \
 && unzip *.zip \
 && cp ./protoc /usr/local/bin/

RUN go get -d github.com/cloudfoundry/bosh-cli && go build -o $GOPATH/bin/bosh github.com/cloudfoundry/bosh-cli
RUN curl -L "https://cli.run.pivotal.io/stable?release=debian64&source=github" > cf.deb && dpkg -i ./cf.deb

RUN go get github.com/onsi/ginkgo/ginkgo
RUN git config --global user.email "cf-loggregator@pivotal.io" && git config --global user.name "Loggregator CI"