<div align="center">
<img width="156" height="130" alt="image" src="https://github.com/user-attachments/assets/48180052-9a47-4c42-970d-22ebacf1f35c" />
</div>

<h4 align="center">
  <a href="[https://ragflow.io/docs/dev/](https://forum.zshield.net/d/5)">Document</a> |
  <a href="https://github.com/zxinfo/zhiriulian/">Roadmap</a> |
</h4>

<details open>
<summary><b>📕 目录</b></summary>

- 💡 [至锐联是什么？](#-至锐联是什么)
- 📌 [近期更新](#-近期更新)
- 🌟 [主要功能](#-主要功能)
- 🔎 [系统架构](#-系统架构)
- 🎬 [快速开始](#-快速开始)
- 🔧 [典型使用场景配置](#-典型使用场景配置)
- 📚 [技术文档](#-技术文档)
- 🤝 [商务合作](#-商务合作)
</details>

## 💡 至锐联是什么？

[至锐联]是一款零信任软件产品，专门为中小企业提供高安全、高效的外网接入企业内部的访问。使用至锐联产品，企业可以指定具体用户访问指定的应用、指定的设备、指定的端口，比使用VPN更加安全。
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

- 系统部署简单，可使用虚拟机部署。
- 无需改动现有网络架构，网关即插即用。

## 🔎 系统架构

<div align="center" style="margin-top:20px;margin-bottom:20px;">
<img width="514" height="228" alt="image" src="https://github.com/user-attachments/assets/5ed78799-e757-48b5-85db-3f0e8371d369" />
</div>

## 🎬 快速开始

### 📝 系统部署条件

- CPU >= 4 核
- RAM >= 4 GB
- Disk >= 20 GB
- OS: CentOS7.5, CentOS7.9(Minimal install)

### 🚀 系统安装
- [系统安装包](https://doc.zshield.net/index.php/s/8PrGFbEfRwyb3XA)
  
1. 将安装包：SDP2.0.3_all.tgz拷贝至系统中，解压，然后进入解压出来的sdp_install_pkg目录。
<!--img width="628" height="142" alt="image" src="https://github.com/user-attachments/assets/7e102147-a10f-4dcc-a99a-c0674512deb2" /-->

2. ./installer.sh执行安装程序，安装结束后服务器会自动重启。
3. 系统重启完成后，手动修改配置文件。
   > vi /opt/zs-sdp/controller/app/service/config/controller_spa.yml
   >
   > 末尾追加需要访问控制中心的终端pc设备IP段（格式例如：192.168.0.0/16），英文逗号分隔。
<img width="311" height="61" alt="image" src="https://github.com/user-attachments/assets/9dad16dd-2c99-420e-8045-f9ca0a4e4928" />

4. 修改零信任控制服务的配置文件，把接入网口名称修改为与接入网口名称一致。
   > vi /opt/zs-sdp/controller/app/service/config/controller_common.yml
   >
   > 找到spa_net_interface字段，将其修改为本机网口名称（例如：eth0）。
<img width="277" height="167" alt="image" src="https://github.com/user-attachments/assets/c3f74dab-2c79-4ffc-9804-f62296a9f648" />

5. 修改零信任网关服务的配置文件，把接入网口名称修改为与接入网口名称一致。
   > vi /opt/zs-sdp/gateway/app/service/config/gateway_spa.yml
   >
   > 找到net_interface字段，将其修改为本机网口名称（例如：eth0）。
<img width="237" height="50" alt="image" src="https://github.com/user-attachments/assets/e414ce35-747d-486c-8182-cdcd1018af79" />

6. 服务重启
   > systemctl restart controller_agent

7. 确认服务状态：
  打开浏览器访问https://{服务器IP}:6443，输入管理员账号密码后即可登录。管理员默认账号密码：super/12345678。
<!--img width="774" height="414" alt="image" src="https://github.com/user-attachments/assets/a9626bd5-490c-44a4-a267-5fb7c1ee39f0" /-->

### 🎮 系统服务设置

至锐联零信任系统包含2个核心服务：控制中心、网关。在免费版中，控制中心和网关都安装在同一个系统中。

1. 网关服务、控制中心服务ID配置

  - 浏览器访问网关管理系统 https://{服务器IP}:5443。在“注册控制中心配置”页面，复制网关ID。
<!--img width="741" height="521" alt="image" src="https://github.com/user-attachments/assets/0ba4eefb-9891-40a4-9ee0-8c6c9acc7f85" /-->

  - 浏览器访问控制中心管理系统 https://{服务器IP}:6443。在“网关管理”页面，点击“新增网关”，输入刚刚复制的网关ID，并点击生成Token令牌，然后点击确定保存。
     
  - 复制生成的Token令牌。回到网关管理系统 https://{服务器IP}:5443。将刚刚复制的token令牌粘贴到“网关TOKEN”配置项中，点击确定保存。
<!--img width="760" height="514" alt="image" src="https://github.com/user-attachments/assets/fd86b0fb-0c24-4c07-bce1-90bb322af684" /-->
   
2. 网关服务、控制中心服务许可证配置
   
  - 浏览器访问控制中心管理系统 https://{服务器IP}:6443。在“系统管理-通信证书管理”页面，点击“生成证书”。填写证明名称、足够长的有效期、备注，用途选择“网关”，然后确定。
<!--img width="516" height="424" alt="image" src="https://github.com/user-attachments/assets/0b52826b-37e2-4758-81da-a84e5e87d6d3" /-->

  - 列表会新增刚生成的证书，点击“下载”。浏览器访问网关管理系统 https://{服务器IP}:5443。进入“注册控制中心配置”页面，在通信证书区域上传刚刚下载的证书，点击确定。
<!--img width="735" height="519" alt="image" src="https://github.com/user-attachments/assets/b6f50ef7-bd5b-4150-bf85-ba6df4076919" /-->

3. 启用网关
   
  - 浏览器访问控制中心管理系统 https://{服务器IP}:6443。在“网关管理”页面中，查看网关状态。默认是停用状态，手动启用。
<!--img width="789" height="142" alt="image" src="https://github.com/user-attachments/assets/d62f390a-b340-4fee-a16c-9d22d460b48c" /-->
   
  - 浏览器访问网关管理系统 https://{服务器IP}:5443。在“注册控制中心配置”页面，查看到状态为：已连接，说明该系统已部署成功。

4. 企业外网映射
   
   通常使用至锐联，是让用户在互联网能访问企业内部指定的资源。此时需要将至锐联的设备IP地址、服务端口映射到外网固定IP地址。
   需要映射的端口：
   
  - 5555（UDP），SPA端口
  - 6666（TCP&UDP），客户端登录认证端口
  - 8888（UDP），建立隧道连接服务使用
  - 10001（TCP&UDP），代理端口
  - 443（TCP），用户登录web客户端使用，如仅使用客户端软件外网接入，则不需要映射该端口

### 🚀 系统管理

1. 管理员浏览器访问控制中心管理系统 https://{服务器IP}:6443
2. 创建用户：进入“用户管理-用户管理”页面。点击“新增”。输入用户名；密码；有效期选择足够长的时间。确定保存。
   
### 🔧 客户端

  至锐联零信任免费版的客户端目前支持Windows系统。
- [客户端安装包](https://doc.zshield.net/index.php/s/T868WqFpFJrWBR4)

1. 下载客户端安装包。
2. 双击运行安装程序即开始安装。安装过程预设有默认安装目录，如需要更换位置请点击<浏览>选择安装目录。点击<安装>，等待安装完成。
3. 启动客户端。首先需要设置访问至锐联零信任的地址（如果是在互联网外部访问企业的至锐联，则需要设置为外网映射后的地址）。输入用户、密码后登录。
<!--img width="618" height="427" alt="image" src="https://github.com/user-attachments/assets/ca44b867-3aa2-4bb7-b3d3-921bffabf96e" /-->
4. 登录成功后，如果在系统中设置了用户可以访问的资源应用，则可以看到应用卡片。
   具体如何配置资源应用，参考下方：典型使用场景配置。

## 🎬 典型使用场景配置
<!--img width="599" height="755" alt="image" src="https://github.com/user-attachments/assets/68f50f22-8497-416d-bd46-4489832eb4c4" /-->

### 📝 从外网访问企业内部Web应用

  允许指定企业员工在家里电脑访问特定的Web管理系统。
1. 管理员进入至锐联控制中心管理系统 https://{服务器IP}:6443
2. 创建应用：进入“资源发布-应用管理”页面。点击“新增”。输入应用名称；应用类型选择“web应用”；是否展示选择“显示”；在下方的地址信息中，主地址填写web管理系统的入口URL（例如http://192.168.100.185:3030/home/ ）；在下方的应用地址中，协议选择BOTH，目的地址填写Web系统的IP地址（例如：192.168.100.185）、端口（例如：3030）。如果web管理系统有多个附带的访问IP地址、端口，可以添加多个。确定保存。
3. 创建访问策略：进入“策略中心-访问控制策略”页面。点击“新增”。输入策略名称；授权应用选择刚才建立的应用。确定保存。
4. 授权用户使用：进入“用户管理-用户授权”页面。对指定的用户点击“授权”。在授权访问策略中选择刚才建立的访问策略。确定保存。
5. 以用户身份打开客户端软件，登录进入后，主界面会显示一个Web应用卡片。点击该应用卡片，会打开本地浏览器程序访问该内部Web系统。

### 🔨 在外网访问企业内部Windows计算机（使用RDP协议）
  允许指定企业员工从家里电脑访问公司内部的办公电脑。
  
1. 管理员进入至锐联控制中心管理系统 https://{服务器IP}:6443
2. 创建应用：进入“资源发布-应用管理”页面。点击“新增”。输入应用名称；应用类型选择“隧道应用”；是否展示选择“显示”；在下方的地址信息中，协议选择BOTH，目的地址填写被访问的Windows计算机的IP地址，端口设置为3389（RDP协议端口）。确定保存。
3. 创建访问策略：进入“策略中心-访问控制策略”页面。点击“新增”。输入策略名称；授权应用选择刚才建立的应用。确定保存。
4. 授权用户使用：进入“用户管理-用户授权”页面。对指定的用户点击“授权”。在授权访问策略中选择刚才建立的访问策略。确定保存。
5. 以用户身份打开客户端软件，登录进入后，主界面会显示一个RDP应用卡片。点击该应用卡片，在弹出框中，应用路径填写：%windir%\system32\mstsc.exe。确定保存。
6. 再次点击该应用卡片，会打开本地RDP客户端程序，输入被访问的企业内网Windows计算机IP地址，即可登入使用。
7. 【备注】企业内网Windows计算机需要打开远程RDP访问许可。通常方法为：在Windows我的电脑右键，属性，找到远程桌面选项，打开启用远程桌面开关。
<!--img width="800" height="632" alt="image" src="https://github.com/user-attachments/assets/61cf74e9-dc04-40c3-8bd9-aafaf65c7619" /-->

## 📚 技术文档
[网站论坛](https://forum.zshield.net/d/5)

包括：
- [部署手册](https://doc.zshield.net/index.php/s/ynFDCWQjzt2cxkD)
- [管理员手册](https://doc.zshield.net/index.php/s/99oa6edk8BZEZGn)
- [用户手册](https://doc.zshield.net/index.php/s/aGkd3QN5Kx2mwsi)

## 🤝 商务合作
  至锐联企业版功能：
  1. 支持导入企业域控
  2. 支持多个网关
  3. 支持集群
  4. 支持Linux客户端
  5. 专业技术支持服务
- [咨询](mail: contact@zshield.net)


