---
layout: page
body_class: page
description: 君子终日乾乾夕惕若厉无咎
---


- 禁止访问特定网站

1. 管理员身份运行记事本；
  
2. 打开C:\Windows\System32\drivers\etc\hosts；

3. 在最下方添加
```
    127.0.0.1 example.com
    127.0.0.1 www.example.com
```
{: .code-block }

并保存；

4. 打开cmd运行
```python
ipconfig /flushdns
```
{: .code-block }

即可。
