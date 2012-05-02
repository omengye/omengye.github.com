---
layout: post
title: "octopress on github"
date: 2012-05-01 21:34
comments: true
categories: octopress
tags: octopress
---
对wordpress烦shi了,来试试octopress把.
优点(抄的)
	1. 使用静态页面；
	2. 不使用数据库；
	3. 使用markdown标记语言编写文章；
	4. 可以与git紧密集成,方便地进行博客的版本管理；
	5. 可以于Github Pages集成,不需要单独的web hosting,只要你有github帐号即可。

首先的话就是构建git环境了,当然,文档中已经给的很清晰了,[linux里配置git](http://help.github.com/linux-set-up-git/)。

2.[对RVM也就是Ruby Version Manager的配置](http://octopress.org/docs/setup/rvm/)见此
{% codeblock lang:objc install RVM %}
bash -s stable < <(curl -s https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer)
echo '[[ -s "$HOME/.rvm/scripts/rvm" ]] && . "$HOME/.rvm/scripts/rvm" # Load RVM function' >> ~/.bash_profile
source ~/.bash_profile
rvm install 1.9.2 && rvm use 1.9.2
rvm rubygems latest
{% endcodeblock %}

3.把octopress用git clone到本地来搞,[这个就是文档了](http://octopress.org/docs/setup/)
{% codeblock lang:objc %}
git clone git://github.com/imathis/octopress.git octopress 
cd octopress
gem install bundler
bundle install
rake install #安装的这个是叫做classic的主题
{% endcodeblock %}

4.对于本地octopress的搞法[见此](http://octopress.org/docs/configuring/)
我要介绍的是这个叫做[octopress-tagcloud](https://github.com/tokkonopapa/octopress-tagcloud) 的东东,由于octopress没有默认的tags所以这玩意还是很有用处的,依照README安放目录把,亲们
{% codeblock lang:objc 不要放错哦,亲 %}
.
├─ plugins/
│  └── tag_cloud.rb
└─ source/
   └─ _includes/
      └─ custom/
         └─ asides/
            ├─ category_list.html
            └─ tag_cloud.html
{% endcodeblock %}
至于用法就是在每篇.markdown文本头部中添加这样的字符了
{% codeblock lang:objc %}
categories: xxx
tags: xxx
{% endcodeblock %}
现在来写一篇文章吧,
{% codeblock lang:objc %}
rake new_post["hello world"]
{% endcodeblock %}
需要强调的是要用markdown语法哦,可以参考[这里](http://wowubuntu.com/markdown/#p)
至于添加一个页面
{% codeblock lang:objc %}
rake new_page[page]
{% endcodeblock %}

5.下面就是把东西都搞到github上把,[创建自己的github pages repo](http://octopress.org/docs/deploying/github/),如果你的github用户名是username,那个就创建一个名称为"username.github.com"的repo,那么这个repo就是你的github pages repo,配置好后用username.github.com就可以访问啦
{% codeblock lang:objc %}
rake setup_github_pages
{% endcodeblock %}
需要输入的URL是这个样子: 
{% codeblock lang:objc %}
git@github.com:username/username.github.com.git
{% endcodeblock %}
接下来在本地预览下生成的网页样子 127.0.0.1:4000
{% codeblock lang:objc %}
rake generate
rake preview
{% endcodeblock %}
如果感觉不错的话就发布把
{% codeblock lang:objc %}
rake deploy
{% endcodeblock %}
最后把source里的东西push到github上把
{% codeblock lang:objc %}
cd octopress/
git add .
git commit -m '说点啥把'
git push origin source
{% endcodeblock %}
以后把写好的文章放到github上用这个一条语句就行啦
{% codeblock lang:objc %}
rake deploy
{% endcodeblock %}




