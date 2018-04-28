<!-- TOC -->
* [��һ��](#��һ��)
* [�ڶ���](#�ڶ���)
* [������](#������)
<!-- TOC -->


## ��һ�� �ַ�������

### ��Ŀ����
>����һ��ԭʼ�ַ��������ݸ��ַ�����ÿ���ַ����ֵĴ���������ASCII�����˳�����µ��������
```java
����������ԭʼ�ַ���Ϊ��
eeefgghhh
��ÿ���ַ����ֵĴ����ֱ��ǣ�
(1).eee        3��
(2).f          1��
(3).gg         2��
(4).hhh        3��
�����������ַ������£�
efghegheh
��д����ʵ���������ܡ�
����ܰ��ʾ��
(1).ԭʼ�ַ����н����ܳ��֡����֡��͡���ĸ����
(2).��ע��������ĸ��Сд��
```

**��������:**
```java
eeefgghhh
```

**�������:**
```java
efghegheh
```

**������**

**����**
```java
eeefgghhh
```
**����**
```java
efghegheh
```

### �ο�����
```java
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        while (in.hasNext()) {
            String s = in.nextLine().trim();
            int[] ascArr = new int[128];
            int max = 0;
            for (int i = 0; i < s.length(); i++) {
                ascArr[s.charAt(i)]++;
                if (ascArr[s.charAt(i)] > max) {
                    max = ascArr[s.charAt(i)];
                }
            }
            for (int i = 0; i < max; i++) {
                for (int j = 0; j < 128; j++) {
                    if (ascArr[j] > 0) {
                        System.out.print((char) j);
                        ascArr[j]--;
                    }
                }
            }
            System.out.println();
        }
    }
}
```

## �ڶ��� ��Ծ����

### ��Ŀ����
>����һ������������ӵ�һ���������һ����������Ծ��ÿ��������Ծ1��ÿ������ֵ��ʾ������λ�ÿ�����Ծ����󳤶ȡ�������������ٵ���Ծ�����������һ������

**��������:**
```
��һ�б�ʾ�ж��ٸ���n
�ڶ��п�ʼ������1��n������һ����һ��
```

**�������:**
```
���һ�У���ʾ������Ծ�Ĵ�����
```

**������**
```
����
7
2
3
2
1
2
1
5
���
3
˵��
7��ʾ������Ҫ����7������������2��ʼ�����ֱ�����������Ծ����󲽳�����ʱ��2��������Ϊ2-2-2-5��2-3-2-5��Ϊ3��
```

### �ο�����
```java
import java.util.*;
public class  Main {
    public static  void main(String[]args){
        Scanner in=new Scanner(System.in);
        while(in.hasNext()){
           int n=in.nextInt();
           int[] arr=new int[n];
           for(int i=0;i<n;i++){
               arr[i]=in.nextInt();
           }
            int jump=0;
            int cur=0;
            int next=0;
            for(int i=0;i<arr.length;i++){
                if(cur<i){
                    jump++;
                    cur=next;
                }
                next=Math.max(next,i+arr[i]);
            }
           System.out.println(jump);
        }
    }
}
```

## ������ �������

### ��Ŀ����
>��д����������ˡ�����ʵ���������ⳤ�ȵĳ�����(����)��ˣ�������.

**��������:**
```
��һ����������A���ַ������ַ���Χ��0��9�����ڶ�����������B���ַ������ַ���Χ��0��9����
```

**�������:**
```
���A��B������˵Ľ�������Ϊ�ַ�������
```

**������**
```
����
1234
4321
���
5332114
˵��
��һ������*�ڶ�������
```

```java
import java.util.Scanner;

public class Main {

    /**
     * ������˻���˼�룬�����ַ�����ת��char���飬ת��int���顣���÷���˼�룬ÿһλ�����;<br>
     * ��ʽ��AB*CD = AC (BC+AD) BD , Ȼ��Ӻ�ǰ��ʮ��λ(BD,(BC+AD),AC)��
     * 
     * @param num1
     * @param num2
     */
    public static String multiply(String num1, String num2) {
        // ���ַ���ת����char����
        char chars1[] = num1.toCharArray();
        char chars2[] = num2.toCharArray();

        // ������Ž���������˻�������
        int result[] = new int[chars1.length + chars2.length];
        int n1[] = new int[chars1.length];
        int n2[] = new int[chars2.length];

        // ��charת����int���飬ΪʲôҪ��ȥһ��'0'�أ���ΪҪ��ȥ0��ascii��õ��ľ���ʵ�ʵ�����
        for (int i = 0; i < chars1.length; i++)
            n1[i] = chars1[i] - '0';
        for (int i = 0; i < chars2.length; i++)
            n2[i] = chars2[i] - '0';

        // �����ˣ���Ϊ��ᷢ�֡�AB*CD = AC(BC+AD)BD , Ȼ���λ��
        for (int i = 0; i < chars1.length; i++) {
            for (int j = 0; j < chars2.length; j++) {
                result[i + j] += n1[i] * n2[j];
            }
        }

        // ��10��λ���Ӻ���ǰ��ʮ��λ
        for (int i = result.length - 1; i > 0; i--) {
            result[i - 1] += result[i] / 10;
            result[i] = result[i] % 10;
        }

        // ת��string������
        String resultStr = "";
        for (int i = 0; i < result.length - 1; i++) {
            resultStr += "" + result[i];
        }
        return resultStr;
    }

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        while (in.hasNext()) {
            String str1 = in.next();
            String str2 = in.next();
            String res = multiply(str1, str2);
            System.out.println(res);
        }
    }
}
```


