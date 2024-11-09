# 关于Jam’s balance问题

## 题面：
Jam 有一个天平和N块砝码。(1≤N≤20)；使用天平只能得知两端质量是否相等。砝码可以放置在左右任意一端。判断天平能否测量质量为M的物体。

## 输入：
第一行有一个整数T(1≤T≤5)，表示测试用例数。
对于每组测试用例：
第一行为N，表示砝码数。
第二行有N个数，第i个数wi(1≤wi≤100)表示
第三行有一个整数M。M为待测物体质量。

## 输出：
输出"YES"or"NO"。

## 思路：
先把这个问题尽可能的拆解
### 天平的原理
天平可以比较两边的质量是否相等。因此，我们可以通过将一些砝码放在一边，待测物体放在另一边，或者将待测物体与一些砝码放在一边，其他砝码放在另一边来实现测量。
### 对于每个砝码
在左边 在右边
### 目标是什么
找到一个方式 让天平两边的质量相同
这里面有这样几个步骤
* 一侧的砝码重量与另外一侧的砝码重量相减
* 对结果取绝对值
* 假如这个绝对值 等于 M 程序结束 能称量
### 数学表达
设砝码的质量分别为w1, w2, ..., wN，我们需要找到一组系数x1, x2, ..., xN，每个砝码都有三种状态：放在左边、放在右边、不使用。我们可以通过二进制位来表示这些状态。

具体来说，对于每个砝码，我们可以用两位二进制数来表示其状态：

    00：不使用该砝码
    01：将该砝码放在左边
    10：将该砝码放在右边

这样，对于 N 个砝码，我们需要 2N 位来表示所有可能的状态。由于每个砝码有3种状态，总共有 3N 种组合。满足以下等式：
x1w1+x2w2+...+xNwN=Mx1​w1​+x2​w2​+...+xN​wN​=M

## 回溯法解决
超时
而且经过剪枝也没办法优化
一直超时

在这里贴出我剪枝之后的回溯法
~~~~java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.Scanner;

public class WeightMeasurement {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int T = scanner.nextInt(); // 测试用例的数量

        for (int t = 0; t < T; t++) {
            int N = scanner.nextInt(); // 秤砣的数量
            int[] weights = new int[N];

            // 读取秤砣的重量
            for (int i = 0; i < N; i++) {
                weights[i] = scanner.nextInt();
            }

            int K = scanner.nextInt(); // 需要测量的物体数量

            List<String> results = new ArrayList<>();

            // 读取需要测量的物体的重量
            for (int k = 0; k < K; k++) {
                int M = scanner.nextInt(); // 物体的重量
                if (canMeasure(weights, M)) {
                    results.add("YES");
                } else {
                    results.add("NO");
                }
            }

            // 输出结果
            for (String result : results) {
                System.out.println(result);
            }
        }

        scanner.close();
    }

    public static boolean canMeasure(int[] weights, int targetWeight) {
        Arrays.sort(weights); // 对秤砣的重量进行排序，以便进行早期剪枝
        return backtrack(weights, targetWeight, 0, 0);
    }

    private static boolean backtrack(int[] weights, int targetWeight, int index, int currentDifference) {
        // 基本情况：如果所有秤砣都已考虑过
        if (index == weights.length) {
            return currentDifference == targetWeight;
        }

        // 剪枝条件
        if (Math.abs(currentDifference) > Math.abs(targetWeight) + sumRemaining(weights, index)) {
            return false;
        }

        // 尝试将当前秤砣放在左边
        if (backtrack(weights, targetWeight, index + 1, currentDifference - weights[index])) {
            return true;
        }

        // 尝试将当前秤砣放在右边
        if (backtrack(weights, targetWeight, index + 1, currentDifference + weights[index])) {
            return true;
        }

        // 尝试不使用当前秤砣
        if (backtrack(weights, targetWeight, index + 1, currentDifference)) {
            return true;
        }

        // 如果以上选项都不行，返回false
        return false;
    }

    private static int sumRemaining(int[] weights, int start) {
        int sum = 0;
        for (int i = start; i < weights.length; i++) {
            sum += weights[i];
        }
        return sum;
    }
}
~~~~


## 二进制枚举
二进制枚举主要是通过将具体的重量先遮住不看
通过枚举出所有秤砣的所有可能状态
找到能够称量的那一种状态
当然了 找到一种就可以
对于单个砝码而言
三种状态：
    00：不使用该砝码
    01：将该砝码放在左边
    10：将该砝码放在右边
在遍历的过程当中，砝码的状态并不是以二进制状态出现的
我们遍历的时候，得到的是他们的状态序号
比如：第一个状态 第二个状态 第三个状态
这里我们举出一个简化的例子，也是课件上面提供的博文
假如我们有四个砝码 他们的重量无所谓
就当做是1 2 3 4
规定：
一个砝码有两个状态
0代表砝码放在左边
1代表砝码放在右边
我们假设遍历到第13个状态了
我们怎么把13快速地提取成一个二进制数1101 并且判断哪些位置是1 哪些位置是0呢
就用到按位与和移位运算
### 按位与
0&0=0;  0&1=0;   1&0=0;    1&1=1;
3&5  即 0000 0011& 0000 0101 = 00000001  因此，3&5的值得1。

所以假如有13
变成0000 1101
我们用0000 0001和他进行与运算
就能得到他的最低位状态为1
### 移位
将0000 0001这个类似探针一样的东西
当中的1
左移一位
探针更新成
0000 0010
用0000 0010&0000 1101
得到0000 0000
说明第二位是0
以此类推
~~~~c++
for(int i = 0; i < (1<<n); i++) //从0～2^n-1个状态
    {
        for(int j = 0; j < n; j++) //遍历二进制的每一位
        {
            if(i & (1 << j))//判断二进制第j位是否存在
            {
                printf("%d ",j);//如果存在输出第j个元素
            }
        }
        printf("\n");
    }
~~~~

### 那有三个状态怎么办呢
三个状态的情况下 我们也可以采用上面的方式来探到每两位的状态
~~~~java
// 使用左移和按位与运算获取第i个砝码的状态
            int bitIndex = 2 * i;
            int mask = 3 << bitIndex; // 生成掩码
            int subStateBit = (state & mask) >> bitIndex; // 获取状态
~~~~
#### bitIndex
因为我们每个状态长度为2 所以我们在探状态的时候 从一个砝码移动到下一个砝码的过程当中
掩码需要左移2i位
这就是bitindex的作用
他一方面代表了第i个砝码的状态的位置
另一方面也让掩码能够正确的左移
#### mask
相当于上面 两状态 的1
在这里是3（11）
用来和00/01/10做&运算
从而从十进制当中提取出二进制状态
11&00=00；11&01=01；11&10=10；
#### subStateBit
`state & mask：使用按位与运算，保留 state 中第 i 个砝码的状态部分。
`>> bitIndex：将结果右移 bitIndex 位，得到第 i 个砝码的状态。
例如，如果 state = 10**10**01，mask = 1100，那么 state & mask 得到 1000，再右移 2 位得到 10
得到了中间这个砝码的状态为10

**现在我们解决了三个状态怎么用类似二进制枚举的方式来进行枚举**
其他的问题都很简单了
代码如下：
~~~~java
import java.util.Scanner;

public class WeightMeasurement01 {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int T = scanner.nextInt(); // 测试用例的数量

        for (int t = 0; t < T; t++) {
            int N = scanner.nextInt(); // 砝码的数量
            int[] weights = new int[N];

            // 读取砝码的重量
            for (int i = 0; i < N; i++) {
                weights[i] = scanner.nextInt();
            }

            int K = scanner.nextInt(); // 需要测量的物体数量

            // 读取需要测量的物体的重量
            for (int k = 0; k < K; k++) {
                int M = scanner.nextInt(); // 物体的重量
                if (canMeasure(weights, M)) {
                    System.out.println("YES");
                } else {
                    System.out.println("NO");
                }
            }
        }

        scanner.close();
    }

    public static boolean canMeasure(int[] weights, int targetWeight) {
        int N = weights.length;
        int totalStates = (int) Math.pow(3, N); // 总状态数

        for (int state = 0; state < totalStates; state++) {
            int leftSum = 0;
            int rightSum = 0;

            for (int i = 0; i < N; i++) {
                // 使用左移和 按位与 运算获取第i个砝码的状态
                int bitIndex = 2 * i;
                int mask = 3 << bitIndex; // 生成掩码
                int subStateBit = (state & mask) >> bitIndex; // 获取状态

                switch (subStateBit) {
                    case 0: // 不使用该砝码
                        break;
                    case 1: // 放在左边
                        leftSum += weights[i];
                        break;
                    case 2: // 放在右边
                        rightSum += weights[i];
                        break;
                }
            }

            // 计算两侧重量的差值
            int balance = Math.abs(leftSum - rightSum);

            if (balance == targetWeight) {
                return true;
            }
        }

        return false;
    }
}
~~~~
能产生预期结果 但是很遗憾

**超时**

这个算法的时间复杂度达到了O(3^N)
每次判断是否能进行称量的时候
都要走一遍所有的状态

那么我们能不能做一些优化
当然可以
这不是废话吗

### 二进制枚举第一次优化：减少状态数
把三种状态减少为两种状态：
使用和不使用
同时，取消左重量和右重量
以总重量作为衡量的标准
但是这里出现了一个问题
形如：7+5-1=11这种重量的出现，是一定需要这些砝码出现在异侧的。我们取消了左重量和右重量，该怎么表示他们的异侧状态呢？
确实没法表示
但既然我们忽略了他们的“方向性”我们就不要在这条死胡同里面走到黑了
我们改换一条路 既然研究重量 这里面的重量是怎么来的呢
重量是由砝码组成的
我们可以非常容易的实现加和，只需要每次找到使用的砝码并且进行+=
而对于上面说的那种状态 只需要在我们使用的砝码产生的sum当中，减去一个或者几个我们使用的砝码 就能得到我们需要的状态了
~~~~java
import java.util.Scanner;

public class WeightMeasurement01 {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int T = scanner.nextInt(); // 测试用例的数量

        for (int t = 0; t < T; t++) {
            int N = scanner.nextInt(); // 砝码的数量
            int[] weights = new int[N];

            // 读取砝码的重量
            for (int i = 0; i < N; i++) {
                weights[i] = scanner.nextInt();
            }

            int K = scanner.nextInt(); // 需要测量的物体数量

            // 读取需要测量的物体的重量
            for (int k = 0; k < K; k++) {
                int M = scanner.nextInt(); // 物体的重量
                if (canMeasure(weights, M)) {
                    System.out.println("YES");
                } else {
                    System.out.println("NO");
                }
            }
        }

        scanner.close();
    }

    public static boolean canMeasure(int[] weights, int targetWeight) {
        int N = weights.length;
        int totalStates = (int) Math.pow(2, N); // 总状态数

        for (int state = 0; state < totalStates; state++) {
            int sum = 0;

            for (int i = 0; i < N; i++) {
                // 使用位运算获取第i个砝码的状态
                if ((state & (1 << i)) != 0) {
                    sum += weights[i];
                }
            }

            if (sum == targetWeight) {
                return true;
            }

            // 检查从总和中减去某些砝码的重量后是否可以测量出目标重量
            for (int i = 0; i < N; i++) {
                if ((state & (1 << i)) != 0) {
                    if (Math.abs(sum - 2 * weights[i]) == targetWeight) {
                        return true;
                    }
                }
            }
        }

        return false;
    }
}
~~~~

仍然超时
时间复杂度为O(2^N)

### 二进制枚举第二次优化：添加结果数组
添加结果数组的一个非常大的优势就在于
只需要过一次所有的状态就可以了
过完一遍，我们就能够把可能产生的所有的重量都存储下来
在查询的时候，只需要去我们的结果数组当中查询就行
~~~~java
import java.util.Scanner;

public class WeightMeasurement01 {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int T = scanner.nextInt(); // 测试用例的数量

        for (int t = 0; t < T; t++) {
            int N = scanner.nextInt(); // 砝码的数量
            int[] weights = new int[N];

            // 读取砝码的重量
            for (int i = 0; i < N; i++) {
                weights[i] = scanner.nextInt();
            }

            int K = scanner.nextInt(); // 需要测量的物体数量

            // 计算所有可能的重量组合并存储到结果数组中
            boolean[] resultArray = new boolean[2005]; // 假设最大重量不超过2004

            for (int state = 0; state < (1 << N); state++) {
                int sum = 0;

                for (int i = 0; i < N; i++) {
                    // 使用位运算获取第i个砝码的状态
                    if ((state & (1 << i)) != 0) {
                        sum += weights[i];
                    }
                }

                // 标记当前和为可达
                resultArray[sum] = true;

                // 检查从总和中减去某些砝码的重量后是否可以测量出目标重量
                for (int i = 0; i < N; i++) {
                    if ((state & (1 << i)) != 0) {
                        int diff = Math.abs(sum - 2 * weights[i]);
                        if (diff <= 2004) {
                            resultArray[diff] = true;
                        }
                    }
                }
            }

            // 读取需要测量的物体的重量
            for (int k = 0; k < K; k++) {
                int M = scanner.nextInt(); // 物体的重量
                if (resultArray[M]) {
                    System.out.println("YES");
                } else {
                    System.out.println("NO");
                }
            }
        }

        scanner.close();
    }
}
~~~~
hdoj可以ac
