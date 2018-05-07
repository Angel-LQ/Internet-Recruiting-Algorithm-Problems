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

<div align="center"> <img src="https://github.com/LyricYang/Internet-Recruiting-Algorithm-Problems/tree/master/NETEASE/pic/Q7Y2017.png" width="300"/> </div><br>

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
- ��Ŀ����ת��������������ļ������Ӽ�������ÿ�δ�ȫ����ѡ������Ԫ�أ�С������Ӽ������ӣ��������Ӽ�����Ϊ2^n����ʹ��dfs��Ȼ��ʱ���Ҵ������ظ�Ԫ�أ���ô��������֦��
������������������a,b������� a+b>a*b�������һ����Ϊ1.��������֤����
��a=1+x,b=1+y����1+x+1+y>(1+x)*(1+y)��--->  1>x*y����x��y����һ��Ϊ0����a,b��һ��Ϊ1.
�ƹ㵽����k��������������a1,a2,...ak������������������������sumС�ڵ��ڻ�pi��
�����ʱ��ѡ��һ����b,��ʹ������sum+b > pi*b����b��ȻΪ1����Ϊ��Ҫ�ǳ��������
��֮�����ѡ���b>1����sum+b <=pi*b����a1,a2,...,ak,b���������������

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