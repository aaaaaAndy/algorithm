十大排序算法时间负责度，空间复杂度与稳定性汇总：

<img src="https://raw.githubusercontent.com/aaaaaAndy/picture/main/images/20211129163249.png" alt="fuzadu" style="zoom:67%;" />

## 一、冒泡排序

**冒泡排序**是最简单的的排序算法。它的思想是重复遍历相邻元素，将需要冒泡的元素一步步交换到顶部。

算法描述如下：

1.   比较相邻的两个元素，如果第一个比第二个大，则交换它们的位置；
2.   从头到尾循环对比相邻元素，等一轮循环结束，那最后一位一定是最大的元素；
3.   再开启新一轮循环进行对比交换，只是这次只需要对比到上一次循环结束时的前一位元素；
4.   重复步骤`1~3`，直到两层循环对比交换结束，即排序完成。

代码实现如下，

-   时间复杂度最好：O(n)
-   时间复杂度最坏：O(n<sup>2</sup>)
-   时间复杂度平均：O(n<sup>2</sup>)

-   空间复杂度：O(1)
-   稳定性：稳定

```javascript
function bubbleSort(list) {
  let tmp;

  for (let i = 0; i < list.length; i++) {
    for (let j = 0; j < list.length - i - 1; j++) {
      if (list[j] > list[j + 1]) {
        tmp = list[j];
        list[j] = list[j + 1];
        list[j + 1] = tmp;
      }
    }
  }

  return list;
}
```

## 二、选择排序

**选择排序**也是一种比较简单的算法，它的思想就是一次次找到当前列表中剩余元素的最小值，然后放到正确的位置上。

算法描述如下：

1.   定义数组下标起始位置`n = 0`；
2.   一次遍历找到数组中最小元素下标`minIndex`，将其与下标`n`对应的值交换位置，此时数组前`n`项已确定序列；
3.   `n += 1`，再次遍历剩余元素，重复第`2`步，一次类推，直至两层循环遍历完成，即数组有序。

代码示例如下：

-   时间复杂度最好：O(n<sup>2</sup>)
-   时间复杂度最坏：O(n<sup>2</sup>)
-   时间复杂度平均：O(n<sup>2</sup>)
-   空间复杂度：O(1)
-   稳定性：不稳定

```javascript
function selectSort(list) {
  let minIndex;
  let tmp;

  for (let i = 0; i < list.length; i++) {
    minIndex = i;
    for (let j = i + 1; j < list.length; j++) {
      if (list[j] < list[minIndex]) {
        minIndex = j;
      }
    }

    tmp = list[i];
    list[i] = list[minIndex];
    list[minIndex] = tmp;
  }

  return list;
}
```

## 三、插入排序

**插入排序**与生活中的打扑克类似，即拿到一张牌，就找到它正确的位置插入就行了。

算法描述如下：

1.   从第一个元素开始，可认为第一个元素为有序序列；
2.   取出下一个元素，在已经排序的元素中从后往前扫描；
3.   如果扫描到的元素大于取出的元素，则将扫描到的元素后移以为；
4.   重复第`3`步，知道找到取出元素小于或等于扫描元素的位置；
5.   将取出元素插入到该扫描元素后；
6.   重复步骤`2~5`知道序列有序；

代码示例如下：

-   时间复杂度最好：O(n)
-   时间复杂度最坏：O(n<sup>2</sup>)
-   时间复杂度平均：O(n<sup>2</sup>)

-   空间复杂度：O(1)
-   稳定性：稳定

```javascript
function insertSort(list) {
  let j;
  let selectValue;

  for (let i = 1; i < list.length; i++) {
    selectValue = list[i];
    j = i - 1;

    while (j >=0 && list[j] > selectValue) {
      list[j + 1] = list[j];
      j--;
    }

    // 注意这里是j + 1
    list[j + 1] = selectValue;
  }

  return list;
}
```



## 四、希尔排序



## 五、归并排序

**归并排序**的性能不受输入数据的影响，因为始终都是O(nlog<sub>2</sub>n)的复杂度，代驾是需要额外的存储空间。它是采用**分治**的思想：先确保每一个子序列都有序，再将两个有序的子序列合并成一个完整的父序列，直至顶层序列。

算法描述如下：

1.   把长度为`n`的序列分为两个长度为`n / 2`的子序列；
2.   对两个子序列继续拆分，知道每个子序列都只有一个元素，此时可认为最终的所有子序列都是有序的；
3.   将有序子序列合并成一个父序列，再将父序列作为新的子序列进行合并，直至数组合并完成；
4.   最终得到一个有序的序列。

代码示例如下：

-   时间复杂度最好：O(nlog<sub>2</sub>n)
-   时间复杂度最坏：O(nlog<sub>2</sub>n)
-   时间复杂度平均：O(nlog<sub>2</sub>n)
-   空间复杂度：O(n)
-   稳定性：稳定

```javascript
**
 * 该函数主要将列表组合
 * @param {array} left 列表1
 * @param {array} right 列表2
 * @return {*[]}
 */
function merge(left, right) {
  const result = [];
  let i = 0;
  let j = 0;

  while (i < left.length && j < right.length) {
    if (left[i] <= right[j]) {
      result.push(left[i]);
      i++;
    } else {
      result.push(right[j]);
      j++;
    }
  }

  while (i < left.length) {
    result.push(left[i]);
    i++;
  }

  while (j < right.length) {
    result.push(right[j]);
    j++
  }

  return result;
}

/**
 * 改函数主要将列表拆开
 * @param {array} arr 待拆开列表
 * @return {*[]|*}
 */
function mergeSort(arr) {
  if (arr.length < 2 ) {
    return arr;
  }

  const mid = Math.floor(arr.length / 2);

  const left = mergeSort(arr.slice(0, mid));
  const right = mergeSort(arr.slice(mid));

  return merge(left, right);
}
```





## 六、快速排序

**快速排序**的最大特点就是快，它的想是先选出一个基准值，通过一次排序将数组分成两部分，其中一部分比基准值都小，另一部分比基准值都大，当然，相等的情况除外，然后继续对两部分进行递归处理，直至这个队列有序。

算法描述如下：

1.   从数列中选择一个元素作为基准值；
2.   设置两个指针，一个从头到尾遍历，一个从尾到头遍历，通过一轮遍历，确保基准值左边都是比它小的值，基准值右边都是比它大值，等于基准值时放在哪一边都可；
3.   递归处理基准值两个的两部分，将其分别作为一个新序列重新执行`1~2`，直至队列有序。

代码示例如下：

-   时间复杂度最好：O(nlog<sub>2</sub>n)
-   时间复杂度最坏：O(n<sup>2</sup>)
-   时间复杂度平均：O(nlog<sub>2</sub>n)

-   空间复杂度：O(n)
-   稳定性：不稳定

```javascript
function quickSort(arr, left, right) {
  if (left < right) {
    let i = left + 1;
    let j = right;
    let num = arr[left];
    let tmp;

    while (i < j) {
      while (arr[j] > num && i < j) j--;
      while (arr[i] < num && i < j) i++;

      tmp = arr[i];
      arr[i] = arr[j];
      arr[j] = tmp;
    }

    if (num > arr[i]) {
      arr[left] = arr[i];
      arr[i] = num;
    }

    quickSort(arr, left, i - 1);
    quickSort(arr, i + 1, right);
  }
}
```



## 七、堆排序



## 八、计数排序



## 九、桶排序



## 十、基数排序







###### 洗牌算法

###### 版本号比较大小

###### 广度优先遍历

###### 用O(n)复杂度合并两个有序数组

###### 数组生成树形结构

