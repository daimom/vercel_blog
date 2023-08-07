---
{"dg-publish":true,"permalink":"/Code/blog-22. telegram api使用/","title":"telegram api使用方法","tags":["💻"],"created":"","updated":""}
---


# 前言
  上一篇寫到用flagger，建立webhook發送通知。
  公司有在用的就skype跟 telegram，所以就....開始吧
  
# 正文

1. 首先你要有telegram帳號 XDDD
2. 加入 @BotFather ，輸入指令 /newBot，開始命名，注意機器人名稱可以不用bot結尾，但@帳號最後一定是Bot結尾
![blog-22.fig-1.jpg](/img/user/Code/blog-22.fig-1.jpg)

3. 建立好了後，會有一組token，請不要隨意給人，因為只要有這組就能發送訊息出去了。

![blog-22.fig-2.jpg](/img/user/Code/blog-22.fig-2.jpg)

4. 
   到此已經完成一半了，再來是使用取得channel的id，先將channel的頻道設公開，並把機器人加入到channel裡面。
   這邊需要記得你的chatid，不能跟其他人的重複，所以需要自己試試。
   
![blog-22.fig-3.jpg](/img/user/Code/blog-22.fig-3.jpg)
ezioflaggernotfiy就是我的chatid，
然後組合一下api，送出去就能取得channel的id，請先將機器人加入到channel裡面。
```
https://api.telegram.org/bot{token}/sendMessage?chat_id={chatid}&text=Hello,world
```
{token} 在 step.3，前面記得加bot
{chatid} 在step.4 ，記得前面要加 `@` 

送出去後，回傳的資料上面會顯示 chat.id，此時就能把channel 設成 private了。

![blog-22.fig-4.jpg](/img/user/Code/blog-22.fig-4.jpg)

5. 如果是公開的channel，就到第四步就結束了。
  如果是私人的話，將chatid改成 ，上面step.4拿到的 chat.id ，即可。
  不用再加@ 在chat_id前面了。此時所用的已是唯一的channel sn。

```
https://api.telegram.org/bot1234:JMwL6qw/sendMessage\?chat_id\=-12345\&text\=hello,telegram
```


6. 如果訊息太長，想要有明顯一點的訊息，可加上parse_mode=html
並在字的前後加上<code>abc</code>，在電腦上看到的字會明顯許多。
   
![blog-22.fig-5.jpg](/img/user/Code/blog-22.fig-5.jpg)
 (fig.5)
 但在手機上的telegram，看不到此特效。


ref.
 - [Telegram Bot機器人申請與Webhook指令全紀錄](http://slashview.com/archive2020/20200319.html)
- [如何獲得正確的telegram channel id?？](https://cloud.tencent.com/developer/ask/146200)
- [ An introduction for developers](https://core.telegram.org/bots#botfather)
- [telegram-sendMessage](https://core.telegram.org/bots/api#sendmessage)
- [sendMessage: Send text messages](https://rdrr.io/cran/telegram.bot/man/sendMessage.html)
- [關於 Telegram 上的解析模式（Markdown、HTML）、文字格式](https://tgtw.cc/post-about-parse-mode-of-telegram)
