---
title: 寻找下一个数
date: 2021-4-12 23:03:38
categories: 
- 算法
tags:
---
早上开车等红绿灯时想到几个月前写的一个算法，应该可以更简单，今天重新写了一遍

- 寻找下一个数字，例如输入345，输出354
>思路：从最右边位和上一位对比，如果大，就往前移，移动完，尾数排序，从小到大，保证次大

- 代码

```objective-c
//字符串分成数组
NSMutableArray *convertStringToArray(NSString *str){
    NSMutableArray *marr = [NSMutableArray array];
    for (NSInteger i = 0; i < str.length; i++) {
        [marr addObject:[str substringWithRange:NSMakeRange(i, 1)]];
    }
    return marr;
}

//数组拼成字符串
NSString *convertArrayToString(NSArray *arr){
    NSMutableString *mstr = [NSMutableString string];
    for (NSString *str in arr) {
        [mstr appendString:str];
    }
    return mstr;
}

//冒泡排序 从小到大
NSString *bubbleSort(NSString *str){
    NSArray *sortedArray = convertStringToArray(str);
    NSMutableArray *marr = [NSMutableArray arrayWithArray:sortedArray];
    //最后一位的索引
    unsigned long j = marr.count-1;
    for (;j>0;j--) {
      
        BOOL didSort = NO;
        //第一轮结束
        for (int i=0; i<j; i++) {
            NSString *pre = marr[i];
            NSString *next = marr[i+1];
            if (pre.integerValue > next.integerValue) {
                [marr exchangeObjectAtIndex:i+1 withObjectAtIndex:i];
                didSort = YES;
            }
        }
        
        if (!didSort) {
            break;
        }
    }
    
    NSMutableString *mstr = [NSMutableString string];
    for (NSString *str in marr) {
        [mstr appendString:str];
    }
    return  mstr;
    
}


NSString *findNextLargerNum(NSString *oriNum){
    NSString *resultStr = oriNum;
    NSMutableArray *oriNumMArr =[NSMutableArray arrayWithArray:convertStringToArray(oriNum)];
    
    for (int j = oriNumMArr.count-1; j>0; j--) {
        
        BOOL getResult = NO;
        NSString *last = oriNumMArr[j];
        for (int i = j-1; i>=0; i--) {
            NSString *pre = oriNumMArr[i];
            if (last.integerValue > pre.integerValue) {
                 [oriNumMArr exchangeObjectAtIndex:i withObjectAtIndex:j];
                NSRange range = NSMakeRange(i+1, oriNumMArr.count - 1 - i);
                NSString *surfixStr = convertArrayToString([oriNumMArr subarrayWithRange:range]);
                NSString *surResultStr = bubbleSort(surfixStr);
                NSString *preStr = convertArrayToString([oriNumMArr subarrayWithRange:NSMakeRange(0,i+1)]);
                resultStr = [NSString stringWithFormat:@"%@%@",preStr,surResultStr];
                getResult = YES;
                break;
            }
        }
        
        
        if (getResult) {
            break;
        }
        
    }
    return resultStr;
}
```
##### 使用：

```
NSString *str = findNextLargerNum(@"8976");
NSLog(@"======%@",str);
//打印结果
======9678
```
