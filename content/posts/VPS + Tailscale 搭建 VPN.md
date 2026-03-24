---
title: "VPS + Tailscale 搭建 VPN"
date: 2026-03-23T14:08:56+08:00
draft: false
url: "posts/vps"

ShowToc: true
TocOpen: true

tags: ["vpn","vps","vultr","tailscale"]
categories: ["tech"]
---


**VPS + Tailscale 搭建 VPN 使用说明书（小白版）**

所需设备
- 一台 Mac 💻
- 一双手 👋

### 1. 购买 VPS

- 注册 VPS 服务商（如 UltaHost、Vultr、Hetzner、Linode、DigitalOcean 等），我用的是 Vultr
- 选择合适的套餐：一般选 [shared CPU](https://eddy.lu/posts/host/) 足够。1 vCPU / 1 GB 内存 / 25 GB SSD，USD 5/month
- 选定节点（如日本 / 新加坡，取决于你想要的出口 IP）
- 操作系统建议选：**Ubuntu 22.04 LTS (64-bit)**

购买后，你会得到：  
- 公网 IP（例如 45.xx.xxx.xxx）
- root 用户名和初始密码 

![](/img/vpsip.png)

  
### 2. 连接 VPS
  
在 Mac 终端机输入：  
  
ssh root@<你的VPS_IP>  
```
ssh root@45.xx.xxx.xxx
```
  
首次登录会提示 

**Are you sure you want to continue connecting (yes/no)? → 输入 yes。**  
然后输入服务商提供的 root 密码。  
  
### 3. 创建普通用户（避免直接用 root）

```
adduser eddy  
```

给系统 sudo 权限，理解为管理员权限。
```
usermod -aG sudo eddy
```

  
⚠️ eddy 换成你想要创建的用户名。
  
测试：  
  
```
ssh eddy@<你的VPS_IP>  
```

期间可能提醒你更新密码。

👉 系统觉得“不够安全”，给你一个警告。
```
BAD PASSWORD: The password contains the user name in some form
```
```
Full Name []:
Room Number []:
Work Phone []:
Home Phone []:
Other []:
```
👉 这些全部可以，直接按 Enter 跳过。

最后它会问：
```
Is the information correct? [Y/n]
```
当然是 Y，不然呢？
  
### 4. 上传 SSH 公钥（免密登录）

✍️ **SSH key = 一把“不会被偷的钥匙”**
用来登录你的服务器（VPS），**替代密码**。
  
在 Mac 上生成密钥（如果还没有）：  
```
ssh-keygen -t ed25519 -C "eddy-mac"  
```

然后一路回车：
```
Enter file in which to save the key (...) → 回车
Enter passphrase → 可以回车（先简单点）
```
  
把公钥上传到 VPS 服务器：  
```
ssh-copy-id eddy@<你的VPS_IP>  
```

如果提示 Are you sure you want to continue connecting (yes/no)?

就给他 yes 下去。

然后会让你输入密码。

👉 输入你刚刚设置的 eddy 用户密码。（输入时不会显示，正常）。

成功后会看到类似：
```
Number of key(s) added: 1
```
✅ 你的 Mac 已经有“钥匙”可以登录服务器了

马上测试看看吧！
先退出服务器：
```
exit
```
然后重新登录：
```
ssh eddy@<你的VPS_IP>
```

👉 如果：

直接进去了
没有让你输密码

那就说明：

🎉 SSH key 登录成功



### 5. 更新系统
  
更新服务器的软件包，相当于手机系统更新 / App 更新。

⚠️ 先确认你已经在 eddy 用户下

终端应该是这样：
```
eddy@vultr:~$
```

```
sudo apt update && sudo apt upgrade -y  
```


如果看到 Pending kernel upgrade，不要慌，是内核更新了，需要重启。
```
sudo reboot
```
再重新登陆
```
ssh eddy@<你的VPS_IP>
```
  
### 6. 安装 Tailscale
  
 

```
curl -fsSL https://tailscale.com/install.sh | sh  
```


期间如果出现粉色的对话框，选 keep the local version currently installed

![](/img/installvps2.png)



这个界面你不用纠结，直接这样做：

✅ 保持默认勾选，直接按 Enter（OK）

![](/img/installvps3.png)


  
### 7. 启用 Exit Node
  

```
sudo tailscale up --ssh --advertise-exit-node --advertise-routes=0.0.0.0/0,::/0  
```
  
👉 它会输出一个 URL，把链接复制到浏览器，用 GitHub 或 Google 登录并授权。我用的是 Github。
  
### 8. 打开转发功能
1️⃣ 开启 IPv4 转发
```
echo 'net.ipv4.ip_forward = 1' | sudo tee -a /etc/sysctl.conf  
```
2️⃣ 开启 IPv6 转发（建议一起开）
```
echo 'net.ipv6.conf.all.forwarding = 1' | sudo tee -a /etc/sysctl.conf  
```
3️⃣ 让配置生效
```
sudo sysctl -p  
```

开启 exit node，在 VPS 上执行：

```
tailscale up --exit-node=45.76.110.122
```


### 9. 配置防火墙（UFW）
  
```
sudo ufw allow OpenSSH  
```
```
sudo ufw allow 41641/udp  
```
```
sudo ufw default deny incoming  
```
```
sudo ufw default allow outgoing  
```
```
sudo ufw default allow routed  
```
```
sudo ufw enable  
```

👉 它会问：
```
Command may disrupt existing ssh connections. Proceed with operation (y/n)?
```

👉 输入：

```
y
```

检查：  
  

```
sudo ufw status verbose  
```
  
👉 需要显示 allow (routed)，代表成功。

### 10. 在 Tailscale 后台启用 Exit Node  
1. 登录 [Tailscale 管理后台](https://login.tailscale.com/admin/machines)
2. 找到你的 VPS → 点开 → 勾选 **Use as Exit Node** → Save  
  


![](/img/exitnode.jpg)
  
### 11. 本地设备选择 Exit Node
- **Mac / iPhone / iPad**  
- 打开 Tailscale 客户端 → Settings → Exit Node → 选择你的 VPS  
- 测试



在 Safari/Chrome 访问 [https://whatismyipaddress.com](https://whatismyipaddress.com)，  
👉 IP 地址应显示为 VPS 的 IP（例如 45.xx.xxx.xxx）。  
  
📙 **说明书总结**  
- **VPS**：你租用的服务器，作为出口  
- **Tailscale**：用来安全连接 VPS 和设备  
- **Exit Node**：让 VPS 成为你的「网络跳板」  
- **结果**：手机/电脑 → 通过 Tailscale → VPS → 外网，出口 IP 在 VPS 所在国家  
- 出现很多「故障」，不懂问 AI 就好了

  