# cce-window

1709 

## IIS
升级windows server， 版本 10.0.16299.1087
`cmd -> sconfig 6 ALL`
本地拉镜像
`docker pull mcr.microsoft.com/windows/servercore/iis:windowsservercore-1709`

起一个iis
`kubectl apply -f iis-1709.yaml`

起一个service，NodePort 80端口


