# cce-window

1709 

## Prepare
申请台ECS，4c16g, 加一块200G数据盘，

RDP到远程桌面

## 升级server
进入powershell
```
sconfig 6 all
```
之后检查server版本为 10.0.16299.1087

## 确认数据盘
因为window镜像较大，需要添加额外数据盘，需要手动diskpart
进入powershell
```
diskpart 
- list disk
- select disk 1
- online disk
- attributes remove readyonly
- create partition
- ASSIGN LETTER=D 
- list volume
- format fs=ntfs label='new' quick compress
```
确认能 `cd D:\`
新建目录 `D:\data`

### 配置docker daemon

修改docker root目录到D盘, 添加 C:\ProgramData\docker\config\daemon.json配置文件
```
{
  "data-root": "D:\\docker"
}
```
重启机器，确认docker正常运行

### 基础镜像
在powershell内先下载基础镜像
```
docker pull microsoft/windowsservercore:1709
docker pull mcr.microsoft.com/windows/servercore/iis:windowsservercore-1709
docker pull microsoft/mssql-server-windows-developer:1709
```

## IIS demo
起一个iis
`kubectl apply -f iis-1709.yaml`

起一个service，NodePort 80端口，
在节点ip:port 验证iis defual页面能打开

## sqlserver demo
在host内新建目录 `D:\data` 用于之后挂盘
在CCE内新增stateful应用，选择sqlserver镜像。具体见 sql-1709.yaml
注意：
1. 配置2个环境变量 sa_password=<YOUR SA PASSWORD> ACCEPT_EULA=Y
2. 挂在数据盘 主机挂在点选 D:\data, 容器内随意 i.e C:\tmp

