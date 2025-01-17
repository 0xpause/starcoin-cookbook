# 如何与 Starcoin 控制台交互

## 如何启动控制台

### 方式一

在节点启动的时候进入控制台。

注意：如果不指定存放数据的目录，以这种方式直接进入交互式控制台，会在 `/tmp` 目录下随机生成一个用于存放当前进程的数据目录。
退出交互式控制台，进程结束，存放数据的目录也会立即被删除。

```shell
starcoin -n dev console
```

在启动交互式控制台时通过 `-d` 选项指定数据目录，则不会在进程结束后将其删除：

```shell
starcoin -n dev -d . console
```

`.` 表示当前目录，也可以使用一个绝对路径来指定存放数据的目录。

```shell
                                                (%&&&&(%&%(  &#
                                        ,#%%%&%%%#/        (%&&%
                                %#%#%%%%#&&%                 %&
                                / %%%                          #&
                            &#%%%#%%%%#                        *&%
                        (#%%%#/ %%%%%%#                      #&%
                    #%#%%#&&   #%%%%%%%(                   &%%&
                (#%%##      #%%%%%%%%%/                *%%
            #%%%&#%%##&&&&%%%(%%%%%%%%%%%&&&&&&&& &%  (&#/#
            ((##%%%%%%%%%%%%%%%%%%%%%%%%&&&&&&&%%  ####
        ###%#(& &#%%%%%%%%%%%%%%%%%%%%%&&&&%##&(%&%
        (#%##       (#%%%%%%%%%%%%%%%%%%&%#(#%%#
        (###(%           &&#%%%%%%%%%%%%%%&%%#&&
    ####                %%%%%%%%%%%%(    %%
    /###/                #%%%%%%%%#%%#     %%#
    /###(                (%%%%%%#%%%##%%%(  *%%#
    ###(                (%%%%###&#     %&#%%&(%%%
    (##(&              &#%#(#               %%&&%
    (###%#       (%%%#((&                    &&%#
        (#%%%%%%#(

     ██████╗████████╗ █████╗ ██████╗  █████╗  █████╗ ██╗███╗  ██╗
    ██╔════╝╚══██╔══╝██╔══██╗██╔══██╗██╔══██╗██╔══██╗██║████╗ ██║
    ╚█████╗    ██║   ███████║██████╔╝██║  ╚═╝██║  ██║██║██╔██╗██║
     ╚═══██╗   ██║   ██╔══██║██╔══██╗██║  ██╗██║  ██║██║██║╚████║
    ██████╔╝   ██║   ██║  ██║██║  ██║╚█████╔╝╚█████╔╝██║██║ ╚███║
    ╚═════╝    ╚═╝   ╚═╝  ╚═╝╚═╝  ╚═╝ ╚════╝  ╚════╝ ╚═╝╚═╝  ╚══╝

starcoin%
```

看到如上的输出，表示成功进入了交互式控制台。

### 方式二

在一个终端启动节点后，再开启另一个终端接入节点来启动控制台。

```shell
# 终端1
starcoin -n dev -d ~
```

此时会在用户目录下生成一个 `dev` 的目录，目录中的 `.ipc` 文件可以用来接入控制台。

```shell
# 终端2
cd ~/dev
starcoin -c starcoin.ipc console
```

## 如何接入控制台

### 通过 IPC 文件

参考[启动控制台中的方式二](#方式二)。

注意：在 Windows 中，IPC 文件所在路径不同。

```cmd
starcoin.exe -c \\.\pipe\starcoin\dev\starcoin.ipc console
```

### 通过 WebSocket

```shell
starcoin -c ws://0.0.0.0:9870 console
```

## 如何通过控制台连接远程节点

### 通过 IPC 文件连接主网

```shell
starcoin -c ~/.starcoin/main/starcoin.ipc console
```

### 通过 WebSocket 连接主网

```shell
# 连接到主网络种子节点
starcoin -c ws://main.seed.starcoin.org:9870 console
```

## 使用本地账户

连接到主网络种子节点后，使用本地帐户数据库来使用与帐户相关的命令。

```shell
starcoin --connect ws://main.seed.starcoin.org:9870 --local-account-dir ~/.starcoin/main/account_vaults console
```

## 通过 Docker 接入控制台

```shell
docker run --rm -it -v  ~/.starcoin/:/root/.starcoin/ starcoin/starcoin:latest /starcoin/starcoin --connect /root/.starcoin/main/starcoin.ipc console
```
