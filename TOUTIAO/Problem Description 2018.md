<!-- TOC -->
* [��һ��](#��һ��)
* [�ڶ���](#�ڶ���)
* [������](#������)
* [������](#������)
* [������](#������)
<!-- TOC -->

## ��һ��

### ��Ŀ������
>��n��Ԫ�ص������У��ҵ���ֵΪk�����ֶ�ȥ�غ�ĸ�����

**��������:**
>��һ�У�n��k��n��ʾ���ָ�����k��ʾ��ֵ 
�ڶ��У�n��������

**���������**
>��ֵΪk�����ֶ�ȥ�غ�ĸ���

**����:**
```
in:
5 2
1 5 3 4 2
out:
3
```

### ����˼·
- ��ָOffer66��֮ÿ��6�� - �������е����⣺��ΪS�����������е�ͷβָ�뷨���������Ϊ��ΪK���������֡���ʵ��һ���ģ�����һ����ʱ�临�ӶȾ�ΪO(2n)�����������ʱ�临�ӶȻ���O(nlogn)

### �ο�����
```java
import java.util.Scanner;
import java.util.Set;
import java.util.TreeSet;

public class Main {
    public static void main(String[] args) {
        // TODO Auto-generated method stub
        Scanner in = new Scanner(System.in);
        while (in.hasNext()) {
            int n = in.nextInt();
            int k = in.nextInt();
            Set<Integer> s = new TreeSet<Integer>();
            for (int i = 0; i < n; i++) {
                s.add(in.nextInt());
            }
            Integer[] arr = new Integer[s.size()];
            Integer[] arrtemp = s.toArray(arr);
            int ans = 0;
            for (int head = 0, tail = 1; tail < arr.length; head++) {
                while (tail < arr.length && arr[tail] - arr[head] < Math.abs(k))
                    tail++;
                if (tail >= arr.length)
                    break;
                if (arr[tail] - arr[head] == Math.abs(k))
                    ans += 1;
            }
            System.out.println(ans);
        }
    }
}
```


## �ڶ���

### ��Ŀ������
>���������ַ���������s��m���ٶ������ֲ����� 
��һ�ֲ�����
```
m = s;
s = s + s;
```
�ڶ��ֲ�����
```
s = s + m;
```
����s, m��ʼ�����£�
```
s = "a";
m = s;
```
����С�Ĳ��������������Խ�sƴ�ӵ����ȵ���n

**��������:**
>һ������n������������Ҫ�õ�s�ַ����ȣ�0<n<10000

**���������**
>һ�������������ܹ���������

**����:**
```
in:
6
out:
3
```

### ����˼·
- ����x������������x-1;
- ����x�Ĳ������������������Ĳ�������+������ϳɺ����Ĳ�����

### �ο�����
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        while (in.hasNext()) {
            int n = in.nextInt();
            int[] dp = new int[n + 1];
            for (int i = 2; i <= n; i++) {
                dp[i] = i - 1;//�����Ĳ�������
                //Ѱ���������
                for (int j = i / 2; j >= 1; j--) {
                    if (i % j == 0) {
                        //ͨ����������Ϲ���Ҳ��һ�������ĺϳɹ���
                        dp[i] = Math.min(dp[i], dp[j] + i / j - 1);
                    }
                }
            }
            System.out.println(dp[n]);
        }
    }
}
```

## ������

### ��Ŀ������
>����ͷ��6�����������Ҫ��ʼ��������췽�����æ����һ��С�ʵ�����ĳ�����Ҫ��ȡһ�����ʽ����������ַ�6ƴ���ļ���������������ʹ������Ӣ�ľ��"."�����������0123456789��
```
66666......6..66666..66666..6...6..66666..66666..66666..66666..66666
6...6......6......6......6..6...6..6......6..........6..6...6..6...6
6...6......6..66666..66666..66666..66666..66666......6..66666..66666
6...6......6..6..........6......6......6..6...6......6..6...6......6
66666......6..66666..66666......6..66666..66666......6..66666..66666
```

**����������**
>��һ��Ϊһ������n 
������n�У�ÿһ��Ϊһ�����ʽ 
����30%�����ݣ����ʽ������`6`, `+`, `-`�����ַ� 
����100%�����ݣ����ʽ������`6`, `+`, `-`, `*`�����ַ���1��n��1001��n��100�����ʽ���Ȳ�����100������`+`, `-`, `*`��Ϊ��Ԫ������������м�����$[-2^{63},2^{63}-1]$֮�ڣ����ս����$[0,2^{63}?1]$֮��

**���������**
>����ÿ������������ַ�`6`ƴ���ļ�������

**����:**
```
in:
2
6+6
6*6
out:
....6..66666
....6......6
....6..66666
....6..6....
....6..66666
66666..66666
....6..6....
66666..66666
....6..6...6
66666..66666
```

### �ο�����

```java
import java.util.Scanner;

public class Main {
    private static String G[][] = {
            { "66666", "....6", "66666", "66666", "6...6", "66666", "66666",
                    "66666", "66666", "66666" },
            { "6...6", "....6", "....6", "....6", "6...6", "6....", "6....",
                    "....6", "6...6", "6...6" },
            { "6...6", "....6", "66666", "66666", "66666", "66666", "66666",
                    "....6", "66666", "66666" },
            { "6...6", "....6", "6....", "....6", "....6", "....6", "6...6",
                    "....6", "6...6", "....6" },
            { "66666", "....6", "66666", "66666", "....6", "66666", "66666",
                    "....6", "66666", "66666" } };

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        while (in.hasNextLine()) {
            int n = Integer.parseInt(in.nextLine());
            for (int i = 0; i < n; i++) {
                String s = in.nextLine();
                long ans = cal(s);
                String ansString = "" + ans;
                int[] digit = new int[ansString.length()];
                for (int k = 0; k < ansString.length(); k++) {
                    digit[k] = ansString.charAt(k) - '0';
                }
                for (int j = 0; j < 5; j++) {
                    String temp = G[j][digit[0]];
                    for (int k = 1; k < digit.length; k++) {
                        temp = temp + ".." + G[j][digit[k]];
                    }
                    System.out.println(temp);
                }

            }
        }
    }

    private static long cal(String s) {
        int n = s.length();
        long sum = 0, cur = 0, prd = 1;
        for (int i = 0; i < n; i++) {
            if (s.charAt(i) <= '9' && s.charAt(i) >= '0')
                cur = cur * 10 + s.charAt(i) - '0';
            else if (s.charAt(i) == '-') {
                sum += prd * cur;
                cur = 0;
                prd = -1;
            } else if (s.charAt(i) == '+') {
                sum += prd * cur;
                cur = 0;
                prd = 1;
            } else {
                prd *= cur;
                cur = 0;
            }
        }
        return sum + prd * cur;
    }
}
```

## ������

### ��Ŀ������
>��һ������`n`������Ԫ�صļ���`a`��һ������`m`������Ԫ�صļ���`b`������magic����Ϊ����һ��������ȡ��һ��Ԫ�أ��ŵ���һ��������в�������ÿ�����ϵ�ƽ��ֵ�����ڲ���ǰ��
ע��һ�����㣺
- �����԰�һ�����ϵ�Ԫ��ȡ�գ�������û��ƽ��ֵ��
- ֵΪx��Ԫ�شӼ���bȡ�����뼯��a��������a���Ѿ���ֵΪx��Ԫ�أ���a��ƽ��ֵ����(��Ϊ����Ԫ�ز����ظ�)��b��ƽ��ֵ���ܻ�ı�(��Ϊx��ȡ����)
�������Խ��ж��ٴ�magic������


**����������**
>��һ��Ϊ��������n��m 
�ڶ���n����������ʾ����a�е�Ԫ�� 
������m����������ʾ����b�е�Ԫ�� 
����100%�����ݣ�`1<n,m<100000` `0<a[i],b[i]<100000000`������a��Ԫ�ػ�����ͬ������b�е�Ԫ�ػ�����ͬ��

**���������**
>���һ����������ʾ�����Խ��еĲ���������

**����:**
```
in:
3 5
1 2 5
2 3 4 5 6
out:
2
```

### �ο�����

```java
import java.util.Arrays;
import java.util.Scanner;
import java.util.Set;
import java.util.TreeSet;

public class Main {
    public static void main(String[] args) {
        Scanner scan=new Scanner(System.in);
        int n,m;
        int cnt;
        n=scan.nextInt();
        m=scan.nextInt();
        double []a=new double[n];
        double []b=new double[m];
        for(int i=0;i<n;++i) {
            a[i]=scan.nextDouble();
        }
        for(int i=0;i<m;++i) {
            b[i]=scan.nextInt();
        }
        Arrays.sort(a);
        Arrays.sort(b);
        double va=avd(a);
        double vb=avd(b);
        if(vb>va) {
            cnt=Maicg(a,b,va,vb);
        }
        else {
            cnt=Maicg(b,a,vb,va);
        }
        System.out.println(cnt);
    }
    static double avd(double []a) {
        double sum=0;
        for(int i=0;i<a.length;++i) {
            sum+=a[i];
        }
        return sum/a.length;
    }
    static int Maicg(double[]a,double[]b,double va,double vb) {
        int cnt=0;
        Set se=new TreeSet();
        for(int i=0;i<a.length;++i) {
            se.add(a[i]);
        }
        int n,m;
        n=a.length;
        m=b.length;
        for(int i=0;i<b.length-1&&b[i]<vb;i++) {
            if(b[i]>va) {
                int j=se.size();
                se.add(b[i]);
                if(j!=se.size()) {
                    va=(va*n+b[i])/(n+1);
                    vb=(vb*m-b[i])/(m-1);
                    cnt++;
                }
            }
        }
        return cnt;
    }
}
```

## ������

### ��Ŀ����
>СT���������һ������С��Ϸ����֪�ڿ�����N���߶Ȼ�����ͬ�����壬СT�տ�ʼ�ڸ߶�Ϊ0�ĵط���ÿ����Ծ����ѡ�����Լ���ǰ�߶Ⱦ���ֵ��С�ڵ���H�����壬��Ծ���󵽴�������Ϊ��ľ���λ�ã���СT�������K�ε���������������ߣ�������ʱ�̣��߶Ȳ���Ϊ����

**����������**
>��һ����������N, K, H
����N�У�ÿ��һ������Ti����ʾ��i���������ظ߶�

**���������**
>һ����������ʾ����������ĸ߶�

**������**
```
���룺
3 3 2
1
3
6
�����
8
```

### �ο�����
```java
import java.util.Scanner;
import java.util.Stack;

public class Main {
    private static int max = 0;

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        while (in.hasNext()) {
            int N = in.nextInt();
            int K = in.nextInt();
            int H = in.nextInt();
            int[] block = new int[N];
            for (int i = 0; i < N; i++) {
                block[i] = in.nextInt();
            }

            HighestLevel(block, 0, K, H, new Stack<Integer>());
            System.out.println(max);
        }
    }

    private static void HighestLevel(int[] block, int cur, int k, int h,
            Stack<Integer> s) {
        // TODO Auto-generated method stub
        if (cur > max)
            max = cur;
        for (int i = 0; i < block.length; i++) {
            if (block[i] - cur > 0 && block[i] - cur <= h) {
                s.push(block[i]);
                cur = cur + (block[i] - cur) * 2;
                HighestLevel(block, cur, k - 1, h, s);
                cur = cur - (cur - block[i]) * 2;
                s.pop();
            }
        }
        return;
    }
}
```
