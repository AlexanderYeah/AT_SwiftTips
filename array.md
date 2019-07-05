### 数组的常用方法

swift 数组有很多的操作方法，但是用的时候用常常想不起来，就列出来看看



| map 和 flatMap |   对数组中的元素进行变形操作   |
| :------------: | :----------------------------: |
|     filter     |       主要对数组进行过滤       |
|     reduce     |       主要对数组进行计算       |
|      sort      |         对数组进行排序         |
|    forEach     |       循环遍历每一个元素       |
|   min 和 max   | 找出数组中最大元素和最小的元素 |
|      drop      |            丢弃元素            |
|    contains    |      元素是否符合某个条件      |
|     index      |              索引              |
| first 和 last  |           开始和末尾           |







```swift

let array1 = ["1","2","3","4","5"];

// 1 普通遍历操作
for  i in array1 {
    print(i);
}


// 2 迭代除了第一个元素之外的所有元素
for i in array1.dropFirst(){
      print(i);
}

// 3 迭代除了最后N个元素之外的所有元素
for i in array1.dropLast(2){
    print(i);
}

// 4 寻找一个指定的元素第一个索引
array1.firstIndex(of: "1");

// 5 筛选出符合某种标准的元素的索引
// filter 是一个高阶函数 因为其本身可以接受函数作为参数 所以称之为高阶函数
// 返回值是一个符合筛选条件的数组

// 找出数组中 大于 2 的元素
let resArr1 = array1.filter { (str) -> Bool in
    return Int(str)! > 2;
}

// 简化的写法是 直接在闭包当中书写判断的表达式
let resArr2 = array1.filter{ Int($0)! > 2 }


// ["3", "4", "5"]
print(resArr1);
print(resArr2);

// 6 filter 的用法
let array2 = ["apple","banana","watermelon","orange"];

// 筛选出字符小于6的元素
let res3 = array2.filter{ $0.count > 6};
// 筛选出字符包含p的元素
let res4 = array2.filter{ $0.contains("p")};

// ["watermelon"]
print(res3);
// ["apple"]
print(res4);



// 7 map 对数组中的元素进行变形操作
let array3 = [2,5,8];
// 对每一个元素+5操作
let res5 = array3.map { (idx) -> Int in
    return idx + 5;
}

// 简化的操操作
let res6 = array3.map{idx in idx + 10};


// [7, 10, 13]
print(res5);
// [12, 15, 18]
print(res6);


// 8 reduce 操作

let array4 = [1,2,3,4,5];

// 8.1 计算数组之和
let red_res1 = array4.reduce(10){
    // $0 代表计算后的结果
    // $1 代表单个的元素
    // 10 代表 $0 = 10
    $0 + $1;
};

// 25
print(red_res1);

// 8.2 另外一种形式的计算
let total_count = array4.reduce(0){(x,y) -> Int in
    
    return x + y;
}

print(total_count);


// 9 sort 排序方法
// 进行大小的结果排序
let array5 = [5,8,2,15];
let sort_res1 =  array5.sorted(){
    $0 < $1;
}

let sort_res2 =  array5.sorted{$0 < $1}

//[2, 5, 8, 15]
print(sort_res1);
print(sort_res2);


// 10  获取数组中的最大值 最小值

print(array5.max() as! Int);
print(array5.min() as! Int);

// 11 forEach 循环遍历每一个元素
array5.forEach { (idx) in
    print(idx);
}


// 12 contains 元素是否符合某个条件
// 判断数组中是否有大于5的元素
array5.contains{$0 > 5};
```



