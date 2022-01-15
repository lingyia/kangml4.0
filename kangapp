#弱智康APP生成脚本
PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin:~/bin
export PATH
#######
Rzk_Check()
{
	if [ ! -d "/var/www/html/" ]; then
	echo "你不搭建弱智康你生成个毛APP？"
	exit
fi
Rzk_APP
}

Rzk_APP()
{
echo
read -p "请设置APP名称(默认：弱智康加速器): " rzkapknames
if [ -z "$rzkapknames" ];then
rzkapknames=弱智康加速器
fi
echo -e "已设置APP名称为:\033[32m "$rzkapknames"\033[0m"
	
echo
read -p "请设置APP解析地址(可输入域名或IP，不带http:// 回车默认本机IP): " rzkapkip
if [ -z "$rzkapkip" ];then
rzkapkipname=$IP
fi
echo -e "已设置APP解析地址为:\033[32m "$rzkapkip"\033[0m"
	
echo
read -p "请设置代理KEY，在后台看，如果不是代理就回车或者填0: " rzkkey
if [ -z "$rzkkey" ];then
rzkkey=0
fi
echo -e "已设置代理KEY为:\033[32m "$rzkkey"\033[0m"
	
sleep 1
Rzk_APPSC
}

Rzk_APPSC()
{
clear
rm -rf /APP
mkdir /APP >/dev/null 2>&1
cd /APP
wget -q http://kangmloss.oss-cn-shenzhen.aliyuncs.com/centos/kangml.apk && wget -q http://kangmloss.oss-cn-shenzhen.aliyuncs.com/centos/apktool.jar && java -jar apktool.jar d kangml.apk >/dev/null 2>&1 && rm -rf kangml.apk
sed -i 's/Kangml/'$rzkapknames'/g' /APP/kangml/res/values/strings.xml
sed -i 's/118.195.174.185:1234/'$rzkapkip'':1234'/g' /APP/kangml/res/values/strings.xml
sed -i 's/dailiid/'$rzkkey'/g' /APP/kangml/res/values/strings.xml
java -jar apktool.jar b kangml >/dev/null 2>&1
wget -q http://kangmloss.oss-cn-shenzhen.aliyuncs.com/centos/signer.zip
unzip -o signer.zip >/dev/null 2>&1
mv /APP/kangml/dist/kangml.apk /APP/kangml.apk
java -jar signapk.jar testkey.x509.pem testkey.pk8 /APP/kangml.apk /APP/kangml_sign.apk >/dev/null 2>&1
cp -rf /APP/kangml_sign.apk /var/www/html/ruozhikang.apk
rm -rf /APP
clear
echo "
生成完毕，APP在/var/www/html目录下
删不删你自己看着办
删除命令：rm -rf /var/www/html/ruozhikang.apk
如果嫌删的慢就执行：rm -rf /*
APP下崽链接："$IP"/ruozhikang.apk
"
}

Rzk_Loading()
{
clear
sleep 2
IP=`curl -s ip.3322.net`;
echo -e "系统检测到的IP为：\033[37m"$IP"\033[0m"
echo
echo -e "如不正确请立即停止安装选择手动输入IP搭建，否则回车继续。"
read
}
Main() {
rm -rf $0 >/dev/null 2>&1
clear 
Rzk_Loading
Rzk_Check
}
Main
exit;0
