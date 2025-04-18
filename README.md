# gh-proxy

## 简介

github release、archive以及项目文件的加速项目，支持clone，有Cloudflare Workers无服务器版本以及Python版本

## 使用

直接在copy出来的url前加`https://gh.api.99988866.xyz/`即可

也可以直接访问，在input输入

***大量使用请自行部署，以上域名仅为演示使用。***

访问私有仓库可以通过

`git clone https://user:TOKEN@ghproxy.com/https://github.com/xxxx/xxxx` [#71](https://github.com/hunshcn/gh-proxy/issues/71)

以下都是合法输入（仅示例，文件不存在）：

- 分支源码：https://github.com/hunshcn/project/archive/master.zip

- release源码：https://github.com/hunshcn/project/archive/v0.1.0.tar.gz

- release文件：https://github.com/hunshcn/project/releases/download/v0.1.0/example.zip

- 分支文件：https://github.com/hunshcn/project/blob/master/filename

- commit文件：https://github.com/hunshcn/project/blob/1111111111111111111111111111/filename

- gist：https://gist.githubusercontent.com/cielpy/351557e6e465c12986419ac5a4dd2568/raw/cmd.py

## Python版本部署

### Docker部署

```
docker run -d --name="gh-proxy-py" \
  -p 8079:80 \
  --restart=always \
  nobody114/gh-proxy:latest
```

第一个8079是你要暴露出去的端口

### 直接部署

安装依赖（请使用python3）

```pip install flask requests```

按需求修改`app/main.py`的前几项配置

*注意:* 可能需要在`return Response`前加两行
```python3
if 'Transfer-Encoding' in headers:
    headers.pop('Transfer-Encoding')
```

### 注意

python版本的机器如果无法正常访问github.io会启动报错，请自行修改静态文件url

python版本默认走服务器（2021.3.27更新）

## Changelog

* 2020.04.10 增加对`raw.githubusercontent.com`文件的支持
* 2020.04.09 增加Python版本（使用Flask）
* 2020.03.23 新增了clone的支持
* 2020.03.22 初始版本

## 链接

[我的博客](https://hunsh.net)

## 参考

[jsproxy](https://github.com/EtherDream/jsproxy/)
