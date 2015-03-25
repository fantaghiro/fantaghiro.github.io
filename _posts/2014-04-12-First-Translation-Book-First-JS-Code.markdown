---
layout: post
title: 值得纪念的第一稿
category: writeups
description: 最近，做成了两件小事，记录一下。
tags:
- 随笔
- 纪念
---

今天是个小小的值得纪念的日子。中午M君与我一同喝了小半杯啤酒，以示庆祝。雪花纯生的啤酒沫依然趣味十足，但是味道真的没有上次喝得那个外国品牌好。那次每口有回甘，这次则是苦味。不过这次要纪念的是开始而不是结束，所以心中记挂着些开头的苦涩，没什么不好。:p 

值得纪念的事情可能莫名其妙，第一桩是我硬着头皮完成了将要译的那本书的SFD——shitty first draft；第二桩是我完成了第一段小JS脚本的编写，也是SFD。不过没关系，自己看起来也羞愧不堪、拿不出手的初稿，会经过慢慢迭代积累，变得越来越好。万事开头难，有SFD诞生是好征兆。以前很想什么事情一开始就做得尽善尽美，这种心情虽然美好，但是直接导致许多事情根本没有去做。心中的宏伟巨著也没有草纸上的两三行字靠谱。这世上从不缺想法，也从不缺有想法的人。但最终是执行和实践赋予了这些想法意义。最近译的这本书，讲到了几个非常有意思的概念，其中一个就是无论如何，尽快把SFD做出来。把每件事情看成一个进化过程，有了SFD可以慢慢迭代、优化。初次所做的事情，效果总易不遂人愿。但是这是正常现象。意识到第一稿通常是“狗屎般”的（excuse me），对我来说卸下了很大的一个心理负担。我不会再拷问自己，我怎么这么差劲、这么笨、这么孤陋。而是会告诉自己，SFD嘛，无可避免，继续做、继续吸取教训、继续迭代，未来一定会越来越好。

下面是我翻译的书中一小节：

>目及之处，都是参加西南偏南艺术节的人群。这个为期两周、展示音乐、电影和交互媒体的盛会吸引着一群年轻人。参会者大多四十未满，他们从世界各地汇聚至此，只为品尝一下令他们心旌荡漾的灵丹妙药：改变。

>改变在以前可没这么流行。在商业领域，改变曾经只是一种结局，是人们为了达成新目标或解决重大问题而左右思量、慎重行事的结果。鉴于改变总是伴随着风险，人们总是小剂量地使用这副药方。一个新鲜的商标或名字就广受欢迎；一点细微的变化就被冠以“新颖和优化”而在广告上宣传，但大的变革却明显受到了压制。大变化往往意味着哪里出了问题或有人犯了错误。然而时至今日，尽管在某些场合还是作为一副药方出现，但对大多数企业以及60,000付费参与西南偏南艺术节的人们来说，改变已经融入了他们的血液。

>现在没有哪个组织是一成不变的了。即使那些最为古板守旧的公司也发生着变化，这并不是因为他们自己变了，而仅仅是因为周遭事物都在进化发展。传统公司可以不费半分力气，就变成过气的公司。它们就像是20世纪50年代的郊区农场，四周围绕着的都是时髦的新建筑——它们原本安全、传统的生存方式无疑正在慢慢拉低自身的价值。

>仅在美国，每年就有超过六百万家创业公司成立。Google、Comecast、Amazon、Cisco和Oracle已经在财富100强的公司席位中稳稳地站住了脚跟，但在十年前的排名中根本找不到它们的身影。Twitter、Facebook、Youtube和Pinterest将全球数十亿人连接起来，它们的成立也不过是上个十年的事情。

>这种公司的起起伏伏自然对就业和职业发展产生巨大影响。成功的传统路线——取得文凭、底层做起、积极积累人脉、遵守游戏规则、慢慢爬到高层、舒服退休养老——现在几乎在人间绝迹。



下面是第一段小JS脚本，很粗糙（#￣▽￣#）。会好的！

{% highlight html linenos %}

<!Doctype html>
<html>
    <head>
        <meta charset="utf-8">
        <style>
            #container{
              height: 820px;
              width: 820px;
              position: relative;
              overflow: hidden;
            }
            #flashcards {
              height: 800px;
              width: 800000px;
              margin-left: 0px;
            }
            .card {
                width: 800px;
                height: 800px;
                border: 1px solid blue;
                border-radius: 20px;
                font-size: 2em;
                transition: all 2s;
                
                display: inline-block;
            }
            .word {
              text-align: center;
              font-size: 200%;
              margin-top: 15%;
              margin-bottom: 5%;
            }
            dd {
              float: left;
              line-height: 1.2em;
            }
            .pos {
              width: 1%;
              font-style: italic;
            }
            .def {
              width: 80%;
            }
            .cnDef {
              margin-left: 1em;
            }
            .sen {
              margin-top: 2em;
              width: 81%;
            }
            .cnSen, .enSen {
              display: block;
              margin-bottom: 0.5em;
            }
            a {
              text-decoration: none;
              border: 1px solid blue;
              width: 4.5em;
              text-align: center;
              border-radius: 2px;
            }
            .nav {
                position: absolute;
                width: 200px;
                bottom: 20px;
                font-size: 30px;
                padding: 5px;
                left: 300px;
            }
        </style>
    </head>
    <body>
      <div id="container">
        <dl id="flashcards" style="margin-left: 0px;">
          <div class="card show">
              <dt class="word">dictionary1</dt>
              <dd class="pos">n.</dd>
              <dd class="def"><span class="enDef">a book in which the words and phrases of a language are listed alphabetically, together with their meanings or their translations in another language</span><span class="cnDef">字典；词典</span></dd>
              <dd class="sen"><span class="enSen">I borrowed a dictionary from Ann.</span><span class="cnSen">我从安那里借了一本词典</span></dd>

          </div>
          <div class="card">
              <dt class="word">dictionary2</dt>
              <dd class="pos">n.</dd>
              <dd class="def"><span class="enDef">a book in which the words and phrases of a language are listed alphabetically, together with their meanings or their translations in another language</span><span class="cnDef">字典；词典</span></dd>
              <dd class="sen"><span class="enSen">I borrowed a dictionary from Ann.</span><span class="cnSen">我从安那里借了一本词典</span></dd>

          </div> 
          <div class="card">
              <dt class="word">dictionary3</dt>
              <dd class="pos">n.</dd>
              <dd class="def"><span class="enDef">a book in which the words and phrases of a language are listed alphabetically, together with their meanings or their translations in another language</span><span class="cnDef">字典；词典</span></dd>
              <dd class="sen"><span class="enSen">I borrowed a dictionary from Ann.</span><span class="cnSen">我从安那里借了一本词典</span></dd>

          </div>
          <div class="card">
              <dt class="word">dictionary4</dt>
              <dd class="pos">n.</dd>
              <dd class="def"><span class="enDef">a book in which the words and phrases of a language are listed alphabetically, together with their meanings or their translations in another language</span><span class="cnDef">字典；词典</span></dd>
              <dd class="sen"><span class="enSen">I borrowed a dictionary from Ann.</span><span class="cnSen">我从安那里借了一本词典</span></dd>

          </div>
          <div class="card">
              <dt class="word">dictionary5</dt>
              <dd class="pos">n.</dd>
              <dd class="def"><span class="enDef">a book in which the words and phrases of a language are listed alphabetically, together with their meanings or their translations in another language</span><span class="cnDef">字典；词典</span></dd>
              <dd class="sen"><span class="enSen">I borrowed a dictionary from Ann.</span><span class="cnSen">我从安那里借了一本词典</span></dd>

          </div>        
                                                 
        </dl>
        <div class="nav">
            <a href="#" class="previous">Previous</a>
            <a href="#" class="next">Next</a>
        </div>
      </div>
        <script>
             window.onload = function(){

                var flashcard = document.getElementById("flashcards");
                var btn = document.getElementsByTagName("a");
                for(i=0;i<btn.length;i++){
                  if(btn[i].className == "previous"){
                    var prev = btn[i];
                  } else if(btn[i].className == "next"){
                    var next = btn[i];
                  }
                }
                var containter = document.getElementById("container");

                function slide(elem, offset, step, interval, num){
                  var newLeft = parseInt(elem.style.marginLeft) + offset; 
                  var maxLeft = Math.abs(offset)*(num-1);

                  function everyStep(){
                    if(offset < 0 && parseInt(elem.style.marginLeft) > newLeft){
                      if(newLeft < -maxLeft){
                        newLeft = 0;
                      }
                      elem.style.marginLeft = parseInt(elem.style.marginLeft) - step + 'px';
                      setTimeout(everyStep, interval);
                    } else if(offset > 0 && parseInt(elem.style.marginLeft) < newLeft){
                      if(newLeft > 0) {
                        newLeft = 0;
                      }
                      elem.style.marginLeft = parseInt(elem.style.marginLeft) + step + 'px';
                      setTimeout(everyStep, interval);
                    } else {
                      elem.style.marginLeft = newLeft + 'px';
                    }
                  }
                  everyStep();
                }

                next.onclick = function(){
                  slide(flashcard, -802, 100, 10, 5);
                }
                prev.onclick = function(){
                  slide(flashcard, 802, 100, 10);
                }
                
             }
        </script> 
    </body>
</html>

{% endhighlight %}
