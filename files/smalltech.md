- 禁止访问特定网站

1. 管理员身份运行记事本；
  
2. 打开C:\Windows\System32\drivers\etc\hosts；

3. 在最下方添加
```
127.0.0.1 example.com
127.0.0.1 www.example.com
```
并保存；

4. 打开cmd运行
```
ipconfig /flushdns
```
即可。
