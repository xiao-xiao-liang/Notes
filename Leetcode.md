# 常用类及其方法

## 1.BigInteger类

处理超出整数范围的超大整数

### 题目描述

输入格式 分两行输入。 𝑎,𝑏≤10^500^。 输出格式 输出只有一行，代表 a+b 的值。

如：$a=1234567890123456789012345678901234567890123456789012345678901234567890$，$b=9876543210987654321098765432109876543210987654321098765432109876543210$，
结果为：$11111111101111111110111111111011111111101111111110111111111011111111100$

### 代码

```java
import java.math.BigInteger;
import java.util.Scanner;

public class BigIntegerAddition {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // 读取两个大整数
        BigInteger a = new BigInteger(scanner.nextLine());
        BigInteger b = new BigInteger(scanner.nextLine());

        // 计算它们的和
        BigInteger sum = a.add(b);

        // 输出结果
        System.out.println(sum);

        scanner.close();
    }
}
```



## 2. Comparator 类

Comparator 类常作为 sorted() 方法的参数传递给 sorted 方法，用来解决给**集合排序**，**自定义排序**规则的问题 。

### 2.1 compare()方法

`Comparator`接口的`compare`方法用于比较两个对象，并指定它们的排序顺序。这个方法有两个参数，分别是要比较的两个对象。根据比较结果，返回一个整数值，表示两个对象的大小关系。

通常情况下，返回值的规则如下：

- 如果第一个对象小于第二个对象，则返回负整数。
- 如果第一个对象等于第二个对象，则返回零。
- 如果第一个对象大于第二个对象，则返回正整数。

```java
@Override
public int compare(Integer o1, Integer o2) {
    return o1-o2;
}
```

如果 $o1-o2$  则是升序排序，如果是 $o2-o1$​ 则是降序排序。

#### 举例

* 对数组进行排序

```java
// 自定义排序规则
Arrays.sort(numbers, (a, b) -> {
    // 比较 a+b 和 b+a 的大小
    String order1 = a + b;
    String order2 = b + a;
    return order2.compareTo(order1); // 降序排列
});
```



## 3.String类

### 3.1 compareTo()方法

`String`类的`compareTo`方法在Java中用于比较两个字符串的字典顺序（基于Unicode值的顺序）。它实现了`Comparable<String>`接口，因此可以对字符串数组或列表进行排序。以下是`String`类`compareTo`方法的工作原理及其实现过程。

#### 工作原理

1. **字符逐一比较**：从第一个字符开始逐个比较两个字符串的字符。
2. **字符不同**：如果字符不同，返回两个字符的差值（基于Unicode码点值）。
3. **字符相同**：继续比较下一个字符。
4. **字符串长度不同**：如果一个字符串是另一个字符串的前缀，返回两个字符串长度的差值。

假设我们有两个字符串`"apple"`和`"apricot"`，逐字符比较过程如下：

- 比较`'a'`和`'a'`，相同，继续。
- 比较`'p'`和`'p'`，相同，继续。
- 比较`'p'`和`'r'`，不同，返回`'p' - 'r'`的差值，即负数，表示`"apple"`小于`"apricot"`。

对于`"apple"`和`"applepie"`：

- 比较`'a'`、`'p'`、`'p'`、`'l'`、`'e'`，所有字符相同。
- 字符长度不同，返回`5 - 8`，即负数，表示`"apple"`小于`"applepie"`。

# 前置知识

## 前缀和

对于数组 $nums$，定义它的前缀和 $s[0]=0$，$\textit{s}[i+1] = \sum\limits_{j=0}^{i}nums[j]$。

根据这个定义，有 $s[i+1]=s[i]+nums[i]$。

例如 $nums=[1,2,1,2]$，对应的前缀和数组为 $s=[0,1,3,4,6]$。

通过前缀和，我们可以把子数组的元素和转换成两个前缀和的差，即

​					$\sum\limits_{j=left}^{right}nums[j]=\sum\limits_{j=0}^{right}nums[j]-\sum\limits_{j=0}^{left-1}nums[j]=s[right+1]-s[left]$
例如 $nums$ 的子数组 $[2,1,2]$ 的和就可以用 $s[4]−s[1]=6−1=5$ 算出来。

> 注1：为方便计算，常用左闭右开区间 $[left,right)$ 来表示从 $nums[left]$ 到 $nums[right−1]$ 的子数组，此时子数组的和为 $s[right]−s[left]$，子数组的长度为 $right−left$。
>
> 注 2：$s[0]=0$ 表示一个空数组的元素和。为什么要额外定义它？想一想，如果要计算的子数组恰好是一个前缀（从 $nums[0]$ 开始），你要用 $s[right]$ 减去谁呢？通过定义 $s[0]=0$​，任意子数组（包括前缀）都可以表示为两个前缀和的差。

<img src="D:\Software\Typora\复制的图片\image-20240526215252759.png" alt="image-20240526215252759" style="zoom:80%;" />

# Leetcode

## 前缀和

### Leetcode [1738. 找出第 K 大的异或坐标值](https://leetcode.cn/problems/find-kth-largest-xor-coordinate-value/)

给你一个二维矩阵 `matrix` 和一个整数 `k` ，矩阵大小为 `m x n` 由非负整数组成。

矩阵中坐标 `(a, b)` 的 **值** 可由对所有满足 `0 <= i <= a < m` 且 `0 <= j <= b < n` 的元素 `matrix[i][j]`（**下标从 0 开始计数**）执行异或运算得到。

请你找出 `matrix` 的所有坐标中第 `k` 大的值（**`k` 的值从 1 开始计数**）。

 

**示例 1：**

> 输入：matrix = [[5,2],[1,6]], k = 1
> 输出：7
> 解释：坐标 (0,1) 的值是 5 XOR 2 = 7 ，为最大的值。

**示例 2：**

> 输入：matrix = [[5,2],[1,6]], k = 2
> 输出：5
> 解释：坐标 (0,0) 的值是 5 = 5 ，为第 2 大的值。

**示例 3：**

> 输入：matrix = [[5,2],[1,6]], k = 3
> 输出：4
> 解释：坐标 (1,0) 的值是 5 XOR 1 = 4 ，为第 3 大的值。

**示例 4：**

> 输入：matrix = [[5,2],[1,6]], k = 4
> 输出：0
> 解释：坐标 (1,1) 的值是 5 XOR 2 XOR 1 XOR 6 = 0 ，为第 4 大的值。

 

**提示：**

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 1000`
- `0 <= matrix[i][j] <= 106`
- `1 <= k <= m * n`

#### 解题思路

类似二维前缀和，定义 $s[i+1]$ 表示左上角在 $(0,0)$，右下角在 $(i,j)$ 的子矩阵异或和，按照【图解】一张图秒懂二维前缀和 中的做法，有

​						$s[i+1][j+1]=s[i+1][j]⊕s[i][j+1]⊕s[i][j]⊕matrix[i][j]$​

由于一个数异或自己等于 000，$s[i+1][j]⊕s[i][j+1]$ 会导致 $s[i][j]$ 这部分被抵消掉，所以要异或进来。

```java
class Solution {
    public int kthLargestValue(int[][] matrix, int k) {
        int m = matrix.length;
        int n = matrix[0].length;
        int[] a = new int[m * n];
        int[][] s = new int[m + 1][n + 1];
        int idx = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                s[i + 1][j + 1] = s[i + 1][j] ^ s[i][j + 1] ^ s[i][j] ^ matrix[i][j];
                a[idx++] = s[i + 1][j + 1];
            }
        }
        Arrays.sort(a);
        return a[idx - k];
    }
}
```



遍历 $matrix$ 的同时，计算 $colSum[j]$，表示第 $j$ 列的当前遍历过的元素的异或和。

那么左上角在$(0,0)$，右下角在 $(i,j)$ 的子矩阵异或和，就是

​						$colSum[0]⊕colSum[1]⊕⋯⊕colSum[j]$
这也可以一边遍历 $matrix$ 一边计算。

```java
public class Solution {
    public int kthLargestValue(int[][] matrix, int k) {
        int m = matrix.length;
        int n = matrix[0].length;
        int[] a = new int[m * n];
        int[] colSum = new int[n];
        int i = 0;
        for (int[] row : matrix) {
            int s = 0;
            for (int j = 0; j < row.length; j++) {
                colSum[j] ^= row[j];
                s ^= colSum[j];
                a[i++] = s;
            }
        }
        Arrays.sort(a);
        return a[i - k];
    }
}
```



## 栈

### Leetcode [1673. 找出最具竞争力的子序列](https://leetcode.cn/problems/find-the-most-competitive-subsequence/)

给你一个整数数组 `nums` 和一个正整数 `k` ，返回长度为 `k` 且最具 **竞争力** 的 `nums` 子序列。

数组的子序列是从数组中删除一些元素（可能不删除元素）得到的序列。

在子序列 `a` 和子序列 `b` 第一个不相同的位置上，如果 `a` 中的数字小于 `b` 中对应的数字，那么我们称子序列 `a` 比子序列 `b`（相同长度下）更具 **竞争力** 。 例如，`[1,3,4]` 比 `[1,3,5]` 更具竞争力，在第一个不相同的位置，也就是最后一个位置上， `4` 小于 `5` 。

 

**示例 1：**

> 输入：nums = [3,5,2,6], k = 2
> 输出：[2,6]
> 解释：在所有可能的子序列集合 {[3,5], [3,2], [3,6], [5,2], [5,6], [2,6]} 中，[2,6] 最具竞争力。

**示例 2：**

> 输入：nums = [2,4,3,3,5,4,9,6], k = 4
> 输出：[2,3,3,4]

 

**提示：**

- `1 <= nums.length <= 105`
- `0 <= nums[i] <= 109`
- `1 <= k <= nums.length`

#### 解题思路

**题意**：返回 $\textit{nums}$ 的长度恰好为 $k$​ 的字典序最小子序列。

由于要返回的是 $nums$ 的一个子序列，我们尝试在遍历 $nums$ 的过程中，去生成字典序最小的子序列。

以示例 2 为例，$nums=[2,4,3,3,5,4,9,6], k=4$。

$nums[0]=2$，目前生成的子序列为 $[2]$。
$nums[1]=4$，由于 $4>2$，不能把子序列中的 $2$ 替换掉，因为这会让字典序变大。由于目标子序列长度为 $k=4$，所以直接把 $4$ 加到子序列的末尾，目前生成的子序列为 $[2,4]$。
$nums[2]=3$，由于 $3<4$，把子序列末尾的 $4$ 去掉，添加 $3$，会让字典序变小。注意，不能继续把 $2$ 也去掉，这会让字典序变大。目前生成的子序列为 $[2,3]$。
$nums[3]=3$，无法让字典序变小，且当前子序列长度不足 $k=4$，所以直接把 $3$ 加到子序列的末尾，目前生成的子序列为 $[2,3,3]$。 $nums[4]=5$，无法让字典序变小，且当前子序列长度不足 $k=4$，所以直接把 $5$ 加到子序列的末尾，目前生成的子序列为 $[2,3,3,5]$。
$nums[5]=4$，由于 $4<5$，把子序列末尾的 $5$ 去掉，添加 $4$，会让字典序变小。注意，不能继续把 $3$ 也去掉，这会让字典序变大。目前生成的子序列为 $[2,3,3,4]$。注意：假如 $k=7$，这里不能把子序列末尾的 $5$ 去掉，因为一旦去掉，即使把后面的所有元素都加到子序列中（得到 $[2,3,3,4,9,6]$），长度也无法达到 $7$，不符合题目要求。
$nums[6]=9$，无法让字典序变小，且当前子序列长度已经等于 $k=4$，所以什么也不做，目前生成的子序列为[$2,3,3,4]$。
$nums[7]=6$，无法让字典序变小，且当前子序列长度已经等于 $k=4$，所以什么也不做，目前生成的子序列为 $[2,3,3,4]$。
按照上面的流程，为了维护生成的子序列，我们需要一个后进先出的数据结构：栈。当然，用列表/数组表示栈也可以。

由于题目要求生成长为 $k$ 的子序列，我们不能无限制地弹出栈顶元素。在弹出栈顶元素之前，必须保证栈中元素个数加上剩余元素个数是大于$k$ 的。如果代码中不写这个判断，最后可能会得到一个长度小于 $k$ 的子序列。

算法如下：

创建一个空栈。
从左到右遍历 $nums$。
设 $x=nums[i]$。如果栈不为空，且 $x$ 小于栈顶，且栈的大小加上剩余元素个数（$n−i$）大于 $k$，则可以弹出栈顶。不断循环直到不满足这三个条件之一。
如果栈的大小小于 $k$，把 $x$ 入栈。
遍历结束，栈（从底到顶的顺序）就是答案。

```java
public class Solution {
    public int[] mostCompetitive(int[] nums, int k) {
        int n = nums.length;
        int[] st = new int[k]; // 用数组模拟栈（栈容量为 k）
        int m = 0; // 栈的大小
        for (int i = 0; i < n; i++) {
            int x = nums[i];
            while (m > 0 && x < st[m - 1] && m + n - i > k) {
                m--; // 出栈
            }
            if (m < k) {
                st[m++] = x; // 入栈
            }
        }
        return st;
    }
}
```

## 单调栈

### Leetcode [503. 下一个更大元素 II](https://leetcode.cn/problems/next-greater-element-ii/)

给定一个循环数组 `nums` （ `nums[nums.length - 1]` 的下一个元素是 `nums[0]` ），返回 *`nums` 中每个元素的 **下一个更大元素*** 。

数字 `x` 的 **下一个更大的元素** 是按数组遍历顺序，这个数字之后的第一个比它更大的数，这意味着你应该循环地搜索它的下一个更大的数。如果不存在，则输出 `-1` 。

 

**示例 1:**

> **输入**: nums = [1,2,1]
> **输出**: [2,-1,2]
> **解释:** 第一个 1 的下一个更大的数是 2；
> 数字 2 找不到下一个更大的数； 
> 第二个 1 的下一个最大的数需要循环搜索，结果也是 2。

**示例 2:**

> **输入**: nums = [1,2,3,4,3]
> **输出**: [2,3,4,-1,4]

 

**提示:**

- `1 <= nums.length <= 104`
- `-109 <= nums[i] <= 109`

#### 思路

本题 $nums$ 是一个循环数组，$nums[n−1]$ 右边是 $nums[0]$。我们可以把 $nums$ 复制一份，拼在 $nums$ 右边，这样就把环形数组变成一般数组了。例如 $[1,2,1]$ 变成 $[1,2,1,1,2,1]$。

##### 方法二：从左到右

栈中记录还没算出「下一个更大元素」的那些数的下标。

只要遍历到比栈顶元素值更大的数，就意味着栈顶元素找到了答案，记录答案，然后从栈顶弹出。

代码实现时，无需真的把数组复制一份，而是用下标模 $n$ 的方式取到对应的元素值。

```java
class Solution {
    public int[] nextGreaterElements(int[] nums) {
        int n = nums.length;
        int[] ans = new int[n];
        Arrays.fill(ans, -1);
        Deque<Integer> stack = new ArrayDeque<>();
        for (int i = 0; i < 2 * n; i++) {
            int x = nums[i % n];
            while (!stack.isEmpty() && x > nums[stack.peek()]) {
                ans[stack.pop()] = x;
            }
            if (i < n) {
                stack.push(i);
            }
        }
        return ans;
    }
}
```



## 数组

### Leetcode [2079. 给植物浇水](https://leetcode.cn/problems/watering-plants/)

你打算用一个水罐给花园里的 `n` 株植物浇水。植物排成一行，从左到右进行标记，编号从 `0` 到 `n - 1` 。其中，第 `i` 株植物的位置是 `x = i` 。`x = -1` 处有一条河，你可以在那里重新灌满你的水罐。

每一株植物都需要浇特定量的水。你将会按下面描述的方式完成浇水：

- 按从左到右的顺序给植物浇水。
- 在给当前植物浇完水之后，如果你没有足够的水 **完全** 浇灌下一株植物，那么你就需要返回河边重新装满水罐。
- 你 **不能** 提前重新灌满水罐。

最初，你在河边（也就是，`x = -1`），在 x 轴上每移动 **一个单位** 都需要 **一步** 。

给你一个下标从 **0** 开始的整数数组 `plants` ，数组由 `n` 个整数组成。其中，`plants[i]` 为第 `i` 株植物需要的水量。另有一个整数 `capacity` 表示水罐的容量，返回浇灌所有植物需要的 **步数** 。

 

**示例 1：**

> 输入：plants = [2,2,3,3], capacity = 5
> 输出：14
> 解释：从河边开始，此时水罐是装满的：
> - 走到植物 0 (1 步) ，浇水。水罐中还有 3 单位的水。
> - 走到植物 1 (1 步) ，浇水。水罐中还有 1 单位的水。
> - 由于不能完全浇灌植物 2 ，回到河边取水 (2 步)。
> - 走到植物 2 (3 步) ，浇水。水罐中还有 2 单位的水。
> - 由于不能完全浇灌植物 3 ，回到河边取水 (3 步)。
> - 走到植物 3 (4 步) ，浇水。
> 需要的步数是 = 1 + 1 + 2 + 3 + 3 + 4 = 14 。

**示例 2：**

> 输入：plants = [1,1,1,4,2,3], capacity = 4
> 输出：30
> 解释：从河边开始，此时水罐是装满的：
> - 走到植物 0，1，2 (3 步) ，浇水。回到河边取水 (3 步)。
> - 走到植物 3 (4 步) ，浇水。回到河边取水 (4 步)。
> - 走到植物 4 (5 步) ，浇水。回到河边取水 (5 步)。
> - 走到植物 5 (6 步) ，浇水。
> 需要的步数是 = 3 + 3 + 4 + 4 + 5 + 5 + 6 = 30 。

**示例 3：**

> 输入：plants = [7,7,7,7,7,7,7], capacity = 8
> 输出：49
> 解释：每次浇水都需要重新灌满水罐。
> 需要的步数是 = 1 + 1 + 2 + 2 + 3 + 3 + 4 + 4 + 5 + 5 + 6 + 6 + 7 = 49 。



**提示：**

- `n == plants.length`
- `1 <= n <= 1000`
- `1 <= plants[i] <= 106`
- `max(plants[i]) <= capacity <= 109`

#### 解题思路

1. 由于需要浇灌所有植物，至少要走 n 步，故初始化答案 ans = n。
2. 初始化水罐中的水量 water = capacity。
3. 从左到右遍历 plants。如果 water < plants[i]，那么我们在上一个位置 x=i−1 就可以返回 x=−1 重新灌满水，再返回到 x=i−1，需要额外走 2i 步，加入答案，把 water 重置为 capacity。然后浇水，把 water 减少 plants[i]。
4. 返回答案。

```java
class Solution {
    public int wateringPlants(int[] plants, int capacity) {
        int n = plants.length;
        int ans = n;
        int water = capacity;
        for (int i = 0; i < n; i++) {
            if (water < plants[i]) {
                ans += i * 2;
                water = capacity;
            }
            water -= plants[i];
        }
        return ans;
    }
}
```

#### 我的思路

用一个数组step记录浇每一个花需要的步数，遍历plants，当水壶的水量 < 第i朵花需要的水时，在上一个位置 x=i−1 就可以返回 x=−1 重新灌满水，需要i步，再从 x = -1 回到 i 把水浇了，需要 i  + 1 步，此时水壶水量 - planst[i]

```java
public int wateringPlants(int[] plants, int capacity) {
    int[] step = new int[plants.length];
    int res = 0, tmp = capacity;
    for (int i = 0; i < plants.length; i++) {
        if (capacity >= plants[i]) {
            capacity -= plants[i];
            step[i] = 1;
        } else {
            step[i] = i+i+1;
            capacity = tmp-plants[i];
        }
    }
    for (int s : step) {
        res += s;
    }
    return res;
}
```



### Leetcode [2391. 收集垃圾的最少总时间](https://leetcode.cn/problems/minimum-amount-of-time-to-collect-garbage/)

给你一个下标从 **0** 开始的字符串数组 `garbage` ，其中 `garbage[i]` 表示第 `i` 个房子的垃圾集合。`garbage[i]` 只包含字符 `'M'` ，`'P'` 和 `'G'` ，但可能包含多个相同字符，每个字符分别表示一单位的金属、纸和玻璃。垃圾车收拾 **一** 单位的任何一种垃圾都需要花费 `1` 分钟。

同时给你一个下标从 **0** 开始的整数数组 `travel` ，其中 `travel[i]` 是垃圾车从房子 `i` 行驶到房子 `i + 1` 需要的分钟数。

城市里总共有三辆垃圾车，分别收拾三种垃圾。每辆垃圾车都从房子 `0` 出发，**按顺序** 到达每一栋房子。但它们 **不是必须** 到达所有的房子。

任何时刻只有 **一辆** 垃圾车处在使用状态。当一辆垃圾车在行驶或者收拾垃圾的时候，另外两辆车 **不能** 做任何事情。

请你返回收拾完所有垃圾需要花费的 **最少** 总分钟数。

**示例 1：**

> 输入：garbage = ["G","P","GP","GG"], travel = [2,4,3]
> 输出：21
> 解释：
> 收拾纸的垃圾车：
> 1. 从房子 0 行驶到房子 1
> 2. 收拾房子 1 的纸垃圾
> 3. 从房子 1 行驶到房子 2
> 4. 收拾房子 2 的纸垃圾
> 收拾纸的垃圾车总共花费 8 分钟收拾完所有的纸垃圾。
> 收拾玻璃的垃圾车：
> 1. 收拾房子 0 的玻璃垃圾
> 2. 从房子 0 行驶到房子 1
> 3. 从房子 1 行驶到房子 2
> 4. 收拾房子 2 的玻璃垃圾
> 5. 从房子 2 行驶到房子 3
> 6. 收拾房子 3 的玻璃垃圾
> 收拾玻璃的垃圾车总共花费 13 分钟收拾完所有的玻璃垃圾。
> 由于没有金属垃圾，收拾金属的垃圾车不需要花费任何时间。
> 所以总共花费 8 + 13 = 21 分钟收拾完所有垃圾。

**示例 2：**

> 输入：garbage = ["MMM","PGM","GP"], travel = [3,10]
> 输出：37
> 解释：
> 收拾金属的垃圾车花费 7 分钟收拾完所有的金属垃圾。
> 收拾纸的垃圾车花费 15 分钟收拾完所有的纸垃圾。
> 收拾玻璃的垃圾车花费 15 分钟收拾完所有的玻璃垃圾。
> 总共花费 7 + 15 + 15 = 37 分钟收拾完所有的垃圾。

 

**提示：**

- `2 <= garbage.length <= 105`
- `garbage[i]` 只包含字母 `'M'` ，`'P'` 和 `'G'` 。
- `1 <= garbage[i].length <= 10`
- `travel.length == garbage.length - 1`
- `1 <= travel[i] <= 100`

#### 解题思路

由于「任何时刻只有一辆垃圾车处在使用状态」，我们可以先让收集 M（金属）的垃圾车从左到右跑一趟，然后让收集 P（纸）的垃圾车从左到右跑一趟，最后让收集 G（玻璃）的垃圾车从左到右跑一趟。

总用时可以拆分成两个部分：

收集垃圾的总用时，这等于所有 garbage[i] 的长度之和。
行驶的总用时，这等于每辆垃圾车的行驶用时之和。对于收集 M 的垃圾车，设 garbage[i] 是最后一个包含 M 的字符串，那么收集 M 的垃圾车的行驶用时为 travel[0]+travel[1]+⋯+travel[i−1]。同理可得另外两辆垃圾车的行驶用时。
下面介绍三种实现方法：

第一种方法针对本题数据，看上去会多次遍历数组，但实际跑的飞快。理由见复杂度分析。
另外两种方法适用性更广，即使有 10^5^种垃圾也可以通过。

**方法一：多次遍历**
先让所有垃圾车都跑满全程，再倒着遍历 garbage，减去多跑的时间。

对于收集 M 的垃圾车，设 *garbage[i]* 是最后一个包含 M 的字符串，那么收集 M 的垃圾车的行驶用时，等于跑满全程的用时，减去多跑的用时 *travel[i]+travel[i+1]+⋯+travel[n−2]*，其中 n 是 *garbage* 的长度。注意 *travel* 的下标和 *garbage* 的下标相差 1。

```java
class Solution {
    public int garbageCollection(String[] garbage, int[] travel) {
        int ans = 0;
        for (String g : garbage) {
            ans += g.length();
        }
        for (int t : travel) {
            ans += t * 3;
        }
        for (char c : new char[]{'M', 'P', 'G'}) {
            for (int i = garbage.length - 1; i > 0 && garbage[i].indexOf(c) < 0; i--) {
                ans -= travel[i - 1]; // 没有垃圾 c，多跑了
            }
        }
        return ans;
    }
}
```



### Leetcode [2644. 找出可整除性得分最大的整数](https://leetcode.cn/problems/find-the-maximum-divisibility-score/)

给你两个下标从 **0** 开始的整数数组 `nums` 和 `divisors` 。

`divisors[i]` 的 **可整除性得分** 等于满足 `nums[j]` 能被 `divisors[i]` 整除的下标 `j` 的数量。

返回 **可整除性得分** 最大的整数 `divisors[i]` 。如果有多个整数具有最大得分，则返回数值最小的一个。



**示例 1：**

> 输入：nums = [4,7,9,3,9], divisors = [5,2,3]
> 输出：3
> 解释：divisors 中每个元素的可整除性得分为：
> divisors[0] 的可整除性得分为 0 ，因为 nums 中没有任何数字能被 5 整除。
> divisors[1] 的可整除性得分为 1 ，因为 nums[0] 能被 2 整除。 
> divisors[2] 的可整除性得分为 3 ，因为 nums[2]、nums[3] 和 nums[4] 都能被 3 整除。 
> 因此，返回 divisors[2] ，它的可整除性得分最大。

**示例 2：**

> 输入：nums = [20,14,21,10], divisors = [5,7,5]
> 输出：5
> 解释：divisors 中每个元素的可整除性得分为：
> divisors[0] 的可整除性得分为 2 ，因为 nums[0] 和 nums[3] 都能被 5 整除。
> divisors[1] 的可整除性得分为 2 ，因为 nums[1] 和 nums[2] 都能被 7 整除。
> divisors[2] 的可整除性得分为 2 ，因为 nums[0] 和 nums[3] 都能被5整除。 
> 由于 divisors[0]、divisors[1] 和 divisors[2] 的可整除性得分都是最大的，因此，我们返回数值最小的一个，即 divisors[2] 。

**示例 3：**

> 输入：nums = [12], divisors = [10,16]
> 输出：10
> 解释：divisors 中每个元素的可整除性得分为：
> divisors[0] 的可整除性得分为 0 ，因为 nums 中没有任何数字能被 10 整除。
> divisors[1] 的可整除性得分为 0 ，因为 nums 中没有任何数字能被 16 整除。 
> 由于 divisors[0] 和 divisors[1] 的可整除性得分都是最大的，因此，我们返回数值最小的一个，即 divisors[0] 。

 

**提示：**

- `1 <= nums.length, divisors.length <= 1000`
- `1 <= nums[i], divisors[i] <= 109`

#### 解题思路

**优化前**
遍历 $d=divisors[i]$，暴力枚举 $nums$ 中的数，统计能被 $d$ 整除的数的个数 $cnt$。取 $cnt$ 最大的 $d$ 作为答案。如果有多个最大的 $cnt$，取其中最小的 $d$。

```java
class Solution {
    public int maxDivScore(int[] nums, int[] divisors) {
        int ans = 0;
        int maxCnt = -1;
        for (int d : divisors) {
            int cnt = 0;
            for (int x : nums) {
                if (x % d == 0) {
                    cnt++;
                }
            }
            if (cnt > maxCnt || cnt == maxCnt && d < ans) {
                maxCnt = cnt;
                ans = d;
            }
        }
        return ans;
    }
}
```

**优化 1**
注意到，小于 $d$ 的正整数无法被 ddd 整除。

把 $nums$ 排序，从大到小遍历 $nums$。只需遍历 $≥d$ 的 $nums[i]$，当 $nums[i]<d$ 时，退出内层循环。

```java
class Solution {
    public int maxDivScore(int[] nums, int[] divisors) {
        Arrays.sort(nums);
        int ans = 0;
        int maxCnt = -1;
        for (int d : divisors) {
            int cnt = 0;
            for (int i = nums.length - 1; i >= 0; i--) {
                int x = nums[i];
                if (x < d) {
                    break;
                }
                if (x % d == 0) {
                    cnt++;
                }
            }
            if (cnt > maxCnt || cnt == maxCnt && d < ans) {
                maxCnt = cnt;
                ans = d;
            }
        }
        return ans;
    }
}
```



### Leetcode [1535. 找出数组游戏的赢家](https://leetcode.cn/problems/find-the-winner-of-an-array-game/)

给你一个由 **不同** 整数组成的整数数组 `arr` 和一个整数 `k` 。

每回合游戏都在数组的前两个元素（即 `arr[0]` 和 `arr[1]` ）之间进行。比较 `arr[0]` 与 `arr[1]` 的大小，较大的整数将会取得这一回合的胜利并保留在位置 `0` ，较小的整数移至数组的末尾。当一个整数赢得 `k` 个连续回合时，游戏结束，该整数就是比赛的 **赢家** 。

返回赢得比赛的整数。

题目数据 **保证** 游戏存在赢家。

 

**示例 1：**

> 输入：arr = [2,1,3,5,4,6,7], k = 2
> 输出：5
> 解释：一起看一下本场游戏每回合的情况：
>
> <img src="D:\Software\Typora\复制的图片\q-example.png" alt="img" style="zoom:67%;" />
>
> 因此将进行 4 回合比赛，其中 5 是赢家，因为它连胜 2 回合。

**示例 2：**

> 输入：arr = [3,2,1], k = 10
> 输出：3
> 解释：3 将会在前 10 个回合中连续获胜。

**示例 3：**

> 输入：arr = [1,9,8,2,3,7,6,4,5], k = 7
> 输出：9

**示例 4：**

>输入：arr = [1,11,22,33,44,55,66,77,88,99], k = 1000000000
>输出：99

 

**提示：**

- `2 <= arr.length <= 10^5`
- `1 <= arr[i] <= 10^6`
- `arr` 所含的整数 **各不相同** 。
- `1 <= k <= 10^9`

#### 解题思路

由于较小的元素会移至数组的末尾，在重新遇到被移至数组末尾的元素之前，$arr$ 的每个元素都会被访问到。

考察游戏执行的流程，本质上是在从左到右遍历 $arr$，求数组最大值（打擂台）。我们要找首个连续 $k$ 回合都是最大值的数。

示例 1 的 $arr=[2,1,3,5,4,6,7], k=2$，从左到右遍历的过程中，历史最大值依次为 $2,3,5,6,7$，其中元素 $5$ 是首个连续 $k$ 回合都是最大值的数。

注：如果把下标 $0$ 也算上的话，$arr[0]=2$ 要连续 $k+1=3$ 个回合都是最大值才能算作答案。

如果遍历完 $arr$ 也没找到这样的数，那么答案就是 $arr$ 的最大值 $mx$，因为此时比 $mx$ 小的数都会移到 $mx$ 的右边，所以后面比大小都是 $mx$ 胜利。

具体算法如下：

初始化 $mx=arr[0], win=0$，从 $arr[1]$ 开始遍历数组。其中 $win$ 用来统计 $mx$ 连续多少个回合是最大值（获胜）。
如果 $arr[i]>mx$，更新 $mx=arr[i]$ 以及 $win=0$。
把 $win$ 加一，如果 $win=k$ 就退出循环。
遍历结束（或者中途退出循环），返回 $mx$。

> 注：由于从 $arr[1]$ 开始遍历没法用 $foreach$ 语法糖，也可以初始化 $win=−1$，从 $arr[0]$​ 开始遍历。

```java
class Solution {
    public int getWinner(int[] arr, int k) {
        int mx = arr[0];
        int win = 0;
        for (int i = 1; i < arr.length && win < k; i++) {
            if (arr[i] > mx) { // 新的最大值
                mx = arr[i];
                win = 0;
            }
            win++; // 获胜回合 +1
        }
        return mx;
    }
}
```



### 滑动窗口

#### Leetcode [1652. 拆炸弹](https://leetcode.cn/problems/defuse-the-bomb/)

##### 题目描述

你有一个炸弹需要拆除，时间紧迫！你的情报员会给你一个长度为 `n` 的 **循环** 数组 `code` 以及一个密钥 `k` 。

为了获得正确的密码，你需要替换掉每一个数字。所有数字会 **同时** 被替换。

- 如果 `k > 0` ，将第 `i` 个数字用 **接下来** `k` 个数字之和替换。
- 如果 `k < 0` ，将第 `i` 个数字用 **之前** `k` 个数字之和替换。
- 如果 `k == 0` ，将第 `i` 个数字用 `0` 替换。

由于 `code` 是循环的， `code[n-1]` 下一个元素是 `code[0]` ，且 `code[0]` 前一个元素是 `code[n-1]` 。

给你 **循环** 数组 `code` 和整数密钥 `k` ，请你返回解密后的结果来拆除炸弹！

 

**示例 1：**

>**输入**：code = [5,7,1,4], k = 3
>**输出**：[12,10,16,13]
>**解释**：每个数字都被接下来 3 个数字之和替换。解密后的密码为 [7+1+4, 1+4+5, 4+5+7, 5+7+1]。注意到数组是循环连接的。

**示例 2：**

>**输入**：code = [1,2,3,4], k = 0
>**输出**：[0,0,0,0]
>**解释**：当 k 为 0 时，所有数字都被 0 替换。

**示例 3：**

> **输入**：code = [2,4,9,3], k = -2
> **输出**：[12,5,6,13]
> **解释**：解密后的密码为 [3+9, 2+3, 4+2, 9+4] 。注意到数组是循环连接的。如果 k 是负数，那么和为 **之前** 的数字。

 

**提示：**

- `n == code.length`
- `1 <= n <= 100`
- `1 <= code[i] <= 100`
- `-(n - 1) <= k <= n - 1`



##### 解题思路

如果 k>0，例如 *code=[3,1,4,1,5,9]*, *k=3*：

1. 计算 ans[0]，即子数组[1,4,1] 的元素和 1+4+1=6。
2. 计算 ans[1]，即子数组[4,1,5] 的元素和，我们可以在 [1,4,1] 的基础上，增加 code[4]=5，减少 code[1]=1，得到 6+5−1=10。
3. 计算 ans[2]，即子数组[1,5,9] 的元素和，我们可以在 [4,1,5] 的基础上，增加 code[5]=9，减少 code[2]=4，得到10+9−4=15。
4. 计算 ans[3]，即子数组 [5,9,3] 的元素和，我们可以在 [1,5,9] 的基础上，增加 code[6 mod 6]=code[0]=3，减少 code[3]=1，得到 15+3−1=17。
5. 计算 ans[4]，即子数组 [9,3,1] 的元素和，我们可以在[5,9,3] 的基础上，增加 code[7 mod 6]=code[1]=1，减少 code[4]=5，得到 17+1−5=13。
6. 计算 ans[5]，即子数组 [3,1,4] 的元素和，我们可以在[9,3,1] 的基础上，增加 code[8 mod 6]=code[2]=4，减少 code[5]=9，得到 13+4−9=8。

对于 *k<0* 的情况也同理。注意无论 *k>0* 还是 *k<0*，窗口都是在向右移动的，所以确定好第一个窗口的位置，就可以把 k>0 和 k<0 两种情况合并起来了。

k>0，第一个窗口的的下标范围为 [1,k+1)。
k<0，第一个窗口的的下标范围为 [n−∣k∣,n)。
在窗口向右滑动时，设移入窗口的元素下标为 *r  mod  n*，则移出窗口的元素下标为 *(r−∣k∣)  mod  n*。

代码实现时，$k=0$ 的特判可以省略。

```java
class Solution {
    public int[] decrypt(int[] code, int k) {
        int n = code.length;
        int[] res = new int[n];
        int r = k > 0 ? k + 1 : n; // 确定第一个窗口的最大下标
        k = Math.abs(k);
        int sum = 0;
        // 确定res[0]的值
        for (int i = r - k; i < r; i++) {
            sum += code[i];
        }
        for (int i = 0; i < n; i++) {
            res[i] = sum;
            sum  = sum + code[r % n] - code[(r - k) % n];
            r++; // r++是为了使窗口向右移动
        }
        return res;
    }
}
```



#### Leetcode [2903. 找出满足差值条件的下标 I](https://leetcode.cn/problems/find-indices-with-index-and-value-difference-i/)

给你一个下标从 **0** 开始、长度为 `n` 的整数数组 `nums` ，以及整数 `indexDifference` 和整数 `valueDifference` 。

你的任务是从范围 `[0, n - 1]` 内找出 **2** 个满足下述所有条件的下标 `i` 和 `j` ：

- `abs(i - j) >= indexDifference` 且
- `abs(nums[i] - nums[j]) >= valueDifference`

返回整数数组 `answer`。如果存在满足题目要求的两个下标，则 `answer = [i, j]` ；否则，`answer = [-1, -1]` 。如果存在多组可供选择的下标对，只需要返回其中任意一组即可。

**注意：**`i` 和 `j` 可能 **相等** 。

 

**示例 1：**

> 输入：nums = [5,1,4,1], indexDifference = 2, valueDifference = 4
> 输出：[0,3]
> 解释：在示例中，可以选择 i = 0 和 j = 3 。
> abs(0 - 3) >= 2 且 abs(nums[0] - nums[3]) >= 4 。
> 因此，[0,3] 是一个符合题目要求的答案。
> [3,0] 也是符合题目要求的答案。

**示例 2：**

> 输入：nums = [2,1], indexDifference = 0, valueDifference = 0
> 输出：[0,0]
> 解释：
> 在示例中，可以选择 i = 0 和 j = 0 。 
> abs(0 - 0) >= 0 且 abs(nums[0] - nums[0]) >= 0 。 
> 因此，[0,0] 是一个符合题目要求的答案。 
> [0,1]、[1,0] 和 [1,1] 也是符合题目要求的答案。 

**示例 3：**

> 输入：nums = [1,2,3], indexDifference = 2, valueDifference = 4
> 输出：[-1,-1]
> 解释：在示例中，可以证明无法找出 2 个满足所有条件的下标。
> 因此，返回 [-1,-1] 。

 

**提示：**

- `1 <= n == nums.length <= 100`
- `0 <= nums[i] <= 50`
- `0 <= indexDifference <= 100`
- `0 <= valueDifference <= 50`

##### 解题思路

不妨假设 $i$ 在左，$j$ 在右，即 $i≤j−indexDifferencei$。

枚举 $j$，寻找左边的 $i$。要想满足 $∣nums[i]−nums[j]∣≥valueDifference$，要找的 $nums[i]$ 应当尽量大或者尽量小，这样差的绝对值才能尽量大。

类似 [121. 买卖股票的最佳时机](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock/)，我们可以在枚举 $j$ 的同时，维护 $nums[0]$] 到 $nums[j−indexDifference]$ 中的最大值 $mx$ 和最小值 $mn$。

例如 $indexDifference=2$，从 $j=2$ 开始遍历数组：

* 遍历到 $nums[2]$，用 $nums[0]$ 更新 $mx$ 和 $mn$。
* 遍历到 $nums[3]$，用 $nums[1]$ 更新 $mx$ 和 $mn$。
* 遍历到 $nums[4]$，用 $nums[2]$ 更新 $mx$和 $mn$。
  依此类推。

这个过程可以保证 $mx$ 和  在数组中的下标 $i$ 满足 $i≤j−indexDifferencei$，即题目的第一个要求。

对于题目的第二个要求，可以转换成如下两个不等式：

* $mx−nums[j]≥valueDifference$
* $nums[j]−mn≥valueDifference$
  满足其一即可返回答案。不用算绝对值的原因见下面的答疑。

由于要输出 $mx$ 或者 $mn$ 在数组中的下标，我们可以记录 $mx$ 在数组中的下标 $maxIdx$，以及 $mn$ 在数组中的下标 $minIdx$。由于知道下标就能知道元素值，所以只需记录下标，无需记录 $mx$ 和 $mn$。

**答疑**
**问**：为什么不用算绝对值？万一 $mx<nums[j]$，并且 $∣mx−nums[j]∣=nums[j]−mx≥valueDifference$，不就错过答案了吗？

**答**：在上述条件成立的前提下，由于 $mn≤mx$，得

​						$nums[j]−mn≥nums[j]−mx≥valueDifference$
所以此时 $mn$ 是满足要求的，不会错过答案。

```java
class Solution {
    public int[] findIndices(int[] nums, int indexDifference, int valueDifference) {
        int maxIdx = 0;
        int minIdx = 0;
        for (int j = indexDifference; j < nums.length; j++) {
            int i = j - indexDifference;
            if (nums[i] > nums[maxIdx]) {
                maxIdx = i;
            } else if (nums[i] < nums[minIdx]) {
                minIdx = i;
            }
            if (nums[maxIdx] - nums[j] >= valueDifference) {
                return new int[]{maxIdx, j};
            }
            if (nums[j] - nums[minIdx] >= valueDifference) {
                return new int[]{minIdx, j};
            }
        }
        return new int[]{-1, -1};
    }
}
```



## 哈希表

### Leetcode [2225. 找出输掉零场或一场比赛的玩家](https://leetcode.cn/problems/find-players-with-zero-or-one-losses/)

给你一个整数数组 `matches` 其中 `matches[i] = [winneri, loseri]` 表示在一场比赛中 `winneri` 击败了 `loseri` 。

返回一个长度为 2 的列表 `answer` ：

- `answer[0]` 是所有 **没有** 输掉任何比赛的玩家列表。
- `answer[1]` 是所有恰好输掉 **一场** 比赛的玩家列表。

两个列表中的值都应该按 **递增** 顺序返回。

**注意：**

- 只考虑那些参与 **至少一场** 比赛的玩家。
- 生成的测试用例保证 **不存在** 两场比赛结果 **相同** 。

 

**示例 1：**

> 输入：matches = [[1,3],[2,3],[3,6],[5,6],[5,7],[4,5],[4,8],[4,9],[10,4],[10,9]]
> 输出：[[1,2,10],[4,5,7,8]]
> 解释：
> 玩家 1、2 和 10 都没有输掉任何比赛。
> 玩家 4、5、7 和 8 每个都输掉一场比赛。
> 玩家 3、6 和 9 每个都输掉两场比赛。
> 因此，answer[0] = [1,2,10] 和 answer[1] = [4,5,7,8] 。

**示例 2：**

> 输入：matches = [[2,3],[1,3],[5,4],[6,4]]
> 输出：[[1,2,5,6],[]]
> 解释：
> 玩家 1、2、5 和 6 都没有输掉任何比赛。
> 玩家 3 和 4 每个都输掉两场比赛。
> 因此，answer[0] = [1,2,5,6] 和 answer[1] = [] 。

 

**提示：**

- `1 <= matches.length <= 105`
- `matches[i].length == 2`
- `1 <= winneri, loseri <= 105`
- `winneri != loseri`
- 所有 `matches[i]` **互不相同**

#### 解题思路

1. 遍历 $matches$，把所有玩家的编号加入哈希集合 $players$​。
2. 将 $winner$ 加入到 $player$ 中并置为 $1$，无论  $winner$ 获胜多少次，始终置为1。(因为返回没输过的，所以只要不为0就满足)
3. 如果 $loser$ 第一次输，把 $loser$ 加入 $player$ 并置为 $-1$，如果不是，用负数的相反数代表输的次数

```java
class Solution {
    public List<List<Integer>> findWinners(int[][] matches) {
        int[] player = new int[100001];
        for(int i = 0;i < matches.length;i++){
            int winner = matches[i][0];
            int loser = matches[i][1];
            if(player[winner] >= 0){
                player[winner] = 1;
            }
            // 如果败者第一次输，那么记录输的次数为-1;如果不是，那么输的次数加1，这里用负数的相反数代表输的次数;
            if(player[loser] >= 0){
                player[loser] = -1;
            }else{
                player[loser]--;
            }
        }
        List<Integer> list0 = new ArrayList<>();
        List<Integer> list1 = new ArrayList<>();
        List<List<Integer>> list = new ArrayList<>();
        for(int i = 0;i < player.length;i++){
            if(player[i] == 1){
                list0.add(i);
            }else if(player[i] == -1){
                list1.add(i);
            }
        }
        list.add(list0);
        list.add(list1);
        return list;
    }
}
```



## 回溯

## 贪心

### Leetcode [53. 最大子数组和](https://leetcode.cn/problems/maximum-subarray/)

给你一个整数数组 `nums` ，请你找出一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

**子数组**是数组中的一个连续部分。



**示例 1：**

> 输入：nums = [-2,1,-3,4,-1,2,1,-5,4]
> 输出：6
> 解释：连续子数组 [4,-1,2,1] 的和最大，为 6 。

**示例 2：**

> 输入：nums = [1]
> 输出：1

**示例 3：**

> 输入：nums = [5,4,-1,7,8]
> 输出：23

 

**提示：**

- `1 <= nums.length <= 105`
- `-104 <= nums[i] <= 104`

 

**进阶：**如果你已经实现复杂度为 `O(n)` 的解法，尝试使用更为精妙的 **分治法** 求解。

#### 思路

如果 $-2,1$ 在一起，计算起点的时候，一定是从 $1$ 开始计算，因为**负数只会拉低总和**，这就是贪心贪的地方！

局部最优：当前“连续和”为负数的时候立刻放弃，从下一个元素重新计算“连续和”，因为负数加上下一个元素 “连续和”只会越来越小。

全局最优：选取最大“连续和”

**局部最优的情况下，并记录最大的“连续和”，可以推出全局最优**。

从代码角度上来讲：遍历 $nums$，从头开始用 $sum$ 累积，如果 $sum$ 一旦加上 $nums[i]$ 变为负数，那么就应该从 $nums[i+1]$ 开始从 $0$ 累积 $sum$ 了，因为已经变为负数的 $sum$，只会拖累总和。

```java
class Solution {
    public int maxSubArray(int[] nums) {
        if (nums.length == 1) {
            return nums[0];
        }
        int res = Integer.MIN_VALUE;
        int sum = 0;
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            res = Math.max(sum, res);
            if (sum < 0) {
                sum = 0;
            }
        }
        return res;
    }
}
```



### Leetcode [55. 跳跃游戏](https://leetcode.cn/problems/jump-game/)

给你一个非负整数数组 `nums` ，你最初位于数组的 **第一个下标** 。数组中的每个元素代表你在该位置可以跳跃的最大长度。

判断你是否能够到达最后一个下标，如果可以，返回 `true` ；否则，返回 `false` 。

 

**示例 1：**

> 输入：nums = [2,3,1,1,4]
> 输出：true
> 解释：可以先跳 1 步，从下标 0 到达下标 1, 然后再从下标 1 跳 3 步到达最后一个下标。

**示例 2：**

> 输入：nums = [3,2,1,0,4]
> 输出：false
> 解释：无论怎样，总会到达下标为 3 的位置。但该下标的最大跳跃长度是 0 ， 所以永远不可能到达最后一个下标。

 

**提示：**

- `1 <= nums.length <= 104`
- `0 <= nums[i] <= 105`

#### 思路

每次移动取最大跳跃步数（得到最大的覆盖范围），每移动一个单位，就更新最大覆盖范围。

**贪心算法局部最优解：每次取最大跳跃步数（取最大覆盖范围），整体最优解：最后得到整体最大覆盖范围，看是否能到终点**。

i 每次移动只能在 cover 的范围内移动，每移动一个元素，cover 得到该元素数值（新的覆盖范围）的补充，让 i 继续移动下去。

而 cover 每次只取 max(该元素数值补充后的范围, cover 本身范围)。

如果 cover 大于等于了终点下标，直接 return true 就可以了。

```java
class Solution {
    public boolean canJump(int[] nums) {
        if (nums.length == 1) return true;
        int n = nums.length;
        int len = 0;
        for (int i = 0; i <= len; i++) {
            len = Math.max(i + nums[i], len);
            if (len >= n - 1) return true;
        }
        return false;
    }
}
```



### Leetcode [122. 买卖股票的最佳时机 II](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/)

给你一个整数数组 `prices` ，其中 `prices[i]` 表示某支股票第 `i` 天的价格。

在每一天，你可以决定是否购买和/或出售股票。你在任何时候 **最多** 只能持有 **一股** 股票。你也可以先购买，然后在 **同一天** 出售。

返回 *你能获得的 **最大** 利润* 。

 

**示例 1：**

> 输入：prices = [7,1,5,3,6,4]
> 输出：7
> 解释：在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5 - 1 = 4。
> 随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6 - 3 = 3。
> 最大总利润为 4 + 3 = 7 。

**示例 2：**

> 输入：prices = [1,2,3,4,5]
> 输出：4
> 解释：在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5 - 1 = 4。
> 最大总利润为 4 。

**示例 3：**

> 输入：prices = [7,6,4,3,1]
> 输出：0
> 解释：在这种情况下, 交易无法获得正利润，所以不参与交易可以获得最大利润，最大利润为 0。

 

**提示：**

- `1 <= prices.length <= 3 * 104`
- `0 <= prices[i] <= 104`

#### 思路：

假如第 $0$ 天买入，第 $3$ 天卖出，那么利润为：$prices[3] - prices[0]$。

相当于 $prices[3]-prices[2]+prices[2]-prices[1]+prices[1]-prices[0]$。

**此时就是把利润分解为每天为单位的维度，而不是从 0 天到第 3 天整体去考虑！**

那么根据 $prices$ 可以得到每天的利润序列：$prices[i] - prices[i - 1]+···+prices[1] - prices[0]$​​。

只需要收集每天的正利润就可以，**收集正利润的区间，就是股票买卖的区间，而我们只需要关注最终利润，不需要记录区间**。

```java
class Solution {
    public int maxProfit(int[] prices) {
        int res = 0;
        for (int i = 1; i < prices.length; i++) {
            res += Math.max(prices[i] - prices[i - 1], 0);
        }
        return res;
    }
}
```



### Leetcode [134. 加油站](https://leetcode.cn/problems/gas-station/)

在一条环路上有 `n` 个加油站，其中第 `i` 个加油站有汽油 `gas[i]` 升。

你有一辆油箱容量无限的的汽车，从第 `i` 个加油站开往第 `i+1` 个加油站需要消耗汽油 `cost[i]` 升。你从其中的一个加油站出发，开始时油箱为空。

给定两个整数数组 `gas` 和 `cost` ，如果你可以按顺序绕环路行驶一周，则返回出发时加油站的编号，否则返回 `-1` 。如果存在解，则 **保证** 它是 **唯一** 的。

 

**示例 1:**

> 输入: gas = [1,2,3,4,5], cost = [3,4,5,1,2]
> 输出: 3
> 解释:
> 从 3 号加油站(索引为 3 处)出发，可获得 4 升汽油。此时油箱有 = 0 + 4 = 4 升汽油
> 开往 4 号加油站，此时油箱有 4 - 1 + 5 = 8 升汽油
> 开往 0 号加油站，此时油箱有 8 - 2 + 1 = 7 升汽油
> 开往 1 号加油站，此时油箱有 7 - 3 + 2 = 6 升汽油
> 开往 2 号加油站，此时油箱有 6 - 4 + 3 = 5 升汽油
> 开往 3 号加油站，你需要消耗 5 升汽油，正好足够你返回到 3 号加油站。
> 因此，3 可为起始索引。

**示例 2:**

> 输入: gas = [2,3,4], cost = [3,4,3]
> 输出: -1
> 解释:
> 你不能从 0 号或 1 号加油站出发，因为没有足够的汽油可以让你行驶到下一个加油站。
> 我们从 2 号加油站出发，可以获得 4 升汽油。 此时油箱有 = 0 + 4 = 4 升汽油
> 开往 0 号加油站，此时油箱有 4 - 3 + 2 = 3 升汽油
> 开往 1 号加油站，此时油箱有 3 - 3 + 3 = 3 升汽油
> 你无法返回 2 号加油站，因为返程需要消耗 4 升汽油，但是你的油箱只有 3 升汽油。
> 因此，无论怎样，你都不可能绕环路行驶一周。

 

**提示:**

- `gas.length == n`
- `cost.length == n`
- `1 <= n <= 105`
- `0 <= gas[i], cost[i] <= 104`

#### 思路

可以换一个思路，首先如果总油量减去总消耗大于等于零那么一定可以跑完一圈，说明 各个站点的加油站 剩油量rest[i]相加一定是大于等于零的。

每个加油站的剩余量rest[i]为gas[i] - cost[i]。

i从0开始累加rest[i]，和记为curSum，一旦curSum小于零，说明[0, i]区间都不能作为起始位置，因为这个区间选择任何一个位置作为起点，到i这里都会断油，那么起始位置从i+1算起，再从0计算curSum。

如图：

<img src="D:\Software\Typora\复制的图片\1683275147-yLDDSA-image.png" alt="image.png" style="zoom:33%;" />

**那么局部最优：当前累加rest[i]的和curSum一旦小于0，起始位置至少要是i+1，因为从i之前开始一定不行。全局最优：找到可以跑一圈的起始位置**。

```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int sum = 0;
        int cnt = 0;
        int start = 0;
        for (int i = 0; i < gas.length; i++) {
            sum += gas[i] - cost[i];
            cnt += gas[i] - cost[i];
            if (sum < 0) {
                sum = 0;
                start = (i + 1) % gas.length;
            }
        }
        return cnt < 0 ? -1 : start;
    }
}
```



### Leetcode [135. 分发糖果](https://leetcode.cn/problems/candy/)

`n` 个孩子站成一排。给你一个整数数组 `ratings` 表示每个孩子的评分。

你需要按照以下要求，给这些孩子分发糖果：

- 每个孩子至少分配到 `1` 个糖果。
- 相邻两个孩子评分更高的孩子会获得更多的糖果。

请你给每个孩子分发糖果，计算并返回需要准备的 **最少糖果数目** 。



 **示例 1：**

> 输入：ratings = [1,0,2]
> 输出：5
> 解释：你可以分别给第一个、第二个、第三个孩子分发 2、1、2 颗糖果。

**示例 2：**

> 输入：ratings = [1,2,2]
> 输出：4
> 解释：你可以分别给第一个、第二个、第三个孩子分发 1、2、1 颗糖果。
>      第三个孩子只得到 1 颗糖果，这满足题面中的两个条件。

 

**提示：**

- `n == ratings.length`
- `1 <= n <= 2 * 104`
- `0 <= ratings[i] <= 2 * 104`

#### 思路

https://www.programmercarl.com/0135.%E5%88%86%E5%8F%91%E7%B3%96%E6%9E%9C.html#%E6%80%9D%E8%B7%AF

```java
class Solution {
    /**
         分两个阶段
         1、起点下标1 从左往右，只要 右边 比 左边 大，右边的糖果=左边 + 1
         2、起点下标 ratings.length - 2 从右往左， 只要左边 比 右边 大，此时 左边的糖果应该 取本身的糖果数（符合比它左边大） 和 右边糖果数 + 1 二者的最大值，这样才符合 它比它左边的大，也比它右边大
    */
    public int candy(int[] ratings) {
        int len = ratings.length;
        int[] candyVec = new int[len];
        candyVec[0] = 1;
        for (int i = 1; i < len; i++) {
            candyVec[i] = (ratings[i] > ratings[i - 1]) ? candyVec[i - 1] + 1 : 1;
        }

        for (int i = len - 2; i >= 0; i--) {
            if (ratings[i] > ratings[i + 1]) {
                candyVec[i] = Math.max(candyVec[i], candyVec[i + 1] + 1);
            }
        }

        int ans = 0;
        for (int num : candyVec) {
            ans += num;
        }
        return ans;
    }
}
```



### Leetcode [860. 柠檬水找零](https://leetcode.cn/problems/lemonade-change/)

在柠檬水摊上，每一杯柠檬水的售价为 `5` 美元。顾客排队购买你的产品，（按账单 `bills` 支付的顺序）一次购买一杯。

每位顾客只买一杯柠檬水，然后向你付 `5` 美元、`10` 美元或 `20` 美元。你必须给每个顾客正确找零，也就是说净交易是每位顾客向你支付 `5` 美元。

注意，一开始你手头没有任何零钱。

给你一个整数数组 `bills` ，其中 `bills[i]` 是第 `i` 位顾客付的账。如果你能给每位顾客正确找零，返回 `true` ，否则返回 `false` 。

 

**示例 1：**

> 输入：bills = [5,5,5,10,20]
> 输出：true
> 解释：
> 前 3 位顾客那里，我们按顺序收取 3 张 5 美元的钞票。
> 第 4 位顾客那里，我们收取一张 10 美元的钞票，并返还 5 美元。
> 第 5 位顾客那里，我们找还一张 10 美元的钞票和一张 5 美元的钞票。
> 由于所有客户都得到了正确的找零，所以我们输出 true。

**示例 2：**

> 输入：bills = [5,5,10,10,20]
> 输出：false
> 解释：
> 前 2 位顾客那里，我们按顺序收取 2 张 5 美元的钞票。
> 对于接下来的 2 位顾客，我们收取一张 10 美元的钞票，然后返还 5 美元。
> 对于最后一位顾客，我们无法退回 15 美元，因为我们现在只有两张 10 美元的钞票。
> 由于不是每位顾客都得到了正确的找零，所以答案是 false。

 

**提示：**

- `1 <= bills.length <= 105`
- `bills[i]` 不是 `5` 就是 `10` 或是 `20` 

#### 思路

由于 10 美元钞票只能用于 20 美元的找零，而 5 美元钞票既可以用于 20 美元的找零，又可以用于 10 美元的找零，更加通用（使用场景更多），所以如果可以用 10 美元，应当优先用 10 美元，其次用 5 美元。如果优先用 5 美元，可能会面临 bills[i]=10 无法找零的情况。

设当前有 five 张 5 美元钞票，ten 张 10 美元钞票。20 美元的无需统计，因为它无法用来找零。

设 b=bills[i]，分类讨论：

如果 b=5，无需找零，five 加一。
如果 b=10，返还 5 美元，five 减一，ten 加一。
如果 b=20 且 ten>0，返还 10+5 美元，five 和 ten 都减一。
如果 b=20 且 ten=0，返还 5+5+5 美元，five 减三。
如果发现 five<0，说明无法正确找零，返回 false。
如果中途没有返回 false，那么循环结束后返回 true。

```java
class Solution {
    public boolean lemonadeChange(int[] bills) {
        int five = 0, ten = 0;
        for (int b : bills) {
            if (b == 5) { // 无需找零
                five++;
            } else if (b == 10) { // 返还 5
                five--;
                ten++;
            } else if (ten > 0) { // 此时 b=20，返还 10+5
                five--;
                ten--;
            } else { // 此时 b=20，返还 5+5+5
                five -= 3;
            }
            if (five < 0) { // 无法正确找零
                return false;
            }
        }
        return true;
    }
}
```





### Leetcode [1005. K 次取反后最大化的数组和](https://leetcode.cn/problems/maximize-sum-of-array-after-k-negations/)

给你一个整数数组 `nums` 和一个整数 `k` ，按以下方法修改该数组：

- 选择某个下标 `i` 并将 `nums[i]` 替换为 `-nums[i]` 。

重复这个过程恰好 `k` 次。可以多次选择同一个下标 `i` 。

以这种方式修改数组后，返回数组 **可能的最大和** 。



**示例 1：**

> 输入：nums = [4,2,3], k = 1
> 输出：5
> 解释：选择下标 1 ，nums 变为 [4,-2,3] 。

**示例 2：**

> 输入：nums = [3,-1,0,2], k = 3
> 输出：6
> 解释：选择下标 (1, 2, 2) ，nums 变为 [3,1,0,2] 。

**示例 3：**

> 输入：nums = [2,-3,-1,5,-4], k = 2
> 输出：13
> 解释：选择下标 (1, 4) ，nums 变为 [2,3,-1,5,4] 。

 

**提示：**

- `1 <= nums.length <= 104`
- `-100 <= nums[i] <= 100`
- `1 <= k <= 104`

#### 思路

贪心的思路，局部最优：让绝对值大的负数变为正数，当前数值达到最大，整体最优：整个数组和达到最大。

局部最优可以推出全局最优。

那么如果将负数都转变为正数了，K依然大于0，此时的问题是一个有序正整数序列，如何转变K次正负，让 数组和 达到最大。

那么又是一个贪心：局部最优：只找数值最小的正整数进行反转，当前数值和可以达到最大（例如正整数数组{5, 3, 1}，反转1 得到-1 比 反转5得到的-5 大多了），全局最优：整个 数组和 达到最大。

那么本题的解题步骤为：

第一步：将数组按照绝对值大小从大到小排序，注意要按照绝对值的大小
第二步：从前向后遍历，遇到负数将其变为正数，同时K--
第三步：如果K还大于0，那么反复转变数值最小的元素，将K用完
第四步：求和

```java
class Solution {
    public int largestSumAfterKNegations(int[] nums, int K) {
    	// 将数组按照绝对值大小从大到小排序，注意要按照绝对值的大小
	nums = IntStream.of(nums)
		     .boxed()
		     .sorted((o1, o2) -> Math.abs(o2) - Math.abs(o1))
		     .mapToInt(Integer::intValue).toArray();
	int len = nums.length;	    
	for (int i = 0; i < len; i++) {
	    //从前向后遍历，遇到负数将其变为正数，同时K--
	    if (nums[i] < 0 && K > 0) {
	    	nums[i] = -nums[i];
	    	K--;
	    }
	}
	// 如果K还大于0，那么反复转变数值最小的元素，将K用完

	if (K % 2 == 1) nums[len - 1] = -nums[len - 1];
	return Arrays.stream(nums).sum();

    }
}
```



### Leetcode [2244. 完成所有任务需要的最少轮数](https://leetcode.cn/problems/minimum-rounds-to-complete-all-tasks/)

给你一个下标从 **0** 开始的整数数组 `tasks` ，其中 `tasks[i]` 表示任务的难度级别。在每一轮中，你可以完成 2 个或者 3 个 **相同难度级别** 的任务。

返回完成所有任务需要的 **最少** 轮数，如果无法完成所有任务，返回 `-1` 。

 

**示例 1：**

> 输入：tasks = [2,2,3,3,2,4,4,4,4,4]
> 输出：4
> 解释：要想完成所有任务，一个可能的计划是：
> - 第一轮，完成难度级别为 2 的 3 个任务。 
> - 第二轮，完成难度级别为 3 的 2 个任务。 
> - 第三轮，完成难度级别为 4 的 3 个任务。 
> - 第四轮，完成难度级别为 4 的 2 个任务。 
> 可以证明，无法在少于 4 轮的情况下完成所有任务，所以答案为 4 。

**示例 2：**

> 输入：tasks = [2,3,3]
> 输出：-1
> 解释：难度级别为 2 的任务只有 1 个，但每一轮执行中，只能选择完成 2 个或者 3 个相同难度级别的任务。因此，无法完成所有任务，答案为 -1 。

 

**提示：**

- `1 <= tasks.length <= 105`
- `1 <= tasks[i] <= 109`

#### 解题思路

每轮完成的都是相同难度级别的任务，假设难度为 $1$ 的任务有 $c$ 个，问题变成：

* 每轮可以把 $c$ 减少 $2$，或者减少 $3$。把 $c$ 减少到 $0$ 最少要多少轮？

例如 $c=10$ 时，$3+3+2+2=10$，最少要 $4$ 轮。

贪心地想，尽量多地使用「减少 333」，可以让轮数尽量少。

分类讨论：

* 如果 $c=1$，无法完成，返回 $−1$。
* 如果 $c=3k (k≥1)$，只用「减少 $3$」就能完成，轮数为 $\dfrac{c}{3} $。
* 如果 $c=3k+1 (k≥1)$，即 $c=3k'+4 (k'≥0)$，我们可以先把 $c$ 减少到 $4$，然后使用两次「减少 $2$」，轮数为 $\dfrac{c-4}{3} + 2 =\dfrac{c+2}{3} = \left\lceil\dfrac{c}{3}\right\rceil$。$\lceil\dfrac{c}{3}\rceil$表示**向上取整**
* 如果 $c=3k+2 (k≥1)$，我们可以先把 $c$ 减少到 $2$，然后使用一次「减少 $2$」，轮数为 $\dfrac{c-2}{3} + 1 = \dfrac{c+1}{3} = \left\lceil\dfrac{c}{3}\right\rceil$。

综上所述，对于 $c(c≥2)$ 个相同难度级别的任务，最少需要操作

​								$\left\lceil\dfrac{c}{3}\right\rceil = \left\lfloor\dfrac{c+2}{3}\right\rfloor$次。

用哈希表统计不同难度任务的个数，按照上式计算轮数，累加轮数即为答案。

```java
public class Solution {
    public int minimumRounds(int[] tasks) {
        Map<Integer, Integer> cnt = new HashMap<>();
        for (int t : tasks) {
            cnt.merge(t, 1, Integer::sum);
        }
        int ans = 0;
        for (int c : cnt.values()) {
            if (c == 1) {
                return -1;
            }
            ans += (c + 2) / 3;
        }
        return ans;
    }
}
```

`merge()` 方法是 Java 8 中 Map 接口新增的一个方法，用于将指定键的值与指定函数的结果进行关联。如果指定的键已经存在，则将指定函数应用于已经存在的键对应的值和给定的值，并将函数的结果存储回指定的键中；如果指定的键不存在，则简单地将指定的键值对存储在 Map 中。

具体语法为：`map.merge(key, value, remappingFunction)`

- `key`：要在 Map 中关联的键。
- `value`：要与指定键相关联的值。
- `remappingFunction`：用于计算新值的函数，如果指定的键已存在，则应用此函数计算新值。

在上述代码中，`cnt.merge(t, 1, Integer::sum)` 的作用是将键为 `t` 的项插入到 `cnt` Map 中。如果 `t` 这个键在 `cnt` 中不存在，就将键值对 `(t, 1)` 插入到 Map 中；如果 `t` 这个键在 `cnt` 中已经存在，则将键为 `t` 的项的值与给定的值 1 进行求和，即执行 `Integer::sum` 方法，然后将计算得到的新值存储回键为 `t` 的项中。



### Leetcode [2589. 完成所有任务的最少时间](https://leetcode.cn/problems/minimum-time-to-complete-all-tasks/)

你有一台电脑，它可以 **同时** 运行无数个任务。给你一个二维整数数组 `tasks` ，其中 `tasks[i] = [starti, endi, durationi]` 表示第 `i` 个任务需要在 **闭区间** 时间段 `[starti, endi]` 内运行 `durationi` 个整数时间点（但不需要连续）。

当电脑需要运行任务时，你可以打开电脑，如果空闲时，你可以将电脑关闭。

请你返回完成所有任务的情况下，电脑最少需要运行多少秒。

 

**示例 1：**

> 输入：tasks = [[2,3,1],[4,5,1],[1,5,2]]
> 输出：2
> 解释：
> - 第一个任务在闭区间 [2, 2] 运行。
> - 第二个任务在闭区间 [5, 5] 运行。
> - 第三个任务在闭区间 [2, 2] 和 [5, 5] 运行。
> 电脑总共运行 2 个整数时间点。

**示例 2：**

> 输入：tasks = [[1,3,2],[2,5,3],[5,6,2]]
> 输出：4
> 解释：
> - 第一个任务在闭区间 [2, 3] 运行
> - 第二个任务在闭区间 [2, 3] 和 [5, 5] 运行。
> - 第三个任务在闭区间 [5, 6] 运行。
> 电脑总共运行 4 个整数时间点。

 

**提示：**

- `1 <= tasks.length <= 2000`
- `tasks[i].length == 3`
- `1 <= starti, endi <= 2000`
- `1 <= durationi <= endi - starti + 1 `

#### 解题思路

##### 方法一：贪心+暴力

**提示 1**
按照区间右端点从小到大排序。

**提示 2**
排序后，对于区间 tasks[i]\textit{tasks}[i]tasks[i] 来说，它右侧的任务区间要么和它没有交集，要么包含它的一部分**后缀**。

例如排序后的区间为 $[1,5],[3,7],[6,8]$，对于 $[1,5]$ 来说，它右边的区间要么和它没有交集，例如 $[6,8]$；要么交集是 $[1,5]$ 的后缀，例如 $[1,5]$ 和 $[3,7]$ 的交集是 $[3,5]$，这是 $[1,5]$ 的后缀（$3,4,5$ 是 $1,2,3,4,5$ 的后缀）。

**提示 3**
遍历排序后的任务，先统计区间内的已运行的电脑运行时间点，如果个数小于 $\textit{duration}$，则需要新增时间点。根据提示 2，尽量把新增的时间点安排在区间 $[\textit{start},\textit{end}$] 的后缀上，这样下一个区间就能统计到更多已运行的时间点。

```java
class Solution {
    public int findMinimumTime(int[][] tasks) {
        Arrays.sort(tasks, (a, b) -> a[1] - b[1]);
        int ans = 0;
        int mx = tasks[tasks.length - 1][1];
        boolean[] run = new boolean[mx + 1];
        for (int[] t : tasks) {
            int start = t[0];
            int end = t[1];
            int d = t[2];
            for (int i = start; i <= end; i++) {
                if (run[i]) {
                    d--; // 去掉运行中的时间点
                }
            }
            for (int i = end; d > 0; i--) { // 剩余的 d 填充区间后缀
                if (!run[i]) {
                    run[i] = true; // 运行
                    d--;
                    ans++;
                }
            }
        }
        return ans;
    }
}
```



### Leetcode [1953. 你可以工作的最大周数](https://leetcode.cn/problems/maximum-number-of-weeks-for-which-you-can-work/)

给你 `n` 个项目，编号从 `0` 到 `n - 1` 。同时给你一个整数数组 `milestones` ，其中每个 `milestones[i]` 表示第 `i` 个项目中的阶段任务数量。

你可以按下面两个规则参与项目中的工作：

- 每周，你将会完成 **某一个** 项目中的 **恰好一个** 阶段任务。你每周都 **必须** 工作。
- 在 **连续的** 两周中，你 **不能** 参与并完成同一个项目中的两个阶段任务。

一旦所有项目中的全部阶段任务都完成，或者仅剩余一个阶段任务都会导致你违反上面的规则，那么你将 **停止工作** 。注意，由于这些条件的限制，你可能无法完成所有阶段任务。

返回在不违反上面规则的情况下你 **最多** 能工作多少周。



**示例 1：**

> 输入：milestones = [1,2,3]
> 输出：6
> 解释：一种可能的情形是：
> - 第 1 周，你参与并完成项目 0 中的一个阶段任务。
> - 第 2 周，你参与并完成项目 2 中的一个阶段任务。
> - 第 3 周，你参与并完成项目 1 中的一个阶段任务。
> - 第 4 周，你参与并完成项目 2 中的一个阶段任务。
> - 第 5 周，你参与并完成项目 1 中的一个阶段任务。
> - 第 6 周，你参与并完成项目 2 中的一个阶段任务。
> 总周数是 6 。

**示例 2：**

> 输入：milestones = [5,2,1]
> 输出：7
> 解释：一种可能的情形是：
> - 第 1 周，你参与并完成项目 0 中的一个阶段任务。
> - 第 2 周，你参与并完成项目 1 中的一个阶段任务。
> - 第 3 周，你参与并完成项目 0 中的一个阶段任务。
> - 第 4 周，你参与并完成项目 1 中的一个阶段任务。
> - 第 5 周，你参与并完成项目 0 中的一个阶段任务。
> - 第 6 周，你参与并完成项目 2 中的一个阶段任务。
> - 第 7 周，你参与并完成项目 0 中的一个阶段任务。
> 总周数是 7 。
> 注意，你不能在第 8 周参与完成项目 0 中的最后一个阶段任务，因为这会违反规则。
> 因此，项目 0 中会有一个阶段任务维持未完成状态。

 

**提示：**

- `n == milestones.length`
- `1 <= n <= 105`
- `1 <= milestones[i] <= 109`

#### 解题思路

本质上来说，我们需要构造一个尽量长的，相邻元素不同的序列，且元素 $x$ 的出现次数不能超过 $milestones[x]$。

示例 1 可以构造的一个序列是 $[2,1,2,1,2,0]$。
示例 2 可以构造的一个序列是 $[0,1,0,1,0,2,0]$。
设 $milestones$ 的元素和为 $s$，这是序列长度的上界。示例 1 可以构造长为 $s=6$ 的序列，但示例 2 不行。看上去，如果有一个 $milestones[i]$ 特别大，我们就没法构造出一个长为 $s$ 的序列了。这个数具体要多大呢？

想一想，一个长为 $k$ 的序列，至多可以有多少个相同元素？

设 $m=max⁡(milestones)$。假设 $milestones[2]=m$。
如果序列长度是奇数，我们可以在偶数下标 $0,2,4,⋯ ,k−1$ 上放置元素 $2$。假设还可以放一个 $2$，那么它必然会和另一个 $2$ 相邻。例如 $k=7$，我们可以在偶数下标 $0,2,4,6$ 上放置 $2$，奇数下标 $1,3,5$ 只能放其它元素。这也说明，序列中元素 $2$ 的个数至多比其它元素的个数之和多 $1$。
如果序列长度是偶数，我们可以在偶数下标 $0,2,4,⋯ ,k−2$ 上放置元素 $2$，奇数下标放其它元素。如果还有 $2$，我们可以在序列末尾再加一个 $2$，转换成序列长度是奇数的情况。
一般地，如果有一个 $milestones[i]=m$ 特别大，大到它比其它元素的个数之和加 $1$ 还要大，即 $m>s−m+1$，那么序列长度将会以其它元素的个数之和为主，即 $2⋅(s−m)+1$。例如示例 2，$s−m=3$，序列长度为 $2⋅3+1=7$，在偶数下标放元素 $0$，奇数下标放其它元素。

剩下要解决的问题是，如果 $m≤s−m+1$，是否一定可以构造一个长为 $s$ 的序列？

可以，构造方法如下：

把 $milestones$ 从大到小排序。以 $milestones=[3,3,2]$ 为例，$s=3+3+2=8$。按照先填偶数下标，再填奇数下标，也就是下标 $0,2,4,6,1,3,5,7$ 的顺序，首先填入三个元素 $0$​，得到

​				$0,\text{\_},0,\text{\_},0,\text{\_},\text{\_},\text{\_}$
继续按照顺序，填入三个元素 $1$，得到

​				$0,1,0,1,0,\text{\_},1,\text{\_}$
最后填入两个元素 $2$，得到

​				$0,1,0,1,0,2,1,2$
按照该构造方法，如果出现两个相邻元素相同的情况，那么它不会是从奇数下标开始填的（这样不会出现相邻相同），而是从某个偶数下标开始填的，然后在填到某个奇数下标时，出现了相邻元素相同的情况，例如下标顺序为 $4,6,1,3$，该元素出现次数至少为 $4$。但是，由于我们已经把 $milestones$ 从大到小排序了，$4$ 必然是最大值，不可能从偶数下标 $4$ 开始，只能从偶数下标 $0$ 开始（注意不能从奇数下标开始），即 $0,2,4,6,1$，这意味着该元素至少出现 $5$ 次，但 $5>8−5+1$，与 $m≤s−m+1$ 的前提不符。

综上所述：

如果 $m>s−m+1$，返回 $2⋅(s−m)+1$。
如果 $m≤s−m+1$，返回 $s$。

```java
class Solution {
    public long numberOfWeeks(int[] milestones) {
        int max = 0;
        long sum = 0L;
        for(int num : milestones){
            if(num > max){
                max = num;
            }
            sum += num;
        }
        return (sum - max + 1) >= max ? sum : 2 * (sum - max) + 1;
    }
}
```



### Leetcode [826. 安排工作以达到最大收益](https://leetcode.cn/problems/most-profit-assigning-work/)

你有 `n` 个工作和 `m` 个工人。给定三个数组： `difficulty`, `profit` 和 `worker` ，其中:

- `difficulty[i]` 表示第 `i` 个工作的难度，`profit[i]` 表示第 `i` 个工作的收益。
- `worker[i]` 是第 `i` 个工人的能力，即该工人只能完成难度小于等于 `worker[i]` 的工作。

每个工人 **最多** 只能安排 **一个** 工作，但是一个工作可以 **完成多次** 。

- 举个例子，如果 3 个工人都尝试完成一份报酬为 `$1` 的同样工作，那么总收益为 `$3` 。如果一个工人不能完成任何工作，他的收益为 `$0` 。

返回 *在把工人分配到工作岗位后，我们所能获得的最大利润* 。

 

**示例 1：**

> 输入: difficulty = [2,4,6,8,10], profit = [10,20,30,40,50], worker = [4,5,6,7]
> 输出: 100 
> 解释: 工人被分配的工作难度是 [4,4,6,6] ，分别获得 [20,20,30,30] 的收益。

**示例 2:**

> 输入: difficulty = [85,47,57], profit = [24,66,99], worker = [40,25,25]
> 输出: 0

 

**提示:**

- `n == difficulty.length`
- `n == profit.length`
- `m == worker.length`
- `1 <= n, m <= 104`
- `1 <= difficulty[i], profit[i], worker[i] <= 105`

#### 解题思路

如果把 $worker$ 按照从小到大的顺序排序，那么第 $i$ 个工人能做的工作，他右边的（$worker$ 值更大的）工人也能做。这意味着，如果我们遍历了所有 $difficulty[j]≤worker[i]$ 的工作，那么从第 $i$ 个工人到第 $i+1$ 个工人，只需要额外遍历 $worker[i]<difficulty[j]≤worker[i+1]$ 的工作。

把 $difficulty$ 和 $profit$ 绑在一起，按照 $difficulty$ 从小到大排序，我们可以在遍历 $worker$ 的同时，用双指针遍历并维护 $difficulty[j]≤worker[i]$ 的最大的 $profit[j]$，即为第 $i$​ 个工人所能获得的最大利润。累加每名工人能获得的最大利润，即为答案。

```java
class Solution {
    public int maxProfitAssignment(int[] difficulty, int[] profit, int[] worker) {
        int n = difficulty.length;
        int[][] jobs = new int[n][2];
        for (int i = 0; i < n; i++) {
            jobs[i][0] = difficulty[i];
            jobs[i][1] = profit[i];
        }
        Arrays.sort(jobs, (a, b) -> a[0] - b[0]);
        Arrays.sort(worker);
        int ans = 0, j = 0, maxProfit = 0;
        for (int w : worker) {
            while (j < n && jobs[j][0] <= w) {
                maxProfit = Math.max(maxProfit, jobs[j++][1]);
            }
            ans += maxProfit;
        }
        return ans;
    }
}
```

#### 其他解法

```java
class Solution {
    public int maxProfitAssignment(int[] difficulty, int[] profit, int[] worker) {
        int[] maxProfit = new int[100001];
        // 对 difficulty 去重，得到每个 difficulty 数值的最大 profit
        for (int i = 0; i < difficulty.length; i++) {
            if (maxProfit[difficulty[i]] < profit[i]) maxProfit[difficulty[i]] = profit[i];
        }
        int max = 0;
        // 对每个 difficulty，记录 <= difficulty 的最大 profit
        for (int i = 0; i < maxProfit.length; i++) {
            if (maxProfit[i] < max) maxProfit[i] = max;
            else max = maxProfit[i];
        }
        int ans = 0;
        for (int i : worker) {
            ans += maxProfit[i];
        }
        return ans;
    }
}
```



## 动态规划

## 记忆化搜索

#### Leetcode [1553. 吃掉 N 个橘子的最少天数](https://leetcode.cn/problems/minimum-number-of-days-to-eat-n-oranges/)

厨房里总共有 `n` 个橘子，你决定每一天选择如下方式之一吃这些橘子：

- 吃掉一个橘子。
- 如果剩余橘子数 `n` 能被 2 整除，那么你可以吃掉 `n/2` 个橘子。
- 如果剩余橘子数 `n` 能被 3 整除，那么你可以吃掉 `2*(n/3)` 个橘子。

每天你只能从以上 3 种方案中选择一种方案。

请你返回吃掉所有 `n` 个橘子的最少天数。

**示例 1：**

> 输入：n = 10
> 输出：4
> 解释：你总共有 10 个橘子。
> 第 1 天：吃 1 个橘子，剩余橘子数 10 - 1 = 9。
> 第 2 天：吃 6 个橘子，剩余橘子数 9 - 2*(9/3) = 9 - 6 = 3。（9 可以被 3 整除）
> 第 3 天：吃 2 个橘子，剩余橘子数 3 - 2*(3/3) = 3 - 2 = 1。
> 第 4 天：吃掉最后 1 个橘子，剩余橘子数 1 - 1 = 0。
> 你需要至少 4 天吃掉 10 个橘子。

**示例 2：**

> 输入：n = 6
> 输出：3
> 解释：你总共有 6 个橘子。
> 第 1 天：吃 3 个橘子，剩余橘子数 6 - 6/2 = 6 - 3 = 3。（6 可以被 2 整除）
> 第 2 天：吃 2 个橘子，剩余橘子数 3 - 2*(3/3) = 3 - 2 = 1。（3 可以被 3 整除）
> 第 3 天：吃掉剩余 1 个橘子，剩余橘子数 1 - 1 = 0。
> 你至少需要 3 天吃掉 6 个橘子。

**示例 3：**

> 输入：n = 1
> 输出：1

**示例 4：**

> 输入：n = 56
> 输出：6

 

**提示：**

- `1 <= n <= 2*10^9`

##### 解题思路

**题意解读**
有三种操作，每次操作，选择其中一种：

* 把 n 减少 1。
* 如果 n 能被 2 整除，把 n 变成 $$ \frac{n}{2} $$
* 如果 n 能被 3 整除，把 n 变成 $$\frac{n}{3} $$

返回把 n 变成 0 的最少操作次数。

**分析**
一个初步的想法是，为了让 n 快速地变小，多做除法比多做减法要更好。

**引理**：在最优操作序列中，不存在「减 1，减 1，再除以 2」这样的操作。

**定理**：在最优操作序列中，如果第一个不是「减 1」的操作是「除以 2」，那么当 n 是偶数时，第一个操作一定是「除以 2」，当 n 是奇数时，前两个操作一定是「减 1，除以 2」。

根据上面找到的子问题，定义 $dfs(i)$ 表示把 $i$ 变成 $0$ 的最少操作次数。

分类讨论：

* 先执行 $i\,mod \,2$ 次减 1 操作，把 $$i$$ 变成 $$2$$ 的倍数，然后再执行一次除以 2，问题变成把 $\left\lfloor i/2 \right\rfloor$ 变成 $0$ 的最小操作次数，即 $dfs(i)=dfs(⌊i/2⌋)+i\, mod \,2\,+1\,。$
* 先执行 $i \,mod\,3$ 次减 1 操作，把 $i$ 变成 $3$ 的倍数，然后再执行一次除以 3，问题变成把 $\left\lfloor i/3 \right\rfloor$ 变成 $0$ 的最小操作次数，即 $dfs(i)=dfs(⌊i/3⌋)+i\,mod \,3\,+\,1。$

二者取最小值，得
					$$dfs(i)=min(dfs(⌊i/2⌋)+i\,mod\,2, dfs(⌊i/3⌋)+i\,mod\,3)\,+\,1$$

递归边界：$$\textit{dfs}(0)=0$$, $$\textit{dfs}(1)=1$$。

递归入口：$$\textit{dfs}(n)$$，即答案。

代码实现时，可以用**记忆化搜索**：用一个哈希表 $$\textit{memo}$$ 记录 $i$ 及其 $$\textit{dfs}(i)$$，再次递归调用 $$\textit{dfs}(i)$$ 时，就可以直接返回 $$\textit{memo}$$ 中保存的数据了。

$\color{#F0F}{222}$

```java
class Solution {
    private final Map<Integer, Integer> memo = new HashMap<>();

    public int minDays(int n) {
        if (n <= 1) {
            return n;
        }
        Integer res = memo.get(n);
        if (res != null) { // 之前计算过
            return res;
        }
        res = Math.min(minDays(n / 2) + n % 2, minDays(n / 3) + n % 3) + 1;
        memo.put(n, res); // 记忆化
        return res;
    }
}
```





## 广度优先搜索BFS

### Leetcode [994. 腐烂的橘子](https://leetcode.cn/problems/rotting-oranges/)

在给定的 `m x n` 网格 `grid` 中，每个单元格可以有以下三个值之一：

- 值 `0` 代表空单元格；
- 值 `1` 代表新鲜橘子；
- 值 `2` 代表腐烂的橘子。

每分钟，腐烂的橘子 **周围 4 个方向上相邻** 的新鲜橘子都会腐烂。

返回 *直到单元格中没有新鲜橘子为止所必须经过的最小分钟数。如果不可能，返回 `-1`* 。

**示例 1：**

**![img](D:\Software\Typora\复制的图片\oranges.png)**

> 输入：grid = [[2,1,1],[1,1,0],[0,1,1]]
> 输出：4

**示例 2：**

> 输入：grid = [[2,1,1],[0,1,1],[1,0,1]]
> 输出：-1
> 解释：左下角的橘子（第 2 行， 第 0 列）永远不会腐烂，因为腐烂只会发生在 4 个方向上。

**示例 3：**

> 输入：grid = [[0,2]]
> 输出：0
> 解释：因为 0 分钟时已经没有新鲜橘子了，所以答案就是 0 。

 

**提示：**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 10`
- `grid[i][j]` 仅为 `0`、`1` 或 `2`

#### 解题思路

**![img](D:\Software\Typora\复制的图片\oranges.png)**

看示例 1：

1. 统计所有初始就腐烂的橘子的位置，加到列表 $q$ 中，现在 $q=[(0,0)]$。
2. 初始化答案 $ans=−1$。模拟橘子腐烂的过程，不断循环，直到 $q$ 为空。
3. 答案加一，在第 $\textit{ans}=0$ 分钟，遍历 $q$ 中橘子的四方向相邻的新鲜橘子，把这些橘子腐烂，$q$ 更新为这些橘子的位置，现在 $q=[(0,1),(1,0)]$。
4. 答案加一，在第 $ans=1$ 分钟，遍历 $q$ 中橘子的四方向相邻的新鲜橘子，把这些橘子腐烂，$q$ 更新为这些橘子的位置，现在 $q=[(0,2),(1,1)]$。
5. 答案加一，在第 $ans=2$ 分钟，遍历 $q$ 中橘子的四方向相邻的新鲜橘子，把这些橘子腐烂，$q$ 更新为这些橘子的位置，现在 $q=[(2,1)]$。
6. 答案加一，在第 $ans=3$ 分钟，遍历 $q$ 中橘子的四方向相邻的新鲜橘子，把这些橘子腐烂，$q$ 更新为这些橘子的位置，现在 $q=[(2,2)]$。
7. 答案加一，在第 $ans=4$ 分钟，遍历 $q$ 中橘子的四方向相邻的新鲜橘子，把这些橘子腐烂，$q$ 更新为这些橘子的位置，由于没有这样的橘子，$q=[]$，退出循环。

为了判断是否有永远不会腐烂的橘子（如示例 2），我们可以统计初始新鲜橘子的个数 $fresh$。在 BFS 中，每有一个新鲜橘子被腐烂，就把 $fresh$ 减一，这样最后如果发现 $fresh>0$，就意味着有橘子永远不会腐烂，返回 $-1$。

注意在 $grid$ 全为 $0$ 的情况下要返回 $0$，但这种情况下 $ans$ 仍为其初始值 −$1$，所以最后返回的是 $max⁡(ans,0)$。

代码实现时，在 BFS 中要将 $grid[i][j]=1$ 的橘子修改成 $2$（或者其它不等于 $1$ 的数），这可以保证每个橘子加入 $q$ 中至多一次。如果不修改，我们就无法知道哪些橘子被腐烂过了，比如示例 1 中 $(0,1)$ 去腐烂 $(1,1)$，而 $(1,1)$在此之后又重新腐烂 $(0,1)$，如此反复，程序就会陷入死循环。读者可以注释掉下面代码中的 $grid[i][j] = 2$ 这行代码试试。

```java
class Solution {
    private static final int[][] DIRECTIONS = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}}; // 四方向

    public int orangesRotting(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        int fresh = 0;
        List<int[]> q = new ArrayList<>();
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 1) {
                    fresh++; // 统计新鲜橘子个数
                } else if (grid[i][j] == 2) {
                    q.add(new int[]{i, j}); // 一开始就腐烂的橘子
                }
            }
        }

        int ans = -1;
        while (!q.isEmpty()) {
            ans++; // 经过一分钟
            List<int[]> tmp = q;
            q = new ArrayList<>();
            for (int[] pos : tmp) { // 已经腐烂的橘子
                for (int[] d : DIRECTIONS) { // 四方向
                    int i = pos[0] + d[0];
                    int j = pos[1] + d[1];
                    if (0 <= i && i < m && 0 <= j && j < n && grid[i][j] == 1) { // 新鲜橘子
                        fresh--;
                        grid[i][j] = 2; // 变成腐烂橘子
                        q.add(new int[]{i, j});
                    }
                }
            }
        }

        return fresh > 0 ? -1 : Math.max(ans, 0);
    }
}
```

|      |           | 流出 | 执行                        | 写结果             |
| ---- | --------- | ---- | --------------------------- | ------------------ |
| LD   | F6,34(R2) | 1    | 2                           | 3                  |
| LD   | F2(45)R3  | 2    | 3                           | 4                  |
| MUL  | F0,F2,F4  | 3    | 4                           | 理论13，实际还没写 |
| SUB  | F8,F2,F6  | 4    | 5                           | 7                  |
| DIV  | F10,F0,F6 | 5    | MUL未写结果，F0未知，未执行 |                    |
| ADD  | F6,F8,F2  | 6    | 7                           | 10                 |

