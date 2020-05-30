# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "bento/ubuntu-18.04"

  config.vm.synced_folder ".", "/go/src/github.com/containernetworking/cni"

  config.vm.provision "shell", inline: <<-SHELL
    set -e -x -u

    apt-get update -y || (sleep 40 && apt-get update -y)
    apt-get install -y git

    wget -qO- https://dl.google.com/go/go1.13.11.linux-amd64.tar.gz | tar -C /usr/local -xz

    echo 'export GOPATH=/go; export PATH=/usr/local/go/bin:$GOPATH/bin:$PATH' >> /root/.bashrc
    eval `tail -n1 /root/.bashrc`

    go get github.com/onsi/ginkgo/ginkgo
    go get github.com/onsi/gomega/...

    cd /go/src/github.com/containernetworking/cni
  SHELL
end
