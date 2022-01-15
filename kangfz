#弱智康孵崽脚本
PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin:~/bin
export PATH
#######
Rzk_Check()
{
if [ ! -f /etc/openvpn/auth_config.conf ]; then
	echo
	echo "\033[1;31m\033[05m 你不搭建弱智康你孵崽个毛啊,请搭建后执行孵崽脚本！ \033[0m"
	exit
fi
if [ ! -f /var/www/html/config.php ]; then
	echo
	echo "\033[1;31m\033[05m 你不搭建弱智康你孵崽个毛啊,请搭建后执行孵崽脚本！ \033[0m"
	exit
fi
}
Rzk_Fuji()
{
	clear
	echo
	read -p "请输入主鸡数据库账号: " rzksqluser
	if [ -z "$rzksqluser" ];then
	rzksqluser=
	fi
	
	echo
	read -p "请输入主鸡数据库密码: " rzksqlpass
	if [ -z "$rzksqlpass" ];then
	rzksqlpass=
	fi
	
	echo
	read -p "请输入主鸡数据库端口: " rzksqlport
	if [ -z "$rzksqlport" ];then
	rzksqlport=
	fi
	
	echo
	read -p "请输入主鸡服务器IP: " rzksqlip
	if [ -z "$rzksqlip" ];then
	rzksqlip=
	fi
	
	echo
	echo "正在为您的系统进行孵崽，请稍等......"
	sleep 3
	SQL_RESULT=`mysql -h${rzksqlip} -P${rzksqlport} -u${rzksqluser} -p${rzksqlpass} -e quit 2>&1`;
	SQL_RESULT_LEN=${#SQL_RESULT};
	if [[ !${SQL_RESULT_LEN} -eq 0 ]];then
	echo
	echo "连接至主鸡数据库失败，请检查您的主鸡数据库密码后重试，脚本停止！";
	exit;
	fi

clear
rm -rf /etc/openvpn/auth_config.conf
echo '#!/bin/bash
mysql_host='$rzksqlip'
mysql_user='$rzksqluser'
mysql_pass='$rzksqlpass'
mysql_port='$rzksqlport'
mysql_data=vpndata
address='$IP'
unset_time=60
del="/root/res/del"
status_file_1="/var/www/html/openvpn_api/user-status-tcp.txt 7075 1194 tcp"
status_file_2="/var/www/html/openvpn_api/user-status-udp.txt 7079 53 udp"
sleep=3'>/etc/openvpn/auth_config.conf && chmod -R 0777 /etc/openvpn/auth_config.conf
rm -rf /var/www/html/config.php
echo '<?php
/* 请勿修改 */
define("_host_","'$rzksqlip'");
define("_user_","'$rzksqluser'");
define("_pass_","'$rzksqlpass'");
define("_port_","'$rzksqlport'");
define("_ov_","vpndata");
define("_openvpn_","openvpn");
define("_iuser_","iuser");
define("_ipass_","pass");
define("_isent_","isent");
define("_irecv_","irecv");
define("_starttime_","starttime");
define("_endtime_","endtime");
define("_maxll_","maxll");
define("_other_","dlid,tian");
define("_i_","i");'>/var/www/html/config.php && chmod -R 0777 /var/www/html/config.php
systemctl disable mariadb.service >/dev/null 2>&1
	if [[ $? -eq 0 ]];then
	echo "" >/dev/null 2>&1
	else
	echo "警告！MariaDB停止失败！请手动停止MariaDB查看失败原因！脚本停止！"
	exit
	fi
	
	sleep 5
	echo
	echo "已成功为您的系统进行孵崽！主鸡IP为："$rzksqlip"！"
}
Rzk_Zhuji()
{
	clear
	echo
	read -p "请输入本地数据库账号: " rzksqluser
	if [ -z "$rzksqluser" ];then
	rzksqluser=
	fi
	
	echo
	read -p "请输入本地数据库密码: " rzksqlpass
	if [ -z "$rzksqlpass" ];then
	rzksqlpass=
	fi
	
	echo
	read -p "请输入本地数据库端口: " rzksqlport
	if [ -z "$rzksqlport" ];then
	rzksqlport=
	fi
	
	echo
	echo "正在为您的系统进行孵崽，请稍等......"
	sleep 3
	SQL_RESULT=`mysql -hlocalhost -P${rzksqlport} -u${rzksqluser} -p${rzksqlpass} -e quit 2>&1`;
	SQL_RESULT_LEN=${#SQL_RESULT};
	if [[ !${SQL_RESULT_LEN} -eq 0 ]];then
	echo
	echo "数据库连接失败，请检查您的数据库密码后重试，脚本停止！";
	exit;
	fi
	
	iptables -A INPUT -p tcp -m tcp --dport 3306 -j ACCEPT
	service iptables save >/dev/null 2>&1
	systemctl restart iptables.service >/dev/null 2>&1
	if [[ $? -eq 0 ]];then
	echo "" >/dev/null 2>&1
	else
	echo "警告！IPtables重启失败！请手动重启IPtables查看失败原因！脚本停止！"
	exit
	fi
	mysql -hlocalhost -P${rzksqlport} -u${rzksqluser} -p${rzksqlpass} <<EOF
grant all privileges on *.* to '${rzksqluser}'@'%' identified by '${rzksqlpass}' with grant option;
flush privileges;
EOF
	systemctl restart mariadb.service >/dev/null 2>&1
	if [[ $? -eq 0 ]];then
	echo "" >/dev/null 2>&1
	else
	echo "警告！MariaDB重启失败！请手动重启MariaDB查看失败原因！脚本停止！"
	exit
	fi
	
	sleep 5
	echo
	echo "已成功为您的系统进行孵崽！您可以在任何搭载弱智康系统鸡器上对接至本服务器！"
	
}
Rzk_Mean()
{
	clear
	sleep 2
	echo
	echo -e "************************************************"
	echo -e "           欢迎使用弱智康快速孵崽助手          "
	echo -e "************************************************"
	echo -e "请选择："
	echo
	echo -e "\033[36m 1、主鸡开启远程数据库权限 \033[0m \033[31m（在主鸡执行，主鸡只需开启一次，后续直接副鸡对接主鸡即可）\033[0m"
	echo ""
	echo -e "\033[36m 2、孵鸡连接主鸡数据库 \033[0m \033[31m（在孵崽鸡执行，每个鸡子无限孵崽主鸡，仅生效最后一次孵崽的鸡器）\033[0m"
	echo
	echo -e "\033[36m 3、退出脚本！\033[0m"
	echo
	echo 
	read -p " 请输入安装选项并回车: " a
	echo
	echo
	k=$a

	if [[ $k == 1 ]];then
	Rzk_Zhuji
	exit;0
	fi
	
	if [[ $k == 2 ]];then
	Rzk_Fuji
	exit;0
	fi

	if [[ $k == 3 ]];then
	exit;0
	fi	
	
	echo -e "\033[31m 输入错误！请重新运行脚本！\033[0m "
	exit;0
}
Rzk_Logo()
{
clear
sleep 2
IP=`curl -s ip.3322.net`;
echo -e "系统检测到的IP为：\033[37m"$IP"\033[0m"
echo
echo -e "如不正确请立即停止安装选择手动输入IP搭建，否则回车继续。"
read
Rzk_Mean
}
Main() {
rm -rf $0 >/dev/null 2>&1
clear 
Rzk_Check
Rzk_Logo
}
Main
exit;0
