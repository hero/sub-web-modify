# sub-web-modify
[本项目](https://sub.v1.mk)重制[原项目](https://github.com/CareyWang/sub-web)CSS样式，解决大部分布局细节问题，增加“暗黑模式”，默认自动切换亮/暗模式（点击“太阳/月亮”图标可手动切换），增加“高级功能”点击显示/隐藏，添加短链接选择/自定义功能，增加近百条远程配置，新增[sub-web聚合API](https://github.com/youshandefeiyang/sub-web-api)，增加从短链接中获取订阅信息并返回至前端界面，增加上传自定义远程配置/JS进阶排序节点/JS进阶筛选节点等功能，感兴趣的朋友可以自建API服务，增加URL传参设置自定义后端（为了兼容[Docker](https://hub.docker.com/r/youshandefeiyang/sub-web-modify)），使用举例：`http://你的IP:8090/?backend=https://api.v1.mk`！<br/>
## 效果预览：
![avatar](https://raw.githubusercontent.com/youshandefeiyang/webcdn/main/dyzh.gif)
### 使用方法【以Linux为例】：
1.安装 [node](https://blog.csdn.net/achabuhecha/article/details/111400068) 和 [yarn](https://classic.yarnpkg.com/en/docs/install#debian-stable) 和 [git](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git)

2.终端执行 `cd /home && git clone https://github.com/youshandefeiyang/sub-web-modify.git && chmod -R 755 sub-web-modify && cd sub-web-modify && yarn install && yarn build`

3.build成功后，需要安装nginx并正确配置，以下为nginx server部分配置，可以参考一下【这块建议新手使用宝塔面板等自动化运维工具，直接将网站目录更改为/home/sub-web-modify/dist即可】！

```shell
server {
    listen 80;
    server_name 你的域名或IP;
    root /home/sub-web-modify/dist;
    index index.html index.htm;
    error_page 404 /index.html;
    gzip on; #开启gzip压缩
    gzip_min_length 1k; #设置对数据启用压缩的最少字节数
    gzip_buffers 4 16k;
    gzip_http_version 1.0;
    gzip_comp_level 6; #设置数据的压缩等级,等级为1-9，压缩比从小到大
    gzip_types text/plain text/css text/javascript application/json application/javascript application/x-javascript application/xml; #设置需要压缩的数据格式
    gzip_vary on;
    location ~* \.(css|js|png|jpg|jpeg|gif|gz|svg|mp4|ogg|ogv|webm|htc|xml|woff)$ {
        access_log off;
        add_header Cache-Control "public,max-age=30*24*3600";
    }
}
```

4.如需进一步修改前端，请在/home/sub-web-modify下执行 `yarn serve` 进行调试即可
