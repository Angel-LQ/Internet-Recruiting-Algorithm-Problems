<!-- TOC -->
* [��һ��](#��һ��)
* [�ڶ���](#�ڶ���)
* [������](#������)
<!-- TOC -->


## ��һ��

### ��Ŀ����
>����һ���������������A�Լ���������`x`��`k`��Ҫ���������A����x֮��ľ���ֵ��С��k��Ԫ�ء���������x��ֵ�ľ���ֵ��ȵ�����Ԫ�أ���ȡ���н�С��Ԫ�ء�

**����������**
>����ĵ�һ��Ϊ�ո�ָ����������飬�ڶ���Ϊ�ո�ָ�����������x��k��
���鳤�Ȳ�����1000������Ԫ�ؾ���ֵ�Ͳ�����1000��k����0�Ҳ��������鳤�ȡ�

**���������**
>ÿ���������ݶ�Ӧһ��������������Ԫ�ؼ��Կո�ָ���

**������**
```
����
1 2 3 4 5 
3 4
���
1 2 3 4
```

### ����˼·
- ��������������飬�������ֵ����������������ֵ�㲻��������
- ά��һ��k��Ԫ�صĶ���

![](index_files/f8afa61c-d484-48d2-9878-1c21d55d0086.png)

```java
import java.util.LinkedList;
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        while (in.hasNextLine()) {
            String s = in.nextLine();
            String[] sArr = s.split(" ");
            int[] arr = new int[sArr.length];
            for (int i = 0; i < sArr.length; i++) {
                arr[i] = Integer.valueOf(sArr[i]);
            }
            String s2 = in.nextLine();
            String[] s2Arr = s2.split(" ");
            int x = Integer.valueOf(s2Arr[0]);
            int k = Integer.valueOf(s2Arr[1]);
            LinkedList<Integer> list = new LinkedList<Integer>();
            for (int i = 0; i < arr.length; i++) {
                if (list.size() < k) {
                    list.add(arr[i]);
                } else {
                    int maxD = Math.abs(list.getFirst() - x);
                    if (Math.abs(arr[i] - x) < maxD) {
                        list.pollFirst();
                        list.add(arr[i]);
                    } else
                        break;
                }
            }
            System.out.print(list.get(0));
            for (int i = 1; i < k; i++) {
                System.out.print(" " + list.get(i));
            }
        }
    }
}
```


## �ڶ��� ��������HR

### ��Ŀ����
>���տ�����У԰��Ƹ��Ҫ��HRС�к�С����Ҫ�����������У��ֱ�ΪA��B��C���������Թ�ȥ����ͬ���С�
����HR�������¹涨��������һ����ѡ�����Թ٣�ÿ������ѡ��һλ������ѡ��ÿ���ʣ�����Թ���������ѡ�������Թٵ�HR��Ҫ�Լ����
����HRС�к�С�̶����������ÿ��ѡ�񶼲�ȡ���Ų��ԣ������С����ѡ��дһ���������ж����Ƿ���Ҫ����������Ҫ����������һ�������Ų��ԡ�

**����������**
>����Ϊ�������������ֱ�����������ҵ����Թ���������Ӣ�Ķ��ŷָ�

**���������**
>��С����Ҫ����������1��
��С�в���Ҫ������������һ��ѡ��Ŀ������ƺ�ѡ����������Ӣ�Ķ��ŷָ�

**������**
```
����
1,8,9
���
1

����
2,0,4
���
C,2
```

### ����˼·
Nim��Ϸ�İ棬����Ϊ0�������ֱذܣ�����A^B^C=0ʱ�����1��Ȼ��Ӯ���������Ϊֻ���������ͺܼ��ˣ�ö�����������ͣ�ֻ�е�������ֵ����������ֵ�������������ֵ��ȥ���������������ֵ���Ǵ���

### �ο�����

```java
import java.util.*;
public class Main{
    public static void main(String[] args){
        Scanner in = new Scanner(System.in);
        while(in.hasNextLine()){
            String[] s = in.nextLine().split(",");
            int A = Integer.parseInt(s[0]);
            int B = Integer.parseInt(s[1]);
            int C = Integer.parseInt(s[2]);
            int temp1 = A^B;
            int temp2 = A^C;
            int temp3 = B^C;
            int res=0;
            if((temp1^C)==0){
                System.out.println(1);
            }else{
                if(C>temp1){
                    res = C-temp1;
                    System.out.println("C,"+res);
                }
                if(B>temp2){
                    res = B-temp2;
                    System.out.println("B,"+res);
                }
                if(A>temp3){
                    res = A-temp3;
                    System.out.println("A,"+res);
                }
            }
        }
    }
}
```


## ������ �������ż��Ϸ

### ��Ŀ����
>ĳ��˾����ϣ���֯��Ա������һ��С��Ϸ���������ա���Ϸ�������£�
N���˲�����Ϸ��վ��һ������������������M��С��ż��Ϊ��������Ϸ��Ȥζ���Ѷȣ�����涨��������Ϸ�������������ﲻ�ܱ��������ߵ��˶����������ϣ�������ܵ�һ���ĳͷ�����Ϸ����ʱӵ����ż�����˽����һ�ݴ󽱡�
�����Ҷ���Ӯ����ݴ󽱣�����վ�ڵ�K��λ�õ�С����Ӯ����Ϸʱ�������ӵ�м�����ż��

**����������**
>����Ϊ�ÿո�ָ���3��������������Ϊ��������Ϸ����N����ż��M��С������λ��K

**���������**
>���Ϊ1��������������С������ܹ�ӵ�е���ż������û�У������0��

**������**
```
����
1 1 0
���
0

����
1 3 1
���
3
```

### ����˼·
Nim��Ϸ�İ棬����Ϊ0�������ֱذܣ�����A^B^C=0ʱ�����1��Ȼ��Ӯ���������Ϊֻ���������ͺܼ��ˣ�ö�����������ͣ�ֻ�е�������ֵ����������ֵ�������������ֵ��ȥ���������������ֵ���Ǵ���

### �ο�����

```java
import java.util.*;
public class Main{
    public static void main(String[] args){
        Scanner in = new Scanner(System.in);
        while(in.hasNext()){
            int N = in.nextInt();
            int M = in.nextInt();
            int k = in.nextInt();
            int[] loc = new int[N+1];
			//�ж�С��λ���Ƿ񳬹���������С��1���������ж�Ϊ�Ƿ�����
            if(k==0||k>N){
                System.out.println(0);
            }else{
                while(M>0){
                    if(M>0){
                        loc[k]++;
                        M--;
                    }
                    for(int i=k;i>1;i--){
                        if(loc[i]-loc[i-1]>1){
                            loc[i-1]++;
                            M--;
                        }
                    }
                    for(int j=k+1;j<=N;j++){
                        if(loc[j-1]-loc[j]>1){
                            loc[j]++;
                            M--;
                        }
                    }
                }
                if(M<0){
                    System.out.println(--loc[k]);
                }else{
                    System.out.println(loc[k]);
                }
            }
        }
    }
}
```