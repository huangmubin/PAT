# 1001 A+B和C(15)


> 题目描述

给定区间[-2的31次方, 2的31次方]内的3个整数A、B和C，请判断A+B是否大于C。

> 输入描述

输入第1行给出正整数T(<=10)，是测试用例的个数。随后给出T组测试用例，每组占一行，顺序给出A、B和C。整数间以空格分隔。

> 输出描述

对每组测试用例，在一行中输出“Case #X: true”如果A+B>C，否则输出“Case #X: false”，其中X是测试用例的编号（从1开始）。

> 输入例子

4
1 2 3
2 3 4
2147483647 0 2147483646
0 -2147483648 -2147483647

> 输出例子

Case #1: false
Case #2: true
Case #3: true
Case #4: false

## C

```
#include <stdio.h>

int main(int argc, const char * argv[]) {
    long int lenght = 0;
    long int datas[10][3];
    scanf("%ld", &lenght);
    for (int i = 0; i < lenght; i++) {
        scanf("%ld %ld %ld", &datas[i][0], &datas[i][1], &datas[i][2]);
    }
    for (int i = 0; i < lenght; i++) {
        printf("Case #%d: ", i + 1);
        if (datas[i][0] + datas[i][1] > datas[i][2]) {
            printf("true\n");
        } else {
            printf("false\n");
        }
    }
    return 0;
}
```

# 1002 数字分类(20)

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB

> 题目描述

给定一系列正整数，请按要求对数字进行分类，并输出以下5个数字：
A1 = 能被5整除的数字中所有偶数的和；
A2 = 将被5除后余1的数字按给出顺序进行交错求和，即计算n1-n2+n3-n4...；
A3 = 被5除后余2的数字的个数；
A4 = 被5除后余3的数字的平均数，精确到小数点后1位；
A5 = 被5除后余4的数字中最大数字。

> 输入描述

每个输入包含1个测试用例。每个测试用例先给出一个不超过1000的正整数N，随后给出N个不超过1000的待分类的正整数。数字间以空格分隔。

> 输出描述

对给定的N个正整数，按题目要求计算A1~A5并在一行中顺序输出。数字间以空格分隔，但行末不得有多余空格。
若其中某一类数字不存在，则在相应位置输出“N”。

> 输入例子

13 1 2 3 4 5 6 7 8 9 10 20 16 18

> 输出例子

30 11 2 9.7 9

## C 

```
#include <stdio.h>
#include <stdlib.h>

int main(int argc, const char * argv[]) {
    int lenght = 0, value = 0, temp = 0, has = 0;
    int *datas;
    scanf("%d", &lenght);
    datas = (int *)malloc(sizeof(int) * lenght);
    for (int i = 0; i < lenght; i++) {
        scanf("%d", &datas[i]);
    }
    
    // A1
    value = 0;
    has = 0;
    for (int i = 0; i < lenght; i++) {
        if (datas[i] % 5 == 0 && datas[i] / 5 % 2 == 0) {
            value += datas[i];
            has++;
        }
    }
    if (has) {
        printf("%d ", value);
    } else {
        printf("N ");
    }
    
    // A2
    value = 0;
    temp = 0;
    has = 0;
    for (int i = 0; i < lenght; i++) {
        if (datas[i] % 5 == 1) {
            if (temp == 0) {
                value += datas[i];
                temp = 1;
            } else {
                value -= datas[i];
                temp = 0;
            }
            has++;
        }
    }
    if (has) {
        printf("%d ", value);
    } else {
        printf("N ");
    }
    
    // A3
    value = 0;
    temp = 0;
    for (int i = 0; i < lenght; i++) {
        if (datas[i] % 5 == 2) {
            value++;
        }
    }
    if (value) {
        printf("%d ", value);
    } else {
        printf("N ");
    }
    
    // A4
    value = 0;
    temp = 0;
    for (int i = 0; i < lenght; i++) {
        if (datas[i] % 5 == 3) {
            value += datas[i];
            temp++;
        }
    }
    if (temp) {
        printf("%.1f ", (double)value / (double)temp);
    } else {
        printf("N ");
    }
    
    // A5
    value = 0;
    temp = 0;
    for (int i = 0; i < lenght; i++) {
        if (datas[i] % 5 == 4) {
            value = value > datas[i] ? value : datas[i];
        }
    }
    if (value) {
        printf("%d", value);
    } else {
        printf("N");
    }
    
    return 0;
}
```

# 1003 数素数

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB

> 题目描述

令Pi表示第i个素数。现任给两个正整数M <= N <= 10000，请输出PM到PN的所有素数。

> 输入描述:

输入在一行中给出M和N，其间以空格分隔。

> 输出描述:

输出从PM到PN的所有素数，每10个数字占1行，其间以空格分隔，但行末不得有多余空格。

> 输入例子:

5 27

> 输出例子:

11 13 17 19 23 29 31 37 41 43
47 53 59 61 67 71 73 79 83 89
97 101 103

## C 

```
#include <stdio.h>

int is_prime(int v) {
    if (v >= 2) {
        int i = 2;
        while (i * i <= v) {
            if (v % i++ == 0) {
                return 0;
            }
        }
        return 1;
    }
    return 0;
}

int main(int argc, const char * argv[]) {
    int i = 1, idx = 0, p = 0;
    int m, n;
    scanf("%d %d", &m, &n);
    while (++i) {
        if (is_prime(i)) {
            idx++;
            if (idx >= m) {
                if (idx < n) {
                    printf("%d", i);
                    p++;
                    p %= 10;
                    if (p) {
                        printf(" ");
                    } else {
                        printf("\n");
                    }
                }
                if (idx == n) {
                    printf("%d", i);
                    p++;
                    p %= 10;
                    break;
                }
            }
        }
    }
    return 0;
}
```

# 1004 福尔摩斯的约会 (20)

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB

> 题目描述

大侦探福尔摩斯接到一张奇怪的字条：“我们约会吧！ 3485djDkxh4hhGE 2984akDfkkkkggEdsb s&hgsfdk d&Hyscvnm”。大侦探很快就明白了，字条上奇怪的乱码实际上就是约会的时间“星期四 14:04”，因为前面两字符串中第1对相同的大写英文字母（大小写有区分）是第4个字母'D'，代表星期四；第2对相同的字符是'E'，那是第5个英文字母，代表一天里的第14个钟头（于是一天的0点到23点由数字0到9、以及大写字母A到N表示）；后面两字符串第1对相同的英文字母's'出现在第4个位置（从0开始计数）上，代表第4分钟。现给定两对字符串，请帮助福尔摩斯解码得到约会的时间。

> 输入描述:

输入在4行中分别给出4个非空、不包含空格、且长度不超过60的字符串。

> 输出描述:

在一行中输出约会的时间，格式为“DAY HH:MM”，其中“DAY”是某星期的3字符缩写，即MON表示星期一，TUE表示星期二，WED表示星期三，THU表示星期四，FRI表示星期五，SAT表示星期六，SUN表示星期日。题目输入保证每个测试存在唯一解。

> 输入例子:

3485djDkxh4hhGE
2984akDfkkkkggEdsb
s&hgsfdk
d&Hyscvnm

> 输出例子:

THU 14:04

## C

```
#include <stdio.h>
#include <string.h>

union {
    char c;
    int i;
} value;

int print_day(int d) {
    int out = 1;
    switch (d) {
        case 65: printf("MON "); break;
        case 66: printf("TUE "); break;
        case 67: printf("WED "); break;
        case 68: printf("THU "); break;
        case 69: printf("FRI "); break;
        case 70: printf("SAT "); break;
        case 71: printf("SUN "); break;
        default: out = 0;
    }
    return out;
}

int print_minute(int min) {
    int out = 2;
    if (min > 47 && min <58) {
        printf("%02d:", min - 48);
    } else if (min > 64 & min < 79) {
        printf("%02d:", min - 55);
    } else {
        out = 1;
    }
    return out;
}

int main(int argc, const char * argv[]) {
    char secret[4][60];
    for (int i = 0; i < 4; i++) {
        scanf("%s", secret[i]);
    }
    
    int index = 0, out = 0;
    for (int p = 0; p < strlen(secret[0]); p++) {
        for (int q = index; q < strlen(secret[1]); q++) {
            if (secret[0][p] == secret[1][q]) {
                value.c = secret[0][p];
                switch (out) {
                    case 0:
                        out = print_day(value.i);
                        if (out == 1) { index = p + 1; }
                        break;
                    case 1:
                        out = print_minute(value.i);
                        break;
                    default:
                        break;
                }
            }
        }
        if (out == 2) { break; }
    }
    int i = 0;
    for (; i < strlen(secret[2]) && i < strlen(secret[3]); i++) {
        if (secret[2][i] == secret[3][i]) {
            value.c = secret[2][i];
            if ((value.i > 64 && value.i < 91) || (value.i > 96 && value.i < 123)) {
                printf("%02d", i);
                break;
            }
        }
    }
    if (i == 0) {
        printf("00");
    }
    return 0;
}
```

# 1005 德才论 (25)

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB

> 题目描述

宋代史学家司马光在《资治通鉴》中有一段著名的“德才论”：“是故才德全尽谓之圣人，才德兼亡谓之愚人，德胜才谓之君子，才胜德谓之小人。凡取人之术，苟不得圣人，君子而与之，与其得小人，不若得愚人。”现给出一批考生的德才分数，请根据司马光的理论给出录取排名。

> 输入描述:

输入第1行给出3个正整数，分别为：N（<=105），即考生总数；L（>=60），为录取最低分数线，即德分和才分均不低于L的考生才有资格被考虑录取；H（<100），为优先录取线——德分和才分均不低于此线的被定义为“才德全尽”，此类考生按德才总分从高到低排序；才分不到但德分到线的一类考生属于“德胜才”，也按总分排序，但排在第一类考生之后；德才分均低于H，但是德分不低于才分的考生属于“才德兼亡”但尚有“德胜才”者，按总分排序，但排在第二类考生之后；其他达到最低线L的考生也按总分排序，但排在第三类考生之后。
随后N行，每行给出一位考生的信息，包括：准考证号、德分、才分，其中准考证号为8位整数，德才分为区间[0, 100]内的整数。数字间以空格分隔。

> 输出描述:

输出第1行首先给出达到最低分数线的考生人数M，随后M行，每行按照输入格式输出一位考生的信息，考生按输入中说明的规则从高到低排序。当某类考生中有多人总分相同时，按其德分降序排列；若德分也并列，则按准考证号的升序输出。

> 输入例子:

14 60 80
10000001 64 90
10000002 90 60
10000011 85 80
10000003 85 80
10000004 80 85
10000005 82 77
10000006 83 76
10000007 90 78
10000008 75 79
10000009 59 90
10000010 88 45
10000012 80 100
10000013 90 99
10000014 66 60

> 输出例子:

12
10000013 90 99
10000012 80 100
10000003 85 80
10000011 85 80
10000004 80 85
10000007 90 78
10000006 83 76
10000005 82 77
10000002 90 60
10000014 66 60
10000008 75 79
10000001 64 90

## C++

```
#include <cstdio>
//#include <cstring>
#include <algorithm>
using namespace std;
//
//struct Student {
//    int n = 0, d = 0, c = 0, s = 0, l = 0;
//};

int n, l, h;

int level(int d, int c) {
    if (d < l || c < l) {
        return 4;
    } else if (d >= h && c >= h) {
        return 0;
    } else if (d >= h && c < h) {
        return 1;
    } else if (d >= c) {
        return 2;
    } else {
        return 3;
    }
}

int cmp(const void* a1, const void* b1) {
    int *a = (int *)a1;
    int *b = (int *)b1;
    if (a[3] != b[3]) {
        return b[3] - a[3];
    } else if (a[1] != b[1]) {
        return b[1] - a[1];
    } else {
        return a[0] - b[0];
    }
}

int main() {
    int tn, td, tc, tl;
    scanf("%d %d %d", &n, &l, &h);
    int rs[4] = {0,0,0,0};
    int stu[4][100010][4];
    for(int i = 0; i < n; i++) {
        scanf("%d %d %d", &tn, &td, &tc);
        tl = level(td, tc);
        if (tl < 4) {
            stu[tl][rs[tl]][0] = tn;
            stu[tl][rs[tl]][1] = td;
            stu[tl][rs[tl]][2] = tc;
            stu[tl][rs[tl]][3] = td + tc;
            rs[tl]++;
        }
    }
    printf("%d\n", rs[0] + rs[1] + rs[2] + rs[3]);
    for (tl = 0; tl < 4; tl++) {
        //sort(stu[tl], stu[tl] + rs[tl], cmp);
        qsort(stu[tl], rs[tl], 4 * sizeof(int), cmp);
        for (int i = 0; i < rs[tl]; i++) {
            printf("%d %d %d\n", stu[tl][i][0], stu[tl][i][1], stu[tl][i][2]);
        }
    }
    return 0;
}
```

# 1006 1016. 部分A+B (15)

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB

> 题目描述

正整数A的“DA（为1位整数）部分”定义为由A中所有DA组成的新整数PA。例如：给定A = 3862767，DA = 6，则A的“6部分”PA是66，因为A中有2个6。现给定A、DA、B、DB，请编写程序计算PA + PB。

> 输入描述:

输入在一行中依次给出A、DA、B、DB，中间以空格分隔，其中0 < A, B < 1010。

> 输出描述:

在一行中输出PA + PB的值。

> 输入例子:

3862767 6 13530293 3

> 输出例子:

399

## C++

```
#include <iostream>
 
int main() {
    int a[2][2];
    scanf("%d %d %d %d", &a[0][0], &a[0][1], &a[1][0], &a[1][1]);
    int r = 0, l;
    for (int i = 0; i < 2; i++) {
        l = 1;
        while (a[i][0] > 0) {
            if ((a[i][0] % 10) == a[i][1]) {
                r = r + a[i][1] * l;
                l *= 10;
            }
            a[i][0] /= 10;
        }
    }
    printf("%d", r);
    return 0;
}
```

# 1007 A除以B (20)

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB

> 题目描述

本题要求计算A/B，其中A是不超过1000位的正整数，B是1位正整数。你需要输出商数Q和余数R，使得A = B * Q + R成立。

> 输入描述:

输入在1行中依次给出A和B，中间以1空格分隔。

> 输出描述:

在1行中依次输出Q和R，中间以1空格分隔。

> 输入例子:

123456789050987654321 7

> 输出例子:

17636684150141093474 3

# C++

```
#include <iostream>
 
int main() {
    char bit[1001];
    char *a = bit;
    int b, t, r, q = 0;
    scanf("%s %d", a, &b);
    t = (q * 10) + (*a - 48);
    r = t / b;
    q = t % b;
    if (r > 0) {
        printf("%d", r);
    }
    a++;
    while (*a != '\0') {
        t = (q * 10) + (*a - 48);
        r = t / b;
        q = t % b;
        printf("%d", r);
        a++;
    }
    printf(" %d", q);
}
```

# 1008 锤子剪刀布 (20)

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB

> 题目描述

大家应该都会玩“锤子剪刀布”的游戏：
现给出两人的交锋记录，请统计双方的胜、平、负次数，并且给出双方分别出什么手势的胜算最大。

> 输入描述:

输入第1行给出正整数N（<=105），即双方交锋的次数。随后N行，每行给出一次交锋的信息，即甲、乙双方同时给出的的手势。C代表“锤子”、J代表“剪刀”、B代表“布”，第1个字母代表甲方，第2个代表乙方，中间有1个空格。

> 输出描述:

输出第1、2行分别给出甲、乙的胜、平、负次数，数字间以1个空格分隔。第3行给出两个字母，分别代表甲、乙获胜次数最多的手势，中间有1个空格。如果解不唯一，则输出按字母序最小的解。

> 输入例子:

10
C J
J B
C B
B B
B C
C C
C B
J B
B C
J J

> 输出例子:

5 3 2
2 3 5
B B

## C++

```
#include <iostream>
using namespace std;
 
struct Player {
    int type[3] = {0,0,0};
    int w, d, l; // win, dogfall, lose
    void win(int t) { type[t]++; w++; }
    void dogfall(int t) { d++; }
    void lose(int t) { l++; }
    char type_char() {
        if (type[0] >= type[1]) {
            if (type[0] > type[2]) {
                return 'C';
            } else {
                return 'B';
            }
        } else {
            if (type[1] > type[2]) {
                return 'J';
            } else {
                return 'B';
            }
        }
    }
} a, b;
 
int main() {
    int n = 0;
    char j, y;
     
    cin >> n;
    for (int i = 0; i < n; i++) {
        cin >> j >> y;
        switch (j) {
            case 'C':
                switch (y) {
                    case 'C': a.dogfall(0); b.dogfall(0); break;
                    case 'J': a.win(0); b.lose(1); break;
                    case 'B': a.lose(0); b.win(2); break;
                } break;
            case 'J':
                switch (y) {
                    case 'C': a.lose(1); b.win(0); break;
                    case 'J': a.dogfall(1); b.dogfall(1); break;
                    case 'B': a.win(1); b.lose(2); break;
                } break;
            case 'B':
                switch (y) {
                    case 'C': a.win(2); b.lose(0); break;
                    case 'J': a.lose(2); b.win(1); break;
                    case 'B': a.dogfall(2); b.dogfall(2); break;
                } break;
        }
    }
     
    printf("%d %d %d\n", a.w, a.d, a.l);
    printf("%d %d %d\n", b.w, b.d, b.l);
    printf("%c %c", a.type_char(), b.type_char());
}
```

# 1009 1019. 数字黑洞 (20)

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB

> 题目描述

给定任一个各位数字不完全相同的4位正整数，如果我们先把4个数字按非递增排序，再按非递减排序，然后用第1个数字减第2个数字，将得到一个新的数字。一直重复这样做，我们很快会停在有“数字黑洞”之称的6174，这个神奇的数字也叫Kaprekar常数。

例如，我们从6767开始，将得到
7766 - 6677 = 1089
9810 - 0189 = 9621
9621 - 1269 = 8352
8532 - 2358 = 6174
7641 - 1467 = 6174
... ...

现给定任意4位正整数，请编写程序演示到达黑洞的过程。

> 输入描述:

输入给出一个(0, 10000)区间内的正整数N。

> 输出描述:

如果N的4位数字全相等，则在一行内输出“N - N = 0000”；否则将计算的每一步在一行内输出，直到6174作为差出现，输出格式见样例,每行中间没有空行。注意每个数字按4位数格式输出。

> 输入例子:

6767

> 输出例子:

7766 - 6677 = 1089
9810 - 0189 = 9621
9621 - 1269 = 8352
8532 - 2358 = 6174

## C++

```
#include <iostream>
#include <cstring>
#include <algorithm>
using namespace std;
 
bool cmp1(char a, char b) {
    return a > b;
}
 
bool cmp2(char a, char b) {
    return a < b;
}
 
int main() {
    char input[5] = {'\0'};
    scanf("%s", input);
    for (int i = 0; i < 4; i++) {
        if (input[i] == '\0') {
            input[i] = '0';
        }
    }
     
    char a[5] = {'\0'}, b[5] = {'\0'}, r = 0;
    do {
        for (int i = 0; i < 4;  i++) {
            a[i] = b[i] = input[i];
        }
        if (a[0] == a[1] && a[0] == a[2] && a[0] == a[3]) {
            printf("%s - %s = 0000\n", a, a);
            break;
        }
        sort(a, a + 4, cmp1);
        sort(b, b + 4, cmp2);
        for (int i = 3; i >= 0; i--) {
            r = r + a[i] - b[i];
            if (r >= 0) {
                input[i] = r + 48;
                r = 0;
            } else {
                input[i] = r + 58;
                r = -1;
            }
        }
        printf("%s - %s = %s\n", a, b, input);
    } while (strcmp(input, "6174") != 0);
}
```

# 1010 月饼 (25)

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB

> 题目描述

月饼是中国人在中秋佳节时吃的一种传统食品，不同地区有许多不同风味的月饼。现给定所有种类月饼的库存量、总售价、以及市场的最大需求量，请你计算可以获得的最大收益是多少。
注意：销售时允许取出一部分库存。样例给出的情形是这样的：假如我们有3种月饼，其库存量分别为18、15、10万吨，总售价分别为75、72、45亿元。如果市场的最大需求量只有20万吨，那么我们最大收益策略应该是卖出全部15万吨第2种月饼、以及5万吨第3种月饼，获得 72 + 45/2 = 94.5（亿元）。

> 输入描述:

每个输入包含1个测试用例。每个测试用例先给出一个不超过1000的正整数N表示月饼的种类数、以及不超过500（以万吨为单位）的正整数D表示市场最大需求量。随后一行给出N个正数表示每种月饼的库存量（以万吨为单位）；最后一行给出N个正数表示每种月饼的总售价（以亿元为单位）。数字间以空格分隔。

> 输出描述:

对每组测试用例，在一行中输出最大收益，以亿元为单位并精确到小数点后2位。

> 输入例子:

3 20
18 15 10
75 72 45

> 输出例子:

94.50

## C++

```
#include <iostream>
#include <algorithm>
using namespace std;

struct Mooncake {
    int inventory, total_price;
    double unit_price;
} cakes[1000];

bool cmp(Mooncake a, Mooncake b) {
    return a.unit_price > b.unit_price;
}

int main(int argc, const char * argv[]) {
    // 输入
    int cake_types, max_need;
    cin >> cake_types >> max_need;
    for (int i = 0; i < cake_types; i++) {
        cin >> cakes[i].inventory;
    }
    for (int i = 0; i < cake_types; i++) {
        cin >> cakes[i].total_price;
        cakes[i].unit_price = (double)cakes[i].total_price / (double)cakes[i].inventory;
    }
    sort(cakes, cakes + cake_types, cmp);
    
    // 计算
    double income = 0;
    int i = 0;
    while (max_need > 0) {
        if (cakes[i].inventory > max_need) {
            income = income + cakes[i].unit_price * (double)max_need;
            max_need = 0;
        } else {
            income += (double)cakes[i].total_price;
            max_need -= cakes[i].inventory;
        }
        i++;
    }
    
    // 输出
    printf("%.2f\n", income);
    return 0;
}
```

# 1011 个位数统计 (15)

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB

> 题目描述

给定一个k位整数N = d_(k-1)*10^(k-1) + ... + d_1*10^1 + d_0 (0<=di<=9, i=0,...,k-1, d_(k-1)>0)，请编写程序统计每种不同的个位数字出现的次数。例如：给定N = 100311，则有2个0，3个1，和1个3。

> 输入描述:

每个输入包含1个测试用例，即一个不超过1000位的正整数N。

> 输出描述:

对N中每一种不同的个位数字，以D:M的格式在一行中输出该位数字D及其在N中出现的次数M。要求按D的升序输出。

> 输入例子:

100311

> 输出例子:

0:2
1:3
3:1

## C++

```
#include <iostream>
using namespace std;

int main(int argc, const char * argv[]) {
    // 输入
    char input[1001], *p;
    scanf("%s", input);
    p = input;
    
    // 计算
    int count[10] = {0};
    while (*p != '\0') {
        count[*p++ - 48]++;
    }
    
    // 输出
    for (int i = 0; i < 10; i++) {
        if (count[i] > 0) {
            printf("%d:%d\n", i, count[i]);
        }
    }
    return 0;
}
```

# 1012 D进制的A+B (20)

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB

> 题目描述

输入两个非负10进制整数A和B(<=2^30-1)，输出A+B的D (1 < D <= 10)进制数。

> 输入描述:

输入在一行中依次给出3个整数A、B和D。

> 输出描述:

输出A+B的D进制数。

> 输入例子:

123 456 8

> 输出例子:

1103

## C++

```
#include <iostream>
using namespace std;

void count(int d, int *r, int *v) {
    *v = *r + *v;
    *r = *v % d;
    *v /= d;
}

int main(int argc, const char * argv[]) {
    // 输入
    int a = 0, b = 0, d = 0;
    scanf("%d %d %d", &a, &b, &d);
    
    // 计算
    int r[64] = {0};
    for (int i = 63; i > 0; i--) {
        count(d, r + i, &a);
        count(d, r + i, &b);
        if (a == 0 && b == 0) {
            break;
        }
    }
    
    // 输出
    for (int i = 0; i < 64; i++) {
        if (d > 0) {
            if (r[i] > 0) {
                d = 0;
            } else {
                continue;
            }
        }
        printf("%d", r[i]);
    }
    
    return 0;
}
```

# 1013 组个最小数 (20)

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB

> 题目描述

给定数字0-9各若干个。你可以以任意顺序排列这些数字，但必须全部使用。目标是使得最后得到的数尽可能小（注意0不能做首位）。例如：给定两个0，两个1，三个5，一个8，我们得到的最小的数就是10015558。现给定数字，请编写程序输出能够组成的最小的数。

> 输入描述:

每个输入包含1个测试用例。每个测试用例在一行中给出10个非负整数，顺序表示我们拥有数字0、数字1、……数字9的个数。整数间用一个空格分隔。10个数字的总个数不超过50，且至少拥有1个非0的数字。


> 输出描述:

在一行中输出能够组成的最小的数。

> 输入例子:

2 2 0 0 0 3 0 0 1 0

> 输出例子:

10015558

## C++

```
#include <iostream>
using namespace std;

int main(int argc, const char * argv[]) {
    // 输入
    int s[10];
    scanf("%d %d %d %d %d %d %d %d %d %d", &s[0], &s[1], &s[2], &s[3], &s[4], &s[5], &s[6], &s[7], &s[8], &s[9]);
    
    // 计算
    
    // 输出
    for (int i = 1; i < 10; i++) {
        if (s[i] != 0) {
            s[i] -= 1;
            printf("%d", i);
            break;
        }
    }
    for (int i = 0; i < 10; i++) {
        for (int j = 0; j < s[i]; j++) {
            printf("%d", i);
        }
    }
    return 0;
}
```

# 1014 科学计数法 (20)

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB

> 题目描述

科学计数法是科学家用来表示很大或很小的数字的一种方便的方法，其满足正则表达式[+-][1-9]"."[0-9]+E[+-][0-9]+，即数字的整数部分只有1位，小数部分至少有1位，该数字及其指数部分的正负号即使对正数也必定明确给出。
现以科学计数法的格式给出实数A，请编写程序按普通数字表示法输出A，并保证所有有效位都被保留。

> 输入描述:

每个输入包含1个测试用例，即一个以科学计数法表示的实数A。该数字的存储长度不超过9999字节，且其指数的绝对值不超过9999。

> 输出描述:

对每个测试用例，在一行中按普通数字表示法输出A，并保证所有有效位都被保留，包括末尾的0。

> 输入例子:

+1.23400E-03

> 输出例子:

0.00123400

## C++

```
#include <iostream>
#include <cstring>
using namespace std;

int main(int argc, const char * argv[]) {
    // 输入
    char const E = 'E';
    char input[9999];
    char *p, *t;
    int e = 0;
    scanf("%s", input);
    p = strchr(input, E);
    t = p + 2;
    while (*t != '\0') {
        e *= 10;
        e = e + *t - 48;
        t++;
    }
    
    // 计算
    if (input[0] == '-') {
        printf("-");
    }
    
    t = input;
    t = t + 3;
    if (*(p + 1) == '+') {
        printf("%c", input[1]);
        while (*t != E) {
            if (e == 0) {
                printf(".%c", *t);
            } else {
                printf("%c", *t);
            }
            e--;
            t++;
        }
        while (e > 0) {
            printf("0");
            e--;
        }
    } else {
        printf("0.");
        e--;
        while (e > 0) {
            printf("0");
            e--;
        }
        printf("%c", input[1]);
        while (*t != E) {
            printf("%c", *t);
            t++;
        }
    }
    return 0;
}
```

# 1015 反转链表 (25)

> 时间限制 2000 ms 内存限制 150400 KB 代码长度限制 100 KB

> 题目描述

给定一个常数K以及一个单链表L，请编写程序将L中每K个结点反转。例如：给定L为1→2→3→4→5→6，K为3，则输出应该为3→2→1→6→5→4；如果K为4，则输出应该为4→3→2→1→5→6，即最后不到K个元素不反转。

> 输入描述:

每个输入包含1个测试用例。每个测试用例第1行给出第1个结点的地址、结点总个数正整数N(<= 105)、以及正整数K(<=N)，即要求反转的子链结点的个数。结点的地址是5位非负整数，NULL地址用-1表示。
接下来有N行，每行格式为：
Address Data Next
其中Address是结点地址，Data是该结点保存的整数数据，Next是下一结点的地址。

> 输出描述:

对每个测试用例，顺序输出反转后的链表，其上每个结点占一行，格式与输入相同。

> 输入例子:

00100 6 4
00000 4 99999
00100 1 12309
68237 6 -1
33218 3 00000
99999 5 68237
12309 2 33218

> 输出例子:

00000 4 33218
33218 3 12309
12309 2 00100
00100 1 99999
99999 5 68237
68237 6 -1

## C++

```
/**
 * 题目要点
    * 给出来的数据中可能不止一个链表，而是多个。
    * 不能把数据排序，否则会超时。
 * 解题思路
    * 先根据下标作为地址输入所有数据
    * 从第一个节点开始访问整个链表，并按分割模块逆序存放下标在输出数组中
    * 对输出数组按顺序输出，但是到最后一个模块时，逆序输出。
 */
#include <iostream>
using namespace std;

#define MAX 100000

int main(int argc, const char * argv[]) {
    // values
    int node = 0, count = 0, space = 0, idx = 0;
    int flg = 0;
    int datas[MAX], nexts[MAX];
    int sorts[MAX];
    
    // input
    scanf("%d %d %d", &node, &count, &space);
    while (count-- > 0) {
        scanf("%d", &idx);
        scanf("%d %d", &datas[idx], &nexts[idx]);
    }
    
    // sort to sorts
    // count: nodes block
    // flg: a point move in nodes block
    count = flg = 0;
    while (flg != -2) {
        flg = space - 1;
        while (flg >= 0) {
            sorts[flg + count] = node;
            node = node != -1 ? nexts[node] : -2;
            flg = sorts[flg + count] != -1 ? flg - 1 : -2;
        }
        count += space;
    }
    
    // output total nodes block except last.
    // if the node is smaller then spcae, then backward out.
    if (count > space) {
        printf("%05d %d ", sorts[0], datas[sorts[0]]);
        for (idx = 1; idx < count - space; idx++) {
            printf("%05d\n%05d %d ", sorts[idx], sorts[idx], datas[sorts[idx]]);
        }
    } else {
        printf("%05d %d ", sorts[space-1], datas[sorts[space-1]]);
        idx = -1;
    }
    
    // output last nodes block
    for (idx = idx + space - 1; idx >= count - space; idx--) {
        if (sorts[idx] == -1) {
            printf("-1\n");
            break;
        } else {
            printf("%05d\n%05d %d ", sorts[idx], sorts[idx], datas[sorts[idx]]);
        }
    }
    return 0;
}
```

# 1016 程序运行时间(15)

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB

> 题目描述

要获得一个C语言程序的运行时间，常用的方法是调用头文件time.h，其中提供了clock()函数，可以捕捉从程序开始运行到clock()被调用时所耗费的时间。这个时间单位是clock tick，即“时钟打点”。同时还有一个常数CLK_TCK，给出了机器时钟每秒所走的时钟打点数。于是为了获得一个函数f的运行时间，我们只要在调用f之前先调用clock()，获得一个时钟打点数C1；在f执行完成后再调用clock()，获得另一个时钟打点数C2；两次获得的时钟打点数之差(C2-C1)就是f运行所消耗的时钟打点数，再除以常数CLK_TCK，就得到了以秒为单位的运行时间。

这里不妨简单假设常数CLK_TCK为100。现给定被测函数前后两次获得的时钟打点数，请你给出被测函数运行的时间。

> 输入描述:

输入在一行中顺序给出2个整数C1和C1。注意两次获得的时钟打点数肯定不相同，即C1 < C2，并且取值在[0, 107]


> 输出描述:

在一行中输出被测函数运行的时间。运行时间必须按照“hh:mm:ss”（即2位的“时:分:秒”）格式输出；不足1秒的时间四舍五入到秒。

> 输入例子:

123 4577973

> 输出例子:

12:42:59

## C++

```
#include <iostream>
using namespace std;

int main(int argc, const char * argv[]) {
    int a, b;
    scanf("%d %d", &a, &b);
    a = (b - a + 50) / 100;
    printf("%02d:%02d:%02d", a / 3600, a / 60 % 60, a % 60);
    return 0;
}
```

# 1017 打印沙漏(20)

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB 判断程序 Standard (来自 小小)

> 题目描述

本题要求你写个程序把给定的符号打印成沙漏的形状。例如给定17个“*”，要求按下列格式打印
 
 *****
  ***
   *
  ***
 *****
 所谓“沙漏形状”，是指每行输出奇数个符号；各行符号中心对齐；相邻两行符号数差2；符号数先从大到小顺序递减到1，再从小到大顺序递
 增；首尾符号数相等。
 
 给定任意N个符号，不一定能正好组成一个沙漏。要求打印出的沙漏能用掉尽可能多的符号。

> 输入描述:

输入在一行给出1个正整数N（<=1000）和一个符号，中间以空格分隔。

> 输出描述:

首先打印出由给定符号组成的最大的沙漏形状，最后在一行中输出剩下没用掉的符号数。

> 输入例子:

19 *

> 输出例子:

*****
 ***
  *
 ***
*****
2

## C++

```
#include <iostream>
#include <math.h>
using namespace std;

int main(int argc, const char * argv[]) {
    int count;
    char sign;
    scanf("%d %c", &count, &sign);
    
    int k = (int)sqrt((double)((count+1)/2));
    int size = k * 2 - 1, line;
    for (int i = k; i > 0; i--) {
        line = i * 2 - 1;
        for (int j = 0; j < (size - line) / 2; j++) {
            printf(" ");
        }
        for (int j = 0; j < line; j++) {
            printf("%c", sign);
        }
        printf("\n");
    }
    for (int i = 2; i <= k; i++) {
        line = i * 2 - 1;
        for (int j = 0; j < (size - line) / 2; j++) {
            printf(" ");
        }
        for (int j = 0; j < line; j++) {
            printf("%c", sign);
        }
        printf("\n");
    }
    printf("%d\n", count - 2 * k * k + 1);
    return 0;
}
```

# 1018 人口普查(20)

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB 判断程序 Standard (来自 小小)

> 题目描述

某城镇进行人口普查，得到了全体居民的生日。现请你写个程序，找出镇上最年长和最年轻的人。
这里确保每个输入的日期都是合法的，但不一定是合理的——假设已知镇上没有超过200岁的老人，而今天是2014年9月6日，所以超过200岁的生日和未出生的生日都是不合理的，应该被过滤掉。

> 输入描述:

输入在第一行给出正整数N，取值在(0, 105]；随后N行，每行给出1个人的姓名（由不超过5个英文字母组成的字符串）、以及按“yyyy/mm/dd”（即年/月/日）格式给出的生日。题目保证最年长和最年轻的人没有并列。

> 输出描述:

在一行中顺序输出有效生日的个数、最年长人和最年轻人的姓名，其间以空格分隔。

> 输入例子:

5
John 2001/05/12
Tom 1814/09/06
Ann 2121/01/30
James 1814/09/05
Steve 1967/11/20

> 输出例子:

3 Tom John

## C++

```
#include <iostream>
using namespace std;

struct Date {
    char name[6];
    int year, month = 9, day = 6;
};

// is a older then b
bool cmp(Date a, Date b) {
    if (a.year == b.year) {
        if (a.month == b.month) {
            return a.day < b.day;
        } else {
            return a.month < b.month;
        }
    } else {
        return a.year < b.year;
    }
}

// cpy b to a
void cpy(Date *a, Date *b) {
    for (int i = 0; i < 6; i++) {
        a->name[i] = b->name[i];
    }
    a->year = b->year;
    a->month = b->month;
    a->day = b->day;
}

int main(int argc, const char * argv[]) {
    int number = 0, count = 0;
    Date new_gay, oldest, youngest, tooold, tooyoung;
    tooold.year = youngest.year = 1814;
    tooyoung.year = oldest.year = 2014;
    scanf("%d", &count);
    for (int i = 0; i < count; i++) {
        scanf("%s %d/%d/%d", new_gay.name, &new_gay.year, &new_gay.month, &new_gay.day);
        if (cmp(new_gay, tooold) || cmp(tooyoung, new_gay)) {
            continue;
        }
        number++;
        if (cmp(new_gay, oldest)) {
            cpy(&oldest, &new_gay);
        }
        if (cmp(youngest, new_gay)) {
            cpy(&youngest, &new_gay);
        }
    }
    
    printf("%d %s %s\n", number, oldest.name, youngest.name);
    return 0;
}
```

# 1019 旧键盘 (20)

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB 判断程序 Standard (来自 小小)

> 题目描述

旧键盘上坏了几个键，于是在敲一段文字的时候，对应的字符就不会出现。现在给出应该输入的一段文字、以及实际被输入的文字，请你列出肯定坏掉的那些键。

> 输入描述:

输入在2行中分别给出应该输入的文字、以及实际被输入的文字。每段文字是不超过80个字符的串，由字母A-Z（包括大、小写）、数字0-9、以及下划线“_”（代表空格）组成。题目保证2个字符串均非空。

> 输出描述:

按照发现顺序，在一行中输出坏掉的键。其中英文字母只输出大写，每个坏键只输出一次。题目保证至少有1个坏键。

> 输入例子:

7_This_is_a_test
_hs_s_a_es

> 输出例子:

7TI

```
#include <iostream>
#include <cstring>
using namespace std;
#define S 81

char *upper(char *s) {
    char *t = s;
    while (*t != '\0') {
        if (*t > 96 && *t < 123) {
            *t = *t - 32;
        }
        t++;
    }
    return s;
}

int main(int argc, const char * argv[]) {
    char want[S], input[S], bad[S];
    scanf("%s\n%s", want, input);
    char *w = upper(want), *i = upper(input), *b = bad;
    while (*w != '\0') {
        if (*w != *i) {
            if (strchr(bad, *w) == NULL) {
                *b++ = *w;
            }
            w++;
        } else {
            w++; i++;
        }
    }
    printf("%s", bad);
    return 0;
}
```

# 1020 完美数列(25)

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB 判断程序 Standard (来自 小小)

> 题目描述

给定一个正整数数列，和正整数p，设这个数列中的最大值是M，最小值是m，如果M <= m * p，则称这个数列是完美数列。现在给定参数p和一些正整数，请你从中选择尽可能多的数构成一个完美数列。

> 输入描述:

输入第一行给出两个正整数N和p，其中N（<= 105）是输入的正整数的个数，p（<= 109）是给定的参数。第二行给出N个正整数，每个数不超过109。

> 输出描述:

在一行中输出最多可以选择多少个数可以用它们组成一个完美数列。

> 输入例子:

10 8
2 3 20 4 5 1 6 7 8 9

> 输出例子:

8

```
#include <iostream>
#include <algorithm>
#define MAX 10
using namespace std;

int main(int argc, const char * argv[]) {
    int count, p_number, datas[MAX];
    scanf("%d %d", &count, &p_number);
    for (int i = 0; i < count; i++) {
        scanf("%d", &datas[i]);
    }
    sort(datas, datas + count);
    int big = 0, size = 0;
    int idx_small = 0, idx_big = 0, idx = 0;
    for (int i = 0; i < count; i++) {
        big = p_number * datas[i];
        if (count - i > size) {
            idx_small = i; idx_big = count;
            idx = (idx_big + idx_small) / 2;
            while (idx_small + 1 < idx_big) {
                if (datas[idx] > big) {
                    idx_big = idx;
                    idx = (idx_big + idx_small) / 2;
                } else {
                    idx_small = idx;
                    idx = (idx_big + idx_small) / 2;
                }
            }
            size = max(idx - i + 1, size);
//            for (int k = count - 1; k > i; k--) {
//                if (datas[k] <= big) {
//                    size = max(k - i + 1, size);
//                    break;
//                }
//            }
        }
    }
    printf("%d\n", size);
    return 0;
}
```
# 1021 1031. 查验身份证(15)

时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB

题目描述

一个合法的身份证号码由17位地区、日期编号和顺序编号加1位校验码组成。校验码的计算规则如下：

首先对前17位数字加权求和，权重分配为：{7，9，10，5，8，4，2，1，6，3，7，9，10，5，8，4，2}；然后将计算的和对11取模得到值Z；最后按照以下关系对应Z值与校验码M的值：

Z：0 1 2 3 4 5 6 7 8 9 10
M：1 0 X 9 8 7 6 5 4 3 2

现在给定一些身份证号码，请你验证校验码的有效性，并输出有问题的号码。

输入描述:

输入第一行给出正整数N（<= 100）是输入的身份证号码的个数。随后N行，每行给出1个18位身份证号码。

输出描述:

按照输入的顺序每行输出1个有问题的身份证号码。这里并不检验前17位是否合理，只检查前17位是否全为数字且最后1位校验码计算准确。如果所有号码都正常，则输出“All passed”。

输入例子:

4
320124198808240056
12010X198901011234
110108196711301866
37070419881216001X

输出例子:

12010X198901011234
110108196711301866
37070419881216001X

## C++

```
#include <iostream>
using namespace std;

int main(int argc, const char * argv[]) {
    int weights[] = {7,9,10,5,8,4,2,1,6,3,7,9,10,5,8,4,2};
    char m_chars[] = {'1','0','x','9','8','7','6','5','4','3','2'};
    char users[100][20];
    int count = 0, right_number = 0, sum = 0;
    scanf("%d", &count);
    for (int i = 0; i < count; i++) {
        scanf("%s", users[i]);
        sum = 0;
        for (int k = 0; k < 17; k++) {
            sum = sum + (users[i][k] - 48) * weights[k];
        }
        sum %= 11;
        if (users[i][17] == m_chars[sum]) {
            users[i][19] = 1;
            right_number++;
        } else {
            users[i][19] = 0;
        }
    }
    
    if (right_number == count) {
        printf("All passed");
    } else {
        for (int i = 0; i < count; i++) {
            if (users[i][19] == 0) {
                printf("%s\n", users[i]);
            }
        }
    }
    return 0;
}
```

# 1022 挖掘机技术哪家强(20)

时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB

> 题目描述

为了用事实说明挖掘机技术到底哪家强，PAT组织了一场挖掘机技能大赛。现请你根据比赛结果统计出技术最强的那个学校。

> 输入描述:

输入在第1行给出不超过105的正整数N，即参赛人数。随后N行，每行给出一位参赛者的信息和成绩，包括其所代表的学校的编号（从1开始连续编号）、及其比赛成绩（百分制），中间以空格分隔。

> 输出描述:

在一行中给出总得分最高的学校的编号、及其总分，中间以空格分隔。题目保证答案唯一，没有并列。

> 输入例子:

6
3 65
2 80
1 100
2 70
3 40
3 0

> 输出例子:

2 150

## C++

```
#include <iostream>
using namespace std;

int main(int argc, const char * argv[]) {
    int count = 0, max = 0, school = 0, score = 0, scores[100001] = {0};
    scanf("%d", &count);
    for (int i = 0; i < count; i++) {
        scanf("%d %d", &school, &score);
        scores[school] += score;
        max = scores[max] > scores[school] ? max : school;
    }
    printf("%d %d\n", max, scores[max]);
    return 0;
}
```

# 1023 旧键盘打字(20)

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB 

> 题目描述

旧键盘上坏了几个键，于是在敲一段文字的时候，对应的字符就不会出现。现在给出应该输入的一段文字、以及坏掉的那些键，打出的结果文字会是怎样？

> 输入描述:

输入在2行中分别给出坏掉的那些键、以及应该输入的文字。其中对应英文字母的坏键以大写给出；每段文字是不超过10^5个字符的串。可用的字符包括字母[a-z, A-Z]、数字0-9、以及下划线“_”（代表空格）、“,”、“.”、“-”、“+”（代表上档键）。题目保证第2行输入的文字串非空。
注意：如果上档键坏掉了，那么大写的英文字母无法被打出。

> 输出描述:

在一行中输出能够被打出的结果文字。如果没有一个字符能被打出，则输出空行。

> 输入例子:

7+IE.
7_This_is_a_test.

> 输出例子:

_hs_s_a_tst

## C++

```
#include <iostream>
#include <cstring>
using namespace std;

int main(int argc, const char * argv[]) {
    char bad_chars[124];
    char input_chars[100001];
    char *c = bad_chars, flag = 0;
    do {
        scanf("%c", c);
        if (*c == '+') {
            for (int i = 65; i < 91; i++) {
                *c++ = i;
            }
            flag = -1;
            c--;
        } else if (*c > 64 && *c < 91) {
            if (flag == -1) {
                *c = *c + 32;
            } else {
                flag = *c++;
                *c = flag + 32;
            }
        }
    } while (*c++ != '\n');
    *--c = '\0';
    
    c = input_chars;
    do {
        scanf("%c", c);
        if (strchr(bad_chars, *c) == NULL) {
            printf("%c", *c);
        }
    } while (*c++ != '\n');
    
    return 0;
}
```

# 1024 有理数四则运算(20)

时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB 判断程序 Standard (来自 小小)

题目描述

本题要求编写程序，计算2个有理数的和、差、积、商。

输入描述:

输入在一行中按照“a1/b1 a2/b2”的格式给出两个分数形式的有理数，其中分子和分母全是整型范围内的整数，负号只可能出现在分子前，分母不为0。

输出描述:

分别在4行中按照“有理数1 运算符 有理数2 = 结果”的格式顺序输出2个有理数的和、差、积、商。注意输出的每个有理数必须是该有理数的最简形式“k a/b”，其中k是整数部分，a/b是最简分数部分；若为负数，则须加括号；若除法分母为0，则输出“Inf”。题目保证正确的输出中没有超过整型范围的整数。

输入例子:

5/3 0/6

输出例子:

1 2/3 + 0 = 1 2/3
1 2/3 - 0 = 1 2/3
1 2/3 * 0 = 0
1 2/3 / 0 = Inf

## C++

```
#include <iostream>
using namespace std;

// 求公约数
int common_divisor(int a, int b) {
    int r = 0;
    do {
        r = a % b;
        a = b;
        b = r;
    } while (r != 0);
    return a;
}

struct Number {
    bool c = true; // 正负号
    int i = 0; // 整数
    int m = 0; // 分子
    int d = 0; // 分母
    
    // 输出完整的分子
    int count_m() {
        return (c ? 1 : -1) * (i * d + m);
    }
    
    // 简化分子分母
    void simplify() {
        c = m * d >= 0;
        m = abs(m);
        d = abs(d);
        i = m / d;
        m = m % d;
        if (m != 0) {
            int c = common_divisor(m, d);
            m = m / c;
            d = d / c;
        }
    }
    
    // 打印信息
    void print() {
        if (i == 0) {
            if (m == 0) {
                printf("0");
            } else {
                if (c) {
                    printf("%d/%d", m, d);
                } else {
                    printf("(-%d/%d)", m, d);
                }
            }
        } else {
            if (m == 0) {
                if (c) {
                    printf("%d", i);
                } else {
                    printf("(-%d)", i);
                }
            } else {
                if (c) {
                    printf("%d %d/%d", i, m, d);
                } else {
                    printf("(-%d %d/%d)", i, m, d);
                }
            }
        }
    }
};

void plus_number(Number a, Number b) {
    Number c;
    c.d = a.d * b.d;
    c.m = a.count_m() * b.d + b.count_m() * a.d;
    c.simplify();
    a.print(); printf(" + "); b.print(); printf(" = "); c.print(); printf("\n");
}

void reduce_number(Number a, Number b) {
    Number c;
    c.d = a.d * b.d;
    c.m = a.count_m() * b.d - b.count_m() * a.d;
    c.simplify();
    a.print(); printf(" - "); b.print(); printf(" = "); c.print(); printf("\n");
}

void multiply_number(Number a, Number b) {
    Number c;
    c.d = a.d * b.d;
    c.m = a.count_m() * b.count_m();
    c.simplify();
    a.print(); printf(" * "); b.print(); printf(" = "); c.print(); printf("\n");
}

void divide_number(Number a, Number b) {
    if (b.count_m() == 0) {
        a.print(); printf(" / "); b.print(); printf(" = Inf\n");
    } else {
        Number c;
        c.d = a.d * b.count_m();
        c.m = a.count_m() * b.d;
        c.simplify();
        a.print(); printf(" / "); b.print(); printf(" = "); c.print(); printf("\n");
    }
}

int main(int argc, const char * argv[]) {
    
    Number a, b, out;
    //a.m = 5; a.d = 3; b.m = 0; b.d = 6;
    scanf("%d/%d %d/%d", &a.m, &a.d, &b.m, &b.d);
    a.simplify();
    b.simplify();
    
    plus_number(a, b);
    reduce_number(a, b);
    multiply_number(a, b);
    divide_number(a, b);
    return 0;
}
```

# 1025 插入与归并(25)

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB

> 题目描述

根据维基百科的定义：
插入排序是迭代算法，逐一获得输入数据，逐步产生有序的输出序列。每步迭代中，算法从输入序列中取出一元素，将之插入有序序列中正确的位置。如此迭代直到全部元素有序。
归并排序进行如下迭代操作：首先将原始序列看成N个只包含1个元素的有序子序列，然后每次迭代归并两个相邻的有序子序列，直到最后只剩下1个有序的序列。
现给定原始序列和由某排序算法产生的中间序列，请你判断该算法究竟是哪种排序算法？

> 输入描述:

输入在第一行给出正整数N (<=100)；随后一行给出原始序列的N个整数；最后一行给出由某排序算法产生的中间序列。这里假设排序的目标序列是升序。数字间以空格分隔。

> 输出描述:

首先在第1行中输出“Insertion Sort”表示插入排序、或“Merge Sort”表示归并排序；然后在第2行中输出用该排序算法再迭代一轮的结果序列。题目保证每组测试的结果是唯一的。数字间以空格分隔，且行末不得有多余空格。

> 输入例子:

10
3 1 2 8 7 5 9 4 6 0
1 2 3 7 8 5 9 4 6 0

> 输出例子:

Insertion Sort
1 2 3 5 7 8 9 4 6 0

> 输入例子:

10
3 1 2 8 7 5 9 4 0 6
1 3 2 8 5 7 4 9 0 6

> 输出例子:

Merge Sort
1 2 3 8 4 5 7 9 0 6

10
3 1 2 8 7 5 9 4 6 0
1 2 3 5 7 8 9 4 6 0

Insertion Sort
1 2 3 4 5 7 8 9 6 0

## C++ 1

```
#include <iostream>
#define MAX 1000
using namespace std;

int merge_flag = 0, insert_flag = 0;
int size = 0;
int insert_array[MAX] = {0};
int merge_array[MAX] = {0};
int complete_array[MAX] = {0};

// 对比数组
bool compare(int *array1, int *array2, int size) {
    for (int i = 0; i < size; i++) {
        if (array1[i] != array2[i]) {
            return false;
        }
    }
    return true;
}

// 打印数组
void print_array(int *array, int size) {
    for (int i = 0; i < size - 1; i++) {
        printf("%d ", array[i]);
    }
    printf("%d\n", array[size - 1]);
}

// 归并排序 - 排序
void sort_merge_sort(int *array, int *temp_array, int idx_start, int idx_mid, int idx_end) {
    int s = idx_start, m = idx_mid, t = idx_start;
    while (s < idx_mid && m < idx_end) {
        if (array[s] < array[m]) {
            temp_array[t++] = array[s++];
        } else {
            temp_array[t++] = array[m++];
        }
    }
    while (s < idx_mid) {
        temp_array[t++] = array[s++];
    }
    while (m < idx_end) {
        temp_array[t++] = array[m++];
    }
    t = idx_start;
    while (t < idx_end) {
        array[t] = temp_array[t];
        t++;
    }
}

// 归并排序 - 归并
void sort_merge(int *array, int *temp_array, int idx_start, int idx_end) {
    int idx_mid = (idx_end + idx_start) / 2;
    if (idx_start < idx_end - 1 && merge_flag != 2) {
        sort_merge(array, temp_array, idx_start, idx_mid);
        sort_merge(array, temp_array, idx_mid, idx_end);
        sort_merge_sort(array, temp_array, idx_start, idx_mid, idx_end);
        if (merge_flag == 0) {
            if (compare(array, complete_array, size)) {
                merge_flag = 1;
            }
        } else if (merge_flag == 1) {
            printf("Merge Sort\n");
            print_array(array, size);
            merge_flag = 2;
        }
    }
}
void sort_merge2(int *array, int *temp_array, int size) {
    int left_point = 0, right_point = 0, left_limit = 0, right_limit = 0, next = 0;
    for (int i = 1; i < size; i *= 2) { // 分块步长
        for (left_point = 0; left_point < size - i; left_point = right_limit) { // 分块
            next = left_point;
            left_limit = right_point = left_point + i;
            right_limit = right_point + i;
            while (left_point < left_limit && right_point < right_limit) {
                if (array[left_point] < array[right_point]) {
                    temp_array[next++] = array[left_point++];
                } else  {
                    temp_array[next++] = array[right_point++];
                }
            }
            while (left_point < left_limit) {
                temp_array[next++] = array[left_point++];
            }
            while (right_point < right_limit) {
                temp_array[next++] = array[right_point++];
            }
        }
        for (next = 0; next < size; next++) {
            array[next] = temp_array[next];
        }
        if (insert_flag == 0) {
            if (compare(array, complete_array, size)) {
                insert_flag = 1;
            }
        } else if (insert_flag == 1) {
            printf("Merge Sort\n");
            print_array(array, size);
            merge_flag = 2;
            break;
        }
    }
}

void sort_insert(int *array, int size) {
    int temp;
    for (int i = 0; i < size && insert_flag != 3; i++) {
        for (int j = i - 1; j >= 0 && insert_flag != 3; j--) {
            if (array[j] > array[j+1]) {
                temp = array[j];
                array[j] = array[j+1];
                array[j+1] = temp;
                if (insert_flag == 1) {
                    insert_flag = 2;
                }
            }
        }
        if (insert_flag == 0) {
            if (compare(array, complete_array, size)) {
                insert_flag = 1;
            }
        } else if (insert_flag == 2) {
            printf("Insertion Sort\n");
            print_array(array, size);
            insert_flag = 3;
        }
    }
}

int main(int argc, const char * argv[]) {
    scanf("%d", &size);
    int value;
    for (int i = 0; i < size; i++) {
        scanf("%d", &value);
        insert_array[i] = merge_array[i] = value;
    }
    for (int i = 0; i < size; i++) {
        scanf("%d", &complete_array[i]);
    }
    sort_insert(insert_array, size);
    if (insert_flag == 0) {
        int temp_array[MAX];
        sort_merge2(merge_array, temp_array, size);
        //sort_merge(merge_array, temp_array, 0, size);
    }
    return 0;
}
```

## C++ 2

```
#include <iostream>
using namespace std;

// 对比数组
bool compare(int *array1, int *array2, int size) {
    for (int i = 0; i < size; i++) {
        if (array1[i] != array2[i]) {
            return false;
        }
    }
    return true;
}

// 打印数组
void print_array(int *array, int size) {
    for (int i = 0; i < size - 1; i++) {
        printf("%d ", array[i]);
    }
    printf("%d\n", array[size - 1]);
}

int main(int argc, const char * argv[]) {
    int lenght, array_compare[100], array_insert[100], array_merge[100], array_merge_temp[100];
    int flag = 0;
    
    // input
    scanf("%d", &lenght);
    for (int i = 0; i < lenght; i++) {
        scanf("%d", &array_insert[i]);
        array_merge[i] = array_insert[i];
    }
    for (int i = 0; i < lenght; i++) {
        scanf("%d", &array_compare[i]);
    }
    
    // insert sort
    int temp = 0;
    for (int i = 1; i < lenght; i++) {
        for (int j = i - 1; j >= 0; j--) {
            if (array_insert[j] > array_insert[j+1]) {
                temp = array_insert[j];
                array_insert[j] = array_insert[j+1];
                array_insert[j+1] = temp;
                if (flag == 1) {
                    flag = 2;
                }
            }
        }
        if (flag == 0) {
            if (compare(array_compare, array_insert, lenght)) {
                flag = 1;
            }
        } else if (flag == 2) {
            printf("Insertion Sort\n");
            print_array(array_insert, lenght);
            return 0;
        }
    }
    
    // merge sort
    int left = 0, right = 0, limit_left = 0, limit_right = 0;
    for (int i = 1; i < lenght; i *= 2) {
        for (left = 0; left < lenght - i; left = limit_right) {
            temp = left;
            right = limit_left = left + i;
            limit_right = right + i;
            while (left < limit_left && right < limit_right) {
                if (array_merge[left] < array_merge[right]) {
                    array_merge_temp[temp++] = array_merge[left++];
                } else {
                    array_merge_temp[temp++] = array_merge[right++];
                }
            }
            while (left < limit_left) {
                array_merge_temp[temp++] = array_merge[left++];
            }
            while (right < limit_right) {
                array_merge_temp[temp++] = array_merge[right++];
            }
        }
        for (temp = 0; temp < lenght; temp++) {
            array_merge[temp] = array_merge_temp[temp];
        }
        if (flag == 0) {
            if (compare(array_compare, array_merge, lenght)) {
                flag = 1;
            }
        } else if (flag == 1) {
            printf("Merge Sort\n");
            print_array(array_merge, lenght);
            return 0;
        }
    }
    return 0;
}
```
# 1026 跟奥巴马一起编程(15)

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB

> 题目描述

美国总统奥巴马不仅呼吁所有人都学习编程，甚至以身作则编写代码，成为美国历史上首位编写计算机代码的总统。2014年底，为庆祝“计算机科学教育周”正式启动，奥巴马编写了很简单的计算机代码：在屏幕上画一个正方形。现在你也跟他一起画吧！

> 输入描述:

输入在一行中给出正方形边长N（3<=N<=20）和组成正方形边的某种字符C，间隔一个空格。

> 输出描述:

输出由给定字符C画出的正方形。但是注意到行间距比列间距大，所以为了让结果看上去更像正方形，我们输出的行数实际上是列数的50%（四舍五入取整）。

> 输入例子:

10 a

> 输出例子:

aaaaaaaaaa
a a
a a
a a
aaaaaaaaaa

## C++

```
#include <iostream>
using namespace std;

int main(int argc, const char * argv[]) {
    int count;
    char sign;
    scanf("%d %c", &count, &sign);
    
    for (int c = 0; c < count; c++) {
        printf("%c", sign);
    }
    printf("\n");
    int rows =  count / 2 - (count % 2 == 1 ? 0 : 1);
    for (int r = 1; r < rows; r++) {
        printf("%c", sign);
        for (int c = 1; c < count - 1; c++) {
            printf(" ");
        }
        printf("%c\n", sign);
    }
    for (int c = 0; c < count; c++) {
        printf("%c", sign);
    }
    printf("\n");
}
```

# 1027 在霍格沃茨找零钱（20）

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB

> 题目描述

如果你是哈利·波特迷，你会知道魔法世界有它自己的货币系统 —— 就如海格告诉哈利的：“十七个银西可(Sickle)兑一个加隆(Galleon)，二十九个纳特(Knut)兑一个西可，很容易。”现在，给定哈利应付的价钱P和他实付的钱A，你的任务是写一个程序来计算他应该被找的零钱。

> 输入描述:

输入在1行中分别给出P和A，格式为“Galleon.Sickle.Knut”，其间用1个空格分隔。这里Galleon是[0, 107]]区间内的整数，Sickle是[0, 17)区间内的整数，Knut是[0, 29)区间内的整数。

> 输出描述:

在一行中用与输入同样的格式输出哈利应该被找的零钱。如果他没带够钱，那么输出的应该是负数。

> 输入例子:

10.16.27 14.1.28

> 输出例子:

3.2.1

## C++

```
#include <iostream>
using namespace std;

struct Money {
    int galleon = 0;
    int sickle = 0;
    int kunt = 0;
    
    void count() {
        sickle = kunt / 29;
        kunt = abs(kunt % 29);
        galleon = sickle / 17;
        sickle = abs(sickle % 17);
    }
};

int main(int argc, const char * argv[]) {
    Money p, a;
    scanf("%d.%d.%d %d.%d.%d", &p.galleon, &p.sickle, &p.kunt, &a.galleon, &a.sickle, &a.kunt);
    a.galleon = a.galleon - p.galleon;
    a.sickle = a.galleon * 17 + a.sickle - p.sickle;
    a.kunt = a.sickle * 29 + a.kunt - p.kunt;
    a.count();
    printf("%d.%d.%d\n", a.galleon, a.sickle, a.kunt);
}
```

# 1028 统计同成绩学生(20)

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB

> 题目描述

本题要求读入N名学生的成绩，将获得某一给定分数的学生人数输出。

> 输入描述:

输入在第1行给出不超过105的正整数N，即学生总人数。随后1行给出N名学生的百分制整数成绩，中间以空格分隔。最后1行给出要查询的分数个数K（不超过N的正整数），随后是K个分数，中间以空格分隔。

> 输出描述:

在一行中按查询顺序给出得分等于指定分数的学生人数，中间以空格分隔，但行末不得有多余空格。

> 输入例子:

10
60 75 90 55 75 99 82 90 75 50
3 75 90 88

> 输出例子:

3 2 0

## C++

```
#include <iostream>
#include <algorithm>
using namespace std;

int main(int argc, const char * argv[]) {
    int score_lenght, scores[100000], count_lenght, counts[100000];
    int out[100000];
    scanf("%d", &score_lenght);
    for (int i = 0; i < score_lenght; i++) {
        scanf("%d", &scores[i]);
    }
    scanf("%d", &count_lenght);
    for (int i = 0; i < count_lenght; i++) {
        scanf("%d", &counts[i]);
    }
    
    for (int j = 0; j < count_lenght; j++) {
        for (int i = 0; i < score_lenght; i++) {
            if (counts[j] == scores[i]) {
                out[j]++;
            }
        }
    }
    
    for (int i = 0; i < count_lenght-1; i++) {
        printf("%d ", out[i]);
    }
    printf("%d\n", out[count_lenght-1]);
}
```

# 1029 到底买不买（20）

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB 判断程序 Standard (来自 小小)

> 题目描述

小红想买些珠子做一串自己喜欢的珠串。卖珠子的摊主有很多串五颜六色的珠串，但是不肯把任何一串拆散了卖。于是小红要你帮忙判断一下，某串珠子里是否包含了全部自己想要的珠子？如果是，那么告诉她有多少多余的珠子；如果不是，那么告诉她缺了多少珠子。
为方便起见，我们用[0-9]、[a-z]、[A-Z]范围内的字符来表示颜色。例如，YrR8RrY是小红想做的珠串；那么ppRYYGrrYBR2258可以买，因为包含了全部她想要的珠子，还多了8颗不需要的珠子；ppRYYGrrYB225不能买，因为没有黑色珠子，并且少了一颗红色的珠子。

> 输入描述:

每个输入包含1个测试用例。每个测试用例分别在2行中先后给出摊主的珠串和小红想做的珠串，两串都不超过1000个珠子。

> 输出描述:

如果可以买，则在一行中输出“Yes”以及有多少多余的珠子；如果不可以买，则在一行中输出“No”以及缺了多少珠子。其间以1个空格分隔。

> 输入例子:

ppRYYGrrYBR2258
YrR8RrY

> 输出例子:

Yes 8

## C++

```
#include <iostream>
using namespace std;

int main(int argc, const char * argv[]) {
    char sell_array[1001], buy_array[1001];
    scanf("%s", sell_array);
    scanf("%s", buy_array);
    
    char *sell_end = sell_array;
    char *buy_end = buy_array;
    while (*sell_end != '\0') { sell_end++; }
    while (*buy_end != '\0') { buy_end++; }
    
    char *sell = sell_array;
    char *buy = buy_array;
    
    while (*sell != '\0') {
        buy = buy_array;
        while (*buy != '\0') {
            if (*buy == *sell) {
                *buy = *--buy_end;
                *buy_end = '\0';
                *sell = *--sell_end;
                *sell_end = '\0';
                sell--;
                break;
            }
            buy++;
        }
        sell++;
    }
    
    int count = 0;
    if (buy_array[0] == '\0') {
        while (sell_end-- != sell_array) { count++; }
        printf("Yes %d\n", count);
    } else {
        while (buy_end-- != buy_array) { count++; }
        printf("No %d\n", count);
    }
}
```

# 1030 有几个PAT（25）

> 时间限制 1000 ms 内存限制 32768 KB 代码长度限制 100 KB 判断程序 Standard (来自 小小)

> 题目描述

字符串APPAPT中包含了两个单词“PAT”，其中第一个PAT是第2位(P),第4位(A),第6位(T)；第二个PAT是第3位(P),第4位(A),第6位(T)。现给定字符串，问一共可以形成多少个PAT？

> 输入描述:

输入只有一行，包含一个字符串，长度不超过105，只包含P、A、T三种字母。

> 输出描述:

在一行中输出给定字符串中包含多少个PAT。由于结果可能比较大，只输出对1000000007取余数的结果。

> 输入例子:

APPAPT

> 输出例子:

2

## C++

```
#include <iostream>
using namespace std;

int main(int argc, const char * argv[]) {
    char inputs[100001];
    scanf("%s", inputs);
    
    long long p_numbers[100001], p = 0, t_numbers[100001], t = 0;
    int lenght = 100001;
    for (int i = 0; i < lenght; i++) {
        if (inputs[i] == '\0') {
            lenght = i;
            break;
        }
        if (inputs[i] == 'P') {
            p++;
        }
        p_numbers[i] = p;
    }
    for (int k = lenght; k >= 0; k--) {
        if (inputs[k] == 'T') {
            t++;
        }
        t_numbers[k] = t;
    }
    
    long long count = 0;
    for (int i = 1; i < lenght - 1; i++) {
        if (inputs[i] == 'A') {
            count = count + p_numbers[i] * t_numbers[i];
            count %= 1000000007;
        }
    }
    
    printf("%lld", count);
    return 0;
}
```
