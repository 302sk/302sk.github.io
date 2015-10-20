---
layout: post
title: 学习可被识别的Markdown格式
categories:
- Writing
tags:
- git
- markdown
---

## markdown需要使用何种格式，才能符合jelly模板
`代码块` 

```c++
printf("hello world\n");
````

{% highlight c %}
int main(int argc, char* argv[])
{
    printf("Hello Markdown\n");
}
{% endhighlight %}

{% highlight javascript %}
function(a,b){
    var c = a + b;
    return c;
}

{% endhighlight %}

---
Item: Computer
Value: 2233
---

