# cce-window

1709 

## Prepare
申请台ECS，4c16g, 加一块200G数据盘，

RDP到远程桌面

### 配置docker daemon

确认数据盘加载ok，如果不行，powershell 
`diskpart - list disk`
- select disk 
- online
- create partition
- ASSIGN LETTER=D 
- list volume
- format fs=ntfs label='new' quick compress

修改C:\ProgramData\docker\config\daemon.json配置文件
```
{
  "data-root": "D:\\docker"
}
```
重启

在powershell内先下载基础镜像
```
docker pull microsoft/windowsservercore:1709
docker pull mcr.microsoft.com/windows/servercore/iis:windowsservercore-1709
docker pull microsoft/mssql-server-windows-developer:1709

```

系统升级
```
sconfig 选择6 All
```
升级windows server， 版本 10.0.16299.1087


## IIS demo

起一个iis
`kubectl apply -f iis-1709.yaml`

起一个service，NodePort 80端口，
在节点ip:port 验证iis defual页面能打开

## sqlserver demo

在host内新建目录 `c:\sql` 用于之后挂盘

