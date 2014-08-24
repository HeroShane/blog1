---
layout: post
title: Paperclip
categories:
    - ror
tags:
    - rails
excerpt: 这篇文章中展示如何使用一个`Paperclip`插件完成上传图片的任务   
---

## 插件安装
可以通过github下载安装
```sh
script/plugin install git://github.com/thoughtbot/paperclip.git
```

## 修改模型
```sh
script/generate paperclip product photo
```
这个生成器有两个参数。第一个是模型的名字，第二个是新添加的附件字段的名字。这个生成器执行后会生成一个迁移任务，给模型添加4个新字段。
{% highlight ruby %}
add_column :products, :photo_file_name, :string
add_column :products, :photo_content_type, :string
add_column :products, :photo_file_size, :integer
add_column :products, :photo_updated_at, :datetime
{% endhighlight %}

我们运行命令：*rake db:migrate*来更新数据库中的products。

下一步修改model代码。我们需要用*has_attribute_file*来告诉模型我们用迁移任务创建的附件字段(attribute field)的名字。
{% highlight ruby %}
class Product < ActiveRecord::Base
	belongs_to :category
	has_attached_file :photo
end
{% endhighlight %}

## 修改视图
{% highlight ruby %}>
<% form_for @product, :html => {:multipart => true} do |form| %>
<ol class="formList">    
    <!-- Other fields go here... -->    
    <li>    
      <%= form.label :photo, "Photo" %>    
      <%= form.file_field :photo %>    
    <li>    
      <%= form.submit "Submit" %>    
    </li>    
  </ol>    
<% end %>
{% endhighlight %}
上面代码等于给form标签添加了，*multipart/form-data*属性。

我们还需要给show页面添加一个*image_tag*标签，指向正确图片路径url。
{% highlight ruby %}>
<%= image_tag @product.photo.url %>
{% endhighlight %}

## 设置图片尺寸
我们添加到产品模型的*has_attached_file*有很多参数。其中一个是允许我们给图片定义不同的尺寸styles参数。我们只需要定义style参数并制定尺寸就可以为每张图片创建一个缩略图。
{% highlight ruby %}>
has_attached_file :photo, :styles => {:small => "150*150>"}
{% endhighlight %}

添加了新的style之后paperclip将会给每张图片生成一张适应150*150像素尺寸的缩略图。尺寸参数结尾的大于号告诉paperclip要保持图片的纵横比，避免图片拉伸变形。但需要服务器上安装了**ImageMagick**来保证生成缩略图功能起作用。

为了让合适的尺寸图片能够在产品视图显示，我们需要修改*image_tag*是图片标签url指向小版图片。
{% highlight ruby %}>
<%= image_tag #product.photo.url(:small) %>
{% endhighlight %}

## 验证附件
{% highlight ruby %}>
validates_attachment_presence :photo    
validates_attachment_size :photo, :less_than => 5.megabytes    
validates_attachment_content_type :photo, :content_type => ['image/jpeg', 'image/png'] 
{% endhighlight %}
通过上面的这些校验方法检查了：附件是否上传、文件大小小于5m、是否为JPEG或PNG格式。用这种办法验证附件可以和验证其他字段一样。有一点要注意的是：检查的文件类型的时候 Internet Explorer 可能与其他浏览器报告不同的MIME类型：IE会认为JPEG文件是image/pjpeg而不是image/jpeg文件。
