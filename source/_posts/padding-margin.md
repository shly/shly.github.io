---
title: padding and margin学习笔记
date: 2016-09-28 21:46:01
tags: 
  - padding
  - margin
categories:
  - 学习笔记
  - 前端学习
---
# padding学习笔记

1. 对于block水平元素：
  1.1 padding暴走则一定会影响尺寸
  1.2 width非auto，padding影响尺寸
  1.3 width为auto或box-sizing为border-box，同事padding值没有暴走，不影响尺寸
<!-- more -->
 当padding-left+padding-right>width时，容器的宽度变为padding-left+padding-right，
容器中的内容按最小尺寸显示(比如是汉字则每行只显示一个字)（width为200px的盒子，padding为200px时，盒子的宽度变为400px）

2. 对于inline水平元素（width和height不能设置）

水平padding影响尺寸，垂直padding不影响尺寸,但是会影响背景色（占据空间），上下文字位置不变化，但是加背景色之后设置垂直padding，背景色的区域会向上下延伸。

## padding应用
1. 高度可控的分割线
1.1 直接使用字符(高度不可控)
1.2 inline-block控制
1.3 使用inline padding

    	注册<span></span>登录

    	span{
      	padding：16px 6px 1px;
      	margin-left:12px;
      	border-left:2px solid;
      	font-size:0;
    	}

## padding负值和百分比值
1. padding负值  padding不支持任何类型的负值
2. padding百分比均是相对于宽度计算的(可用实现正方形)
3. inline水平元素的padding值
  3.1 同样相对于宽度计算
  3.2 默认的高度宽度细节有差异
  3.3 padding会断行
  空inline元素+padding高度也不等，因为inline元素的垂直padding会让“幽灵空白节点”显现，也就是规范中的“strut”出现。可font-size为0解决。

## 标签元素的内置padding
1. ol/ul li元素内置padding-left,单位是px不是em，padding-left22-25比较合适，网页开发文字大小12或14
2. 表单元素内置的padding值。
  2.1 所有浏览器input/textarea有内置padding
  2.2 所有浏览器button按钮内置padding
  2.3 部分浏览器select下拉内置padding
  2.4 所有浏览器radio、CheckBox单复选框无内置padding，设了也没用
  2.5 button按钮元素padding最难控制

    2.5.1 chrome浏览器正常
    2.5.2 fireFox浏览器设置padding：0 左右仍有padding，解决方式

         button::-moz-focus-inner{padding:0px}

    2.5.3 3 ie
      ie7文字越多，左右padding逐渐变大，解决方式

          button{overflow:visible;}

    2.5.4 padding与高度计算的不兼容

         <button id='btn'></button>
         <label for='btn'>按钮</label>
         label{
           display: inline-block;
           line-height:20px;
           padding:10px;
         }

## padding与图形绘制
  1. 三道杠
          <div class='line-tri'></div>
          .line-tri{
            width:150px;height:30px;
            border-top:30px solid;
            border-bottom:30px solid;
            background-color:currentcolor;
            background-clip:content-box;
          }
  2. 白眼效果

         <div class='eye'></div>
         .eye{
          width:150px;
          height:150px;
          padding:10px;
          border:10px solid;
          border-radius:50%;
          background-color:currentcolor;
          background-clip:content-box;
         }
## padding布局应用
1. 使用百分比单位构建固定比例布局结构
2. 配合margin实现等高布局

      .child-orange,.child-green{
        margin-bottom: -600px;
        padding-bottom: 600px;
      }

3. 两栏自适应布局，原理：浮动具有破坏性

        <div class="box">
          <img src="1.jpg">
          <div class="content">
          很多内容。。。。
          </div>
        </div>
        img{
         float:left;
        }
        .content{
         padding-left:120px;
        }
        或
        <div class="box">
          <img src="1.jpg">
          很多内容。。。。
        </div>
        img{
        float:left;
         margin-left:120px;
        }
        .box{
         padding-left:120px;
        }

# margin学习笔记

## margin与百分比单位

1. 水平方向百分比/垂直方向百分比
2. 普通元素百分比/绝对定位元素百分比
  2.1 普通元素百分比计算规则：margin百分比都是相对于容器宽度计算的
  2.2 绝对定位：相对于第一个定位祖先元素的宽度计算的

## margin重叠
1. margin重叠通常特性
  1.1 block水平元素上发生（不包括float和absolute元素）
  1.2 不考虑writing-mode，只发生在垂直方向（margin-top和margin-bottom）
2. margin重叠3中情景
  2.1 相邻的兄弟元素
  2.2 父元素和第一个或最后一个子元素
  2.3 空的block元素margin:1em 0;占据高度为1em
3. margin-top重叠
  3.1 父元素非块状格式化上下文
  3.2 父元素没有border-top设置
  3.3 父元素没有padding-top设置
  3.4 父元素和第一个子元素之间没有inline元素分隔
4. margin-bottom重叠
  4.1 父元素非块状格式化上下文
  4.2 父元素没有border-bottom设置
  4.3 父元素没有padding-bottom设置
  4.4 父元素和第一个子元素之间没有inline元素分隔
  4.5 父元素没有height，min-height,max-height限制
5. 空block重叠
  5.1 元素没有border设置
  5.2 元素没有padding设置
  5.3 里面没有inline元素
  5.4 没有height，或者min-height
6. 重叠的计算规则
  6.1 正正取大
  6.2 正负值相加
  6.3 负负最负值（自身高度永远为0）
7. 善于margin重叠

       .list{
        margin-top:15px;
        margin-bottom:15px;
       }//上下margin都使用增强健壮性

## margin:auto

auto为剩余空间（比如当不设置宽度时，一个div如果自动填充全部空间，则给它设置了宽度后，剩下的空间则为剩余空间）

## margin负值定位

1. margin负值下的两端对齐（margin改变元素尺寸）

      .box{
          width: 1200px;
          margin:auto;
          background: orange;
      }
      .ul{
          overflow: hidden;
          margin-right: -20px;
      }
      .li{
          width: 386.66px;
          height: 300px;
          margin-right: 20px;
          background: green;
          float: left;
      }
2. margin负值下的等高布局（margin改变元素占据空间）

3. margin负值下的两栏自适应布局

## margin无效情况解析

1. inline元素垂直margin无效
2. margin重叠
3. display:table-cell/display:table-row等声明的margin无效（margin应用于display为table相关类型之外的所有。）
4. position:absolute与margin。绝对定位元素非定位方向的margin是“无效的”（有效，对定位没有影响，但是影响占据的空间，肉眼看上去没有影响）
5. 鞭长莫及导致的无效
6. 内联特性导致的margin无效（受制于内联元素的对齐方式）

## 了解margin-start/margin-end等
正常流:margin-start=margin-left

