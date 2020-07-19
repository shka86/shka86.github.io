ubuntuにdocker導入
===

dockerの説明って、超入門的なのがなくないか？と思ってとりあえず触ってみた記録。
いろいろやってみてわかったことは、dockerってのは試行錯誤してもすぐに振出しに戻れるってこと。

インストール
---
1. sudo apt install docker
1. sudo apt install docker.io
1. docker -v

ご挨拶する
---
1. sudo docker run hello-world

        Unable to find image 'hello-world:latest' locally
        latest: Pulling from library/hello-world
        1b930d010525: Pull complete 
        Digest: sha256:d1668a9a1f5b42ed3f46b70b9cb7c88fd8bdc8a2d73509bb0041cf436018fbf5
        Status: Downloaded newer image for hello-world:latest

    → hello-worldコンテナがなかったのでdocker hubから取得してきたよ

        Hello from Docker!
        This message shows that your installation appears to be working correctly.

        To generate this message, Docker took the following steps:
         1. The Docker client contacted the Docker daemon.
         2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
            (amd64)
         3. The Docker daemon created a new container from that image which runs the
            executable that produces the output you are currently reading.
         4. The Docker daemon streamed that output to the Docker client, which sent it
            to your terminal.

        To try something more ambitious, you can run an Ubuntu container with:
         $ docker run -it ubuntu bash

        Share images, automate workflows, and more with a free Docker ID:
         https://hub.docker.com/

        For more examples and ideas, visit:
         https://docs.docker.com/get-started/


ご機嫌伺いする
---

    $ sudo docker ps -a


サヨナラする
---

- コンテナの削除

        $ sudo docker rm b1de95d065fa



- イメージの削除

        $ sudo docker rmi hello-world



pythonの開発環境を作る
---

- イメージを取得

        sudo docker pull python

- コンテナを起動

        sudo docker run -it -w /app -v $(pwd):/app python bash

    これで python -V すると最新版が見えるはず。
    コンテナ起動前とバージョンが違っているっはず。

- aptでsphinxを導入する

        apt install python3-sphinx




centos6を導入
---

1. imageとってくる

        sudo docker pull centos:centos6


1. imageの確認

        sudo docker images

1. imageの詳細

        sudo docker inspect centos:centos6



1. containerの起動

        centos6上でこんにちは
        sudo docker run centos:centos6 echo "hello world"

        動いたかの確認
        sudo docker ps -a
        Exit(0)は正常終了

        containerの中で作業する

        sudo docker run -it centos


1. containerの削除


        sudo docker rm <container>


1. containerで作業する

        sudo docker run -it centos bash
        とか
        sudo docker run -it -w /app -v $(pwd):/app python bash
        とか

        抜けるには
        exit
        再開するには
        sudo docker start <CONTAINER ID>
        sudo docker attach <CONTAINER ID>

1. 何かしらいじったcontainerをimageにする

        sudo docker commit <container ID> username/hogehoge

1. dockerのimageをファイルにして持ち歩く save/load

githubにあげてもいいかもしんない。

        sudo docker save <image name> -o <filename>
        tarballができる

        sudo docker load -i <filename>


### そのcentos6の中に

- pythonを導入する

        yum install xz
        tar xvf Python-3.8.1.tar.xz


- docker環境を導入する

        yum install epel-release

        tee /etc/yum.repos.d/docker.repo <<- 'EOF'
        [dockerrepo]
        name=Docker Repository
        baseurl=https://yum.dockerproject.org/repo/main/centos/$releasever/
        enabled=1
        gpgcheck=1
        gpgkey=https://yum.dockerproject.org/gpg
        EOF

        yum install docker-engine

        service docker start

        sh -c "curl -L https://github.com/docker/compose/releases/download/1.5.2/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose"



