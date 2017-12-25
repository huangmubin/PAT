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
