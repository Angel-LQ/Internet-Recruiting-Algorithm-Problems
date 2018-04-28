<!-- TOC -->
* [��һ��](#��һ��)
* [�ڶ���](#�ڶ���)
* [������](#������)
<!-- TOC -->


## ��һ��

### ��Ŀ����
>��һ���Ź�������飬����n����������������������������һ�����ȵ���λ�����磬ԭ����Ϊ`[1,2,3,4,5,6]`��������λ5��λ�ü������`[6,1,2,3,4,5]`,���ڶ�����λ������飬��Ҫ����ĳ��Ԫ�ص�λ�á������һ�����Ӷ�Ϊlog������㷨����������
����һ��int����A��Ϊ��λ������飬ͬʱ���������Сn����Ҫ���ҵ�Ԫ�ص�ֵx���뷵��x��λ��(λ�ô��㿪ʼ)����֤������Ԫ�ػ��졣

**��������:**
```
[6,1,2,3,4,5],6,6 
���أ�0
```

### ����˼·
- ԭ�������������龭�������ƶ��õ����������򣬶��Ҵ��м�Ԫ��Ϊ���İ������Ϊ�����֣���߻��ұ߱�Ȼ��һ��������ģ���˿��Կ���ʹ��һЩ�б�����������С���ҷ�Χ�����Ը�����һ�����εĴ����ƵĶ��ֲ����㷨��

### �ο�����

```java
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        while (in.hasNext()) {
            int n = in.nextInt();
            int x = in.nextInt();
            int[] source = new int[n];
            for (int i = 0; i < n; i++) {
                source[i] = in.nextInt();
            }
            int result = finder(source, n, x);
            System.out.println(result);
        }
    }
    public static int finder(int[] arr, int n, int x) {
        int left = 0;
        int right = n - 1;
        while (left <= right) {
            int mid = (left + right) / 2;
            if (arr[mid] == x)
                return mid;
            if (arr[mid] < x) {
                if (arr[left] > arr[mid] && x > arr[right])
                    right = mid - 1;
                else
                    left = mid + 1;
            } else {
                if (arr[mid] > arr[right] && x < arr[left])
                    left = mid + 1;
                else
                    right = mid - 1;
            }
        }
        return -1;
    }
}
```

## �ڶ���

### ��Ŀ����
>���ڴ�ͳ�ĺ�ŵ����Ϸ������һ����չ�������дӴ�С���õ�n��Բ�̣���ʼʱ����Բ�̶�������ߵ������ϣ����պ�ŵ����Ϸ��Ҫ������Ҫ�����е�Բ�̶��Ƶ��ұߵ������ϣ���ʵ��һ��������ӡ�����ƶ��켣��
����һ��int n����ʾ��n��Բ�̡��뷵��һ��string���飬���е�Ԫ������Ϊÿ���ƶ���������������ʽΪ�� move from [left/mid/right] to [left/mid/right]��

**��������:**
```
1
���أ�move from left to right
```

### ����˼·
- �Ȱ��������ӱ���0��1��2��
�������Ǵ�����x������y�ƶ�n���̣����ڴ�Ĳ��ܷ�С�����棬�����ƶ�������һ����ʱ��ǰ��n-1��һ����˳�����ڵ��������ӣ�����Ϊ3-x-y���ϣ������һ����x�Ƶ�y���ٰ�3-x-y�ϵ�ȫ�ƶ���y��

### �ο�����

```java
import java.util.*;
public class Hanoi {
    private String[] pos = {"left", "mid", "right"};
    public ArrayList<String> getSolution(int n) {
        return getSolution(n, 0, 2);
    }
    public ArrayList<String> getSolution(int n, int from, int to) {
        if(n==0) return new ArrayList<String>();
        ArrayList<String> list = getSolution(n-1, from, 3-from-to);
        list.add("move from "+pos[from]+" to "+pos[to]);
        list.addAll(getSolution(n-1, 3-from-to, to));
        return list;
    }
}
```

## ������

### ��Ŀ����
>�ɼ����ϻ��˼���������������һ�����ֵ�ʱ�򣬶�Ӧ���ַ��Ͳ�����֡����ڸ���Ӧ�������һ�����֡��Լ���������Щ��������Ľ�����ֻ���������

**�����ʽ��**
>������2���зֱ������������Щ�����Լ�Ӧ����������֡����ж�ӦӢ����ĸ�Ļ����Դ�д������ÿ�������ǲ�����105���ַ��Ĵ������õ��ַ�������ĸ[a-z, A-Z]������0-9���Լ��»��ߡ�_��������ո񣩡���,������.������-������+���������ϵ���������Ŀ��֤��2����������ִ��ǿա�
ע�⣺����ϵ��������ˣ���ô��д��Ӣ����ĸ�޷��������

**�����ʽ��**
>��һ��������ܹ�������Ľ�����֡����û��һ���ַ��ܱ��������������С�

**��������:**
```
����������
7+IE.
7_This_is_a_test.
���������
_hs_s_a_tst
```

### ����˼·
- �ò����͵���������¼���˵ļ��̣������±����ַ���ASCII�롣����Ҫ������ַ�������Ӧ�ļ���û�л��������

### �ο�����
```java
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String a = sc.nextLine();
        String b = sc.nextLine();
        boolean[] broken = new boolean[500]; // ������¼�����Ƿ���
        for (int i = 0; i < 500; i++) {
            broken[i] = false;
        }

        for (int i = 0; i < a.length(); i++) { // ���»��ļ��̵Ĳ���ֵ
            broken[a.charAt(i)] = true;
            if (a.charAt(i) >= 'A' && a.charAt(i) <= 'Z') {
                broken[a.charAt(i) + 32] = true;
            }
        }
        // �������
        for (int i = 0; i < b.length(); i++) {
            if (broken['+'] || broken['\''] || broken['-'] || broken['.']) {
                if (!broken[b.charAt(i)]
                        && (b.charAt(i) < 'A' || b.charAt(i) > 'Z')) {
                    System.out.print(b.charAt(i));
                }
            } else {
                if (!broken[b.charAt(i)]) {
                    System.out.print(b.charAt(i));
                }
            }
        }
        System.out.println();
    }
}
```