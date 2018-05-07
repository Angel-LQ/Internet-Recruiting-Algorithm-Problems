<!-- TOC -->
* [��һ��](#��һ��)
* [�ڶ���](#�ڶ���)
* [������](#������)
* [������](#������)
* [������](#������)
* [������](#������)
* [������](#������)
* [�ڰ���](#�ڰ���)
<!-- TOC -->


## ��һ��

### ��Ŀ����
>ƽ������n�����Σ����½�����(x1[i],y1[i])�����Ͻ�����(x2[i],y2[i])���ж��ص����������Ŀ�Ƕ��١�������������������й�����������Ϊ�������ص��ģ������Ǳ߽�ͽ��䡣������ƽ�����ص��������ĵط��ľ�����Ŀ��

**��������:**
>����������У���һ�б�ʾ������Ŀn���ڶ���x1-->���½Ǻ����꣬������y1-->���½������꣬������x2-->���ϽǺ����꣬������y2-->���Ͻ������ꡣ

**�������:**
>�������ص��ľ�����Ŀ����������ص����1.

### ����˼·
- �������һ�����������ķ�ʽ�������Ե�һ��Ϊ��׼���Ժ���ľ��ν����������жϣ�������룬���֦��������������ص�������Ҫ�������Ƿ�������ص������ڵģ������ߵݹ��������ֵ���ɡ�ͬʱ����Ҫ��ÿ����Ϊ��׼����������һ�Σ�����̰��˼�뱣�����ֵ��

### �ο�����

```java
import java.util.Scanner;
public class Main {
    public static int solve(int[] x1, int[] x2, int[] y1, int[] y2, int k,
            int xa, int ya, int xb, int yb) {
        if (k == x1.length)
            return 0;
        else {
            if (x1[k] >= xb || y1[k] >= yb || xa >= x2[k] || ya >= y2[k])// �ų�����������
                return solve(x1, x2, y1, y2, k + 1, xa, ya, xb, yb);
            else {
                int xa1 = Math.max(xa, x1[k]);
                int ya1 = Math.max(ya, y1[k]);
                int xb1 = Math.min(xb, x2[k]);
                int yb1 = Math.min(yb, y2[k]);// �����ǰ���μ������ڣ�������������
                return Math.max(solve(x1, x2, y1, y2, k + 1, xa, ya, xb, yb),
                        solve(x1, x2, y1, y2, k + 1, xa1, ya1, xb1, yb1) + 1);// ��ǰ�����㲻��
            }
        }
    }
    public static void main(String[] args) {
        // TODO Auto-generated method stub
        Scanner sc = new Scanner(System.in);
        while (sc.hasNext()) {
            int n = sc.nextInt();
            int[] x1 = new int[n];
            int[] y1 = new int[n];
            int[] x2 = new int[n];
            int[] y2 = new int[n];
            for (int i = 0; i < n; i++) {
                x1[i] = sc.nextInt();
            }
            for (int i = 0; i < n; i++) {
                y1[i] = sc.nextInt();
            }
            for (int i = 0; i < n; i++) {
                x2[i] = sc.nextInt();
            }
            for (int i = 0; i < n; i++) {
                y2[i] = sc.nextInt();
            }
            int ans = 1;
            for (int i = 0; i < x1.length; i++)// �����Բ�ͬ����Ϊ�������м��㣬ͬʱ����Ӧ�������Ϊ��׼ֵ�������ֵ��
            {
                int num = solve(x1, x2, y1, y2, 0, x1[i], y1[i], x2[i], y2[i]);
                ans = Math.max(num, ans);
            }
            System.out.println(ans);
        }
    }
}
```

## �ڶ���
### ��Ŀ����
>ţţ��ǰ����ʦ����õ���һ�����������ԣ�x,y����ţţ�������Ǿ����Ƕ����ˡ�����ţţ�ǵ���ʦ������x��y��������n,����x����y���������ڵ���k��ţţϣ�����ܰ�������һ���ж��ٸ����ܵ����ԡ�

**��������:**
>�����������������n,k(1<=n<=10^5,0<=k<=n-1)

**���������**
>����ÿ���������������һ����������ʾ���ܵ�����������

**���ӣ�**

���룺
```
5 2
```
���
```
7
```
˵��
```
���������������У���2,3����2,4����2,5����3,4����3,5����4,5����5,3��
```

### ����˼·

- ����ѭ������
- ����ÿ��ѭ����������������k��Ԫ�صĸ���,�Լ�ʣ�µ�һ��ѭ����������������������ڵ���k��Ԫ�صĸ���
- ����
```
n=10 k=2
i= 1  %  3 =  1
i= 2  %  3 =  2
i= 3  %  3 =  0
i= 4  %  3 =  1
i= 5  %  3 =  2
i= 6  %  3 =  0
i= 7  %  3 =  1
i= 8  %  3 =  2
i= 9  %  3 =  0
i=10  %  3 =  1
```

### �ο�����

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        while (in.hasNext()) {
            int n = in.nextInt();
            int k = in.nextInt();
            if (k == 0)
                System.out.println(1L * n * n);
            else {
                long ans = 0L;
                for (int i = k + 1; i <= n; i++) {
                    ans += (n / i) * (i - k);
                    if (n % i >= k)
                        ans += n % i - k + 1;
                }
                System.out.println(ans);
            }
        }
    }
}
```

## ������

### ��Ŀ����
>Ϊ���ҵ��Լ�����Ĺ�����ţţ�ռ���ÿ�ֹ������ѶȺͱ��ꡣţţѡ�����ı�׼�����ѶȲ�������������ֵ������£�ţţѡ�񱨳���ߵĹ�������ţţѡ�����Լ��Ĺ�����ţţ��С���������ţţ��æѡ������ţţ��Ȼʹ���Լ��ı�׼������С����ǡ�ţţ��С���̫���ˣ�������ֻ�ð�������񽻸����㡣

**��������:**
>ÿ���������һ������������
ÿ�����������ĵ�һ�а����������������ֱ��ʾ����������N(N<=100000)��С��������M(M<=100000)��
��������N��ÿ�а����������������ֱ��ʾ��������Ѷ�Di(Di<=1000000000)�ͱ���Pi(Pi<=1000000000)��
��������һ�а���M�����������ֱ��ʾM��С��������ֵAi(Ai<=1000000000)��
��֤������������ı�����ͬ��

**�������:**
>����ÿ��С��飬�ڵ�����һ�����һ����������ʾ���ܵõ�����߱��ꡣһ���������Ա������ѡ��

**��������1:**
```
3 3
1 100
10 1000
1000000000 1001
9 10 1000000000
```

**�������1:**
```
100
1000
1001
```

### ����˼·
- ά��һ����N+M����dp[N+M]�����飬��¼��ͬ�����Ͳ�ͬ�Ѷ��µ����н��
- ���Ӷ� MAX��O(NlogN),O(MlogM),O(N+M))

![](https://github.com/LyricYang/Internet-Recruiting-Algorithm-Problems/tree/master/NETEASE/pic/Q3_2018.png)

### �ο�����

```java
import java.util.Arrays;
import java.util.Comparator;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        while (in.hasNext()) {
            int N = in.nextInt();
            int M = in.nextInt();
            int[][] mission = new int[N + 1][2];
            int[][] person = new int[M + 1][2];
            for (int i = 1; i <= N; i++) {
                mission[i][0] = in.nextInt();
                mission[i][1] = in.nextInt();
            }
            for (int i = 1; i <= M; i++) {
                person[i][0] = in.nextInt();
                person[i][1] = i;
            }

            Arrays.sort(mission, new Comparator<Object>() {
                @Override
                public int compare(Object o1, Object o2) {
                    int[] one = (int[]) o1;
                    int[] two = (int[]) o2;
                    if (one[0] > two[0])
                        return 1;
                    else if (one[0] < two[0])
                        return -1;
                    else
                        return 0;
                }
            });
            Arrays.sort(person, new Comparator<Object>() {
                @Override
                public int compare(Object o1, Object o2) {
                    int[] one = (int[]) o1;
                    int[] two = (int[]) o2;
                    if (one[0] > two[0])
                        return 1;
                    else if (one[0] < two[0])
                        return -1;
                    else
                        return 0;
                }
            });

            int[] DP = new int[N + M + 1];
            int[] location = new int[M + 1];
            int index = 1;
            int left = 1;
            int right = 1;
            while (left <= N && right <= M) {
                if (mission[left][0] < person[right][0]) {
                    DP[index++] = mission[left++][1];
                } else if (mission[left][0] == person[right][0]) {
                    DP[index] = mission[left++][1];
                    location[person[right][1]] = index;
                    right++;
                    index++;
                } else {
                    location[person[right][1]] = index;
                    index++;
                    right++;
                }
            }
            while (right <= M) {
                location[person[right][1]] = index;
                index++;
                right++;
            }
            for (int i = 1; i <= N + M; i++) {
                DP[i] = Math.max(DP[i - 1], DP[i]);
            }
            for (int i = 1; i <= M; i++) {
                System.out.println(DP[location[i]]);
            }
        }
    }
}
```

## ������

### ��Ŀ����
>СQ�õ�һ�����������: 1, 12, 123,...12345678910,1234567891011...��
����СQ�����ܷ�3����������ʺܸ���Ȥ��
СQ����ϣ�����ܰ�������һ�´����еĵ�l������r��(�����˵�)�ж��ٸ������Ա�3������

**��������:**
>���������������l��r(1 <= l <= r <= 1e9), ��ʾҪ�����������ˡ�

**�������:**
>���һ������, ��ʾ�������ܱ�3���������ָ�����

**��������1:**
```
2 5
```

**�������1:**
```
3
```

**����˵��1:**
```
12, 123, 1234, 12345...
����12, 123, 12345�ܱ�3����
```

### ����˼·
- ÿ�����ּ������ܱ�3����
- ����ѭ��������Ϊ2��0��������

### �ο�����

```java
import java.util.*;
public class Main{
    public static void main(String[] args){
        Scanner in = new Scanner(System.in);
        while(in.hasNext()){
            int left = in.nextInt();
            int right = in.nextInt();
            int result = 0;
            for(int i=left;i<=right;i++){
                if(i%3==0||i%3==2){
                    result++;
                }
            }
            System.out.println(result);
        }
    }
}
```

## ������

### ��Ŀ����
>СQ���ڸ�һ������Ϊn�ĵ�·���·�ư��÷�����
Ϊ�����������,СQ�ѵ�·��Ϊn������,��Ҫ�����ĵط���'.'��ʾ, ����Ҫ�������ϰ��������'X'��ʾ��
СQ����Ҫ�ڵ�·������һЩ·��, ���ڰ�����posλ�õ�·��, ��յ·�ƿ�������pos - 1, pos, pos + 1������λ�á�
СQϣ���ܰ��þ����ٵ�·����������'.'����, ϣ�����ܰ�������һ��������Ҫ����յ·�ơ�

**��������:**
>����ĵ�һ�а���һ��������t(1 <= t <= 1000), ��ʾ����������
������ÿ����һ����������, ��һ��һ��������n(1 <= n <= 1000),��ʾ��·�ĳ��ȡ�
�ڶ���һ���ַ���s��ʾ��·�Ĺ���,ֻ����'.'��'X'��

**�������:**
>����ÿ����������, ���һ����������ʾ������Ҫ����յ·�ơ�

**��������1:**
```
2
3
.X.
11
...XX....XX
```

**�������1:**
```
1
3
```

### ����˼·
- ��Ϊ·��ֻ����������λ�ã����Խ���·����ֳ�����һ��������ۣ�����8�����
- ��������������������һ��λ����'.'����·������1���������������һ��λ����'X'�����±�������һλ���½��з��鿼��

```
...  ..X  .X.  .XX
XXX  XX.  X.X  X..
```

### �ο�����

```java
import java.util.*;
public class Main{
    public static void main(String[] args){
        Scanner in = new Scanner(System.in);
        while(in.hasNextLine()){
            int t = Integer.parseInt(in.nextLine());
            for(int i=0;i<t;i++){
                int n = Integer.parseInt(in.nextLine());
                String s = in.nextLine();
                int res = 0;
                int index=0;
                while(index<s.length()){
                    if(index+2>=s.length()){
                        break;
                    }
                    if(s.charAt(index)=='X')
                        index++;
                    else{
                        index+=3;
                        res++;
                    }
                }
                if(index+1<=s.length())
                    if(s.charAt(index)=='.')
                        res++;
                    else if(index+2==s.length()){
                        if(s.charAt(index+1)=='.')
                            res++;
                    }
                System.out.println(res);
            }
        }
    }
}
```

## ������

### ��Ŀ����
>ţţȥ�Ġ���ʦ�Ҳ��Σ����ŵ�ʱ�����򱱷���������������·�ˡ���Ȼ��������һ�ŵ�ͼ����������Ҫ֪���Լ������ĸ���������������

**��������:**
>ÿ���������һ������������
ÿ�����������ĵ�һ�а���һ������������ʾת����Ĵ���N(N<=1000)��
��������һ�а���һ������ΪN���ַ�������L��R��ɣ�L��ʾ����ת��R��ʾ����ת��

**�������:**
>���ţţ�������ķ���N��ʾ����S��ʾ�ϣ�E��ʾ����W��ʾ����

**��������1:**
```
3
LRR
```

**�������1:**
```
E
```

### ����˼·

- ��������ͬ��������ת��ת������Ĳ�ͬ���򣬼�ģ�����߹��̡�

### �ο�����
```java
import java.util.*;

public class Main{
    public static void main(String[] args){
        Scanner in = new Scanner(System.in);
        while(in.hasNextLine()){
            int N = Integer.parseInt(in.nextLine());
            String s = in.nextLine();
            String res = "N";
            for(int i=0;i<s.length();i++){
                if(res.equals("N")){
                    if(s.charAt(i)=='L')
                        res="W";
                    else
                        res="E";
                }
                else if(res.equals("S")){
                    if(s.charAt(i)=='L')
                        res="E";
                    else
                        res="W";
                }
                else if(res.equals("E")){
                    if(s.charAt(i)=='L')
                        res="N";
                    else
                        res="S";
                }
                else if(res.equals("W")){
                    if(s.charAt(i)=='L')
                        res="S";
                    else
                        res="N";
                }
            }
            System.out.println(res);
        }
    }
}
```

## ������

### ��Ŀ����
>ţţ����˯��ͷ�����������˺ܶ����ӣ�ֻ�����������ʱ�����Ż��ѹ������Ҿ������𴲡���������������ҪX���ӵ�����ң��Ͽ�ʱ��Ϊ�����AʱB�֣��������������ʲôʱ���𴲡�

**��������:**
>ÿ���������һ������������
ÿ�����������ĵ�һ�а���һ������������ʾ���ӵ�����N(N<=100)��
��������N��ÿ�а���������������ʾ������������ʱ��ΪHi(0<=Hi<24)ʱMi(0<=Mi<60)�֡�
��������һ�а���һ����������ʾ������������ҪX(0<=X<=100)���ӵ�����ҡ�
��������һ�а���������������ʾ�Ͽ�ʱ��ΪA(0<=A<24)ʱB(0<=B<60)�֡�
���ݱ�֤������һ�����ӿ�����ţţ��ʱ������ҡ�

**�������:**
>�������������ʾţţ������ʱ�䡣

**��������1:**
```
3 
5 0 
6 0 
7 0 
59 
6 59
```

**�������1:**
```
6 0
```

### ����˼·

- ��ʱ�ָ�ʽ��ʱ��ת��Ϊ���ӱ�ʾ��ʱ�䣬�ҵ�����С����ʱ�䣨�Ͽ�ʱ��-·��ʱ�䣩������ʱ��

### �ο�����

```java
import java.util.*;
public class Main{
    public static void main(String[] args){
        Scanner in = new Scanner(System.in);
        while(in.hasNext()){
            int N = in.nextInt();
            int[] alarm=new int[N];
            for(int i=0;i<N;i++){
                alarm[i]=in.nextInt()*60+in.nextInt();
            }
            int X = in.nextInt();
            int school = in.nextInt()*60+in.nextInt();
            int wakeup = school-X;
            Arrays.sort(alarm);
            int index=Arrays.binarySearch(alarm,wakeup);
            int res=0;
            if(index<0){
                res=-index-2;
            }
            else{
                res = index;
            }
            System.out.println(alarm[res]/60+" "+alarm[res]%60);
        }
    }
}
```

## �ڰ���

### ��Ŀ����
>ţţ׼���μ�ѧУ��֯�Ĵ���, ����ǰţţ׼����������װ��һЩ��ʳ, ţţ�ı�������Ϊw��
ţţ����һ����n����ʳ, ��i����ʳ���Ϊv[i]��
ţţ��֪������������������������������,��һ���ж�������ʳ�ŷ�(�����Ϊ0Ҳ��һ�ַŷ�)��


**��������:**
>�����������
��һ��Ϊ����������n��w(1 <= n <= 30, 1 <= w <= 2 * 10^9),��ʾ��ʳ�������ͱ�����������
�ڶ���n��������v[i](0 <= v[i] <= 10^9),��ʾÿ����ʳ�������

**�������:**
>���һ��������, ��ʾţţһ���ж�������ʳ�ŷ���

**��������1:**
```
3 10
1 2 4
```

**�������1:**
```
8
```

**����˵��1:**
>������ʳ�����С��10,����ÿ����ʳ�з���Ͳ��������������һ����2*2*2 = 8�������

### �ο�����

```java
import java.util.*;
public class Main{
    public static void main(String[] args){
        Scanner in = new Scanner(System.in);
        while(in.hasNext()){
            int n = in.nextInt();
            int w = in.nextInt();
            int[] v = new int[n];
            for(int i=0;i<n;i++){
                v[i]=in.nextInt();
            }
            Arrays.sort(v);
            int[][] dp = new int[v.length][w+1];
            for(int j=0;j<=w;j++){
                if(j>=v[0])
                    dp[0][j]=2;
                else
                    dp[0][j]=1;
            }
            for(int i=1;i<v.length;i++){
                for(int j=0;j<=w;j++){
                    if(j-v[i]>=0)
                        dp[i][j]=dp[i-1][j]+dp[i-1][j-v[i]];
                    else
                        dp[i][j]=dp[i-1][j];
                }
            }
            System.out.println(dp[v.length-1][w]);
        }
    }
}
```
- Exception in thread "main" java.lang.OutOfMemoryError: Java heap space

```java
import java.util.*;
public class Main{
    public static void main(String[] args){
        Scanner in = new Scanner(System.in);
        while(in.hasNext()){
            int n = in.nextInt();
            int w = in.nextInt();
            int[] v = new int[n];
            for(int i=0;i<n;i++){
                v[i]=in.nextInt();
            }
            long res = putSolution(v,w,n-1);
            System.out.println(res);
        }
    }
    public static long putSolution(int[] v,int w,int n){
        if(w<0)
            return 0;
        if(n==0&&w>=v[0])
            return 2;
        if(n==0&&w<v[0])
            return 1;
        return putSolution(v,w,n-1)+putSolution(v,w-v[n],n-1);
    }
}
```
- ���г�ʱ:���ĳ���δ���ڹ涨ʱ�������н����������Ƿ�ѭ���д���㷨���Ӷȹ���
caseͨ����Ϊ80.00%
