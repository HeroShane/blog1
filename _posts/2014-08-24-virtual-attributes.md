---
layout: post
title: rails虚拟属性
categories:
    - ror
tags:
    - rails
excerpt: 虚拟属性   
---
**数据库文件定义**
{% highlight objc %}
create_table "users" , force => true do |t|
	t.string "first_name"
	t.string "last_name"
	t.string "password"
end
{% endhighlight %}

我们想在用户界面，只显示全名full_name字段，而不是first_name和last_name。我们可以使用虚拟属性来进行实现。我们首先要修改视图代码。把名和姓字段进行合并。
**/app/views/users/new.html.erb**
{% highlight objc %}
<h1>Register</h1>      
<% form_for @user do |form| %>      
<ol class="formList">      
  <li>      
    <%= form.label :full_name, 'Full Name' %>      
    <%= form.text_field :full_name %>      
  </li>      
  <li>      
    <%= form.label :password, 'Password' %>      
    <%= form.password_field :password %>      
  </li>      
</ol>      
<% end %> 
{% endhighlight %}

现在，如果我们提交表单就会查找User模型中现在还不存在的full_name字段。我们可以创建full_name的虚拟属性来创建这个字段。
{% highlight objc %}
class User < ActiveRecord::Base
	#Getter
	def full_name
		[first_name , last_name].join(' ')
	end

	#Setter
	def full_name(name)
		split = name.split(' ' 2)
		self.first_name = split.first
		self.last_name = split.last
	end
end 
{% endhighlight %}

