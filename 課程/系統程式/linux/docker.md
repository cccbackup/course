# docker 

## 基本觀念

* Image : 系統映像 (某個已儲存的版本）
* Container : 容器 （某個執行中的版本）

## 指令列表

* [電子書: 全面易懂的Docker指令大全](https://joshhu.gitbooks.io/dockercommands/content/) (超讚！）
    * [Container指令基礎](https://joshhu.gitbooks.io/dockercommands/content/Containers/ContainersBasic.html)

```
-t：attach時Container的螢幕會接到原來的螢幕上。
-i：attach時鍵盤輸入會被Container接手
-d：背景執行 (demon)

$ docker run -it --name test busybox
```

## 參考

* 參考： [Ubuntu Linux 安裝 Docker 步驟與使用教學](https://blog.gtwang.org/virtualization/ubuntu-linux-install-docker-tutorial/)
* 書：Docker —— 從入門到實踐
    * https://philipzheng.gitbooks.io/docker_practice/
* [docker中如何删除image（镜像）](http://yaxin-cn.github.io/Docker/how-to-delete-a-docker-image.html)

## 安裝

```
$ sudo apt-get install docker.io
$ service docker status
$ sudo usermod -aG docker <username> // 然後登出後再重新登入 （如果是系統管理員帳號就不用做）
$ docker version
$ docker search ubuntu
$ docker pull ubuntu
$ docker images
```

## 執行

```
$ docker run ubuntu /bin/echo 'Hello world'
$ docker run -i -t ubuntu
```


## 使用


```
$ docker run -t -i node/riscv /bin/bash
.. 進入 docker 操作 ...

$ docker ps -l    列出最新執行版
CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS                     PORTS               NAMES
4a7f5447b4b5        node/riscv          "/bin/bash"         About a minute ago   Exited (0) 9 seconds ago                       naughty_kowalevski

$ docker ps -a   列出所有執行版
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                       PORTS               NAMES
4a7f5447b4b5        node/riscv          "/bin/bash"         2 minutes ago       Exited (0) 51 seconds ago                        naughty_kowalevski
dc2393700ec1        node:carbon         "/bin/bash"         8 minutes ago       Up 8 minutes                                     objective_edison
93850632e972        node:carbon         "/bin/bash"         8 minutes ago       Exited (0) 8 minutes ago                         romantic_leavitt
5414b1135fcf        ubuntu              "/bin/bash"         2 hours ago         Up 2 hours                                       jolly_hawking
857c3b164321        node:carbon         "/bin/bash"         12 months ago       Exited (0) 12 months ago                         zealous_mahavira
02847d7babe8        ubuntu:latest       "/bin/bash"         12 months ago       Exited (255) 12 months ago                       agitated_yonath


$ docker commit dc2393 node/riscv  將該執行儲存 ...
```

## History

* riscv history -- 

```
495  git clone https://github.com/riscv/riscv-tools.git
  496  which riscv64-unknown-elf-gcc
  497  ln -s /usr/local/bin/riscv64gcc /usr/local/bin/riscv64-unknown-elf-gcc
  498  ln -s /usr/local/bin/riscv64-unknown-elf-gcc /usr/local/bin/riscv64gcc
  499  riscv64gcc
  500  docker images
  501  docker ps 
  502  docker ps -l
  503  docker login
  504  docker commit bacbb ccc/riscv
  505  docker tag cccriscv ccc/riscv
  506  docker tag cccriscv ccckmit/ccc/riscv
  507  docker tag bacbb ccc/riscv
  508  docker tag e34bd ccc/riscv
  509  docker push ccc/riscv
  510  docker push ccckmit/ccc/riscv
  511  docker push ccckmit/ccc/riscv
  512  docker images
  513  docker images
  514  docker ps -l
  515  docker rename 8a11d ccckmit/riscv
  516  docker rename 8a11d cccriscv
  517  docker images
  518  docker ps -l
  519  docker commit 10818 cccriscv
  520  docker commit 8a11d cccriscv
  521  docker images
  522  docker push ccckmit/cccriscv
  523  docker push ccckmit/cccriscv:latest
  524  docker push cccriscv:latest
  525  docker push ccckmit/cccriscv:latest
  526  docker build -t ccckmit/cccriscv:latest .
  527  docker tag 22c66 docker.io/ccckmit/cccriscv
  528  docker push docker.io/ccckmit/cccriscv
  529  history

```

another

```
root@5fff36eeda8f:/home/c2riscv/example/01-hello# history

   10  vim /home/.bashrc
   11  source /home/.bashrc
   13  ln -s riscv64-unknown-elf-gcc riscv64gcc

   24  git clone https://github.com/cccbook/c2riscv.git
   25  cd c2riscv/
   26  ls
   27  cd example

   31  riscv64gcc hello.c -o hello.o
   32  ./hello.o
   33  spike pk hello.o
   34  cat /home/.bashrc
   35  history

```
