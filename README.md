# cce-window

1709 

## Prepare
申请台ECS，4c16g, RDP，
powershell
下载基础镜像
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


