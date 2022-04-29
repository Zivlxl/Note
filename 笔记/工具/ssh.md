ssh教程：https://wangdoc.com/ssh/index.html

### ssh 拷贝文件

`scp`是 secure copy 的缩写，相当于`cp`命令 + SSH。它的底层是 SSH 协议，默认端口是22，相当于先使用`ssh`命令登录远程主机，然后再执行拷贝操作。

`scp`主要用于以下三种复制操作。

- 本地复制到远程。
- 远程复制到本地。
- 两个远程系统之间的复制。

使用`scp`传输数据时，文件和密码都是加密的，不会泄漏敏感信息。



#### 本地文件复制到远程

复制本机文件到远程系统的用法如下。

```
# 语法
$ scp SourceFile user@host:directory/TargetFile

# 示例
$ scp file.txt remote_username@10.10.0.2:/remote/directory
```

下面是复制整个目录的例子。

```
# 将本机的 documents 目录拷贝到远程主机，
# 会在远程主机创建 documents 目录
$ scp -r documents username@server_ip:/path_to_remote_directory

# 将本机整个目录拷贝到远程目录下
$ scp -r localmachine/path_to_the_directory username@server_ip:/path_to_remote_directory/

# 将本机目录下的所有内容拷贝到远程目录下
$ scp -r localmachine/path_to_the_directory/* username@server_ip:/path_to_remote_directory/
```



#### 远程文件复制到本地

从远程主机复制文件到本地的用法如下。

```
# 语法
$ scp user@host:directory/SourceFile TargetFile

# 示例
$ scp remote_username@10.10.0.2:/remote/file.txt /local/directory
```

下面是复制整个目录的例子。

```
# 拷贝一个远程目录到本机目录下
$ scp -r username@server_ip:/path_to_remote_directory local-machine/path_to_the_directory/

# 拷贝远程目录下的所有内容，到本机目录下
$ scp -r username@server_ip:/path_to_remote_directory/* local-machine/path_to_the_directory/
$ scp -r user@host:directory/SourceFolder TargetFolder
```



#### 两个远程系统之间的复制

本机发出指令，从远程主机 A 拷贝到远程主机 B 的用法如下。

```
# 语法
$ scp user@host1:directory/SourceFile user@host2:directory/SourceFile

# 示例
$ scp user1@host1.com:/files/file.txt user2@host2.com:/files
```

系统将提示你输入两个远程帐户的密码。数据将直接从一个远程主机传输到另一个远程主机。



#### `scp`支持一次复制多个文件

```
$ scp source1 source2 destination
```

上面命令会将`source1`和`source2`两个文件，复制到`destination`。

注意，如果所要复制的文件，在目标位置已经存在同名文件，`scp`会在没有警告的情况下覆盖同名文件。



#### 参数项

**（1）`-c`**

`-c`参数用来指定文件拷贝数据传输的加密算法。

```
$ scp -c blowfish some_file your_username@remotehost.edu:~
```

上面代码指定加密算法为`blowfish`。

**（2）`-C`**

`-C`参数表示是否在传输时压缩文件。

```
$ scp -c blowfish -C local_file your_username@remotehost.edu:~
```

**（3）`-F`**

`-F`参数用来指定 ssh_config 文件，供 ssh 使用。

```
$ scp -F /home/pungki/proxy_ssh_config Label.pdf root@172.20.10.8:/root
```

**（4）`-i`**

`-i`参数用来指定密钥。

```
$ scp -vCq -i private_key.pem ~/test.txt root@192.168.1.3:/some/path/test.txt
```

**（5）`-l`**

`-l`参数用来限制传输数据的带宽速率，单位是 Kbit/sec。对于多人分享的带宽，这个参数可以留出一部分带宽供其他人使用。

```
$ scp -l 80 yourusername@yourserver:/home/yourusername/* .
```

上面代码中，`scp`命令占用的带宽限制为每秒 80K 比特位，即每秒 10K 字节。

**（6）`-p`**

`-p`参数用来保留修改时间（modification time）、访问时间（access time）、文件状态（mode）等原始文件的信息。

```
$ scp -p ~/test.txt root@192.168.1.3:/some/path/test.txt
```

**（7）`-P`**

`-P`参数用来指定远程主机的 SSH 端口。如果远程主机使用默认端口22，可以不用指定，否则需要用`-P`参数在命令中指定。

```
$ scp -P 2222 user@host:directory/SourceFile TargetFile
```

**（8）`-q`**

`-q`参数用来关闭显示拷贝的进度条。

```
$ scp -q Label.pdf mrarianto@202.x.x.x:.
```

**（9）`-r`**

`-r`参数表示是否以递归方式复制目录。

**（10）`-v`**

`-v`参数用来显示详细的输出。

```
$ scp -v ~/test.txt root@192.168.1.3:/root/help2356.txt
```