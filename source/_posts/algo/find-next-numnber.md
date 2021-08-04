---
title: 寻找下一个数
date: 2020-11-15 23:03:38
categories: 
- 算法
tags:
---
- 寻找下一个数字，例如输入345，输出354
>思路：从最右边位和上一位对比，如果大，就往前移，移动完，尾数排序，从大到小，保证次大
-代码

```
//字符串逆序
NSString *reverseStr(NSString *str){
    NSMutableString *string=[[NSMutableString alloc] init];
    for(int i=0;i<str.length;i++){
        [string appendString:[str substringWithRange:NSMakeRange(str.length-1-i, 1)]];
    }
    return string;
}

//字符串分成数组
NSMutableArray *separateStringToArray(NSString *str){
    NSMutableArray *marr = [NSMutableArray array];
    for (NSInteger i = 0; i < str.length; i++) {
        [marr addObject:[str substringWithRange:NSMakeRange(i, 1)]];
    }
    return marr;
}


NSString *findNextLargerNum(NSString *oriNum){


    NSMutableString *finalStr = [NSMutableString string];


    NSMutableArray *marr = separateStringToArray(oriNum);
    for (NSInteger i = marr.count - 1; i > 0; i--) {
        NSNumber *lastNum = [marr objectAtIndex:i];
        NSNumber *preNum = [marr objectAtIndex:i-1];
        if (lastNum.integerValue > preNum.integerValue) {
            //截取字符串
            NSString *rightStr = reverseStr([oriNum substringWithRange:NSMakeRange(i, oriNum.length - i)]);
            NSString *leftStr = [oriNum substringWithRange:NSMakeRange(0,i)];
            //第i-1位截取出来
            NSString *leftCompareStr = [oriNum substringWithRange:NSMakeRange(i-1, 1)];
            //和右边逐个对比
            for (int j = 0; j < rightStr.length; j++) {
                NSString *rightCompareStr = [rightStr substringWithRange:NSMakeRange(j, 1)];
                if (leftCompareStr.integerValue < rightCompareStr.integerValue) {
                    NSMutableArray *finalArr = separateStringToArray([NSString stringWithFormat:@"%@%@",leftStr,rightStr]);
                    NSInteger leftIndex = [finalArr indexOfObject:leftCompareStr];
                    NSInteger rightIndex = [finalArr indexOfObject:rightCompareStr];
                    [finalArr exchangeObjectAtIndex:leftIndex withObjectAtIndex:rightIndex];
                    for (NSString *str in finalArr) {
                        [finalStr appendString:str];
                    }
                    break;
                }
            }
        }
    }

    return finalStr.length?finalStr:oriNum;
}
```
##### 使用：

```
NSString *str = findNextLargerNum(@"8976");
NSLog(@"======%@",str);
//打印结果
======9678
```
