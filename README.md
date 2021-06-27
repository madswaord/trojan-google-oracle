# trojan-google-oracle  
set up trojan services on centos7  
#准备工作  
1.google cloud vps / oracle cloud vps  




#搭建Trojan  
一.关掉selinux  
 sudo -i  
 sestatus  
 cat /etc/selinux/config  
 sed -i '/SELINUX/s/enforcing/disabled/' /etc/selinux/config  
 reboot  
 
 重新连接后
 sudo -i  
 sestatus #查看状态  
 
二.关掉centos 防火墙  
 
 firewall-cmd --state #查看防火墙状态    
 systemctl stop firewalld.service #关闭防火墙    
 systemctl disable firewalld.service #禁止防火墙开机后启动  
 
三.安装基础依赖环境

 yum -y install wget  

  
四.开始运行Trojan安装代码  
 三个代码必须分开以确保能拿到证书  
 
 1. wget -N --no-check-certificate "https://raw.githubusercontent.com/V2RaySSR/Trojansh/master/trojan1.sh" && chmod +x trojan1.sh && ./trojan1.sh  
 按提示填入 cloudflare解析新域名至vps xxx.xxxx.com, 系统开始部署nginx及trojan， 打开 http://xxx.xxxx.com 可看到站点  
   
   
 2. 按顺序输入以下命令安装  
   1. yum update -y  
   2. yum install -y curl  
   3. yum install -y socat  
   4. curl https://get.acme.sh | sh
   5. 安装 Acme 脚本之后，请先执行下面的命令（下面的邮箱为你的邮箱）
~/.acme.sh/acme.sh --register-account -m xxxx@xxxx.com  
 3. Nginx 的方式验证申请  
  ~/.acme.sh/acme.sh --issue  -d mydomain.com   --nginx  #域名要替换成自己的  
  
 4. 安装证书到指定文件夹  
  ~/.acme.sh/acme.sh --installcert -d mydomain.com --key-file /root/private.key --fullchain-file /root/cert.crt  #域名要记得替换  
  
 5. wget -N --no-check-certificate "https://raw.githubusercontent.com/V2RaySSR/Trojansh/master/trojan2.sh" && chmod +x trojan2.sh && ./trojan2.sh  
 6. 提示证书已签发后进行下一步 否则重复2，3，4后再输入以下  
   wget -N --no-check-certificate "https://raw.githubusercontent.com/V2RaySSR/Trojansh/master/trojan3.sh" && chmod +x trojan3.sh && ./trojan3.sh  
  成功后保存trojan账户信息密码  
  
五. 安装bbr加速  
  wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh  
  选2安装 选7  
  进入安装界面 ./tcp.sh  
  
 
