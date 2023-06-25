---
# type: docs 
title: Excel 基本操作
linkTitle: Excel
date: 2022-12-06T10:18:27+08:00
featured: true
draft: false
comment: false
toc: true
reward: true
pinned: false
carousel: false
series:
categories: []
tags: []
images: []
---

Excel 操作内容及思路

<!--more-->

**## 1. 基础原则  ##**

设计原则 ：数据源，参数数，报表

相关操作在哪里设置就在哪里取消

二八原则：先去掌握那些最重要的20%的知识，再去根据自己的需要去扩展

想要学好：网易云课堂，腾讯课堂，学习完了需要讲给别人听或者形成写做

>高效整理技巧复制功能：选择性粘贴，可以粘贴列宽，公式等

>数据护航：工作表保护与打印，可以设置工作表的密码及打印配置

>批量制作：邮件合并,可以把Excel里面结合到Word中来打印



**## 2. 常用函数  ##**

>三种单元格引用

    一种是相对引用，适应于行列均不固定的情况；
    一种是绝对引用，适用行列均固定的情况；
    第三种是混合引用，列固定行不固定或者行固定列不固定。
    三种引用方式可以通过在固定的行列前加$符号或通过F4来切换

>逻辑函数

    IF/AND/OR

    IF:根据对指定条件的逻辑判断的真假结果，返回相对应的内容。
    使用格式：=IF(Logical,Value_if_true,Value_if_false)
    DEMO: =IF(A1+C1=E1,"正确","错误")

    AND需要多个条件同时成立时才成立

    OR多个条件中任意一个条件成立即成立

>文本函数

    LEFT/RIGHT/MID/LEN/LENB/TEXT

    MID:从文本字符串中指定的起始位置返回指定长度的字符。
    使用格式：=MID(Text,Start_num,Num_chars)
    DEMO: =MID(C2,17,1)

    LEFT:从一个文本字符串的第一个字符开始，截取指定数目的字符。
    使用格式：=LEFT(text,num_chars)
    DEMO: =LEFT(C2,2)

    LEN:统计文本字符串中字符数目。
    使用格式：=LEFT(text,num_chars)
    DEMO: =LEN(A2)

    TEXT:将数值转化为设置单元格格式中的数字——格式类型。
    使用格式：=TEXT(value,format_text)
    DEMO:=TEXT(MID(C2,7,8),"0000-00-00")



>日期类函数

    TODAY/NOW/DATE/EDATE/DATEDIF

    TODAY:给出指定数值的日期。
    使用格式：=DATE(year,month,day) 
    DEMO:=DATE(A2,B2+1,0)

    DATEDIF:计算返回两个日期参数的差值
    使用格式：=DATEDIF(date1,date2 ,”y”)
             =DATEDIF(date1,date2 ,”m”)
             =DATEDIF(date1,date2 ,”d”)
    DEMO: =DATEDIF([@入职日期],TODAY(),"D")

    EDATE:计算开始日期之前(或后)的X月份后的日期。
    使用格式：=EDATE(start_date,months)
    DEMO: =EDATE(A2,C2*12)



>查找引用类函数

    VLOOKUP/HLOOKUP/LOOKUP

    VLOOKUP:按列查找，最终返回该列所需查询列序所对应的值。
    使用格式：=VLOOKUP（Lookup_value,Table_array,Col_index_number,Range_lookup）
    DEMO: =VLOOKUP($G$1,表1,6,0)

    LOOKUP:在一组从小到大的数组中，返回被查找值所处区间对应的返回值。
    使用格式：=LOOKUP（Lookup_value, Lookup_vector, Result_vector ）
    DEMO: =LOOKUP([@绩效得分],$P$2:$P$6,$Q$2:$Q$6)


>条件计数求和函数

    SUMIF/SUMIFS/COUNTIF/COUNTIFS

    SUMIFS:对一组给定条件指定的单元格求和
    使用格式：=SUMIFS（求和区域,条件区域1,条件1）
    DEMO:=SUMIFS(表2[人数],表2[省份],J1)


**## 3. 数据汇总分析与呈现  ##**

> 数据分析：排序、筛选、分类汇总、合并计算

> 数据分析神器：数据透视

> 数据图表可视化看板

![图片示例](/images/chartpig.png)


