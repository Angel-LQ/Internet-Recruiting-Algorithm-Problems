<!-- TOC -->
* [��һ�⣺�ϳ���](#��һ��-�ϳ���)
* [�ڶ��⣺��������](#�ڶ���-��������)
* [�����⣺�³���](#������-�³���)
* [�����⣺�����](#������-�����)
* [�����⣺��ƻ��](#������-��ƻ��)
* [�����⣺�Ǽʴ�Խ](#������-�Ǽʴ�Խ)
* [�����⣺�ر�ͼ](#������-�ر�ͼ)
* [�ڰ��⣺���л�ԭ](#�ڰ���-���л�ԭ)
* [�ھ��⣺�������](#�ھ���-�������)
* [��ʮ�⣺���˵Ĵ���](#��ʮ��-���˵Ĵ���)
* [��ʮһ�⣺��Ҫ��](#��ʮһ��-��Ҫ��)
* [��ʮ���⣺���С��](#��ʮ����-���С��)
* [��ʮ���⣺ͳ�ƻ���](#��ʮ����-ͳ�ƻ���)
* [��ʮ���⣺������С��](#��ʮ����-������С��)
* [��ʮ���⣺�������򷽷�](#��ʮ����-�������򷽷�)
* [��ʮ���⣺С��ϲ���ĵ���](#��ʮ����-С��ϲ���ĵ���)
* [��ʮ���⣺Fibonacci����](#��ʮ����-Fibonacci����)
* [��ʮ���⣺������Ϸ](#��ʮ����-������Ϸ)
<!-- TOC -->

## ��һ�� �ϳ���

### ��Ŀ����
>�� n ��ѧ��վ��һ�ţ�ÿ��ѧ����һ������ֵ��ţţ����� n ��ѧ���а���˳��ѡȡ k ��ѧ����Ҫ����������ѧ����λ�ñ�ŵĲ���� d��ʹ���� k ��ѧ��������ֵ�ĳ˻�������ܷ������ĳ˻���

**��������:**
>ÿ��������� 1 ������������ÿ���������ݵĵ�һ�а���һ������ n (1 <= n <= 50)����ʾѧ���ĸ�������������һ�У����� n ����������˳���ʾÿ��ѧ��������ֵ ai��-50 <= ai <= 50������������һ�а�������������k �� d (1 <= k <= 10, 1 <= d <= 50)��

**�������:**
>���һ�б�ʾ���ĳ˻���

**������**
```
����
3
7 4 7
2 50

���
49
```

### ����˼·
- ���ö�̬�滮����Maxval[i][j]��ʾ�Ե�i����Ϊ���һ���ˣ�һ��ѡȡ��j+1����ʱ�����˻���
ͬ��Minval[i][j]��ʾͬ��״̬�µ���С�˻������������д��ڸ�������������ĳ������ĸ��������������ļ���ֵ�������Ҫͬʱ��¼��Сֵ����
Maxval[i][j]����Ȼ��Maxval[i][j-1]��أ��������ΪMaxval[i][j]����������ɣ�һ������������Ϊ��ѡֵ����һ������Maxval[i][j-1]����һ���˺�õ���ֵ��Ȼ��ȡ���ǵļ���ֵ���ɴ˿��Եõ�״̬ת�Ʒ������£�

<div align="center"> <img src="https://github.com/LyricYang/Internet-Recruiting-Algorithm-Problems/blob/master/NETEASE/pic/Q1Y2017.jpg"/> </div><br>

### �ο�����

```java
import java.util.*;

public class Main{
    public static void main(String[] args){
        Scanner in = new Scanner(System.in);
        while(in.hasNext()){
            int n=in.nextInt();
            int[] power = new int[n];
            for(int i=0;i<n;i++){
                power[i]=in.nextInt();
            }
            int k=in.nextInt();
            int d=in.nextInt();
            System.out.println(MaxPower(power,k,d));
        }
    }
    static long max(long a, long b) {
        return a > b ? a : b;
    };

    static long min(long a, long b) {
        return a < b ? a : b;
    };

    private static long MaxPower(int[] array, int k, int d) {
        long dpMax[][] = new long[array.length][k + 1];
        long dpMin[][] = new long[array.length][k + 1];
        // dpMax[i][j] ��ʾ������Ԫ��A��i������βʱ�� ���г���Ϊj�����˻����
        for (int i = 0; i < array.length; i++) {
            dpMax[i][1] = array[i];
            dpMax[i][0] = array[0];
        }

        // ״̬ת�Ʒ����� dpMax[i][j] = max(dpMax[i-1][j-1]* A[i], dpMin[i-d][j-1] * A[i])

        long maxSoFar = Long.MIN_VALUE;
        for (int j = 2; j <= k; j++) {
            for (int i = j - 1; i < array.length; i++) {
                dpMax[i][j] = Long.MIN_VALUE;
                dpMin[i][j] = Long.MAX_VALUE;
                for (int x = 1; x <= d && (i - x) >= j - 2; x++) {
                    // �����ڶ���Ԫ���Լ�����֮ǰ��Ԫ���������ٻ�Ҫ��j-1���� �����±�i-x��Ҫ����j-2
                    long resMax = max(dpMax[i - x][j - 1] * array[i], dpMin[i - x][j - 1] * array[i]);
                    long resMin = min(dpMax[i - x][j - 1] * array[i], dpMin[i - x][j - 1] * array[i]);

                    if (resMax > dpMax[i][j])
                        dpMax[i][j] = resMax;
                    if (resMin < dpMin[i][j])
                        dpMin[i][j] = resMin;

                }
            }
        }

        for (int i = k-1; i < array.length; i++) {
            if (dpMax[i][k] > maxSoFar) {
                maxSoFar = dpMax[i][k];
            }
        }

        return maxSoFar;

    }

}
```

## �ڶ��� ��������

### ��Ŀ����
>����һ�� n �� m �еĵ��Σ����� '.' ��ʾ����ͨ�е�λ�ã�'X' ��ʾ����ͨ�е��ϰ���ţţ�� (x0 , y0 ) λ�ó���������������Σ���һ�����Ϸ����ͬ���ǣ���ÿһ��ֻ�ܰ���һЩָ���Ĳ����������Σ�Ҫ��ÿһ���������Գ������εı߽磬Ҳ���ܵ����ϰ��ϡ����εĳ��ڿ���������ĳ������ͨ�е�λ���ϡ�ţţ��֪�������£�����Ҫ���ٲ��ſ����뿪������Ρ�

**��������:**
>ÿ��������� 1 ������������ÿ�����������ĵ�һ�а����������� n �� m��1 <= n, m <= 50������ʾ���εĳ��Ϳ��������� n �У�ÿ�� m ���ַ����������Σ����ν����ٰ������� '.'����������һ�У������������� x0, y0����ʾţţ�ĳ���λ�ã�0 <= x0 < n, 0 <= y0 < m�����Ͻǵ�����Ϊ ��0, 0��������λ��һ���� '.'����֮���һ�а���һ������ k��0 < k <= 50����ʾţţ�Ϸ��Ĳ��������������� k �У�ÿ���������� dx, dy ��ʾÿ�ο�ѡ���ƶ����к��в�����-50 <= dx, dy <= 50��

**�������:**
>���һ��һ�����ֱ�ʾ��������Ҫ���ٴ��ƶ������뿪���Σ������Զ�޷��뿪����� -1�����²��������У�ţţ�������������ƶ��������п�ͨ�е�λ��.�ϣ����γ�����������������½ǣ�ţţ���뿪��Ҫ�ƶ��Ĵ�����࣬Ϊ3�Ρ�

**������**
```
����
3 3
...
...
...
0 1
4
1 0
0 1
-1 0
0 -1

���
3
```

### ����˼·
- ����������Ϊ����û�п���ͨ�еĵ㣬��ţţ�����ˣ����-1�������û�������ĵ㣬ţţ���ܻ�����ಽ���Ƕ��١�
BFS�㷨�������ͼ�ÿ�������̵��ﲽ�����ҵ������˵ĵ㣬���߲������ĵ㡣
 1. �ֱ���stepMap��stepLen�����ʾ���Σ��������ơ�������stepMap��-2��ʾ'X'��-1��ʾ'.'��
 2. ��stepMap�����õ�ǰλ��Ϊ0���ڲ����������ܵ���λ�ã���Ԫ��Ϊ-1��λ�ã�����ֵΪ��ǰ����+1
 3. ��λ���������������Ա��´�������
 4. ѭ��2��3����ֱ��û����һ�ֵ������㡣

### �ο�����

```java
import java.util.*;

public class Main{
    public static void main(String[] args){
        Scanner in = new Scanner(System.in);
        while(in.hasNextLine()){
            String line1 = in.nextLine();
            String[] line1Arr = line1.split(" ");
            int n = Integer.parseInt(line1Arr[0]);
            int m = Integer.parseInt(line1Arr[1]);
            int[][] stepMap = new int[n][m];
            for(int i=0;i<n;i++){
                String mapLine = in.nextLine();
                for(int j=0;j<mapLine.length();j++){
                    if(mapLine.charAt(j)=='.'){
                        stepMap[i][j]=-1;
                    }else{
                        stepMap[i][j]=-2;
                    }
                }
            }
            String start = in.nextLine();
            String[] startArr = start.split(" ");
            int x0 = Integer.parseInt(startArr[0]);
            int y0 = Integer.parseInt(startArr[1]);
            int k = Integer.parseInt(in.nextLine());
            int[][] stepLen = new int[k][2];
            for(int i=0;i<k;i++){
                String stepLine = in.nextLine();
                String[] stepLIneArr = stepLine.split(" ");
                stepLen[i][0]=Integer.parseInt(stepLIneArr[0]);
                stepLen[i][1]=Integer.parseInt(stepLIneArr[1]);
            }
            LinkedList<Integer> xQueue = new LinkedList<>();
            LinkedList<Integer> yQueue = new LinkedList<>();
            stepMap[x0][y0]=0;
            xQueue.add(x0);
            yQueue.add(y0);
            //BFS����
            while(xQueue.size()>0&&yQueue.size()>0){
                int curX = xQueue.poll();
                int curY = yQueue.poll();
                for(int i=0;i<k;i++){
                    int x = curX+stepLen[i][0];
                    int y = curY+stepLen[i][1];
                    if(x>=0 && x<n && y>=0 && y<m && stepMap[x][y] == -1){
                        stepMap[x][y] = stepMap[curX][curY]+1;
                        xQueue.add(x);
                        yQueue.add(y);
                    }
                }
            }
            int res=-1;
            boolean flag=false;
            for(int i=0;i<n;i++){
                for(int j=0;j<m;j++){
                    if(stepMap[i][j]==-1){
                        flag=true;
                        res=-1;
                        break;
                    }
                    else{
                        if(stepMap[i][j]>res){
                            res=stepMap[i][j];
                        }
                    }
                }
                if(flag){
                    break;
                }
            }
            System.out.println(res);
        }
    }
}
```


## ������ �³���

### ��Ŀ����
>ţţ�볢��һЩ�µ�����ÿ��������ҪһЩ��ͬ�Ĳ��ϣ���������е�������Ҫ׼�������ֲ�ͬ�Ĳ��ϡ�

**��������:**
>ÿ��������� 1 ������������ÿ�����������ĵ� i �У���ʾ��ɵ� i ��������Ҫ��Щ���ϣ����������ÿո����������ֻ������дӢ����ĸ�Ϳո������ļ������� 50 �У�ÿһ�в����� 50 ���ַ���

**�������:**
>���һ��һ�����ֱ�ʾ�������������Ҫ�����ֲ�ͬ�Ĳ��ϡ�

**������**
```
����
BUTTER FLOUR
HONEY FLOUR EGG

���
4
```

### ����˼·
- ����������������������Ҫ��while���ж������Ƿ����������set����¼����Ĳ������࣬�ﵽȥ��Ŀ�ģ����������������Ҫ��ʳ�����ࡣ

### �ο�����

```java
import java.util.*;
public class Main{
    public static void main(String[] args){
        Scanner in = new Scanner(System.in);
        Set<String> Material = new HashSet<>();//��¼ʳ�����࣬����ȥ��
        while(in.hasNext()){
            Material.add(in.next());
        }
        System.out.println(Material.size());
        Material.clear();
    }
}
```

## ������ �����

### ��Ŀ����
>ţţ�� 15 �������������������ص���Ϸ��ţţ��������������أ���������ؿ��Կ�����һ�����Σ�ÿ��λ����һ����ֵ���ָ���صķ����Ǻ��������������ֳ� 16 �ݣ���Ϊ�쵼�ɲ���ţţ���ǻ�ѡ�������ܼ�ֵ��С��һ����أ� ��Ϊţţ��õ����ѣ���ϣ��ţţȡ�õ���صļ�ֵ�;����ܴ���֪�����ֵ�������Ƕ�����

**��������:**
>ÿ��������� 1 ������������ÿ�����������ĵ�һ�а����������� n �� m��1 <= n, m <= 75������ʾ��صĴ�С���������� n �У�ÿ�а��� m �� 0-9 ֮������֣���ʾÿ��λ�õļ�ֵ��

**�������:**
>���һ�б�ʾţţ����ȡ�õ����ļ�ֵ��

**������**
```
����
4 4
3332
3233
3332
2323

���
2
```

### ����˼·

- �ٶ�����ֵΪmid������ö�����е�λ�ã�����ѭ������Ȼ�󿴺������ж��ٵ���ö�ٺ���ʱ�����ⲿ�ֵ�4�����Σ��µ�һ��������һ��֮�䱻���ŵı߽��Լ����������γɵ��ĸ����Σ��ļ�ֵ�����ڵ���mid��˵����һ���еú��������λ�ÿ�ʼ��������ö�ٺ��С�������պ��еĵ������ڵ���4����ô˵�����ֵmid�Ǻ���ģ����򲻺���ͨ�������Ĳ���ѹ�����䣬���ձ�Ȼ�ܹ��õ��𰸡�

### �ο�����
```java
import java.util.*;

public class Main{
    public static void main(String[] args){
        Scanner in = new Scanner(System.in);
        while(in.hasNextLine()){
            String line1 = in.nextLine();
            String[] line1Arr = line1.split(" ");
            int n = Integer.parseInt(line1Arr[0]);
            int m = Integer.parseInt(line1Arr[1]);
            int[][] map = new int[n+1][m+1];
            int[][] sum = new int[n+1][m+1];
            for(int i=1;i<=n;i++){
                String line = in.nextLine();
                for(int j=0;j<m;j++){
                    map[i][j+1] = line.charAt(j)-'0';
                }
            }
            
            for(int i=1;i<=n;i++){
                for(int j=1;j<=m;j++){
                    sum[i][j]=sum[i-1][j]+sum[i][j-1]-sum[i-1][j-1]+map[i][j];
                }
            }
            int l=0;
            int r=sum[n][m];
            int ans=0;
            while(l<=r){
                int mid = (l+r)>>1;
                if(judge(sum,mid,n,m)){
                    l=mid+1;
                    ans=mid;
                }
                else{
                    r=mid-1;
                }
            }
            System.out.println(ans);
        }
    }

    public static int calc(int[][] sum,int x,int y,int i,int j){
        return sum[x][y]-sum[x][j]-sum[i][y]+sum[i][j];
    }

    public static boolean judge(int[][] sum,int x,int n,int m){
        for(int i=1;i<=m-3;i++){
            for(int j=i+1;j<=m-2;j++){
                for(int k=j+1;k<=m-1;k++){
                    int last=0;
                    int cnt=0;
                    for(int r=1;r<=n;r++){
                        int s1=calc(sum,r,i,last,0);
                        int s2=calc(sum,r,j,last,i);
                        int s3=calc(sum,r,k,last,j);
                        int s4=calc(sum,r,m,last,k);
                        if(s1>=x&&s2>=x&&s3>=x&&s4>=x){
                            last=r;
                            cnt++;
                        }
                    }
                    if(cnt>=4){
                        return true;
                    }
                }
            }
        }
        return false;
    }
}
```

## ������ ��ƻ��

### ��Ŀ����
>n ֻ��ţ����һ�ţ�ÿ����ţӵ�� ai ��ƻ����������Ҫ������֮��ת��ƻ����ʹ�����������ţӵ�е�ƻ��������ͬ��ÿһ�Σ���ֻ�ܴ�һֻ��ţ��������ǡ������ƻ������һ����ţ�ϣ���������Ҫ�ƶ����ٴο���ƽ��ƻ�������������������� -1��

**��������:**
>ÿ���������һ������������ÿ�����������ĵ�һ�а���һ������ n��1 <= n <= 100������������һ�а��� n ������ ai��1 <= ai <= 100����

**�������:**
>���һ�б�ʾ������Ҫ�ƶ����ٴο���ƽ��ƻ���������������������� -1��

**������**
```
����
4
7 15 9 5

���
3
```

### ����˼·
- �����ж�ƻ���ܲ��ܱ�ţ���֣�������������-1��
- ���ܾ��֣������ֵ��������ÿͷţӵ�е�ƻ�������ֵ�Ƿ��2�ı����������������-1��
- �Ӵ��ھ�ֵ��ţ���ó�ƻ���Ĵ������С�ھ�ֵ��ţƻ���Ĵ�����ͬ������ھ�ֵ��ƻ����Ŀ����2��Ϊ�����Ĳ�����

### �ο�����

```java
import java.util.*;
public class Main{
    public static void main(String[] args){
        Scanner in = new Scanner(System.in);
        while(in.hasNext()){
            int n = in.nextInt();
            int[] appleMap = new int[n];
            int appleSum = 0;
            for(int i=0;i<n;i++){
                appleMap[i]=in.nextInt();
                appleSum+=appleMap[i];
            }
            int result=0;
            if(appleSum%n==0){
                int avg = appleSum/n;
                for(int i=0;i<n;i++){
                    int diff = appleMap[i]-avg;
                    if(diff%2==0){
                        if(diff>0)
                            result+=diff/2;
                    }else{
                        System.out.println(-1);
                        return;
                    }
                }
            }else{
                System.out.println(-1);
                return;
            }
            System.out.println(result);
        }
    }
}
```

## ������ �Ǽʴ�Խ

### ��Ŀ����
>�����������һ��Ӷ��־��ܵ��������������������Ҫ�����ڷ���ͽ���Ĺ��̣���ѧ�Ҹ���ʵ�����ݹ��ƣ�����ڷ�������У������� x �̶ȵ���ģ���ô�ڽ���Ĺ����оͻ���� x2 �̶ȵ���ģ�����ɴ�������ĳ����������;öȣ��������ͻᱬը׹�١���һ���;ö�Ϊ h �ķ������������ڷ��й����в�������ģ���ôΪ�˱�֤����԰�ȫ�ĵ���Ŀ�ĵأ�ֻ���������⣬���෢������п��Գ��ܶ��ٳ̶ȵ���ģ�

**��������:**
>ÿ���������һ������������ÿ��������������һ��һ������ h ��1 <= h <= 10^18����

**�������:**
>���һ��һ��������ʾ�����

**������**
```
����
10

���
2
```

### ����˼·
- ��һ��򵥵����һԪ���η���(X^2+x=h)���㷨�⣬ֻҪ���������ʽ�Ϳ��Եó��𰸣�
- ��Ϊ����ֵ�Ѿ������������ķ�Χ����Ҫ��long����ʾ��
- ��Ȼ����ͨ���������ķ�ʽ��ȡֵ��Scanner��ʽ��ȡֵ���˺ö౶��


### �ο�����

```java
import java.io.*;
public class Main {
    public static void main(String[] args) throws Exception{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        long h = Long.parseLong(br.readLine());
        long result = (long)(-1 + Math.sqrt(1 + 4 * h)) / 2;
        System.out.println(result);
    }
}
```

## ������ �ر�ͼ

### ��Ŀ����
>ţţ�õ���һ���ر�ͼ��˳�Ųر�ͼ��ָʾ��ţţ������һ���ر��У��ر�������һ�����أ�����ÿ�λ���ʾ�����ַ��� s �� t�����ݹ��ϵĴ�˵��ţţ��Ҫÿ�ζ��ش� t �Ƿ��� s �������С�ע�⣬�����в�Ҫ����ԭ�ַ������������ģ����紮 abc�����������о��� {�մ�, a, b, c, ab, ac, bc, abc} 8 �֡�

**��������:**
>ÿ���������һ������������ÿ�����������������г��Ȳ����� 10 �Ĳ������ո�Ŀɼ� ASCII �ַ�����

**�������:**
>���һ�� ��Yes�� ���� ��No�� ��ʾ�����

**������**
```
����
x.nowcoder.com
ooo

���
YES
```

### ����˼·
- ��̬�滮����һ��s�ַ������ȵ�dp���飬��¼t�ַ�����ÿ���ַ�ǰ�ж��ٸ�s�е��ַ���
<div align="center"> <img src="https://github.com/LyricYang/Internet-Recruiting-Algorithm-Problems/blob/master/NETEASE/pic/Q7Y2017.jpg"/> </div><br>

### �ο�����

```java
import java.io.*;
public class Main{
    public static void main(String[] args)throws Exception{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        String s=null;
        while((s = in.readLine()) != null){
            String t = in.readLine();
            int[] map = new int[s.length()];
            int loc=0;
            for(int i=0;i<map.length;i++){
                if(s.charAt(i)==t.charAt(loc))
                    loc++;
                map[i]=loc;
                if(loc==t.length()){
                    break;
                }
            }
            if(loc==t.length()){
                System.out.println("Yes");
            }else{
                System.out.println("No");
            }
        }
    }
}
```

## �ڰ��� ���л�ԭ

### ��Ŀ����
>ţţ����ҵ������һ������Ϊ n ������ A��������а����˴�1��n��n������������ΪһЩԭ��������һЩλ�ã������� 10 �����������ˣ�����ţţ�ǵ��������˳��Ե������� k��˳�����ָ���� i < j �� A[i] < A[j] �Ķ����������ţţ��������������Ҫ��ĺϷ����е���Ŀ��

**��������:**
>ÿ���������һ������������ÿ�����������ĵ�һ�а����������� n �� k��1 <= n <= 100, 0 <= k <= 1000000000������������ 1 �У����� n �����ֱ�ʾ���� A�����е���0�����ʾ�������λ�ã������� 10 ������

**�������:**
>���һ�б�ʾ�Ϸ���������Ŀ��

**������**
```
����
5 5
4 0 0 2 0

���
2
```

### ����˼·

���ȣ�˳��Եĸ�������Ӱ�졣Ҳ����˵����������A��˵�����ӣ����룩һ�����֣���A��˳��Ը������䣬����������A+1��˳��Ը���=����A��˳���+�²�������ֲ�����˳���.
�����ƹ㵽������c�����֣�������A+c��˳���=����A��˳���+����c��˳���+ÿ���²�������ֲ���˳��ԣ���c�����֣���
���ԣ�
1. ���ȼ����Ѿ����������ֹ���arrbase��˳��ԣ�
2. Ȼ�����ȱʧ�����ֹ���canbase��˳��ԣ�
3. ������ÿ��ȱʧ�����ֲ�����˳��ԣ�

����2,3���裬���Խ�ȱʧ�����֣����飩����ȫ���С�

### �ο�����

```java
import java.io.*;
import java.util.*;

public class Main{
    public static void main(String[] args) throws Exception{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        String line1=null;
        while((line1=in.readLine())!=null){
            String[] s1 = line1.trim().split(" ");
            int n = Integer.parseInt(s1[0]);
            int k = Integer.parseInt(s1[1]);
            String line2 = in.readLine();
            String[] s2=line2.trim().split(" ");
            int[] arr = new int[n];
            for(int i=0;i<n;i++){
                arr[i]=Integer.parseInt(s2[i]);
            }
            int x1 = 0;
            int x2 = 0;
            int x3 = 0;
            for(int i=0;i<n;i++){
                if(arr[i]==0){
                    continue;
                }else{
                    for(int j=i+1;j<n;j++){
                        if(arr[j]==0)
                            continue;
                        else{
                            if(arr[i]<arr[j]){
                                x1++;
                            }
                        }
                    }
                }
            }
            k-=x1;
            List<Integer> indexs = new ArrayList<>();
            List<Integer> values = new ArrayList<>();
            List<Integer> temp = new ArrayList<>();
            for(int i = 0;i < n;i++){
                if(arr[i] > 0){
                    temp.add(arr[i]);
                }else{
                    indexs.add(i);
                }
            }
            
            for(int i = 1;i <= n;i++){
                if(!temp.contains(i)){
                    values.add(i);
                }
            }
            int res = count(arr,indexs,values,k);
            System.out.println(res);
        }
    }
    
    public static int count(int[] array,List<Integer> indexs,List<Integer> values,int k){
        int count = 0;
        if(indexs.size()==0){
            if(k==0)
                return 1;
            else
                return 0;
        }
        int index = indexs.remove(0);
        for(int i=0;i<values.size();i++){
            int value = values.get(i);
            array[index]=value;
            int pairs = getPairs(array,index);
            if(pairs<=k){
                values.remove(i);
                count+=count(array,indexs,values,k-pairs);
                values.add(i,value);
            }
        }
        array[index]=0;
        indexs.add(0,index);
        return count;
    }
    public static int getPairs(int[] array,int index){
        int count=0;
        for(int i=0;i<array.length;i++){
             if((i < index && array[i] < array[index]) || (i > index && array[i] > array[index])){
                count++;
            }
        }
        return count;
    }
}
```

## �ھ��� �������

### ��Ŀ����
>�����һ�����ң������������һ����������������û���㹻��ɫ�����ϡ�Ϊ��������򵥣���������������ʾ��ͬ��ɫ�����ϡ���֪���������Ҫ��n����ɫ�����ϣ������ڿ���ȥ�̵깺��һЩ���ϣ������̵겻�ܱ�֤�ܹ�Ӧ������ɫ�����ϣ���������Ҫ�Լ����һЩ���ϡ�������ֲ�һ������ɫA����ɫB���Ͽ��Բ���(A XOR B)������ɫ������(�²���������Ҳ��������������ϲ����µ���ɫ,XOR��ʾ������)�������ڼ��Լ�ľ������빺����ٵ����Ͼ�����Ҫ�����Լ�ְ����Ա������Ҫ����������������Ҫ��������ɫ�����ϣ�

**��������:**
>��һ��Ϊ�����������Ҫ����ɫ����n (1 �� n �� 50)
�ڶ���Ϊn����xi(1 �� xi �� 1,000,000,000)����ʾ��Ҫ�ĸ�������.

**�������:**
>���������Ҫ���̵깺���������ɫ������ע����ܹ������ɫ��һ����ʹ���ڻ��У�ֻ��Ϊ�˲����µ���ɫ��

**������**
```
����
3
1 7 3

���
3
```

### ����˼·
�������ѧ��˼�Ǹ��ݸ����ļ�������Ҫ�ҵ����ٵ����ָ��ݹ��������ͬΪ0����ͬΪ1�����Եõ������ļ�������

1. ��������ԭ�򣬺��������뵽λ���㡣����001,010,100�������1~7֮��������������ԣ�����𰸵�����Ӧ����������ֵ�λ����

2. �ڸ�����N�����У�������һЩ���ǿ�������������������ɣ�������Ҫ�ҵ���������ļ�������Ҳ�������⼸����ͨ���������������ɸ���������������ôʲô�ǡ������������أ� 
����������е��ȣ�ͨ��������ȱ任����ĶԽ����ϵ�Ԫ�ظ�������Ӧ�˾���Ԫ���������ųɵ������ӿռ��ά���� 
����֮��ֻҪ����˾�����ȣ���ôͨ�����ȱ任�ǿ��Ի�ԭԭʼ����ġ�

3. ��������ķ���������ֻ��Ҫ�Ը�������������������λ����Ȼ������˹��Ԫ�����õ��ȵĸ�����Ϊ��Ҫ������ٵ����ָ���

### �ο�����

```java
import java.io.*;
import java.util.*;

public class Main{
    public static void main(String[] args)throws Exception{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        String line1=null;
        while((line1=in.readLine())!=null){
            int n = Integer.parseInt(line1);
            String line2 = in.readLine();
            String[] s2 = line2.trim().split(" ");
            int[] arr = new int[n];
            for(int i=0;i<n;i++){
                arr[i] = Integer.parseInt(s2[i]); 
            }
            int count = 0;
            Arrays.sort(arr);
            for(int i=n-1; i>=0; i--){
                for(int j=i-1; j>=0; j--){
                    if(highbit(arr[i]) == highbit(arr[j])){
                        arr[j] = arr[j] ^ arr[i];
                    }
                }
                Arrays.sort(arr);
            }
            for(int i=0 ;i<n;i++)
                if(arr[i] !=0){
                    count++;
            }
            System.out.println(count);
        }
    }
    public static int highbit(int x){
        for(int i=31;i>=0;i--)
        {
           int m = (x>>i)&1;
           if(m != 0)
               return i+1;
        }
        return 0;
    }
}
```

## ��ʮ�� ���˵Ĵ���

### ��Ŀ����
>һ������������n����ÿ�������涼��һ������(ӵ����ͬ����������������)�����һ�����������˵ĵ��ҽ���������ĺ���ĺʹ���������ĺ���Ļ���
���磺��������������ĺ�����{1, 1, 2, 3}��������Ӿ������˵ģ���Ϊ1 + 1 + 2 + 3 > 1 * 1 * 2 * 3
������ʵ��Ӵ������Ƴ�һЩ��(�����Ƴ�0��,���Ǳ��Ƴ���)��Ҫʹ�Ƴ���Ĵ��������˵ġ����������̼���һ������Ի�õĶ����ֲ�ͬ�����˵Ĵ��ӡ�

**��������:**
>��һ������һ��������n(n �� 1000)
�ڶ���Ϊn����������xi(xi �� 1000)

**�������:**
>������Բ��������˵Ĵ�����

**������**
```
����
3
1 1 1

���
2
```

### ����˼·
- ��Ŀ����ת��������������ļ������Ӽ�������ÿ�δ�ȫ����ѡ������Ԫ�أ�С������Ӽ������ӣ��������Ӽ�����Ϊ2^n����ʹ��dfs��Ȼ��ʱ���Ҵ������ظ�Ԫ�أ���ô������**��֦**��������������������a,b�������`a+b>a*b`�������һ����Ϊ1.��������֤����
��`a=1+x,b=1+y����1+x+1+y>(1+x)*(1+y)��--->  1>x*y`����x��y����һ��Ϊ0����a,b��һ��Ϊ1.�ƹ㵽����k��������������a1,a2,...ak������������������������sumС�ڵ��ڻ�pi�������ʱ��ѡ��һ����b,��ʹ������`sum+b > pi*b`����b��ȻΪ1����Ϊ��Ҫ�ǳ����������֮�����ѡ���b>1����`sum+b <=pi*b`����a1,a2,...,ak,b���������������
<div align="center"> <img src="https://github.com/LyricYang/Internet-Recruiting-Algorithm-Problems/blob/master/NETEASE/pic/Q10Y2017.jpg"/> </div><br>

### �ο�����

```java
import java.io.*;
import java.util.*;
public class Main{
    public static void main(String[] args)throws Exception{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        String line1=null;
        while((line1=in.readLine())!=null){
            int n = Integer.parseInt(line1);
            String line2 = in.readLine();
            String[] Arr2 = line2.trim().split(" ");
            int[] boll = new int[n];
            for(int i=0;i<n;i++){
                boll[i]=Integer.parseInt(Arr2[i]);
            }
            Arrays.sort(boll);
            int result = calc(boll,0,0,1);
            System.out.println(result);
        }
    }
    public static int calc(int[] boll,int index,int sum,int mult){
        int count=0;
        for(int i=index;i<boll.length;i++){
            sum+=boll[i];
            mult*=boll[i];
            if(sum>mult){
                count+=1+calc(boll,i+1,sum,mult);
            }else if(boll[i]==1){
                count+=calc(boll,i+1,sum,mult);
            }else
                break;
            sum-=boll[i];
            mult/=boll[i];
            while(i<boll.length-1&&boll[i]==boll[i+1]){
                i++;
            }
        }
        return count;
    }
}
```

## ��ʮһ�� ��Ҫ��

### ��Ŀ����
>����С����һ��W*H��������ӣ�������б��Ϊ0~H-1��������б��Ϊ0~W-1��ÿ������������Է�һ�鵰�⣬�������鵰���ŷ����þ��벻�ܵ���2������������������(x1,y1),(x2,y2)��ŷ����þ���Ϊ:
( (x1-x2) * (x1-x2) + (y1-y2) * (y1-y2) ) ������ƽ������
С����֪�������ԷŶ��ٿ鵰������������

**��������:**
>ÿ������������񳤿�W,H���ÿո�ָ�.(1 �� W��H �� 1000)

**�������:**
>���һ�������Էŵĵ�����

**������**
```
����
3 2

���
4
```

### ����˼·
- **�㷨һ**�����ư˻ʺ����⣬��һ������W,H������`G`��¼�Ƿ������ֹ���⣬��Loc[0,0]��ʼ��������G[0,0]��ֵΪ1��ŷ����þ���Ϊ2��λ�ø�ֵΪ-1����Loc[0,2]=-1��Loc[2,0]=-1��������������ֵΪ0����Է��õ��⣬�����ܣ��ñ���count��¼���õ���Ĵ�����
- �㷨���Ӷ�**O(WH)**,�ռ临�Ӷ�**O(WH)**

- **�㷨��**��������4������2�������ȼ���������ۼ��ɡ�����λ�þ��Ǽ��ÿ��2*2�������ε�����
<div align="center"> <img src="https://github.com/LyricYang/Internet-Recruiting-Algorithm-Problems/blob/master/NETEASE/pic/Q11Y2017.jpg"/> </div><br>

### �ο�����

```java
import java.util.*;
import java.io.*;

public class Main{
    public static void main(String[] args)throws Exception{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        String line = null;
        while((line=in.readLine())!=null){
            String[] strArr = line.trim().split(" ");
            int W = Integer.parseInt(strArr[0]);
            int H = Integer.parseInt(strArr[1]);
            int[][] map = new int[W][H];
            int count=0;
            for(int i=0;i<W;i++){
                for(int j=0;j<H;j++){
                    if(map[i][j]==0){
                        count++;
                        delPlace(i,j,map);
                    }
                }
            }
            System.out.println(count);
        }
    }
    
    public static void delPlace(int i,int j,int[][] map){
        map[i][j]=1;
        if(i-2>=0){
            map[i-2][j]=-1;
        }
        if(i+2<map.length){
            map[i+2][j]=-1;
        }
        if(j-2>=0){
            map[i][j-2]=-1;
        }
        if(j+2<map[0].length){
            map[i][j+2]=-1;
        }
    }
}
```

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
 
public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
        String str = null;
        String[] string;
        int w, h, count = 0;
        while((str = reader.readLine()) != null) {
            string = str.split(" ");
            w = Integer.parseInt(string[0]);
            h = Integer.parseInt(string[1]);
            if(w % 4 == 0 || h % 4 ==0) {
            count = w * h / 2;
            }
            else if(w % 2 == 0 && h % 2 == 0) {
                count = (w * h / 4 + 1) / 2;
            }
            else {
                count = (w * h) / 2 + 1;
            }
            System.out.println(count);
        }
    }
}
```


## ��ʮ���� ���С��

### ��Ŀ����
>��һƬ1000*1000�Ĳݵأ�С�׳�ʼվ��(1,1)(�����Ͻǵ�λ��)��С����ÿһ��������������ƶ������ڵĲݵ��ϳԲ�(С�ײ����߳��߽�)�����ɳ�����ȥ��׽�ɰ���С�ף���������n�����塣��i�����屻�����ں�����Ϊxi ��������Ϊyi ��λ���ϣ�С��һ������һ�����壬���ᱻ������׽����Ϊ��ȥ���С�ף���Ҫ֪��С�����ٶ�������ܻ�����һ�����壬�Ӷ���ǰ���С�ס�

**��������:**
>��һ��Ϊһ������n(n �� 1000)����ʾ����һ��ӵ��n�����塣
�ڶ�����n������xi����ʾ��i������ĺ�����
��������n������yi����ʾ��i�������������
��֤���궼�ڲݵط�Χ�ڡ�

**�������:**
>���һ������,��ʾС�����ٿ��ܶ���������볬��������

**������**
```
����
3
4 6 8
1 2 1

���
3
```

### ����˼·
- ����ÿ���������(1,1)�����ʱ�伴Ϊ�������

### �ο�����

```java
import java.io.*;

public class Main{
    public static void main(String[] args)throws Exception{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        String L1 = null;
        while((L1=in.readLine())!=null){
            int n=Integer.parseInt(L1);
            String L2 = in.readLine();
            String[] L2Arr = L2.trim().split(" ");
            int[] X=new int[n];
            for(int i=0;i<n;i++){
                X[i]=Integer.parseInt(L2Arr[i]);
            }
            String L3 = in.readLine();
            String[] L3Arr = L3.trim().split(" ");
            int[] Y=new int[n];
            for(int i=0;i<n;i++){
                Y[i]=Integer.parseInt(L3Arr[i]);
            }
            int result=Integer.MAX_VALUE;
            for(int i=0;i<n;i++){
                int diff=X[i]-1+Y[i]-1;
                if(diff<result)
                    result=diff;
            }
            System.out.println(result);
        }
    }
}
```

## ��ʮ���� ͳ�ƻ���

### ��Ŀ����
>�����Ĵ�����һ�������ͷ�����һ�����ַ��������硰level�����ߡ�noon���ȵȾ��ǻ��Ĵ��������ǳ�ϲ������ӵ�жԳ����Ļ��Ĵ������յ�ʱ�����õ���������ֱ����ַ���A���ַ���B���������ǳ�������û�а취���ַ���B�����ַ���Aʹ�������ַ�����һ�����Ĵ�������ܻ��������󣬰�����Ѱ���ж����ֲ���취����ʹ�´���һ�����Ĵ�������ַ���B�����λ�ò�ͬ�Ϳ���Ϊ��һ���İ취��
���磺
A = ��aba����B = ��b����������4�ְ�B����A�İ취��
* ��A�ĵ�һ����ĸ֮ǰ: "baba" ���ǻ��� 
* �ڵ�һ����ĸ��a��֮��: "abba" �ǻ��� 
* ����ĸ��b��֮��: "abba" �ǻ��� 
* �ڵڶ�����ĸ'a'֮�� "abab" ���ǻ��� 
�������������Ĵ�Ϊ2

**��������:**
>ÿ���������ݹ����С�
��һ��Ϊ�ַ���A
�ڶ���Ϊ�ַ���B
�ַ������Ⱦ�С��100��ֻ����Сд��ĸ

**�������:**
>���һ�����֣���ʾ���ַ���B�����ַ���A֮�󹹳�һ�����Ĵ��ķ�����

**������**
```
����
aba
b

���
2
```

### ����˼·
- ��B���뵽A�в��ж��Ƿ��ǻ����ַ�����

### �ο�����

```java
import java.io.*;
public class Main{
    public static void main(String[] args)throws Exception{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        String A = null;
        while((A=in.readLine())!=null){
            String B=in.readLine();
            int count=0;
            for(int i=0;i<=A.length();i++){
                String comb = A.substring(0,i)+B+A.substring(i,A.length());
                if(isPalindrome(comb))
                    count++;
            }
            System.out.println(count);
        }
    }
    
    public static boolean isPalindrome(String s){
        int head=0;
        int tail=s.length()-1;
        while(head<tail){
            if(s.charAt(head)==s.charAt(tail)){
                head++;
                tail--;
            }else{
                return false;
            }
        }
        return true;
    }
}
```

## ��ʮ���� ������С��

### ��Ŀ����
>С�����Ǹо�������������Ϊ�����С�׾�����ȥѰ�ұ��ǳԡ��ʼС����һ����ʼλ��x_0������С�������ĵ�ǰλ��x����ֻ��ͨ�����ص������ƶ��� 4 * x + 3����8 * x + 7����Ϊʹ����������Ҫ�ķ�̫��������������ֻ��ʹ�������������100,000�Ρ��������������ܱ�1,000,000,007������λ��(���磺λ��0��λ��1,000,000,007��λ��2,000,000,014��)��С����Ҫ���æ����������Ҫʹ�ö��ٴ������������ܳԵ����ǡ�

**��������:**
>����һ����ʼλ��x_0,��Χ��1��1,000,000,006

**�������:**
>���С��������Ҫʹ�����������Ĵ��������ʹ�ô���ʹ���껹û�ҵ����ǣ������-1

**������**
```
����
125000000

���
1
```

### ����˼·
- [˼·](https://blog.csdn.net/fcxxzux/article/details/52138964#t0)

### �ο�����

```java
import java.io.*;
public class Main{
    public static void main(String[] args)throws Exception{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        String L1=null;
        while((L1=in.readLine())!=null){
            long x0=Long.parseLong(L1);
            x0%=1000000007;
            int times=4;
            int result=-1;
            for(int i=1;i<300000;i++){
                long n=(x0*times+times-1)%1000000007;
                if(n==0){ 
                    result=(i+1)/3+((i+1)%3>0?1:0); 
                    break; 
                }
                times=times*2%1000000007;
            }
            System.out.println(result>100001?-1:result);
        }
    }
}
```


## ��ʮ���� �������򷽷�

### ��Ŀ����
>������n���ַ��������������ַ������ȶ��ǲ�ͬ�ġ��������ѧϰ���������ַ��������򷽷��� 1.�����ַ������ֵ����������磺
"car" < "carriage" < "cats" < "doggies < "koala"
2.�����ַ����ĳ����������磺
"car" < "cats" < "koala" < "doggies" < "carriage"
������֪���Լ�����Щ�ַ�������˳���Ƿ��������������򷽷�������Ҫæ�ų���Ҷ��������Ҫ������æ��֤��

**��������:**
>�����һ��Ϊ�ַ�������n(n �� 100)
��������n��,ÿ��һ���ַ���,�ַ������Ⱦ�С��100������Сд��ĸ���

**�������:**
>�����Щ�ַ����Ǹ����ֵ������ж����Ǹ��ݳ����������"lexicographically",
������ݳ������ж������ֵ����������"lengths",
������ַ�ʽ���������"both"���������"none"

**������**
```
����
3
a
aa
bbb

���
both
```

### ����˼·
- �򵥱Ƚ�ǰ���ַ������ֵ���ͳ��ȡ�

### �ο�����

```java
import java.io.*;
import java.util.*;

public class Main{
    public static void main(String[] args)throws Exception{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        String L1=null;
        while((L1=in.readLine())!=null){
            int n = Integer.parseInt(L1);
            String[] strArr = new String[n];
            int[] lenArr = new int[n];
            for(int i=0;i<n;i++){
                strArr[i]=in.readLine();
                lenArr[i]=strArr[i].length();
            }
            boolean cond0 = true;
            boolean cond1 = true;
            for(int i=1;i<n;i++){
                if(strArr[i].compareTo(strArr[i-1])<=0){
                    cond0=false;
                    break;
                }
            }
            for(int i=1;i<n;i++){
                if(lenArr[i]<=lenArr[i-1]){
                    cond1=false;
                    break;
                }
            }
            if(cond0&&cond1){
                System.out.println("both");
            }
            else if(cond0){
                System.out.println("lexicographically");
            }else if(cond1){
                System.out.println("lengths");
            }else{
                System.out.println("none");
            }
        }
    }
}
```

## ��ʮ���� С��ϲ���ĵ���

### ��Ŀ����
>С��ϲ���ĵ��ʾ����������ԣ�
1.����ÿ����ĸ���Ǵ�д��ĸ
2.����û��������ȵ���ĸ
3.����û�����硰xyxy��(�����x��yָ�Ķ�����ĸ�����ҿ�����ͬ)�����������У������п��ܲ�������
���磺
С�ײ�ϲ��"ABBA"����Ϊ����������������'B'
С�ײ�ϲ��"THETXH"����Ϊ�������������"THTH"
С�ײ�ϲ��"ABACADA"����Ϊ�������������"AAAA"
С��ϲ��"A","ABA"��"ABCBA"��Щ����
����һ�����ʣ���Ҫ�ش�С���Ƿ��ϲ��������ʡ�

**��������:**
>����Ϊһ���ַ��������ɴ�д��ĸ��ɣ�����С��100

**�������:**
>���С��ϲ�����"Likes",��ϲ�����"Dislikes"

**������**
```
����
AAA

���
Dislikes
```

### ����˼·
- �㷨һ������Լ���������൱��������ʽ�Ĺ��췽ʽ��
- �㷨����ǰ�������������жϣ���Ҫ�ǵ�������������¼�ظ��ַ����ַ����е�λ�ã�����ͬ�ظ��ַ�֮���λ���໥���棬�򷵻�false��

### �ο�����

```java
import java.io.*;
import java.util.*;

public class Main{
    public static void main(String[] args)throws Exception{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        String L1=null;
        while((L1=in.readLine())!=null){
            if(isAllUpCase(L1) && isConEql(L1) && isThrEql(L1))
                System.out.println("Likes");
            else
                System.out.println("Dislikes");
        }
    }
    public static boolean isAllUpCase(String word){
        return word.matches("[A-Z]+");
    }
    public static boolean isConEql(String word){
        return !word.matches(".*(.)(\\1).*");
    }
    public static boolean isThrEql(String word){
        return !word.matches(".*(.).*(.)(.*\\1)(.*\\2).*");
    }
}
```

```java
import java.io.*;
import java.util.*;

public class Main{
    public static void main(String[] args)throws Exception{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        String L1=null;
        while((L1=in.readLine())!=null){
            if(isAllUpCase(L1) && isConEql(L1) && isThrEql(L1))
                System.out.println("Likes");
            else
                System.out.println("Dislikes");
        }
    }
    public static boolean isAllUpCase(String word){
        for(int i=0;i<word.length();i++){
            if(word.charAt(i)>'Z'&&word.charAt(i)<'A')
                return false;
        }
        return true;
    }
    public static boolean isConEql(String word){
        for(int i=1;i<word.length();i++){
            if(word.charAt(i-1)==word.charAt(i))
                return false;
        }
        return true;
    }
    public static boolean isThrEql(String word){
        ArrayList<Integer> numList = new ArrayList<>();
        for(int i=1;i<word.length();i++){
            for(int j=i-1;j>=0;j--){
                if(word.charAt(i)==word.charAt(j)){
                    numList.add(j);
                    numList.add(i);
                    break;
                }
            }
        }
        if(numList.size()<4){
            return true;
        }
        for(int i=0;i<numList.size()-3;i+=2){
            if(numList.get(i+2)>numList.get(i)&&numList.get(i+2)<numList.get(i+1))
                return false;
        }
        return true;
    }
}
```

## ��ʮ���� Fibonacci����

### ��Ŀ����
>Fibonacci��������������ģ�
F[0] = 0
F[1] = 1
for each i �� 2: F[i] = F[i-1] + F[i-2]
��ˣ�Fibonacci���о����磺0, 1, 1, 2, 3, 5, 8, 13, ...����Fibonacci�����е������ǳ�ΪFibonacci��������һ��N�����������Ϊһ��Fibonacci����ÿһ������԰ѵ�ǰ����X��ΪX-1����X+1�����ڸ���һ����N��������Ҫ���ٲ����Ա�ΪFibonacci����

**��������:**
>����Ϊһ��������N(1 �� N �� 1,000,000)

**�������:**
>���һ����С�Ĳ�����ΪFibonacci��"

**������**
```
����
15

���
2
```

### ����˼·
- �ҵ��������Nǰ���Fibonacci��������N��ǰ��Fibonacci���Ĳ�ֵ��ѡ��С�Ĳ�ֵ��Ϊ��С������

### �ο�����

```java
import java.util.*;
import java.io.*;
public class Main{
    public static void main(String[] args)throws Exception{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        String L1=null;
        while((L1=in.readLine())!=null){
            int N = Integer.parseInt(L1);
            int fir=0;
            int sec=1;
            int sum=1;
            while(sum<N){
                fir=sec;
                sec=sum;
                sum=fir+sec;
            }
            int result=Math.min(N-sec,sum-N);
            System.out.println(result);
        }
    }
}
```

## ��ʮ���� ������Ϸ

### ��Ŀ����
>С����������һ��������Ϸ��С�׸���һϵ�е�������������ʹ����Щ��������Ϸ��ÿ��С�׻�����˵һ�����ֳ�����Ȼ������Ҫ����һϵ��������ѡȡһ���ֳ��������ǵĺ͵���С����˵�����֡� ���磺 ���{2,1,2,7}�����е�һϵ������С��˵��������11.����Եõ�����2+2+7 = 11.�����Ƥ��С������㣬��˵��������6����ô��û�а취ƴ�ճ���Ϊ6 ����С�׸���n�����������ҳ��޷���n������ѡȡ������͵������е���С����

**��������:**
>�����һ��Ϊ���ָ���n (n �� 20)
�ڶ���Ϊn����xi (1 �� xi �� 100000)

**�������:**
>�����С������n����ѡȡ�����ɵ���

**������**
```
����
3
5 1 2

���
4
```

### ����˼·

���ӣ�
```
������ļ�����nums = {1, 2, 2, 7}
��N��ʾĿǰ�ܱ��1-N�����е�����
һ��ʼʲô��û�У��ܴճ���Ǯ��0��N=0
N = 0���õ���0������nums[0]=1���ж�һ���µ�����1��ԭ���ķ�ΧN+1�Ĵ�С��ϵ��1<=N+1(1)����˿��ԡ���ȫ�ء�����Χ��N = N+1�� N=1��Ҳ����˵�õ�1�����ֿ��Ա�ʾ0-1��
N = 1�����õ���1������nums[1]=2���ж�һ���µ�����2��ԭ���ķ�ΧN+1�Ĵ�С��ϵ��2<=N+1(2)����˿��ԡ���ȫ�ء�����Χ��N = N+2�� N=3��Ҳ����˵��ǰ�������ֿ��Ա�ʾ0-3��
N = 3�����õ���2������nums[1]=2���ж�һ���µ�����2��ԭ���ķ�ΧN+1�Ĵ�С��ϵ��2<=N+1(4)����˿��ԡ���ȫ�ء�����Χ��N = N+2�� N=5��Ҳ����˵��ǰ�������ֿ��Ա�ʾ0-5��
N = 5�����õ���3������nums[3]=7���ж�һ���µ�����7��ԭ���ķ�ΧN+1�Ĵ�С��ϵ��7>N+1(6)����˲����ԡ���ȫ�ء�����Χ�ˣ�Ҳ����˵��ǰ�������ֻ���ֻ���Ա�ʾ0-5��
�ɴˣ��������ֻ�ܱ�ʾ0-5�ˣ����ܱ�ʾ6��
```
��ѧ���ͣ�
```
��1<=x<=N+1��ʱ�� 
ԭ���������Ѿ�������ǰ���һ�����ֱ�ʾ1-N�ˣ���������һ���µ�����x����1~N+1�ķ�Χ�ڣ���ô�������ڿ��Ա�ʾ1~N+x�ķ�Χ�ˡ�
ԭ���ǿ��Ա�ʾ1~N�ˣ�Ȼ����N+1����ô��ʾN+1�����ǿ�����x+(N+1-x)����(N+1-x)������϶�����1~N�ķ�Χ�ע������������������Ϳ�����ǰ�������ʾ�����ˡ�

֤����N>=N+1-x>=1
1<=x<=N 
->
-1>=-x>=-N
->
N+1-1>=N+1-x>=N+1-N
->
N>=N+1-x>=1
֤�ϡ�
```

### �ο�����

```java
import java.io.*;
import java.util.*;

public class Main{
    public static void main(String[] args)throws Exception{
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        String L1 = null;
        while((L1=in.readLine())!=null){
            int n=Integer.parseInt(L1);
            String L2 = in.readLine();
            String[] L2Arr=L2.trim().split(" ");
            int[] num = new int[n];
            for(int i=0;i<n;i++){
                num[i]=Integer.parseInt(L2Arr[i]);
            }
            Arrays.sort(num);
            int miss=0;
            for(int i=0;i<n;i++){
                if(num[i]>miss+1) break;
                miss+=num[i];
            }
            System.out.println(miss+1);
        }
    }
}
```