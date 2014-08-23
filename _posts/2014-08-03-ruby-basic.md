---
layout: post
title: Ruby基本语法
categories:
    - Ruby
tags:
    - ruby基础
excerpt: Ruby基本语法    
---

>原文链接：http://ihower.tw/rails3/ruby.html

## 字符串String

使用單引號或雙引號括起來的是字串String物件：

{% highlight ruby %}
puts 'Hello, world!'
puts ''
puts 'Good-bye.'
{% endhighlight %}

字串相加可以使用加號，要注意的是**字串不能直接跟數字相加**，會發生例外錯誤：

{% highlight ruby %}
puts 'I like ' + 'apple pie.'
puts 'You\'re smart!'

puts '12' + 12
#<TypeError: can't convert Fixnum into String>
{% endhighlight %}

更多字串方法示範：

{% highlight ruby %}
var1 = 'stop'
var2 = 'foobar'
var3 = "aAbBcC"

puts var1.reverse # 'pots'
puts var2.length # 6
puts var3.upcase
puts var3.downcase
{% endhighlight %}
----------------------------------

## Ruby完全为对象

{% highlight ruby %}
# 輸出 "UPPER"
puts "upper".upcase

# 輸出 -5 的絕對值
puts -5.abs

# 輸出 Fixnum 類別
puts 99.class

# 輸出 "Ruby Rocks!" 五次
5.times do
  puts "Ruby Rocks!"
end
{% endhighlight %}
----------------------------------

## 局部变量 Local Variable

區域變數使用小寫開頭，偏好單字之間以底線_來分隔。範例如下：

{% highlight ruby %}
composer = 'Mozart'
puts composer + ' was "da bomb", in his day.'

my_composer = 'Beethoven'
puts 'But I prefer ' + my_composer + ', personally.'
{% endhighlight %}
----------------------------------

## 类型转换 Conversions

{% highlight ruby %}
var1 = 2
var2 = '5'

puts var1.to_s + var2 # 25
puts var1 + var2.to_i # 7

puts 9.to_f / 2 # 4.5
{% endhighlight %}
----------------------------------

## 常量 Constant

大寫開頭的是為常數，範例如下：

{% highlight ruby %}
Foo = 1
Foo = 2 # (irb):3: warning: already initialized constant Foo

RUBY_PLATFORM # => "x86_64-darwin10.7.0"
ENV # => { "PATH" => "....", "LC_ALL" => "zh_TW.UTF-8" }
{% endhighlight %}
----------------------------------

## 空值 nil

表示未設定值、未定義的狀態：

{% highlight ruby %}
nil # nil
nil.class # NilClass

nil.nil? # true
42.nil? # false

nil == nil # true
false == nil # false
{% endhighlight %}
---------------------------------

## 注解

* 单行注解
{% highlight ruby %}
# this is a comment line
# this is a comment line
{% endhighlight %}

* 多行注解
{% highlight ruby %}
=begin
    This is a comment line
    This is a comment line
=end
{% endhighlight %}
---------------------------------

## 字串符號Symbols

>為什麼不就用字串呢？這是因為使用Symbol可以獲得執行上的效率，相同名稱的Symbol不會再重複建構物件，範例如下：

{% highlight ruby %}
puts "foobar".object_id      # 輸出 2151854740
puts "foobar".object_id      # 輸出 2151830100
puts :foobar.object_id       # 輸出 577768
puts :foobar.object_id       # 輸出 577768
{% endhighlight %}

object_id方法會回傳Ruby內部的記憶體配置編號，你會發現相同內容的字串，也會是不同的新物件，但是Symbol不會。這種特性讓Symbol的主要用途是當做雜湊Hash的鍵，一會就會介紹到。
---------------------------------

## 数组 Array

使用中括號，索引從0開始。注意到陣列中的元素是不限同一類別，想放什麼都可以：

{% highlight ruby %}
a = [ 1, "cat", 3.14 ]

puts a[0] # 輸出 1
puts a.size # 輸出 3

a[2] = nil
puts a.inspect # 輸出 [1, "cat", nil]
a[99] # nil
{% endhighlight %}

>inspect方法會將物件轉成適合給人看的字串

如果讀取一個沒有設定的陣列元素，預設值是nil。更多陣列方法範例：

{% highlight ruby %}
colors = ["red", "blue"]

colors.push("black")
colors << "white"
puts colors.join(", ") # red, blue, black, white

colors.pop
puts colors.last #black
{% endhighlight %}
---------------------------------

## 集合 hash

Hash是一種鍵值對(Key-Value)的資料結構，雖然你可以使用任何物件當作Key，但是通常我們使用Symbol當作Key。例如：

{% highlight ruby %}
config = { :foo => 123, :bar => 456 }
puts config["foo"] # 輸出 123
config["nothing"] # 是 nil
{% endhighlight %}

在Ruby 1.9支援新的語法，比較簡約：

{% highlight ruby %}
config = { foo: 123, bar: 456 } # 等同於 { :foo => 123, :bar => 456 }
{% endhighlight %}

如果讀取一個不存在的值，例如上述範例的nothing，預設值是nil。

>注意到Ruby 1.8的Hash不像Array，你無法預測裡面的鍵值順序。例如輸入{ :a => 1, :b=> 2, :c => 3 }.merge( :d => 4 )會輸出成{:a=>1, :d=>4, :b=>2, :c=>3}。這個問題在Ruby 1.9獲得修正，會依照你給的順序輸出成{:a=>1, :b=>2, :c=>3, :d=>4}。如果你想確保無論Ruby 1.8或1.9都要用有順序的Hash，在Rails環境中可以用**`ActiveSupport::OrderedHash`**。
---------------------------------

## 流程控制

else if寫成elsif：

{% highlight ruby %}
total = 26000

if total > 100000
  puts "large account"
elsif total > 25000
  puts "medium account"
else
  puts "small account"
end
{% endhighlight %}

另外如果要執行的if程式只有一行，可以將if放到行末即可：

{% highlight ruby %}
puts "greater than ten" if total > 10
{% endhighlight %}

三元運算子expression ? true_expresion : false_expression可以讓我們處理簡易的if else條件，例如以下的程式：

{% highlight ruby %}
x = 3
if x > 3
  y = "foo"
else
  y = "bar"
end
{% endhighlight %}

改用三元運算子之後，可以縮減程式行數：

{% highlight ruby %}
x = 3
y = ( x > 3 )? "foo" : "bar"
{% endhighlight %}

控制結構Case

{% highlight ruby %}
case name
    when "John"
      puts "Howdy John!"
    when "Ryan"
      puts "Whatz up Ryan!"
    else
      puts "Hi #{name}!"
end
{% endhighlight %}

迴圈 while, loop, until, next and break

* while用法範例：

{% highlight ruby %}
i=0
while ( i < 10 )
  i += 1
  next if i % 2 == 0 #跳過雙數
end
{% endhighlight %}

* until用法範例：

{% highlight ruby %}
i = 0
i += 1 until i > 10
puts i
# 輸出 11
{% endhighlight %}

* loop用法範例：

{% highlight ruby %}
i = 0
loop do
  i += 1
  break if i > 10 # 中斷迴圈
end
{% endhighlight %}

>不過你很快就會發現寫Ruby很少用到while、until、loop，我們會使用迭代器。
---------------------------------

## 真或假

記住，**只有false和nil是假，其他都為真**。

{% highlight ruby %}
puts "not execute" if nil
puts "not execute" if false

puts "execute" if true # 輸出 execute
puts "execute" if “” # 輸出 execute (和JavaScript不同)
puts "execute" if 0 # 輸出 execute (和C不同)
puts "execute" if 1 # 輸出 execute
puts "execute" if "foo" # 輸出 execute
puts "execute" if Array.new # 輸出 execute
{% endhighlight %}
---------------------------------

## 正規表示法Regular Expressions

與Perl類似的語法，使用=~：
{% highlight ruby %}
# 抓出手機號碼
phone = "123-456-7890"
if phone =~ /(\d{3})-(\d{3})-(\d{4})/
  ext  = $1
  city = $2
  num  = $3
end
{% endhighlight %}

---------------------------------

## 方法定义 Method

使用def開頭end結尾來定義一個方法：

{% highlight ruby %}
def say_hello(name)
  result = "Hi, " + name
  return result
end

puts say_hello('ihower')
# 輸出 Hi, ihower
{% endhighlight %}

**方法中的return是可以省略的**，Ruby就會回傳最後一行運算的值。上述方法可以改寫成：

{% highlight ruby %}
def say_hello(name)
  "Hi, " + name
end
{% endhighlight %}

**呼叫方法時，括號也是可以省略的**，例如：

{% highlight ruby %}
say_hello 'ihower'
{% endhighlight %}

不過，除了一些方法慣例不加之外(例如puts和Rails中的`redirect_to`、`render`方法)，絕大部分的情況加上括號比較無疑義。
---------------------------------

## ?與!的慣例

方法名稱可以用?或!結尾，前者表示會回傳Boolean值，後者暗示會有某種副作用(side-effect)。範例如下：

{% highlight ruby %}
array=[2,1,3]

array.empty? # false
array.sort # [1,2,3]

array.inspect # [2,1,3]

array.sort! # [1,2,3]
array.inspect # [1,2,3]
{% endhighlight %}
---------------------------------

## 类 Class

Ruby的類別其實也是一種常數，所以也是大寫開頭，使用new方法可以建立出物件，例如之前所學的字串、陣列和雜湊，也可以用以下方式建立：

{% highlight ruby %}
color_string = String.new
color_string = "" # 等同

color_array = Array.new
color_array = [] # 等同

color_hash = Hash.new
color_hash = {} # 等同

time  = Time.new # 內建的時間類別
puts time
{% endhighlight %}

來看看如何自定類別：

{% highlight ruby %}
class Person # 大寫開頭的常數

    def initialize(name) # 建構式
        @name = name # 物件變數
    end

    def say(word)
        puts "#{word}, #{@name}" # 字串相加
    end

end

p1 = Person.new("ihower")
p2 = Person.new("ihover")

p1.say("Hello") # 輸出 Hello, ihower
p2.say("Hello") # 輸出 Hello, ihover
{% endhighlight %}

>注意到雙引號裡的字串可以使用#{var}來做字串嵌入，相較起用加號+相加字串可以更有效率。

除了物件方法與物件變數，Ruby也有屬於類別的方法和變數：

{% highlight ruby %}
class Person

    @@name = “ihower” # 類別變數

    def self.say # 類別方法
        puts @@name
    end
end

Person.say # 輸出 ihower
{% endhighlight %}

所有的物件變數(@開頭)、類別變數(@@開頭)，都是封裝在類別內部的，類別外無法存取：

{% highlight ruby %}
class Person
    def initialize(name)
        @name = name
    end
end

p = Person.new('ihower')
p.name 						# 出現 NoMethodError 錯誤
p.name = 'peny'  		    # 出現 NoMethodError 錯誤
{% endhighlight %}

為了可以存取到@name，我們必須定義方法：

{% highlight ruby %}
class Person

   def initialize(name)
    @name = name
   end

   def name
     @name
   end

   def name=(name)
     @name = name
   end
end

p = Person.new('ihower')
p.name
=> "ihower"
p.name="peny"
=> "peny"		    # 出現 NoMethodError 錯誤
{% endhighlight %}
---------------------------------

## 類別Class定義範圍內也可以執行程式

跟其他程式語言不太一樣，Ruby的類別層級內也可以執行程式，例如以下：

{% highlight ruby %}
class Demo
    puts "foobar"
end 		    # 出現 NoMethodError 錯誤
{% endhighlight %}

當你載入這個類別的時候，就會執行puts "foobar"輸出foobar。會放在這裡的程式，主要的用途是來做`Meta-programming`。例如，上述定義物件變數的存取方法實在太常見了，因此Ruby提供了attr_accessor、attr_writer、attr_reader類別方法可以直接定義這些方法。上述的程式可以改寫成：

{% highlight ruby %}
class Person
  attr_accessor :name
end

p = Person.new('ihower')
p.name
=> "ihower"
p.name="peny"
=> "peny"
{% endhighlight %}

這裡的attr_accessor其實就是一個類別方法。
---------------------------------

## 方法封装

類別中的方法預設是public的，宣告private或protected的話，該行以下的方法就會套用：

{% highlight ruby %}
class MyClass

    def public_method
    end

    private

    def private_method_1
    end

    def private_method_2
    end

    protected

    def protected_method
    end
end
{% endhighlight %}

Ruby的private和protected定義和其他程式語言不同，都是可以在整個繼承體系內呼叫。兩著差別在於private只有不指定接受者(receiver)時才可以呼叫，你甚至不能打self.private_method_1，預設一定就是self當成private方法的接受者。而protected方法除了可以被一個類別或子類別的物件呼叫，也可以讓另一個相同類別的物件來當做接受者。

>在物件導向的術語中，object.call_method的意思是object收到執行call_method的指令，也就是object是call_method方法的接受者(receiver)。因此，你甚至可以改寫成object.__send__(:call_method)
---------------------------------

## Class 继承

Ruby使用小於`<`符號代表類別繼承：

{% highlight ruby %}
class Pet
    attr_accessor :name, :age

    def say(word)
        puts "Say: #{word}"
    end
end

class Cat < Pet
    def say(word)
        puts "Meow~"
        super
    end
end

class Dog < Pet
    def say(word, person)
        puts "Bark at #{person}!"
        super(word)
    end
end

Cat.new.say("Hi")
Dog.new.say("Hi", "ihower")
{% endhighlight %}

输出：

{% highlight ruby %}
Meow~
Say: Hi
Bark at ihower!
Say: Hi
{% endhighlight %}

這個範例中，Cat和Dog子類別覆寫了Pet say方法，其中的super是用來呼叫被覆寫掉的Pet say方法。另外，沒有括號的super和有括號的super()是有差異的，前者Ruby會自動將所有參數都代進去來呼叫父類別的方法，後者則是自己指定參數。此例中如果Dog say裡只寫super，則會發生wrong number of arguments的錯誤，這是因為Ruby會傳say("Hi", "ihower")給Pet say而發生錯誤。
---------------------------------

## 迭代 Iterator

不同於while迴圈用法，Ruby習慣使用迭代器(Iterator)來走訪迴圈，例如each是一個陣列的方法，它會走訪其中的元素，其中的do .... end是each方法的參數，稱作匿名方法(code block)。範例程式如下：

{% highlight ruby %}
languages = ['Ruby', 'Javascript', 'Perl']
languages.each do |lang|
    puts "I love #{lang}!"
end
# I Love Ruby!
# I Love Javascript!
# I Love Perl!
{% endhighlight %}

其中兩個直線|中間的lang被稱作Block variable區塊變數，每次迭代都會被設定成不同元素。其他迭代器範例如：

{% highlight ruby %}
# 反覆三次
3.times do
    puts 'Good Job!'
end
# Good Job!
# Good Job!
# Good Job!

# 從一數到九
1.upto(9) { |x| puts x }

# 多一個索引區塊變數
languages = ['Ruby', 'Javascript', 'Perl']
languages.each_with_index do |lang, i|
    puts "#{i}, I love #{lang}!"
end
# 0, I Love Ruby!
# 1, I Love Javascript!
# 2, I Love Perl!
{% endhighlight %}

(Code block)的形式除了do ... end，也可以改用大括號。通常單行會會用大括號，多行會用do ... end的形式。

{% highlight ruby %}
3.times { puts "Hello" }
{% endhighlight %}

* 其他迭代方式範例

{% highlight ruby %}
# 迭代並造出另一個陣列
a = [ "a", "b", "c", "d" ]
b = a.map {|x| x + "!" }
puts b.inspect

# 結果是 ["a!", "b!", "c!", "d!"]

# 找出符合條件的值
b = [1,2,3].find_all{ |x| x % 2 == 0 }
b.inspect
# 結果是 [2]

# 迭代並根據條件刪除
a = [51, 101, 256]
a.delete_if {|x| x >= 100 }
# 結果是 [51]

# 客製化排序
[2,1,3].sort! { |a, b| b <=> a }
# 結果是 [3, 2, 1]

# 計算總和
(5..10).inject {|sum, n| sum + n }

# 找出最長字串find the longest word
longest = ["cat", "sheep", "bear"].inject do |memo,word|
    ( memo.length > word.length )? memo : word
end
{% endhighlight %}

> <=>是比較運算子，當兩個數字相等於回傳0，第一個數字較大時回傳1，反之回傳-1

* 僅執行一次呼叫

除了迭代，也有Code block只會執行一次，例如用來開檔。往常我們在檔案處理完畢之後，會使用close方法：

{% highlight ruby %}
file = File.new("testfile", "r")
# ...處理檔案
file.close
{% endhighlight %}

改用Code block語法之後，Ruby可以在Code block結束後自動關檔：

{% highlight ruby %}
File.open("testfile", "r") do |file|
    # ...處理檔案
end
# 檔案自動關閉
{% endhighlight %}

Code block的這個特性不只讓你少打close方法，更可以避免你忘記(不然就語法錯誤了)，也有視覺上縮排的好處。

* Yield

在方法中使用yield可以執行Code block參數：

{% highlight ruby %}
# 定義方法
def call_block
    puts "Start"
    yield
    yield
    puts "End"
end

call_block { puts "Blocks are cool!" }
# 輸出
# "Start"
# "Blocks are cool!"
# "Blocks are cool!"
# "End"
{% endhighlight %}

* 帶有參數的Code block

{% highlight ruby %}
def call_block
    yield(1)
    yield(2)
    yield(3)
end

call_block { |i|
    puts "#{i}: Blocks are cool!"
}
# 輸出
# "1: Blocks are cool!"
# "2: Blocks are cool!"
# "3: Blocks are cool!"
{% endhighlight %}

* Proc object

可以將Code block明確轉成一個變數：

{% highlight ruby %}
def call_block(&block)
    block.call(1)
    block.call(2)
    block.call(3)
end

call_block { |i| puts "#{i}: Blocks are cool!" }

# 或是先宣告出 proc object
proc_1 = Proc.new { |i| puts "#{i}: Blocks are cool!" }
proc_2 = lambda { |i| puts "#{i}: Blocks are cool!" }

call_block(&proc_1)
call_block(&proc_2)

# 輸出
# "1: Blocks are cool!"
# "2: Blocks are cool!"
# "3: Blocks are cool!"
{% endhighlight %}

* 傳遞不定參數

{% highlight ruby %}
def my_sum(*val)
    val.inject { |sum, v| sum + v }
end

puts my_sum(1,2,3,4) # val 變數就是 [1,2,3,4]
# 輸出 10

def my_print(a, b, options)
    puts a
    puts b
    puts options[:x]
    puts options[:y]
    puts options[:z]
end

my_print("A", "B", { :x => 123, :z => 456 } )
my_print("A", "B", :x => 123, :z => 456) # 結果相同
# 輸出 A
# 輸出 B
# 輸出 123
# 輸出 nil
# 輸出 456
{% endhighlight %}
---------------------------------

## 错误处理

使用rescue可以將例外救回來：

{% highlight ruby %}
begin
    puts 10 / 0 # 這會丟出 ZeroDivisionError 的例外錯誤
rescue => e
    puts e.class # 如果發生例外會執行 rescue 這一段
ensure
    # 無論有沒有發生例外，ensure 這一段都一定會執行
end
# 輸出 ZeroDivisionError
{% endhighlight %}

使用raise可以手動觸發例外錯誤：

{% highlight ruby %}
raise "Not works!!"
# 丟出一個 RuntimeError

# 自行自定例外物件
class MyException < RuntimeError
end

raise MyException
{% endhighlight %}
---------------------------------

## Module

Module是Ruby一個非常好用的功能，它跟Class類別非常相似，你會在裡面定義方法。只是你不能用new來建立它。它的第一個用途是可以當做Namespace來放一些工具方法：

{% highlight ruby %}
module MyUtil

    def self.foobar
        puts "foobar"
    end
end

MyUtil.foobar
# 輸出 foobar
{% endhighlight %}

另一個更重要的功能是Mixins，可以將一個Module混入類別之中，這樣這個類別就會擁有此Module的方法。這回讓我們拆成兩個檔案，debug.rb和foobar.rb，然後在foobar.rb中用require來引用debug.rb：

首先是debug.rb

{% highlight ruby %}
module Debug
    def who_am_i?
        puts "#{self.class.name}: #{self.inspect}"
    end
end
{% endhighlight %}

然後是foobar.rb

{% highlight ruby %}
require "./debug"
class Foo
    include Debug # 這個動作叫做 Mixin
end

class Bar
    include Debug
end

f = Foo.new
b = Bar.new
f.who_am_i? # 輸出 Foo: #<Foo:0x00000102829170>
b.who_am_i? # 輸出 Bar: #<Bar:0x00000102825b88>
{% endhighlight %}

Ruby使用Module來解決多重繼承的問題，不同類別之間但是擁有相同的方法，就可以改放在Module裡面，然後include它即可。
---------------------------------

## Metaprogramming用程式寫程式

Metaprogramming是很進階的技巧，這裡示範define_method方法可以動態定義方法：

{% highlight ruby %}
class Dragon
    define_method(:foo) { puts "bar" }

    ['a','b','c','d','e','f'].each do |x|
        define_method(x) { puts x }
    end
end

dragon = Dragon.new
dragon.foo # 輸出 "bar"
dragon.a # 輸出 "a"
dragon.f # 輸出 "f"
{% endhighlight %}
---------------------------------

## Introspection反射機制

Ruby擁有許多反射方法，可以動態知道物件的資訊：

{% highlight ruby %}
# 這個物件有什麼方法
Object.methods
=> ["send", "name", "class_eval", "object_id", "new", "singleton_methods", ...]

# 這個物件有這個方法嗎？
Object.respond_to? :name
=> true
{% endhighlight %}

