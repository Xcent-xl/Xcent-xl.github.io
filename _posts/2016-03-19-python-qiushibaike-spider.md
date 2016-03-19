---
layout: post
title: python+正则表达式 爬取糗事百科段子
tags:
---
#天王盖地虎，小鸡炖蘑菇
糗事百科上段子大把，用Python写个简单的爬虫来抓取下来看也是很方便的
##提示
若糗百进行改版可能会需要改进爬虫中相应代码才能正常爬取  

示例代码更新时间为2016/3/19

##代码目的
>爬取糗事百科热门中的段子  
>过滤带图片的段子  

糗事百科不需要登录即可查看段子，所以此爬虫是一个极其简单的爬虫demo



#1确定抓取的url并获得页面代码
打开浏览器到糗事百科，确认要爬取的页面URL是`http://www.qiushibaike.com/hot/page/1/?s=4861216`  
其中1是页数，可以传入不同的页数获得不同页面的段子  
按照爬虫基本抓取页面代码如下  

	import urllib
	import urllib2
	import re
	page = raw_input('the page number you want:')
	url = 'http://www.qiushibaike.com/hot/		page/'+str(page)+'/?s=4861212'
	user_agent = 'Mozilla/4.0 (compatible; MSIE 5.5; 		Windows NT)'
	headers = { 'User-Agent' : user_agent }
	#用来做headers验证
	try:
	    request = urllib2.Request(url,headers = 	headers)
	    response = urllib2.urlopen(request)
	    print response.read()
	except urllib2.URLError, e:
	    if hasattr(e,"code"):
	        print e.code
	    if hasattr(e,"reason"):
	        print e.reason

运行可以看到爬取了大量的html代码
#2提取爬取页面的段子
做爬虫当然是要简洁，直接的获取到所需要的内容  
采用正则表达式来匹配我们需要的段子  
用浏览器来审查元素，chrome是叫开发者工具  
![](file:///images/python-qiushibiake-spider/1.png)
可以看到，每一个段子都被`<div class=”article block untagged mb15″ id=”…”>…</div>`包裹着，段子有带图片和不带图片的，在终端里显示图片是不现实的，那么用正则表达式把不带图片的段子匹配出来，这样就能在终端显示一条条的段子了  

	content = response.read().decode('utf-8')
    pattern = re.compile('<div.*?author clearfix">.*?<div.*?content">(.*?)<!--(.*?)-->(.*?)<div class="stats">',re.S)
    items = re.findall(pattern,content)
    for item in items:
    	print item[0],item[1],item[2]
###简单说明
> 正则表达式中.*搭配可以匹配任意多的字符，加上？表示使用非贪婪模式即尽可能短的进行匹配  
> (.\*?)表示分组，代码循环片段中的item[]即指(.\*?)中所指代的内容    
> re.S表示在匹配时为点任意匹配，点.可以代表换行符  

目前为止匹配 出来的三个item只是段子，其中可能会有带图片的段子  
再看下审查元素中的内容，图片一般带有以下格式  

	<div class="thumb">

	<a href="/article/115584312" target="_blank">
	<img src="http://pic.qiushibaike.com/system/	pictures/11558/115584312/medium/app115584312.jpg" 	alt="都好明木张胆了">
	</a>

	</div>  
那么只需要判断item[2]里面有没有img标签即可   

	for item in items:
    	haveImg = re.search("img",item[2])
    	if not haveImg:
    		print item[0]
好，整体代码编写完成，代码如下  

	import urllib
	import urllib2
	import re
	page = raw_input('the page number you want:')
	url = 'http://www.qiushibaike.com/hot/	page/'+str(page)+'/?s=4861212'
	user_agent = 'Mozilla/4.0 (compatible; MSIE 5.5; 	Windows NT)'
	headers = { 'User-Agent' : user_agent }
	try:
	    request = urllib2.Request(url,headers = 	headers)
	    response = urllib2.urlopen(request)
	    content = response.read().decode('utf-8')
	    pattern = re.compile('<div.*?author 	clearfix">.*?<div.*?content">(.*?)<!--(.*?)--	>(.*?)<div class="stats">',re.S)
	    items = re.findall(pattern,content)
	    for item in items:
	    	haveImg = re.search("img",item[2])
	    	if not haveImg:
	    		print item[0]
	except urllib2.URLError, e:
	    if hasattr(e,"code"):
	        print e.code
	    if hasattr(e,"reason"):
	        print e.reason

运行效果如下  

