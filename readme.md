# UranusPy



终于... 我们发布了Uranus 的Python SDK。目的是让大家可以在简单的几行代码之下构建自己的聊天机器人、私人助手、消息传送机器人… 甚至是可以集成到你的代码当中捕捉exception传到你的setu上....

只有你想不到没有做不到，首先关于Uranus是什么东西，以及Setu(对标Telegram的社交软件)是什么东西，参考我们的知乎专栏的文章：[传送门](https://zhuanlan.zhihu.com/p/53717894).



## Install

安装uranuspy直接从pip安装：

```
sudo pip3 install uranuspy
```



## 构建第一个聊天机器人

接下来我将演示如何在10行代码以内构建自己的聊天机器人，首先我们需要的终极效果是这样的：



![](https://s1.ax1x.com/2018/12/31/F4JsbV.jpg)



什么？如何通过python代码实现它？十分简单啦，首先从 http://loliloli.pro 下载西兔软件(目前只有安卓端)， 注册一个机器人账号，你可以给机器人修改一个酷炫的头像，然后记得将性别修改为机器人，这样可以被系统找到，从而给其他人提供服务。



好了，接下来的得写代码了，可以说用uranuspy非常简洁了：



```python
from uranuspy.core import UranusCore
from uranuspy.core import TEXT_MSG, IMG_MSG, VOICE_MSG

# run
agent = UranusCore('jarvis', 'xxxxxxx')
agent.run_forever()
global_op = agent.get_global_op()

def msg_callback(data):
    print('-- callback: \n', data)
    content = data['content']
    sender_name = data['sender_name']
    return 'I know this is msg: {}, from: {}'.format(content, sender_name)


agent.register_callback(msg_callback)
```



简单的说一下步骤：

1. 调用UranusCore，传入机器人账号和密码，就可以得到一个agent，接下来的所有操作都将由agent完成；
2. 做一个方法，有消息说到之后调用的方法；
3. 注册这个方法
4. 这一步optional，如果你需要一个实例去给别人发消息，那只需要调用`get_global_op()`即可



OK，以上几部，就可以构建一个自己的聊天机器人啦！最后跟大家说一下我们目前用这个sdk实现的功能：

- 接收代码的bug…… 代码除了bug，自动给我发消息；
- 给家里的监控添加人脸识别，当有人脸检测到的时候，自动把人脸图片发给我.... (这样我就可以知道到底是哪个偷开了我的家门，等等... 隔壁老王？？？)