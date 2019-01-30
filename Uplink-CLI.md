# Uplink CLI 教程

Uplink CLI是我们连接Storj网络的客户端程序, 学习本教程前请先按照 [test network](Test-network.md) 配置好网络。

## 安装和配置

首先需要安装Golang(版本不低于1.11) [Go 1.11](https://www.golang.org/). 
获得uplink, 请执行:

```bash
go get -u storj.io/storj/cmd/uplink
```

上述命令会安装uplink的可执行程序到你配置的GOPATH目录下, 默认为 `~/go/bin`.

为你的Satellite配置Uplink之前你需要首先纪录下你的Satellite的地址和账户API Key。
[S3 gateway](S3-Gateway.md) 和Uplink可以共享同一份配置文件, 所以如果你已经配置好了S3网关这一步就可以跳过了。

接下来你需要选择一个密码, 请妥善保管好你的密码。你的密码在你访问你所有文件时会被用到, 如果你丢失了你的密码就无法恢复你的文件了。

下面的命令使用默认配置项配置了你的uplink, 你可以运行它:

```bash
~/go/bin/uplink setup --api-key abc123 --satellite-addr 127.0.0.1:7778 \
  --enc-key highlydistributedridiculouslyresilient
```

至此你已经做好了准备,下面介绍如何使用uplink操作Storj网络。

## 使用方式

`uplink` 有一系列的操作符, 例如:

 * `cat` - 在标准输出中输出文件.
 * `cp` - 从外部拷贝一个文件到Storj内部.
 * `ls` - 列出Storj的bucket下所有的文件.
 * `mb` - 新建一个新的bucket.
 * `mount` - 挂在你系统上的一个文件到Storj的bucket.
 * `put` - 向Storj中的文件写入.
 * `rb` - 删除一个bucket.
 * `rm` - 删除一个文件.

可以通过`--help`命令查看每个命令的使用方式, 下面列出几个常见操作的示例:

#### 创建Bucket

```bash
uplink mb sj://bucket-name
```

#### 上传文件

```bash
uplink cp ~/Desktop/your-large-file.mp4 sj://bucket-name
```

#### 展示Bucket下所有文件

```bash
uplink ls sj://bucket-name/
```

#### 下载文件

```bash
uplink cp sj://bucket-name/your-large-file.mp4 ~/Desktop/your-large-file.mp4
```

#### 删除文件

```bash
uplink rm sj://bucket-name/your-large-file.mp4
```

#### 文件系统中展示文件

```bash
mkdir -p ~/bucket-name
uplink mount sj://bucket-name/ ~/bucket-name/
```

目前仅适用于Linux操作系统, Windows和MacOS随后支持!

## 总结

到这里你已经掌握了如何通过Uplink操作Storj网络。

我们还有一篇介绍和Amazon S3集成的教程 [S3 Gateway](S3-Gateway.md) 欢迎阅读. 有任何问题可以通过Issue告诉我们。

去中心化这个世界吧,少年!
