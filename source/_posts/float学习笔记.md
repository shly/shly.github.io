---
title: float学习笔记
date: 2017-05-02 20:24:15
tags: 
  - css
  - float
categories:
  - 学习笔记
  - css学习
---
# 大Float

## float的历史

浮动设计的初衷是： “文字环绕效果”
<!-- more -->
## 包裹与破坏
1. 包裹（BFC）
  1. 收缩
  2. 坚挺
  3. 隔绝
2. 破坏（无宽度，无图片，无浮动）父元素塌陷（不是bug是标准）

## 清除浮动带来的影响
1. 在脚部插入clear:both;
  1. html block底部插入div
  2. css after伪元素
  
          .clearfix:after{
              content:'';
              display:block;
              height:0;
              width:0;
              overflow:hidden;
              clear:both;
          }
          .clearfix{
            *zoom:1;
          }
          或
          .clearfix:after{
              content:'';
              display:table;
              clear:both;
          }
          .clearfix{
            *zoom:1;
          }
      
2. 父元素BFC（IE8+）或haslayout（IE6/IE7）

## float的滥用
1. 浮动可以使元素block化
2. 去空格化

## float与流体布局
1. 单侧固定
2. 智能自适应尺寸
一侧float 另一侧display：table-cell(IE8+)display:inline-block(IE7)

## float 与兼容性
ie7
 1. 含clear的浮动元素包裹不正确的问题
 2. 浮动元素倒数第二个莫名垂直间距的问题
 3. 浮动元素最后一个字符重复的问题
 4. 浮动元素楼梯排列问题
 5. 浮动元素和文本不在同一行的问题
 
        div>左侧标题<span>右浮动</span></div>
        
    修改方式
    
        <div><span>左浮动</span><span>右浮动</span></div>

