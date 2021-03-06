##  [落网]音乐

* 落网的音乐逼格真的很高，都是自己喜欢的民谣类型，故爬虫抓取之。

### 说明
* 整个网站还是很简单的，没有模拟登陆，验证码啥的，甚至请求头都不用写。知乎查了一下落网历史，发现听不容易的，所以爬虫也不要写的太暴力，温柔的爬取就行了。

### 准备
* 工具：python 2.7,PyCharm
* 类库：Requests,BeautifulSoup,os

### 分析
* 进入落网官网，发现如下图所示,其中804就是期刊，每一期都有十几首音乐。
![](http://7xrl8j.com1.z0.glb.clouddn.com/%E6%AF%8F%E4%B8%80%E6%9C%9F%E6%AD%8C%E5%8D%95.jpg)

* 点击页面进入HTML元素页面，可以看见歌曲名字，专辑名，歌者，但是怎么没有歌曲资源的url？
![](http://7xrl8j.com1.z0.glb.clouddn.com/%E6%AD%8C%E6%9B%B2%E5%90%8D%E5%AD%97.jpg)

* 没有歌曲的url我们就不能下载，那么我们要看看我们每一次换歌曲，发生了什么请求，点击审查元素，如下结果
![](http://7xrl8j.com1.z0.glb.clouddn.com/%E6%AD%8C%E6%9B%B2url.jpg)

* 如上图所示一个Request url，我们复制进浏览器地址输入栏，发现如下所示，没错这就是我们下载的url了
![](http://7xrl8j.com1.z0.glb.clouddn.com/%E6%AD%8C%E6%9B%B2.jpg)

### 开始
* 开始之前我们要获取歌曲相应的信息，我们采用bs这个库来解析Html元素
* 我们采用requests这个库来进行网络请求与下载，下载音乐就要用到稍微逼格高一点的用法了，我们下载它的响应流文件，可参考
* [Requests响应体内容工作流](http://cn.python-requests.org/en/latest/user/advanced.html)

### 总结
* 抓取还是比较简单的
* 我们抓取的目的就是把歌曲下载到本地，自由不用联网的听，速度个人感觉不要太追求，不要坑人家服务器啊。

### 参考
* [落网爬虫](https://github.com/shuson/luooder.git)

### 结果
![](http://7xrl8j.com1.z0.glb.clouddn.com/%E7%BB%93%E6%9E%9C.jpg)

##爬虫基础

* [Python基础](http://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000)
* [爬虫初步一](http://cuiqingcai.com/1052.html)
* [爬虫初步二](http://zhuanlan.zhihu.com/xlz-d)

##爬虫进阶
* [Scrapy入门文档](http://scrapy-chs.readthedocs.org/zh_CN/0.24/intro/tutorial.html)
* [Scrapy初级实战](http://www.ituring.com.cn/article/114408)
* [Scrapy初级实战之数据可视化](http://aljun.me/post/9)
  
# 豆瓣爬虫
* [豆瓣爬虫裸写版](http://www.thinksaas.cn/group/topic/353600/)

# 百度爬虫
####一：py2.7 根据关键字从百度下载图片，并且能够根据需要过滤图片。
* [py3.0作者博客](http://lovenight.github.io)  **Thank you**
* 最近做App需要图片资源，就想写个爬虫爬，想起来以前收藏的py3.0版本，改成2.7版本。
* 改动之后下载图片的数量可以**自己控制**，下载之后的图片可**根据尺寸保留**。

# 知乎爬虫
#####一：firstLogin模拟登录知乎--代码解读思路整理。
* 很多网站需要登录才能访问更多的内容，so登录必不可少，这部分代码也是我fork的源码的author.py（在第二部分可见，尊重作者，感谢：）
* 首先要想模拟登录，浏览器的工作原理一定要了解一点，推荐Chorme浏览器自带的审查元素（右键即可）然后观察Network的变化
* 模拟登录首先要构建Header请求头，这是让请求网站认为你是浏览器（not spider）
* 第二步要获取xsrf--详细请看http://baike.baidu.com/link?url=x5M7ywYtlBL5LDGsZ61VTJHzS582Y1uZnXgor_LszDF0k7-BY7RA8YwkJ02yxxk-hAANTw32wcHGRRl3Xqi2-a  我们要做的就是利用re或者bs去相应的网站获得这个参数，以证明我们不是坏银==
* 正确输入账号密码之后，肯定要输入验证码啦==简单的思路就是把验证码下载下来，然后人眼识别，手动填入（当然大神的源码中，能够直接破解，自动填写，但是在我的win7上好像不可以==）所以我稍微改了一下，用网页自动打开==
* 首次登陆成功之后，以后肯定不想重复再做这些啦，所以有cookie的存在啊~~注意一点：firstLogin代码执行并不是一开始就执行main函数--会先检查cookie==
* 在firstLogin代码里面有详细的步骤（删除了一些原来大神的完善代码），只是为了自己更好理解一下，思路更加清晰一些(尊重产权==)

#####二：getImgs爬取知乎问题下的图片--女生拥有短发是怎样一种体验？
* 这一小段代码作用是，从知乎网上down图片，之前看到一个帖子--女生短发是一种什么样的体验？看到里面好多美女图片，就想着全部下载下来==
* 登录的代码比较简单（大都大同小异），引用的是这位大牛写的author.py模块--https://github.com/wuchangfeng/zhihu-python--自己也在学习他的源码，down在工程里，索性直接引用了。十分欣赏。
* 遇到网页需要加载更多时候，思路我看了http://lovenight.github.io这位大牛的，后来发现1中的代码也有这一部分的处理，我就自己对着浏览器的请求以及1中大神的代码，写出来了。
* 之所以没有pull到1中大神project中,因为自己代码太渣。总之，会继续加上新的想法的。加油。

####三：getQuestion_topic爬取某个话题下面的所有问题。
* 输入“生活”这个话题时，浏览器返回http://www.zhihu.com/topic/19551147这个url，其中19551147就是这个话题的link-id。
* 上面那个link-id 很重要http://www.zhihu.com/topic/******/questions?page=# 。用link-id替换这个*****，用数字（1，2,3....）替换#
* 代码已写，思路以上。
* 可以文件存储或者数据库存储。
* 后面的自己不想写了，感觉没啥意思，准备爬全局问题，监测一天的问题导向。

####四：**getImgs**爬取知乎问题下的图片--女生拥有短发是怎样一种体验？
* 加上了Thread,Quene跑的快飞起了--五六分钟爬了1000条左右
* 加上的异常处理，碰到了不能下载下来的，直接跳过去
* 线程的知识参考[简书作者](http://www.jianshu.com/p/544d406e0875)**感谢**

####五：要干嘛？还没想好==
* 所有话题下面的问题http://www.zhihu.com/topic/19776751/top-answers

####六：getFocus批量关注某个话题下面的用户
* 详细请见代码
* 有点疑问 批量获得关注者 那个start参数有什么规律==
* 更新了最新的代码，start是十位数的时间戳

##### todolist
* 把一中的代码优化成多线程，跑的太慢了，自己就爬了大概400多就关了它(而答案的数量有1560，一个答案至少一张图片吧)
* 爬取知乎神评论，网上看到了关键的思想，好像有点数据挖掘的意思，会尽快弄出来
* 爬取某一天知乎出现的评论最高的词或者其他的，用数据挖掘,分析的思想来处理
* 爬取某个用户关注,回答，收藏等信息来分析该用户的行为特征.....
