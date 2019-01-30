# S3 网关教程

S3网关是我们提供的适配Amazon S3的客户端, 学习本教程前请先按照 [test network](Test-network) 配置好网络。


## 安装和配置

首先需要安装Golang(版本不低于1.11) [Go 1.11](https://www.golang.org/). 
获得S3网关, 请执行:

```bash
go get -u storj.io/storj/cmd/gateway
```

上述命令会安装gateway的可执行程序到你配置的GOPATH目录下, 默认为 `~/go/bin`.

为你的Satellite配置Gateway之前你需要首先纪录下你的Satellite的地址和账户API Key。
[Uplink CLI](Uplink-CLI) 和Gateway可以共享同一份配置文件, 所以如果你已经配置好了Uplink这一步就可以跳过了。

接下来你需要选择一个密码, 请妥善保管好你的密码。你的密码在你访问你所有文件时会被用到, 如果你丢失了你的密码就无法恢复你的文件了。

下面的命令使用默认配置项配置了你的gateway, 你可以运行它:

```bash
~/go/bin/gateway setup --api-key abc123 --satellite-addr 127.0.0.1:7778 \
  --enc-key highlydistributedridiculouslyresilient
```

至此你已经做好了准备,下面介绍如何使用gateway操作Storj网络。

## 运行

命令 `gateway` 会启动一个守护进程。如果你在使用Storj的测试网络, 默认已经有一个gateway在运行了。
你可以通过指定不同端口启动另外一个网关, 操作命令如下:

```bash
~/go/bin/gateway run --address :7776
```
网关启动之后会输出你的接入点(endpoint), 秘钥(access key)和密码(secret key)。


## 使用Amazon S3命令行工具

开始之前请确保已经安装了 [AWS S3 CLI
installed](https://docs.aws.amazon.com/cli/latest/userguide/installing.html).

打开一个新的终端, 输入如下命令:

```
$ aws configure
AWS Access Key ID [None]: eUXZt66VWTTpcwgBazQnPsuSYri
AWS Secret Access Key [None]: xDkJKUqJVhAj69CGH1VPqDPi47Q
Default region name [None]: us-east-1
Default output format [None]:
```

接下来测试一下 AWS S3 CLI 的操作命令!

#### 创建Bucket

```bash
aws s3 --endpoint=http://localhost:7777/ mb s3://bucket-name
```

#### 上传对象

```bash
aws s3 --endpoint=http://localhost:7777/ cp ~/Desktop/your-large-file.mp4 s3://bucket-name
```

#### 展示Bucket下所有对象

```bash
aws s3 --endpoint=http://localhost:7777/ ls s3://bucket-name/
```

#### 下载对象

```bash
aws s3 --endpoint=http://localhost:7777/ cp s3://bucket-name/your-large-file.mp4 ~/Desktop/your-large-file.mp4
```

#### 为一个对象生成一个URL

```bash
aws s3 --endpoint=http://localhost:7777/ presign s3://bucket-name/your-large-file.mp4
```

(URL 可以通过浏览器访问到)

#### 删除对象

```bash
aws s3 --endpoint=http://localhost:7777/ rm s3://bucket-name/your-large-file.mp4
```

## 总结

恭喜你已经学会了如何操作Amazon S3的适配网关, 整合S3网关的Storj使用起来非常方便。

我们还有一篇Uplink的使用教程 [Uplink](Uplink-CLI) 欢迎阅读. 有任何问题可以通过Issue告诉我们。

去中心化这个世界吧,少年!
