### ssl证书
1. 用letsencrypt创建，使用certbot-auto
```
# 获取
wget https://dl.eff.org/certbot-auto
# 设置为可执行
chmod a+x certbot-auto
# 自动部署
./certbot-auto certonly
```
部署过程中会出现多次选择确认，根据自己的需求确认即可
成功后会提示
```
Congratulations! Your certificate and chain have been saved at  
/etc/letsencrypt/live/xxx.com/fullchain.pem. Your cert will
expire on 2016-10-05. To obtain a new or tweaked version of this
certificate in the future, simply run certbot-auto again. To
non-interactively renew *all* of your certificates, run
"certbot-auto renew"
```
2. 创建自动续期任务
* 使用脚本进行续期
```
vim ssl_auto_auth.sh
```
```
#/bin/sh
#续期   说明：只用renew的话，会先检查证书是否需要更新，距离到期30天以内才会执行更新，否则会提示不需要更新。（昨天更新了证书，今天直接用renew，提示不允许更新）
#这里方便测试，增加参数--force-renew，能够强制立即更新
./certbot-auto renew --force-renew
#移动新生成的证书文件
cp /etc/letsencrypt/live/yourDomain/fullchain.pem /mnt/web/letsTemp # 这里配置的是ssl相关的配置地址(如nginx或这Apache)
cp /etc/letsencrypt/live/yourDomain/privkey.pem /mnt/web/letsTemp
```
* 创建定时任务
这里使用crontab创建任务
```
crontab -e
```
选择编辑器打开文件编辑
```
# min hour day month week 这里设置的是每周1早上3点运行该任务尝试更新证书
0 3 * * 1 sh /path/ssl_auto_auth.sh > /dev/null 2>&1 &
```

