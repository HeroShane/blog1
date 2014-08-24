---
layout: post
title: mongodb和rails结合使用
categories:
    - ror
tags:
    - rails
    - mongodb
excerpt: 书写规范示例    
---

## 使用Mongodb创建Rails应用
{% highlight ruby %}
rails todo
{% endhighlight %}

我们将使用MongodbMapper来驱动MongoDB到rials。我们在/config/enviroment.rb配置文件中添加如下内容：
{% highlight ruby %}
config.gem "mongo_mapper"
{% endhighlight %}

在Rails的initializer文件中的MongoDB需要配置一些额外的配置。在/config/initializers文件目录下创建mongodb_config.rb文件，并在该文件中添加如下语句，用来配置MongodbMapper将使用的数据库名字。
/config/initializers/mongo_config.rb
{% highlight ruby %}
MongoMapper.datebase = "todo=#{Rails.env}"
{% endhighlight %}

由上可知，通过指定Rails运行环境参数，我们可以在不同的运行环境下创建互不干扰的数据库。还有运行如下语句，保证RailsMapper的gem已经安装：
{% highlight ruby %}
sudo rake gems:install
{% endhighlight %}

## 项目背景
项目中有一个Project的model和一个Tasks的model。他们有has_many关系。

* 首先，我们需要通过如下语句创建项目的layout：
{% highlight ruby %}
script/generate nifty_layout
{% endhighlight %}

* 然后，通过generate和nifty的scaffold创建project的model，这个表只有一个字段叫做name。而且，我们需要这个加上参数--skip-migration来创建：
{% highlight ruby %}
script/generate nifty_scaffold project name:string --skip-imagration
{% endhighlight %}

* 上面的脚手架会创建model、controller和view。然而，默认创建的是ActiveRecord是基于schema的model：
/app/models/project.rb
{% highlight ruby %}
class Project < ActiveRecord::Base
	attr_accessible :name
end
{% endhighlight %}

* 我们需要把ActiveRecord的model，改成MongoDB的类型，也就是把继承关系从1ActiveRecord::Base换成MongoMapper::Document。我们使用key这个方法标明该MongoMapper的字段属性。我们的属性是name，字段类型为string：
/app/models/project.rb
{% highlight ruby %}
class Project
	include MongoMapper::Document
	key :name,String
end
{% endhighlight %}

* MongoMapper从Rails开发语句来看MongoMapper和ActiveRecord是完全相同的。甚至，MongoMapper还是支持ActiveRecord的验证方式：
/app/models/project.rb
{% highlight ruby %}
validates_presence_of :name
{% endhighlight %}

可以基于下面的语法表述：
{% highlight ruby %}
class Project
	include MongoMapper::Document
	key :name.string, :required => true
end
{% endhighlight %}

* 添加更多的属性，如下我们需要添加一个priority的属性。
/app/models/project.rb
{% highlight ruby %}
class Project
	include MongoMapper::Document
	
	key :name,String :required => true
	key :priority ,Integer
end
{% endhighlight %}

* 如同ActiveRecord支持的一样，model属性可以直接和form元素关联。
/app/views/projects/_form.html.erb
{% highlight ruby %}
<% form_for @project do ||f %>
	<%= f.error_messages %>
	<p>
		<%= f.lable :name %>	
		<%= f.text_field :name %>
	</p>
	<p>
		<%= f.lable :priority %>	
		<%= f.select :priority , [1,2,3,4,5] %>
	</p>
	<p><%= f.submit "Submit" %></p>
<% end %>
{% endhighlight %}

在显示页面我们可以做以下修改：
{% highlight ruby %}
<% title "Project" %>    
<p>    
  <strong>Name:</strong>    
  <%=h @project.name %>    
</p>    
<p>    
  <strong>Priority:</strong>    
  <%=h @project.priority %>    
</p>    
<p>    
  <%= link_to "Edit", edit_project_path(@project) %> |    
  <%= link_to "Destroy", @project, :confirm => 'Are you sure?', :method => :delete %> |    
  <%= link_to "View All", projects_path %>    
</p>
{% endhighlight %}

* 处理表间关系
一个Project对应多个Task。值得注意的是，prohect_id之前在ActiveRecord都是integer类型，这里我们使用字符串类型：
{% highlight ruby %}
script/generate nifty_scaffold task project_id:string name:string completed:boolean --skip-migration
{% endhighlight %}

修改Task model指定继承MongoMapper如下：
/app/models/Task.rb
{% highlight ruby %}
class Task
	include MongoMapper::Document
	
	key :project_id, ObjectId
	key :name, String
	key :completed, Boolean

	belongs_to :project
end
{% endhighlight %}

处理不同表之间的关联，我们可以像ActiveRecord一样定义belongs_to，在MondoMapper需要用many来代替：
/app/models/project.rb
{% highlight ruby %}
class Task
	include MongoMapper::Document
	
	key :name,string  , :required => true
	key :priority,Integer
	many :tasks
end
{% endhighlight %}

**/app/views/tasks/_form.html.erb**
{% highlight ruby %}
<% form_for @task do |f| %>
	<%= f.error_messages %>
	<p>
		<%= f.lable :project_id %>
		<%= f.collection_select :project_id, Project.all, :id , :name %>
	</p>

{% endhighlight %}

**/app/views/tasks/show.html.erb**
{% highlight ruby %}
<% title "Task" %>
<p>
	<strong>Project:</strong>
	<%=h @task.project.name %>
</p>
{% endhighlight %}

## MongoDB查询

{% highlight ruby %}
Project.all

Project.find("")

Project.all(:priority => 3)

Project.all(:priority.gte => 3)

Project.all(:priority.in => [2,3])

{% endhighlight %}

