# Cloudflare-API-DDNS 
说明：该脚本可实现自动更新 Cloudflare 的 DNS 记录，检查频率高达每分钟检查一次 

# 特点： 
1、公网ip获取方式为从本机执行脚本获取，也就是执行命令的主机是自己拨号并有一个公网ip 
2、需要用到 ifconfig 命令，需要安装 net-tool s这个软件包  
3、因为用到了 source 命令，所以需要用 bash 执行环境，而不是 sh
     
备注： 关于第一点限制说明，执行脚本的主机必须有公网ip，这样就可以不受第三方接口的限制，比如接口频率限制，响应时间不稳定等，直接本机获取公网ip  
  
安装 net-tools  
  
```
apt-get install net-tools 
```

脚本使用方法

```
wget -N --no-check-certificate https://raw.githubusercontent.com/niehui/cloudflare-api-ddns/main/cf-ddns.sh
```
```
vi cf-ddns.sh
```
```
chmod +x cf-ddns.sh
```
```
./cf-ddns.sh
```

设置定时任务

输入 crontab -e ，在文件里面添加一行：
```
*/2 * * * * /root/cf-ddns.sh >/dev/null 2>&1
```
说明：每 2 分钟执行脚本检测本机 IP，如跟上一次的 IP 相同，则退出；不同则通过 API 更新至 CloudFlare 的 DNS。

如果需要日志文件，上述代码请替换成下面代码.
```
*/2 * * * * /root/cf-ddns.sh >> /var/log/cf-ddns.log 2>&1
```
原作者有视频介绍链接

哔站视频介绍 https://www.bilibili.com/video/BV1A5411A7DR/  
油管视频介绍 https://www.youtube.com/watch?v=3XmMTWJI8XE   
