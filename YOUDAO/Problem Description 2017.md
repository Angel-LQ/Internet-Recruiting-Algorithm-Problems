<!-- TOC -->
* [��һ��](#��һ��-ϴ��)
* [�ڶ���](#�ڶ���-�������)
<!-- TOC -->

## ��һ�� ϴ��

### ��Ŀ����
>ϴ����������ʮ�ֳ�����������Ҫдһ������ģ��ϴ�ƵĹ��̡� ������Ҫϴ2n���ƣ����ϵ��������ǵ�1�ţ���2�ţ���3��һֱ����2n�š����ȣ����ǰ���2n���Ʒֳ����ѣ��������ŵ�1�ŵ���n�ţ��ϰ�ѣ����������ŵ�n+1�ŵ���2n�ţ��°�ѣ������žͿ�ʼϴ�ƵĹ��̣��ȷ������ֵ����һ���ƣ��ٷ������ֵ����һ���ƣ����ŷ������ֵĵ����ڶ����ƣ��ٷ������ֵĵ����ڶ����ƣ�ֱ�����������ֵĵ�һ���ơ����Ű��ƺϲ������Ϳ����ˡ� ������6���ƣ��ʼ�Ƶ�������1,2,3,4,5,6�����ȷֳ����飬��������1,2,3����������4,5,6����ϴ�ƹ����а�˳�������6,3,5,2,4,1�������������ٴκϳ�һ����֮�����ǰ��մ������µ�˳�������ƣ��ͱ��������1,4,2,5,3,6�� ���ڸ���һ��ԭʼ���飬������⸱��ϴ��k��֮��������µ����С�

**��������:**
>��һ��һ����T(T �� 100)����ʾ��������������ÿ�����ݣ���һ��������n,k(1 �� n,k �� 100)��������һ����2n����a1,a2,...,a2n(1 �� ai �� 1000000000)����ʾԭʼ������ϵ��µ����С���

**�������:**
>����ÿ�����ݣ����һ�У����յ����С�����֮���ÿո��������Ҫ����ĩ�������Ŀո�

**������**
```
����
3 3 1 1 2 3 4 5 6 3 2 1 2 3 4 5 6 2 2 1 1 1 1
���
1 4 2 5 3 6 1 5 4 3 2 6 1 1 1 1
```

### ����˼·
- �ڶ�ȡ����ʱ�͸���ϴ�ƴ����������ÿ���������յ�λ�á�

### �ο�����
```java
import java.util.*;
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int groups = sc.nextInt();
        while (groups-- > 0){
            int n = sc.nextInt();
            int k = sc.nextInt();
            int[] res = new int[2*n];
            for(int i=0;i<2*n;i++){
                int tmp = i ;
                for(int j = 0; j < k;j++){
                    if (tmp < n) tmp = 2*tmp;
                    else tmp = 2 * (tmp - n)+1;
                }
                res[tmp]=sc.nextInt();
            }
            if(res.length> 0) System.out.print(res[0]);
            for(int i = 1;i< 2*n;i++){
                System.out.print(" "+res[i]);
            }
            System.out.println();
        }
    }
}
```




## �ڶ��� �������

### ��Ŀ����
>С��ͬѧ��1��n��n�����ְ���һ����˳�������һ������Q�С��������Զ���Qִ�������³���
```
while(!Q.empty())              //���в��գ�ִ��ѭ��
{
    int x=Q.front();            //ȡ����ǰ��ͷ��ֵx
    Q.pop();                 //������ǰ��ͷ
    Q.push(x);               //��x�����β
    x = Q.front();              //ȡ����ʱ���ͷ��ֵ
    printf("%d\n",x);          //���x
    Q.pop();                 //������ʱ��Ķ�ͷ
}
```
��ȡ����ͷ��ֵ������ʱ�򣬲���������ǰ��ͷ��
С��ͬѧ���֣���γ���ǡ�ð�˳�������1,2,3,...,n������С�������㹹���ԭʼ�Ķ��У�����������

**��������:**
>��һ��һ������T��T �� 100����ʾ����������ÿ����������һ����n��1 �� n �� 100000�������������n֮�Ͳ�����200000��

**�������:**
>����ÿ�����ݣ����һ�У���ʾԭʼ�Ķ��С�����֮����һ���ո��������Ҫ����ĩ�������Ŀո�.

**������**
```
����
4
1
2
3
10
���
1
2 1
2 1 3
8 1 6 2 10 3 7 4 9 5
```

### ����˼·
- ����һ���ҹ��ɣ��Ӽ��������ҳ����ֺ���������λ�õĹ�ϵ
$$loc=2*i-1 \qquad loc \lt n$$

$$loc=2*(loc-n) \qquad loc \ge n$$

- ��������ԭʼ���в����������

### �ο�����
```java
import java.util.*;
public class Main{
    public static void main(String[] args){
        Scanner in = new Scanner(System.in);
        while(in.hasNext()){
            int T = in.nextInt();
            for(int i=0;i<T;i++){
                int n=in.nextInt();
                int[] res = new int[n];
                for(int j=1;j<=n;j++){
                    int tmp = 2*j-1;
                    while(tmp>=n){
                        tmp=2*(tmp-n);
                    }
                    res[tmp]=j;
                }
                System.out.print(res[0]);
                for(int k=1;k<n;k++){
                    System.out.print(" "+res[k]);
                }
                System.out.println();
            }
        }
    }
}
```

```java
import java.util.LinkedList;
import java.util.Scanner;
public class Main{
    public static LinkedList<Integer> func(int n){
        LinkedList<Integer> help=new LinkedList<Integer>();
        for(int i=n;i>=1;i--){
            help.addFirst(i);
            help.addFirst(help.removeLast());
        }
        return help;
    }
    public static void main(String[] args){
        int t;
        Scanner scan = new Scanner(System.in);
        t=scan.nextInt();
        int n;
        LinkedList<Integer> res;
        while(t-->0){
            n=scan.nextInt();
            res=func(n);
            for(int i=0;i<n-1;i++){
                System.out.print(res.removeFirst()+" ");
            }
            System.out.println(res.removeFirst());
        }
    }
}
```