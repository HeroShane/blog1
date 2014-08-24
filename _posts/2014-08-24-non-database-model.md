---
layout: post
title: 非数据库数据模型
categories:
    - ror
tags:
    - rails
excerpt: 如何在Rails程序中创建一个不依赖后端数据库的表单。    
---

>**转载信息：**
>> http://cn.asciicasts.com/episodes/193-tableless-model

## 背景说明
我们要在每一篇文章上加上一个"分享这篇文章"的链接。这个链接会打开一个表单，让用户填入以下信息，然后通过电子邮件来分享一篇文章。我们只想用这些输入信息来发送一封邮件，并不打算保留这些信息。那么，如何在没有相应的数据库表情况下来创建一个表单和数据模型呢？

实现方法是，我们先来创建一个有数据库表的数据模型，然后再修改程序把数据库表去掉。那么我们用[nifty scaffold](https://github.com/ryanb/nifty-generators) generator这个工具来生成一个基本结构。

我们需要提交一个表单、并创建一个资源，我们需要创建一个数据模型。我们是要把一篇文章的细节通过电子邮件推荐给其他人，所以我们新的数据库模型名字就叫做`Recommendation`。

`Recommendation`数据模型中包含的字段有：电子邮件发送者、电子邮件的接收者、要推荐文章的id、以及发送的消息内容。相应的控制器中需要new和create这两个动作。我们可以通过下面的命令来创建这个基本结构：
{% highlight ruby %}
script/generate nifty_scaffold recommendation from_email:string to_email:string article_id:integer message:text new create
{% endhighlight %}

虽然我们实际上不需要数据表，但接下来我们还是需要执行数据迁移任务来创建数据库（之后我们会回滚这个数据迁移任务）
{% highlight ruby %}
rake db:migrate
{% endhighlight %}

有了数据模型和控制器，我们来加一个链接，使其调用RecommendationController控制器中的new动作，传入参数是我们要推荐文章的id。
在/app/views/articles/show.html.erb中加入推荐链接：
{% highlight ruby %}
<p>
	<%= link_to "Share this article" , new_recommendation_path(:articlr_id => @article.id) %>
	<%= link_to "Back to Articles" , articles_path %>
</p>
{% endhighlight %}

接下来，我们用一个隐藏字段来保存article_id。
修改:/app/views/recommendations/new.html.erb
{% highlight ruby %}
<% title "New Recommendation" %>
<% form_for @recommendation do |f| %>
	<%= f.error_messages %>
	<%= f.hidden_field :article_id %>
	<p>
		<%= f.lable :form_email %><br/>
		<%= f.text_field :form_email %>
	</p>
	<p>
		<%= f.lable :to_email %><br/>
		<%= f.text_field :to_email %>
	</p>
	<p>
		<%= f.lable :message %><br/>
		<% f.text_area :message %>
	</p>
	<p><%= f.submit "Submit" %></p>
<%end%>
<p><%= link_to "Back to Lists" , recommendations_path %></p>
{% endhighlight %}

如果我们填写这个表单并提交，我们就会在数据库中建出一个新的Recommendation数据，但是现在的情况是，我们只像发送一份电子邮件，不需要吧电子邮件存入数据库。在Rails程序中，create动作通常是用来把一个新的数据模型保存到数据库中。但是也不是绝对的，在这里我们只想检查一下新的Recommen数据模型是否合法。
{% highlight ruby %}
def create
	@recommendation = Recommendation.new(params[:recommendation])
	if @recommendation.valid?
		flash[:notice] = "Successfully created recommendation."
		redirect_to @recommendation
	else
		render :action => "new"
	end
end
{% endhighlight %}

现在，我们回滚到最后的那个数据迁移任务，把Recommendation数据表删除，然后看我们的表单能否正常工作。我们也需要删除数据迁移文件。
{% highlight ruby %}
rm db/migrate/*_recommendations.rb
{% endhighlight %}

删除了数据表，我们刷新表单页面会看到错误信息。程序找不到Recommendation数据表，因为ActiveRecord依赖每个数据模型关联的数据表。

如何创建一个不依赖数据表的数据模型？重载ActiveRecord数据模型中的一些方法，然后手工定义数据模型的字段，而不用后台的数据库。在我们的Recommendation数据模型中，我们加入两个重载的方法，然后用column类方法来像数据迁移文件中那样定义数据字段。
在/app/models/recommendation.rb定义：
{% highlight ruby %}
class Recommendation < ActiveRecord::Base
	def self.columns() @columns || =[]; end

	def self.columns(name, sql_type =nil, default=nil, null=true)
		columns << ActiveRecord::ConnectionAdapters::Column.new(name.to_s, default, sql_type.to_s, null)
	end
	
column :from_email, :string
column :to_email, :string
column :article_id, string
column :message, :text
end
{% endhighlight %}

当我们再刷新推荐文章时，我们可以看到正确的表单了。不过，数据字段现在是定义在数据模型中了，而不是从数据库中取出来了。

但是，既然我们已经不使用数据库，为什么还要Recommendation类继承自ActiveRecord::Base。Rails对于ActiveRecord耦合度很低。我们可以很容易的创建一个不基于ActiveRecord数据模型。但让我们的数据模型继承自ActiveRecord能给我们带来很多好处。我们能用它来完成许多其他功能。诸如：数据检查机制。我们可以在我们的数据模型中用ActiveRecord的数据检查机制来检查电子邮箱地址的格式以及消息的长度是否合适。
在/app/models/recommendation.rb加入数据检查机制:
{% highlight ruby %}
validates_formate_of :form_email, :to_email, :width => /^[-a-z0-9_+\.]+\@([-a-z0-9]+\.)+[a-z0-9]{2,4}$/i
validates_length_of :message, :maximum => 500
{% endhighlight %}

另外一个，我们的数据模型继承自ActiveRecord原因是，我们依然可以使用数据关联关系。在Recommendation中，既然article_id是一个数据项，那么我们依旧可以在数据模型中定义下面的关联，我们就可以随时获取到关联的Article对象了。
{% highlight ruby %}
belongs_to :article
{% endhighlight %}
