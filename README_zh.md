<div align="center">
<a href="https://demo.ragflow.io/">
<img src="web/src/assets/logo-with-text.png" width="350" alt="ragflow logo">
</a>
</div>

<p align="center">
  <a href="./README.md"><img alt="README in English" src="https://img.shields.io/badge/English-DFE0E5"></a>
  <a href="./README_zh.md"><img alt="简体中文版自述文件" src="https://img.shields.io/badge/简体中文-DBEDFA"></a>
</p>

<h4 align="center">
  <a href="https://ragflow.io/docs/dev/">Document</a> |
  <a href="https://github.com/infiniflow/ragflow/issues/4214">Roadmap</a> |
  <a href="https://twitter.com/infiniflowai">Twitter</a> |
  <a href="https://discord.gg/NjYzJD3GM3">Discord</a> |
  <a href="https://demo.ragflow.io">Demo</a>
</h4>

#

<details open>
<summary><b>📕 目录</b></summary>

- 💡 [RAGFlow 是什么？](#-RAGFlow-是什么)
- 🎮 [Demo](#-demo)
- 📌 [近期更新](#-近期更新)
- 🌟 [主要功能](#-主要功能)
- 🔎 [系统架构](#-系统架构)
- 🎬 [快速开始](#-快速开始)
- 🔧 [系统配置](#-系统配置)
- 🔨 [以源代码启动服务](#-以源代码启动服务)
- 📚 [技术文档](#-技术文档)
- 📜 [路线图](#-路线图)
- 🏄 [贡献指南](#-贡献指南)
- 🙌 [加入社区](#-加入社区)
- 🤝 [商务合作](#-商务合作)

</details>

## 💡 至锐联 是什么？

[至锐联]免费版是一款零信任软件产品，专门为中小企业提供高安全、高效的外网接入企业内部的访问。使用至锐联产品，企业可以指定具体用户访问指定的应用、指定的设备、指定的端口，比简单使用VPN更加安全。
[至锐联]免费版由志翔科技研发，带50个永久License，可以在企业内网私有化部署，让中小企业能低成本、高安全地使用零信任产品的特性。

## 🔥 近期更新

- 2025-10-16 志翔科技正式推出[至锐联]免费版。

## 🌟 主要功能

### 🍭 **网络隐身术：让黑客"看不见"你的服务器**

- 采用SPA单包认证技术，默认关闭所有端口，杜绝90%以上的主动攻击。
- 只有通过认证的设备才能"敲门"，并建立连接。

### 🍱 **最小权限访问：给每个员工配备"定制钥匙"**

- 按使用者-使用对象进行细致权限控制，杜绝越权访问。（例如：市场部只能访问CRM，财务部仅可见OA）
- 支持按"时间/地点/设备健康度"动态授权。（例如：仅允许北京IP在9:00-18:00访问）

### 🌱 **轻量部署：IT小白也能快速上线**

- 兼容Windows/macOS/Linux，客户端体积＜10MB。
- 无需改动现有网络架构，网关即插即用。

## 🔎 系统架构

<div align="center" style="margin-top:20px;margin-bottom:20px;">
<img src="https://github.com/infiniflow/ragflow/assets/12318111/d6ac5664-c237-4200-a7c2-a4a00691b485" width="1000"/>
</div>

## 🎬 快速开始

### 📝 系统部署条件

- CPU >= 4 核
- RAM >= 4 GB
- Disk >= 20 GB
- OS: CentOS7.5, CentOS7.9(Minimal install)

### 🚀 系统安装

1. 将安装包：SDP2.0.3_all.tgz拷贝至系统重，解压，然后进入解压出来的sdp_install_pkg目录。
<img width="628" height="142" alt="image" src="https://github.com/user-attachments/assets/7e102147-a10f-4dcc-a99a-c0674512deb2" />

2. ./installer.sh执行安装程序，安装结束后服务器会自动重启。
3. 系统重启完成后，手动修改配置文件。

   > vi/opt/zs-sdp/controller/app/service/config/controller_spa.yml
   >
   > 末尾追加需要访问控制中心的终端pc设备IP段，英文逗号分隔。
<img width="663" height="200" alt="image" src="https://github.com/user-attachments/assets/d5ceedad-a9eb-45cd-804d-4e5706464bda" />

4. 修改零信任控制服务的配置文件，把接入网口名称修改为与接入网口名称一致。
   > vi/opt/zs-sdp/controller/app/service/config/controller_common.yml
<img width="617" height="654" alt="image" src="https://github.com/user-attachments/assets/5eb37019-ce5d-4b9f-a6da-1033aa61adcc" />

5. 修改零信任网关服务的配置文件，把接入网口名称修改为与接入网口名称一致。
   > vi/opt/zs-sdp/gateway/app/service/config/gateway_spa.yml
<img width="752" height="190" alt="image" src="https://github.com/user-attachments/assets/4c14187a-ce6a-4cef-9372-d8fbbd75d70f" />

6. 服务重启
   > systemctl restart controller_agent

7. 确认服务状态：
  打开浏览器输入控制中心IP：https://{服务器IP}:6443，输入管理员账号密码后即可登录。管理员默认账号密码：super/12345678。

   _出现以下界面提示说明服务器启动成功：_
   <img width="774" height="414" alt="image" src="https://github.com/user-attachments/assets/a9626bd5-490c-44a4-a267-5fb7c1ee39f0" />


   _好戏开始，接着奏乐接着舞！_

### 🔧 系统服务设置

至锐联零信任系统包含2个核心服务：控制中心、网关。在免费版中，控制中心和网关都安装在同一个系统中。

1. 网关服务、控制中心服务ID配置。
   浏览器访问https://{服务器IP}:5443网关配置页面。
   在“注册控制中心配置”页面，复制网关ID。
<img width="741" height="521" alt="image" src="https://github.com/user-attachments/assets/0ba4eefb-9891-40a4-9ee0-8c6c9acc7f85" />

   浏览器访问https://{服务器IP}:6443控制中心配置页面。
   在网关管理页面，点击“新增网关”，输入刚刚复制的网关ID，并点击生成Token令牌，然后点击确定保存。
   复制生成的Token令牌。

   回到https://{服务器IP}:5443网关配置页面。
   将刚刚复制的token令牌粘贴到“网关TOKEN”配置项中，点击确定保存。
<img width="760" height="514" alt="image" src="https://github.com/user-attachments/assets/fd86b0fb-0c24-4c07-bce1-90bb322af684" />
   
2. 网关服务、控制中心服务许可证配置。
   浏览器访问https://{服务器IP}:6443控制中心配置页面。
   在系统管理-通信证书管理页面，点击“生成证书”。填写证明名称、足够长的有效期、备注，用途选择“网关”，然后确定。
<img width="516" height="424" alt="image" src="https://github.com/user-attachments/assets/0b52826b-37e2-4758-81da-a84e5e87d6d3" />
   列表会新增刚生成的证书，点击“下载”。

   浏览器访问https://{服务器IP}:5443网关配置页面。
   进入“注册控制中心配置”页面，在通信证书区域上传刚刚下载的证书，点击确定。
<img width="735" height="519" alt="image" src="https://github.com/user-attachments/assets/b6f50ef7-bd5b-4150-bf85-ba6df4076919" />

3. 启用网关
  浏览器访问https://{服务器IP}:6443控制中心配置页面。
  在网关管理页面中，查看网关状态。默认是停用状态，手动启用。
<img width="789" height="142" alt="image" src="https://github.com/user-attachments/assets/d62f390a-b340-4fee-a16c-9d22d460b48c" />
   
  浏览器访问https://{服务器IP}:5443网关配置页面。
  在“注册控制中心配置”页面，状态为：已连接，说明该系统已部署成功。

### 🔧 客户端


## 🎬 典型使用场景配置
<img width="599" height="755" alt="image" src="https://github.com/user-attachments/assets/68f50f22-8497-416d-bd46-4489832eb4c4" />

### 📝 Web应用
### 🔧 在外网访问内网PC

## 📚 技术文档

- [Quickstart](https://ragflow.io/docs/dev/)
- [Configuration](https://ragflow.io/docs/dev/configurations)
- [Release notes](https://ragflow.io/docs/dev/release_notes)
- [User guides](https://ragflow.io/docs/dev/category/guides)
- [Developer guides](https://ragflow.io/docs/dev/category/developers)
- [References](https://ragflow.io/docs/dev/category/references)
- [FAQs](https://ragflow.io/docs/dev/faq)

## 📜 路线图

详见 [RAGFlow Roadmap 2025](https://github.com/infiniflow/ragflow/issues/4214) 。

## 🏄 开源社区

- [GitHub Discussions](https://github.com/orgs/infiniflow/discussions)

## 🤝 商务合作

- [预约咨询](https://aao615odquw.feishu.cn/share/base/form/shrcnjw7QleretCLqh1nuPo1xxh)

## 👥 加入社区

扫二维码添加 RAGFlow 小助手，进 RAGFlow 交流群。

<p align="center">
  <img src="https://github.com/infiniflow/ragflow/assets/7248/bccf284f-46f2-4445-9809-8f1030fb7585" width=50% height=50%>
</p>
