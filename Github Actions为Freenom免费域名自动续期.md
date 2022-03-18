Github Actions为Freenom免费域名自动续期
日期： July 29, 2020
今天说的教程是利用github actions执行php续期脚本（不需要有机器执行，有github账号就行），玩法也很简单，只要fork一下再配置一下就可以开玩了。

1、项目
php项目： https://github.com/luolongfei/freenom
docker：https://hub.docker.com/r/rouroux/freenom-automatic-renewal

2、准备
准备github账号一个。
发信邮箱：为了方便理解又称机器人邮箱，用于发送通知邮件。目前支持Gmail、QQ邮箱以及163邮箱，程序会自动判断发信邮箱类型并使用合适的配置。 因为谷歌的安全机制,不推荐推荐使用Gmail。推荐用163邮箱作为机器人邮箱。
收信邮箱：用于接收机器人发出的通知邮件。推荐使用QQ邮箱，QQ邮箱唯一的好处只是收到邮件会在QQ弹出消息。

3、设置邮箱
这里以163邮箱作为机器人邮箱为例。
在设置>POP3/SMTP/IMAP下，开启POP3/SMTP服务和IMAP/SMTP服务并保存。开启之后，会自动给你授权密码，密码单独保存，只显示一次。
这里设置好之后，开始下一步。

4、部署

（1）：Fork仓库
进入项目地址，点击右上方的Fork

（2）依次点击自己仓库上栏 【Setting】-> 【Secrets】 -> 【Add a new secret】

（3）在你 Fork 的本仓库下的 Settings -> Secrets 页面追加以下几个secret变量。

这几个变量是必须的：
FREENOM_USERNAME # Freenom账户 Freenom Account
FREENOM_PASSWORD # Freenom账户密码
MAIL_USERNAME #机器人邮箱，就是上一步中设置的163邮箱。
MAIL_PASSWORD #这里填写你获得的授权密码
TO #接收通知的邮箱
MAIL_ENABLE #是否启用邮件推送功能true：启用，false：不启用
这几个是可选配置，因为不是每个人都有电报或者多账号。
MULTIPLE_ACCOUNTS
TELEGRAM_CHAT_ID
TELEGRAM_BOT_TOKEN
TELEGRAM_BOT_ENABLE
NOTICE_FREQ

5、启用Actions

（1） 点击Action再点击I understand my workflows, go ahead and enable them 

（2） 修改任意文件后提交一次 

6、最后

Freenom是地球上唯一一个提供免费顶级域名的商家，如果你申请了一堆，还是不同时段，那么手动续期还是会累死个人的。这个时候自动续期域名不可少。脚本每天 10:00 执行，如果你需要修改，找到run.yml 文件，路径：freenom/.github/workflows/run.yml

由于创建虚拟环境会消耗 2 分钟左右的时间，故任务会延迟 2 分钟左右执行。

参考
大鸟博客，https://www.daniao.org/9787.html
