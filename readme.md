# 1.求最小公倍数
## 1.1辗转相除法
```
public class Main{
    public static void main(String[] argv){
        Scanner in = new Scanner(System.in);
        int num1 = in.nextInt();
        int num2 = in.nextInt();
        
        System.out.println(minMultiNumber(num1, num2));
    
    }
    
    public static int minMultiNumber(int a, int b){
        return (a*b)/maxGongYue(a, b);
    }
	// 辗转相除法
    public static int maxGongYue(int a, int b){
    
        if(a<b){
            int temp = a;
            a = b;
            b = temp;
        }
        
        if(a%b==0){
            return b;
        }
        
        int res = 0;
        res = maxGongYue(b, a%b);
        return res;
    }
}
```
## 1.2更相减损术
```
public class Main{
    public static void main(String[] argv){
        Scanner in = new Scanner(System.in);
        int num1 = in.nextInt();
        int num2 = in.nextInt();
        
        System.out.println(minMultiNumber(num1, num2));
    
    }
    
    public static int minMultiNumber(int a, int b){
    
        
        return (a*b)/maxGongYue(a, b);
        
    }

    public static int maxGongYue(int a, int b){
    
        if(a<b){
            int temp = a;
            a = b;
            b = temp;
        }
        
        if(a==b){
            return b;
        }
        
        int res = 0;
        res = maxGongYue(b, a-b);
        return res;
    }
}
```

# 2.求解立方根
```
import java.util.Scanner;
import java.text.DecimalFormat;

public class Main {
    public static void main(String[] argv){
        
        Scanner in = new Scanner(System.in);
        double input = in.nextDouble();
        System.out.println(getCubeRoot(input));
        
    }
    
    public static double getCubeRoot(double input){
        
        double i;
        for(i=0.0; i<=input; i=i+0.05){
            
            if(i*i*i>input)
                break;
        }
        DecimalFormat df = new DecimalFormat("#.0");
        return Double.parseDouble(df.format(i));
    }
}
```
# 3.字符逆序
将一个字符串str的内容颠倒过来，并输出。str的长度不超过100个字符。 如：输入“I am a student”，输出“tneduts a ma I”。

```
import java.lang.StringBuilder;
import java.util.Scanner;

public class Main{
    
    public static void main(String[] argv){
        Scanner in = new Scanner(System.in);
        String input = in.nextLine();  // 读入字符串
        System.out.println(reverseString(input));
    }
    public static String reverseString(String input){
        
        StringBuilder res = new StringBuilder();
        for(int i=input.length()-1; i>=0; i--){
            res.append(input.charAt(i));
        }
        return res.toString();
    }
}
```

# 4记负均正2
```
import java.util.Scanner;
import java.text.DecimalFormat;

public class Main{
    
    public static void main(String[] argv){
        
        Scanner in = new Scanner(System.in);
        String[] ss = in.nextLine().split(" ");
        long noNagtiveCnt = 0;
        long nagtiveCnt = 0;
        double total = 0.0;
        for(int i=0; i<ss.length; i++){
            int num = Integer.parseInt(ss[i]);
            if(num<0){
                nagtiveCnt++;
            }else{
                total = total + num;
                noNagtiveCnt++;
            }
        }
        System.out.println(nagtiveCnt);
        if(noNagtiveCnt==0){
            System.out.println("0.0");
        }else{
            DecimalFormat df = new DecimalFormat("##0.0");
            System.out.println(df.format(total/noNagtiveCnt));
        }
    }
}
```

# 5字符串分割
```
import java.util.Scanner;
import java.util.ArrayList;
import java.util.List;

public class Main{

    public static void main(String[] argv){
        Scanner in = new Scanner(System.in);
        while(in.hasNextInt()) {  # 这里必须加入输入流判断，否则容易输入不正确
            int num = in.nextInt();
            for (int i = 0; i < num; i++) {
                String temp = in.next();
                StringBuilder tempStringBuilder = new StringBuilder(temp);
                while (tempStringBuilder.length() % 8 != 0) {
                    tempStringBuilder.append('0');
                }
                temp = tempStringBuilder.toString();
                for (int j = 0; j < temp.length(); j = j + 8) {
                    System.out.println(temp.substring(j, j + 8));
                }
            }
        }
    }
}
```

# 6.Redraiment是走梅花桩的高手。
## 思路
本题与最大上升子序列长度一样。采用常规的dp算法求解。
```
import java.util.Scanner;
import java.util.List;
import java.util.Arrays;

public class Main{
    public static void main(String[] argv){
        int num = 0;
        Scanner in = new Scanner(System.in);
        // 为了处理多个case，额外添加的外层循环
        while(in.hasNext()){
            if(in.hasNextInt()){
                num = in.nextInt();
            }
            int[] nums = new int[num];
            for(int i=0; i<num; i++){
                if(in.hasNextInt())
                    nums[i] = in.nextInt();
            }
            int[] dp = new int[nums.length];
            for(int i=0; i<dp.length; i++){
                dp[i] = 1;
            }
            int max = 0;
            for(int i=1; i<dp.length; i++){
                for(int j=0; j<i; j++){
                    if(nums[i]>nums[j]&&(dp[j]+1>dp[i])){
                        dp[i] = dp[j]+1;
                    }
                }
                max = Math.max(dp[i], max);
            }
            System.out.println(max);
        }
    }
}
```

## 注意
- 牛客网的oj测试平台存在多个case测试的情况，此时需要在正常输入的外层套循环判断输入
```
	while(in.haveNext()){
	// 你的算法
	}
```

# 7. 字符统计
### 思路
1. 使用一个Int[128]来作为字符计数器，统计字符的数量。字符的ASCILL范围为0-127，与数组的默认索引对应。
2. 找出最大频数，从最大频数向1暴力搜索，每个频数从ascill值为0向最大127搜索，找到便添加至res字符串中。


```
    public static void main(String[] args){

        Scanner in = new Scanner(System.in);
        String str;
        while(in.hasNext()){
            str = in.next();
            // 过滤非字母数字空的的字符
            str = str.replaceAll("[^0-9a-zA-Z' ']", "");
            int[] counter = new int[129];
            // 统计各个字符出现的频数
            for(int i=0; i<str.length(); i++){
                counter[(int)str.charAt(i)]++;
            }
            // 找出最大频数
            int maxCnt = 0;
            for(int i=0; i<128; i++){
                if(counter[i]>maxCnt)
                    maxCnt = counter[i];
            }
            // 按照频数从大到小顺序，输出字符
            StringBuilder res = new StringBuilder();
            while(maxCnt>=0){
                for(int i=0; i<128; i++){
                    if(counter[i]>0&&maxCnt==counter[i])
                        res.append((char)i);
                }
                maxCnt--;
            }
            System.out.println(res.toString());
        }
    }
```

# 8.排序
自己写的排序算法超时，使用内置排序算法通过了。。。
```
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main{

    public static void main(String[] arg) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String line;
        while((line = br.readLine()) !=null){
            int n = Integer.parseInt(line);
            String[] numStr = br.readLine().split(" ");
            int method = Integer.parseInt(br.readLine());
            int[] nums = new int[n];
            for(int i=0; i<nums.length; i++){
                nums[i] = Integer.parseInt(numStr[i]);
            }
            quiteSort(nums, 0, nums.length-1, method);  // 升序
            StringBuilder res = new StringBuilder();
            for(int nn:nums){
                res.append(nn);
                res.append(" ");
            }
            System.out.println(res.toString().trim());
        }
    }
    public static void quiteSort(int[] nums, int low, int high, int method){

        if(low<high){
            int axi = nums[low];
            int i=low, j=high;
            // 划分
            if(method==0){
                while(i<j){
                    // 在右区间找到第一个比枢值小的索引
                    while(i<j&&nums[j]>axi)  j--;
                    // 将右区间第一个比枢值小的值，移动至左区间
                    if(i<j)  nums[i] = nums[j];
                    // 找到左区间第一个比枢值大的索引
                    while(i<j&&nums[i]<axi)  i++;
                    // 将左区间第一个比枢值大的值移动至右区间
                    if(i<j)  nums[j] = nums[i];
                }
            }else if(method==1){
                while(i<j){
                    while(i<j&&nums[j]<axi)  j--;
                    if(i<j)  nums[i] = nums[j];
                    while(i<j&&nums[i]>axi)  i++;
                    if(i<j)  nums[i] = nums[i];
                }
            }
            nums[i] = axi;
            quiteSort(nums, low, i-1, method);
            quiteSort(nums, i+1, high, method);
        }
    }
}
```
```
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Scanner;
import java.util.Arrays;

public class Main{

    public static void main(String[] arg) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String line;
        while((line = br.readLine()) !=null){
            int n = Integer.parseInt(line);
            String[] numStr = br.readLine().split(" ");
            int method = Integer.parseInt(br.readLine());
            int[] nums = new int[n];
            for(int i=0; i<nums.length; i++){
                nums[i] = Integer.parseInt(numStr[i]);
            }
            Arrays.sort(nums);
            StringBuilder res = new StringBuilder();
            
            if(method==0){
                for(int nn:nums){
                    res.append(nn);
                    res.append(" ");
                }
            }else if(method==1){
                for(int i=nums.length-1; i>=0; i--){
                    res.append(nums[i]);
                    res.append(" ");
                }
            }
            System.out.println(res.toString().trim());
        }
    }

}
```

# 9.等差数列
```
import java.util.Scanner;

public class Main{

    public static void main(String[] argv){
        Scanner in = new Scanner(System.in);
        while(in.hasNext()){
            int num = in.nextInt();
            if(num>0)
                System.out.println((int)((3.0*num*num+num)/2.0));
            else{
                System.out.println("-1");
            }
        }
    }
}
```
# 10.自守数
### 思路
从输入整数n,向下自减，暴力遍历所有数值。关键在于如何判断是否为存在尾数关系。

尾数关系的判断：通过将两个数值，转换为字符串，在分别从尾部开始，逐一判断是否相等。

```
import java.util.Scanner;

public class Main{

    public static void main(String[] argv){

        Scanner in = new Scanner(System.in);
        while(in.hasNext()){
            int num = in.nextInt();
            int cnt = 0;
            while(num>=0){
                if(isLeaveSelf(num)){
                    cnt++;
                }
                num--;
            }
            System.out.println(cnt);
        }
    }

    public static boolean isLeaveSelf(int num){

        long sqrtNum = num*num;
        String sqrtNumStr = String.format("%s", sqrtNum);
        String numStr = String.format("%s", num);

        int p1 = sqrtNumStr.length()-1;
        int p2 = numStr.length()-1;

        while(p2>=0){
            if(p1>=0&&numStr.charAt(p2--)!=sqrtNumStr.charAt(p1--))
                return false;
        }
        return true;
    }

}
```





