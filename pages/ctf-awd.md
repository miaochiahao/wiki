# AWD

> From https://yunlongs.cn/2019/01/15/CTF-AWD-%E5%B8%B8%E7%94%A8%E6%93%8D%E4%BD%9C%E6%80%BB%E7%BB%93/



## 备份数据库

```bash
mysqldump -u 用户名 -p 密码 数据库名 > back.sql # 备份单个数据库
mysqldump --all-databases > bak.sql # 备份所有数据库
mysql -u 用户名 -p 密码 数据库名 < bak.sql # 还原mysql数据库
```



## 防止系统文件修改

```bash
chattr +i /etc/profile
chattr -i /etc/profile
```

