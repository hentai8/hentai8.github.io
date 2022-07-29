---
layout: post
---




# ltc√√





## Dockerfile

```dockerfile
FROM ubuntu:20.04
LABEL maintainer="hentai8<496983136@qq.com>"

WORKDIR /home/ltc

COPY ./ ./

EXPOSE 9332
EXPOSE 9333
EXPOSE 9334

RUN ["/bin/bash", "-c", "bash ./run.sh"]
ENTRYPOINT [ "/bin/bash" ,"-c", "bash ./entrypoint.sh"]
```



## build

```
docker build -t hentai8/ltc:0.18.1.1 .
```





## run

```shell
docker run -d --network host -v 配置文件路径:/home/config/litecoin.conf -v 外部数据地址:/ltc-data hentai8/ltc:0.18.1.1
```



## config

```shell
root@node1:/home/config# cat litecoin.conf 
server=1
datadir=/ltc-data
```





高度获取

```shell
curl --user 账号:密码 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockcount", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9332/
```



# doge√√





## Dockerfile

```shell
FROM ubuntu:20.04
LABEL maintainer="hentai8<496983136@qq.com>"

WORKDIR /home/doge

COPY ./ ./

EXPOSE 22557
EXPOSE 22556
EXPOSE 22555

RUN ["/bin/bash", "-c", "bash ./run.sh"]
ENTRYPOINT [ "/bin/bash" ,"-c", "bash ./entrypoint.sh"]
```







## build

```
docker build -t hentai8/doge:1.14.4.1 .
```



## run

```shell
docker run -d --network host -v 配置文件路径:/home/config/dogecoin.conf -v 外部数据地址:/doge-data hentai8/doge:1.14.4.1
```





## config

```shell
root@node1:/home/config# cat dogecoin.conf 
server=1
datadir=/doge-data
```





高度获取

```shell
curl --user 账号:密码 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockcount", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:22555/
```





得瑟得瑟

```shell
curl
```



# dero√×



***<u>内核环境冲突</u>***



本地+wallet

![image-20210927150059670](C:\work\各币种节点docker化.assets\image-20210927150059670.png)



## Dockerfile

```dockerfile
FROM ubuntu:20.04
LABEL maintainer="hentai8<496983136@qq.com>"

WORKDIR /home/dero

COPY ./ ./

EXPOSE 20202
EXPOSE 20206
EXPOSE 20209

RUN ["/bin/bash", "-c", "bash ./run.sh"]
ENTRYPOINT [ "/bin/bash" ,"-c", "bash ./entrypoint.sh"]
```



## build

```
docker build -t hentai8/dero:2.2.1-0.0 .
```



## 

```
docker build -t hentai8/dero:2.2.1-0.1 .
```



## 

```
docker build -t hentai8/dero:2.2.1-0.2 .
```





## 

```
docker build -t hentai8/dero:2.2.1-0.3 .
```



## entrypoint

运行命令写在entrypoint.sh中，多个命令同时运行用``&``分隔

```shell
./derod-linux-amd64 --data-dir=/dero-data & ./dero-wallet-cli-linux-amd64 --daemon-address 47.100.40.199 --wallet-file /dero-wallet & tail -f /dev/null
```





```shell
./derod-linux-amd64 --data-dir=/dero-data & tail -f /dev/null
```



## run

```shell
docker run -d --network host -v 外部entrypoint.sh地址:/home/dero/entrypoint.sh -v 外部数据地址:/dero-data hentai8/dero:2.2.1-0.3
```









# xmr√√



节点+walletrpc

![image-20210927150108067](C:\work\各币种节点docker化.assets\image-20210927150108067.png)





## Dockerfile

```dockerfile
FROM ubuntu:20.04
LABEL maintainer="hentai8<496983136@qq.com>"

WORKDIR /home/xmr

COPY ./ ./

EXPOSE 18080
EXPOSE 18081
EXPOSE 8442

RUN ["/bin/bash", "-c", "bash ./run.sh"]
ENTRYPOINT [ "/bin/bash" ,"-c", "bash ./entrypoint.sh"]
```



## build

```shell
docker build -t hentai8/xmr:v0.17.2.3.0 .
```





## entrypoint

运行命令写在entrypoint.sh中，多个命令同时运行用``&``分隔

```shell
./monerod --config-file /home/config/bitmonero.conf --detach & ./monero-wallet-rpc & tail -f /dev/null
```





## run

```shell
docker run -d --network host -v /home/config/xmr/bitmonero.conf:/home/config/bitmonero.conf -v 外部wallet配置文件:/home/config/walletmonero.conf -v 外部entrypoint.sh地址:/home/xmr/entrypoint.sh -v 外部数据地址:/xmr-data -v 外部钱包地址:内部钱包地址 hentai8/xmr:v0.17.2.3.0
```





获取高度

```shell
curl http://127.0.0.1:18081/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_block_count"}' -H 'Content-Type: 


application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "count": 86276,
    "status": "OK",
    "untrusted": false
  }

```



# ~~sc~~













# qrl√√







节点+walletrpc

![image-20210927150108067](C:\work\各币种节点docker化.assets\image-20210927150108067.png)





## Dockerfile

```dockerfile
# FROM ubuntu:20.04
FROM python:3.9
LABEL maintainer="hentai8<496983136@qq.com>"

WORKDIR /home/qrl

COPY ./ ./

EXPOSE 19000
EXPOSE 19007
EXPOSE 19009
EXPOSE 19010
EXPOSE 18090

RUN ["/bin/bash", "-c", "bash ./run.sh"]
ENTRYPOINT [ "/bin/bash" ,"-c", "bash ./entrypoint.sh"]
```



## build

```shell
docker build -t hentai8/qrl:2.1.2.0 .
```





## entrypoint

运行命令写在entrypoint.sh中，多个命令同时运行用``&``分隔

```shell
start_qrl --qrldir /qrl-data
```

<img src="C:\work\各币种节点docker化.assets\image-20211011153410573.png" alt="image-20211011153410573" style="zoom:67%;" />





## run

```shell
docker run -d --network host -v 外部entrypoint.sh地址:/home/qrl/entrypoint.sh -v 外部数据地址:/qrl-data -v 外部钱包地址:内部钱包地址 hentai8/qrl:2.1.2.0
```











# ~~fzs~~















# ~~hns~~











# ckb√√



```shell
./ckb run -C <ckb-path>
```





```dockerfile
FROM ubuntu:20.04
LABEL maintainer="hentai8<496983136@qq.com>"

WORKDIR /home/ckb

COPY ./ ./

EXPOSE 8114
EXPOSE 8115

RUN ["/bin/bash", "-c", "bash ./run.sh"]
ENTRYPOINT [ "/bin/bash" ,"-c", "bash ./entrypoint.sh"]
```





## build

```shell
docker build -t hentai8/ckb:v0.100.0.0 .
docker build -t hentai8/ckb:v0.42.0.0 .
docker build -t hentai8/ckb:v0.101.1.0 .
docker build -t hentai8/ckb:v0.101.3.0 .
```



## run

```shell
docker run -d --network host -v 外部数据地址:/ckb-data hentai8/ckb:v0.100.0.0

docker run -d --network host -v 外部数据地址:/ckb-data hentai8/ckb:v0.42.0.0

docker run -d --network host -v 外部数据地址:/ckb-data hentai8/ckb:v0.101.1.0

docker run -d --network host -v /data/ckb-data:/ckb-data hentai8/ckb:v0.101.3.0

docker run -d --network host -v /data/ckb-data:/ckb-data hentai8/ckb:v0.101.4.0
```



















# kda√√



```
DxPool
日本：
52.199.102.11
54.248.139.229
美国：
35.172.250.72
欧洲：
52.57.79.205

Poolmars
52.207.216.28
54.237.158.109
13.36.108.230
```





```
rsync -avz --delete "jp1.chainweb.com::db" "/data/kda-data"
```



```
curl -sk https://127.0.0.1:444/chainweb/0.0/mainnet01/cut
```



**如果需要不健康重启，需要用kill手动杀死，而非exit**



## Dockerfile

```dockerfile
FROM ubuntu:18.04
LABEL maintainer="hentai8<496983136@qq.com>"

WORKDIR /home/chainweb-node

COPY ./ ./

EXPOSE 444 
EXPOSE 1848

HEALTHCHECK --interval=30s --timeout=3s --retries=3 --start-period=60s\
  CMD curl -f --retry 3 --max-time 5 --retry-delay 5 --retry-max-time 10 -sk https://127.0.0.1:444/chainweb/0.0/mainnet01/cut || bash -c 'kill -s 15 -1 && (sleep 10; kill -s 9 -1)'

RUN ["/bin/bash", "-c", "bash ./run.sh"]
ENTRYPOINT [ "/bin/bash" ,"-c", "bash ./entrypoint.sh"]

```



## run

```shell
docker run -d -v 外部config路径:/home/config/config.yaml -v 外部数据地址:/kda-data -p 444:444 -p 1848:1848 hentai8/kda:2.11.1

docker run -it -v /home/config/kda/config.yaml:/home/config/config.yaml -v /data/kda-data:/kda-data -p 444:444 -p 1848:1848 hentai8/kda:2.12.1.0 /bin/bash

docker run -it -v /home/config/kda/config.yaml:/home/config/config.yaml -v /data/kda-data:/kda-data -p 444:444 -p 1848:1848 hentai8/kda:2.13.0 /bin/bash

docker run -it -v /home/config/kda/config.yaml:/home/config/config.yaml -v /data/kda-data:/kda-data -p 444:444 -p 1848:1848 hentai8/kda:2.13.1.0 /bin/bash

docker run -it -v /home/config/kda/config.yaml:/home/config/config.yaml -v /data/kda-data:/kda-data -p 444:444 -p 1848:1848 hentai8/kda:2.15.0 /bin/bash

docker run -it --restart=always -v /home/config/kda/config.yaml:/home/config/config.yaml -v /data/kda-data:/kda-data -p 444:444 -p 1848:1848 hentai8/kda:2.15.0.1 /bin/bash

docker run -d --restart=always -v /home/config/kda/config.yaml:/home/config/config.yaml -v /data/kda-data:/kda-data -p 444:444 -p 1848:1848 hentai8/kda:2.15.0.2
```

### 一定要打开1848和444端口



### k:地址，public-key前面没有k:

```yaml
miners:
        -
          account: k:8372f0a8661247e39971ff2551a5e95de4110b8c090f5ddd93eb6fbb7d13d732
          public-keys: [ 8372f0a8661247e39971ff2551a5e95de4110b8c090f5ddd93eb6fbb7d13d732 ]
          predicate: keys-all
        -
          account: 96569b08da3a631b1ca7f2cc768f2f14723510ace3b36b36f3be07f233d65596
          public-keys: [ 96569b08da3a631b1ca7f2cc768f2f14723510ace3b36b36f3be07f233d65596 ]
          predicate: keys-all
        -
          account: c50b9acb49ca25f59193b95b4e08e52e2ec89fa1bf308e6436f39a40ac2dc4f3
          public-keys: [ c50b9acb49ca25f59193b95b4e08e52e2ec89fa1bf308e6436f39a40ac2dc4f3 ]
          predicate: keys-all
        -
          account: 81387a6c0f3f362fa578a11f65624d78f77d326d93d943de72994dece6cae7d4
          public-keys: [ 81387a6c0f3f362fa578a11f65624d78f77d326d93d943de72994dece6cae7d4 ]
          predicate: keys-all
```



# lbc√√







## Dockerfile

```dockerfile
FROM ubuntu:20.04
LABEL maintainer="hentai8<496983136@qq.com>"

WORKDIR /home/lbc

COPY ./ ./

EXPOSE 5278
EXPOSE 5279

RUN ["/bin/bash", "-c", "bash ./run.sh"]
ENTRYPOINT [ "/bin/bash" ,"-c", "bash ./entrypoint.sh"]
```



## build



```shell
docker build -t hentai8/lbc:v0.17.3.3.0 .
docker build -t hentai8/lbc:v0.17.4.6.0 .
```



## run



```shell
docker run -d --network host -v 配置文件路径:/home/config/lbccoin.conf -v 外部数据地址:/lbc-data hentai8/lbc:v0.17.4.6.0
```









# stc√√



```shell
./starcoin -d /mnt/star/ -n main --disable-miner-client true --http-apis all
```







## Dockerfile

```dockerfile
FROM ubuntu:20.04
LABEL maintainer="hentai8<496983136@qq.com>"

WORKDIR /home/stc

COPY ./ ./

EXPOSE 9870
EXPOSE 9850

RUN ["/bin/bash", "-c", "bash ./run.sh"]
ENTRYPOINT [ "/bin/bash" ,"-c", "bash ./entrypoint.sh"]
```





## build

```shell
docker build -t hentai8/stc:v1.7.0.1 .
```



docker build -t hentai8/stc:v1.10.1.0 .



**更新时删除startcoin.ipc文件**

## run

```shell
docker run -d --network host -v 外部数据地址:/stc-data hentai8/stc:v1.7.0.1
docker run -d --network host -v 外部数据地址:/stc-data hentai8/stc:1.9.1.0

docker run -d --network host -v 外部数据地址:/stc-data hentai8/stc:1.10.1.0
```



















# simple√√

```shell
./sipe --config /home/config/sipe.toml
```





## Dockerfile

```dockerfile
FROM ubuntu:20.04
LABEL maintainer="hentai8<496983136@qq.com>"

WORKDIR /home/sipe

COPY ./ ./

EXPOSE 8545 8546 30312 30312/udp

RUN ["/bin/bash", "-c", "bash ./run.sh"]
ENTRYPOINT [ "/bin/bash" ,"-c", "bash ./entrypoint.sh"]
```





## build

```shell
docker build -t hentai8/simple:v2.0.3.1 .
```







## run

```shell
docker run -d --network host -v 外部数据地址:/root/.simplechain -v 配置文件路径:/home/config/sipe.toml hentai8/simple:v2.0.3.1
```



docker run -d --network host -v /data/sipe-data:/root/.simplechain -v /home/config/sipe/entrypoint.sh:/home/sipe/entrypoint.sh hentai8/simple:v2.0.3.1

















# sugar√√





## Dockerfile

```dockerfile
FROM ubuntu:20.04
LABEL maintainer="hentai8<496983136@qq.com>"

WORKDIR /home/sugar

COPY ./ ./

EXPOSE 34230
EXPOSE 9051

RUN ["/bin/bash", "-c", "bash ./run.sh"]
ENTRYPOINT [ "/bin/bash" ,"-c", "bash ./entrypoint.sh"]
```





## build

```shell
docker build -t hentai8/sugar:0.16.3.0 .
```







## run

```shell
docker run -d --network host -v 外部数据地址:/sugar-data -v 配置文件路径:/home/config/sugarcoin.conf hentai8/sugar:0.16.3.0
```



























# sumo√√



***<u>sumo和xmr冲突</u>***



## Dockerfile

```dockerfile
FROM ubuntu:20.04
LABEL maintainer="hentai8<496983136@qq.com>"

WORKDIR /home/sumo

COPY ./ ./

EXPOSE 19734
EXPOSE 19733
EXPOSE 8442

RUN ["/bin/bash", "-c", "bash ./run.sh"]
ENTRYPOINT [ "/bin/bash" ,"-c", "bash ./entrypoint.sh"]
```





## build

```shell
docker build -t hentai8/sumo:v0.8.1.0.1 .
```





```shell
curl --digest --user dxsumo:u8ewtwlYImODve0v http://172.21.21.103:19736/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_balance","params":{"account_index":0,"address_indices":[0,1]}}' -H 'Content-Type: application/json'
```



## entrypoint

运行命令写在entrypoint.sh中，多个命令同时运行用``&``分隔

```shell
./sumokoind --config-file /home/config/sumocoin.conf & ./sumo-wallet-rpc & tail -f /dev/null 
```



```shell
./sumokoind --config-file /home/config/bitleth.conf & echo "miao╰(*°▽°*)╯"
ti1=`date +%s`    #获取时间戳
ti2=`date +%s`
i=$(($ti2 - $ti1 ))
while [[ "$i" -ne "10" ]]
do
        ti2=`date +%s`
        i=$(($ti2 - $ti1 ))
done
./sumo-wallet-rpc --config-file ../config/wallet.conf & tail -f /dev/null

```









## run

```shell
docker run -d -p 19734:19734 -p 19733:19733 -p 8443:8442 -v /home/config/sumocoin.conf:/home/config/sumocoin.conf -v 外部wallet配置文件:/home/config/walletsumo.conf -v 外部entrypoint.sh地址:/home/sumo/entrypoint.sh -v 外部数据地址:/sumo-data -v 外部钱包地址:内部钱包地址 hentai8/sumo:v0.8.1.0.1
```













# kva√√



***<u>端口和sugar冲突</u>***



## Dockerfile

```dockerfile
FROM ubuntu:20.04
LABEL maintainer="hentai8<496983136@qq.com>"

WORKDIR /home/kva

COPY ./ ./

EXPOSE 9337
EXPOSE 9338


RUN ["/bin/bash", "-c", "bash ./run.sh"]
ENTRYPOINT [ "/bin/bash" ,"-c", "bash ./entrypoint.sh"]
```





## build

```shell
docker build -t hentai8/kva:0.16.8.0.0 .
```







## run

```shell
docker run -d --network host -v 外部数据地址:/kva-data -v 配置文件路径:/home/config/kevacoin.conf hentai8/kva:0.16.8.0.0
```



















# evox（xmr）√√

节点+walletrpc





## Dockerfile

```dockerfile
FROM ubuntu:20.04
LABEL maintainer="hentai8<496983136@qq.com>"

WORKDIR /home/evox

COPY ./ ./

EXPOSE 52923
EXPOSE 52922
EXPOSE 52921

RUN ["/bin/bash", "-c", "bash ./run.sh"]
ENTRYPOINT [ "/bin/bash" ,"-c", "bash ./entrypoint.sh"]
```



## build

```shell
docker build -t hentai8/evox:v0.1.0.6.0 .
```





## entrypoint

运行命令写在entrypoint.sh中，多个命令同时运行用``&``分隔

```shell
./bin/evolutiond --config-file /home/config/bitevox.conf --detach & echo "miao╰(*°▽°*)╯" & tail -f /dev/null
```





## run

```shell
docker run -d --network host  -v /home/config/bitevox.conf:/home/config/bitevox.conf -v 外部wallet配置文件:/home/config/walletevox.conf -v 外部entrypoint.sh地址:/home/evox/entrypoint.sh -v 外部数据地址:/evox-data -v 外部钱包地址:内部钱包地址 hentai8/evox:v0.1.0.6.0
```









# lthn(xmr)√√



重启后需要手动进去 启动

```
./letheand --config-file /home/config/bitlthn.conf
```

节点+walletrpc





## Dockerfile

```dockerfile
FROM ubuntu:20.04
LABEL maintainer="hentai8<496983136@qq.com>"

WORKDIR /home/lthn

COPY ./ ./

EXPOSE 48782
EXPOSE 38782

RUN ["/bin/bash", "-c", "bash ./run.sh"]
ENTRYPOINT [ "/bin/bash" ,"-c", "bash ./entrypoint.sh"]
```







## build

```shell
docker build -t hentai8/lthn:v3.1.0 .
```





## entrypoint

运行命令写在entrypoint.sh中，多个命令同时运行用``&``分隔

```shell
./letheand --config-file /home/config/bitleth.conf --detach & echo "miao╰(*°▽°*)╯" & tail -f /dev/null
```



```shell
./letheand --config-file /home/config/bitleth.conf & echo "miao╰(*°▽°*)╯"
ti1=`date +%s`    #获取时间戳
ti2=`date +%s`
i=$(($ti2 - $ti1 ))
while [[ "$i" -ne "10" ]]
do
        ti2=`date +%s`
        i=$(($ti2 - $ti1 ))
done
./lethean-wallet-rpc --config-file ../config/wallet.conf & tail -f /dev/null

```



## run

```shell
docker run -d --network host  -v /home/config/bitlthn.conf:/home/config/bitlthn.conf -v 外部wallet配置文件:/home/config/walletleth.conf -v 外部entrypoint.sh地址:/home/lthn/entrypoint.sh -v 外部数据地址:/lthn-data -v 外部钱包地址:内部钱包地址 hentai8/lthn:v3.1.0
```





高度获取

```shell
curl http://127.0.0.1:48782/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"getblockcount"}' -H 'Content-Type: application/json'


{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "count": 1,
    "status": "OK"
  }

```







# erg√√







## Dockerfile

```dockerfile
FROM ubuntu:20.04
LABEL maintainer="hentai8<496983136@qq.com>"

WORKDIR /home/ltc

COPY ./ ./

EXPOSE 9030
EXPOSE 9053

RUN ["/bin/bash", "-c", "bash ./run.sh"]
ENTRYPOINT [ "/bin/bash" ,"-c", "bash ./entrypoint.sh"]
```



## build

```
docker build -t hentai8/ergo:4.0.32.0 .
```

apt-get install default-jre

apt-get install default-jdk



## run

```shell
docker run -d --network host -v 配置文件路径:/home/config/ergo.conf -v 外部数据地址:/ergo-data hentai8/ergo:4.0.32.0
sudo docker run -d -p 9030:9030 -p 0.0.0.0:9053:9053 -v /data/ergo-data/node:/home/ergo/.ergo  -v /home/config/ergo/ergo.conf:/etc/myergo.conf ergoplatform/ergo:v4.0.34 --mainnet -c /etc/myergo.conf
```



## config

```shell
root@node1:/home/config# cat litecoin.conf 
server=1
datadir=/ltc-data
```





高度获取

```shell
curl --user 账号:密码 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockcount", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:9332/
```



```shell

```





# P.S.



## **sumo lthn 需要进入容器手动启动节点和钱包**











# mammoth（）



## step

```shell
apt-get update;
apt install -y software-properties-common;
要输入6和70
apt-get install -y git;
add-apt-repository -y ppa:ondrej/nginx-mainline;
apt-get update;
apt-get -y install curl vim wget unzip apt-transport-https lsb-release ca-certificates libz-dev net-tools nginx-extras;
add-apt-repository -y ppa:ondrej/php;
apt-get update;
apt-get install -y php7.4-fpm php7.4-mysql php7.4-curl php7.4-gd php7.4-mbstring php7.4-xml php7.4-xmlrpc php7.4-zip php7.4-opcache php7.4-bcmath php7.4-dev;
apt-get install -y php-pear;
pecl install grpc;
很慢
echo "extension=grpc.so" >> /etc/php/7.4/fpm/php.ini
echo "extension=grpc.so" >> /etc/php/7.4/cli/php.ini
sed -i 's/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/' /etc/php/7.4/fpm/php.ini;
service php7.4-fpm restart;
php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');";
php composer-setup.php;
php -r "unlink('composer-setup.php');";
mv composer.phar composer;
chmod +x composer;
mv composer /usr/local/bin;
#curl -LO https://deployer.org/deployer.phar;
#mv deployer.phar /usr/local/bin/dep;
#chmod +x /usr/local/bin/dep;
配置ssh密钥
git clone -b test ssh://git@intchains.in:16622/epool/mammoth.git
composer install --ignore-platform-reqs
填充配置文件
填充nginx文件
```

















































./sipe --minertype stratum --stratum.port 0.0.0.0:8802 --port 30313 --rpc --rpcaddr 172.21.29.15 --rpcport 8546 --etherbase Sibef7e0f5267086972eba922c8d1c2b3d06b198ef --mine --minerthreads 0





