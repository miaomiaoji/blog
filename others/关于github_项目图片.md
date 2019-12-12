
# github过慢或者图片显示问题
## 加速
1、为了加速，在系统的hosts中添加GitHub网站中用到的域名以及对应的IP;(windows系统hosts文件的位置C:\Windows\System32\drivers\etc )  
2、从浏览器控制台可以查看有哪些出现ERR_CONNECTION_RESET或者ERR_CONNECTION_XX的错误的域名，在[https://www.ipaddress.com/](https://www.ipaddress.com/)查询一些域名的IP;我查询了下列网站
```
192.30.253.113 github.com  
185.199.108.154  github.githubassets.com  
185.199.109.154  github.githubassets.com  
185.199.110.154  github.githubassets.com  
185.199.111.154  github.githubassets.com  
52.216.22.43 github-cloud.s3.amazonaws.com  
199.232.28.133 githubusercontent.com  
199.232.4.133 avatars3.githubusercontent.com  
199.232.4.133 avatars2.githubusercontent.com  
199.232.4.133 avatars0.githubusercontent.com  
199.232.4.133 avatars1.githubusercontent.com 
```
## 特殊情况——网络状况
1、20191210检测raw.githubusercontent.com报错，访问不到这个域名。偶尔又可以访问到，如果你也遇到这种情况......国内的网络真让人XX（在md中使用上传到GitHub项目中的图片结果会访问这个域名，无论是绝对路径或者相对路径）  
2、可以拖拽图片到issue中，这样拖动的图片地址存储在域名user-images.githubusercontent.com下，这个域名图片很少出现G显示不了的状况  

## 本地编辑代码和MD文件
使用命令行或者Github Desktop客户端下载或者同步代码，比浏览器快或者至少感觉上快，图片使用相对路径也不会影响本地显示。
多使用github命令，更快的熟悉团队合作。  
1、git clone项目到本地，代码和MD文件都可以使用IDE编辑和查看，然后同步到GitHub上  
2、vscode需要安装几个插件——“Markdown ALL in One”和“Markdown Preview Github Styling” 

## 终极方法
1、既然md文件中的图片被保存在不稳定的域名，那就学习使用markdown来编写UML图或者其他不需要用到域名的方式。本质依然是构建更好的本地环境，舍弃浏览器和不稳定的网络，完成任务之后再同步。
- [建模工具的使用——plantuml/mermaid](../others/建模工具.md)

2、突破那堵墙，ha！

