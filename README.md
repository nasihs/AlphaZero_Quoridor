# AlphaZero_Quoridor
An AlphaZero implementation of game Quoridor

# 项目介绍

Chinese only now.

暂时只用中文介绍，本项目主要实现AlphaZero算法的Quoridor游戏。

## Quoridor

Quoridor中文称作步步为营，是国外非常流行的桌游，大致界面如下所示（图片来自百度图片）：

![](https://github.com/cryer/AlphaZero_Quoridor/raw/master/images/1.jpg)

游戏规则(百度百科)：

* 你可以看到本路径棋横10条、竖8条凹下的路径，20个挡板，四人不同颜色的木人。
* 游戏开始前，所有玩家（2-4）每人一个小木人，平分所有挡板。
* 游戏开始，木人放在边路，开始向对岸行驶，谁最先到达对岸者为胜利者。如果玩家为3人或4人，一人胜利之后，其他玩家还可以继续争夺第二名、第三名。你可以在棋盘的任何方向行走，每次只能一步或者放挡板。放挡板的目的是阻挡对方到达对岸，如果选择放挡板的话，木人就不能走路，如果木人走一步，就不能放挡板。

* 当两子相邻的时候可以跳过对面棋子，在对面棋子的另外三个方向上都可以移动，也就是相当于走了两步

虽然该游戏可以四人玩，但是由于博弈树和AlphaZero一般处理两人博弈游戏，所以我们只考虑两人游戏的情况，两人处于对岸。每人十个挡板，挡板不可以复用，用完
就没有了，棋子先到达对岸获胜。

## 简要分析

我们知道围棋的动作空间为361，中国象棋为2068，步步为营的动作空间则为140，其中128个挡板的动作空间，64个横向和64个竖向，加上4个平时的上下左右棋子移动
和8个特殊情况的棋子移动，也就是两子相邻的情况。棋盘棋子的移动范围是9\*9。

## 棋盘状态的表示

AlphaGo Zero围棋的棋盘状态表示为48\*19\*19,其中19\*19是棋盘的大小，48是围棋的规则，这些是手工制定的，包含气等信息。而AlphaZero的围棋
棋盘状态用17\*19\*19,17是历史的落子信息，也就是说舍弃了人类的制定规则。

步步为营的棋面状态可以自行设计，只要合理就行，本个项目采用26\*9\*9,9\*9是棋面的大小，26包含竖直挡板的信息，横挡板的信息，玩家棋子位置信息，
剩余挡板数量信息和先后手信息等等，详细参考代码。

## 策略价值网络

Zero版本相比Go的版本一大改进，就是合并了策略网络和价值网络，并且用残差网络代替的普通的卷积结构，我本次也采用了残差网络，
用了5个残差块，每个残差块由2部分卷积结构组成，网络相对还是蛮深的，也只是一个初步的网络结构，后续有很大可能改进。

## 关于代码

本项目是一个长期的项目，目前还处于起步阶段，代码也是刚刚初步完成，只处于能跑通的阶段，很多地方还不完善，代码结构也没有优化，算法本身的很多参数也
调整，可以Star关注我长期的更新。

* 另外，代码很多部分我都给出了详细的中文注释，我相信可以让你更快的了解代码，让你轻松的看代码。


# MIT License

```

Copyright (c) 2018 kurumi

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

```
