## 1 序列 Sequence

序列协议是集合类型结构中的基础。

一个序列是代表有一系列具有相同类型的值，并且对这些值进行迭代。



协议中主要有两个参数，一个是元素Element，一个就是迭代器Iterator

```swift
    /// A type representing the sequence's elements.
    associatedtype Element where Self.Element == Self.Iterator.Element

    /// A type that provides the sequence's iteration interface and
    /// encapsulates its iteration state.
    associatedtype Iterator : IteratorProtocol

    /// Returns an iterator over the elements of this sequence.
    __consuming func makeIterator() -> Self.Iterator
```





迭代器是遵守 IterratorProtocal 协议的，其核心方法就是next(),每一次的调用就会返回下一个元素，一直到最后的值为空的时候，不再进行返回。其实代码的英文注释也是蛮清楚的😁

```swift
public protocol IteratorProtocol {

    /// The type of element traversed by the iterator.
    associatedtype Element

    /// Advances to the next element and returns it, or `nil` if no next element
    /// exists.
    ///
    /// Repeatedly calling this method returns, in order, all the elements of the
    /// underlying sequence. As soon as the sequence has run out of elements, all
    /// subsequent calls return `nil`.
    ///
    /// You must not call this method if any other copy of this iterator has been
    /// advanced with a call to its `next()` method.
    ///
    /// The following example shows how an iterator can be used explicitly to
    /// emulate a `for`-`in` loop. First, retrieve a sequence's iterator, and
    /// then call the iterator's `next()` method until it returns `nil`.
    ///
    ///     let numbers = [2, 3, 5, 7]
    ///     var numbersIterator = numbers.makeIterator()
    ///
    ///     while let num = numbersIterator.next() {
    ///         print(num)
    ///     }
    ///     // Prints "2"
    ///     // Prints "3"
    ///     // Prints "5"
    ///     // Prints "7"
    ///
    /// - Returns: The next element in the underlying sequence, if a next element
    ///   exists; otherwise, `nil`.
    mutating func next() -> Self.Element?
}

```



所以呢，要是自己定义一个sequence，只需要实现markIterator方法就可以了



```swift
// 自定义反转一个迭代器

// 先定义一个实现IteratorProtocol 的类型
struct ReverseIterator<T>:IteratorProtocol{
    typealias Element = T;
    
    var arr : [Element];
    var idx = 0;
    
    init(arr:[Element]) {
        self.arr = arr;
        idx = arr.count - 1;
    }
    
    
    mutating func next() -> T? {
        if idx < 0 {
            return nil;
        }else{
            let ele = arr[idx];
            idx = idx - 1;
            return ele;
        }
    }
}


// 再来定义sequence

struct ReverceSequence<T>:Sequence{
    
    var arr:[T];
    
    init(arr:[T]) {
        self.arr = arr;
    }
    
    __consuming func makeIterator() -> ReverseIterator<T> {
        return ReverseIterator(arr: self.arr);
    }
}



//
let array = [2,5,8,10];
for i in ReverceSequence(arr: array){
    // 10 8 5 2
   print(i, separator: "-", terminator: "-");
}




```



## 2 子序列 SubSequence

子序列作为序列的关联类型，SubSequence 常常用作返回值的子类型。

1 prefix  和 suffix  获取开头和结尾的n个元素

2 prefix（while:） 从开始开始 满足结束为止

3 dropFirst 和 dropLast 移除第一个或者最后一个

4 drop（while:）移除元素 知道条件不为真的时候

5 spilt   按照指定的分割元素截断操作

```swift
let array2 = [1,2,5,8];
 	
let iterator1 =  array2.makeIterator();
// 
for i  in array2.dropFirst(){
    print(i);
}
```

