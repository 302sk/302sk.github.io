I:---
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

```python
def hello():
    print("hello")
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


电器 | 价格
------|------
洗衣机| 2233

