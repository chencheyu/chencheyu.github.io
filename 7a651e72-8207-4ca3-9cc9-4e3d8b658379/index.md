---
date: 2025-03-08
publish: true
slug: 14a935d5-c143-4654-bdd7-40c74ed567a9
tags:
- CS/Sitcon2025
title: Heap.md
uuid: 5046860f-3b05-454d-b1b5-13d6789629f1
---
https://docs.google.com/presentation/d/1sHGLOxjZtccfWvdpzXdfbMnH8qeix-fh/mobilepresent?slide=id.p1
Heap 是處理極值的資料結構
完全二元樹所有的父節點都比子節點要小，就屬於 min heap
只交換左右子節點，確定交換子樹

## 複雜度

| 操作      | 描述                    | 時間複雜度    |
| ------- | --------------------- | -------- |
| build   | 採用羅伯特·弗洛伊德提出的較快方式建立堆積 | O(n)     |
| insert  | 向堆積中插入一個新元素           | O(log⁡n) |
| update  | 將新元素提升使其符合堆積的性質       | O(log⁡n) |
| get     | 取得當前堆積頂元素的值           | O(1)     |
| delete  | 刪除堆積頂元素，有時稱 Peek      | O(log⁡n) |
| heapify | 使刪除堆積頂元素的堆積再次成為堆積     | O(log⁡n) |

## l

通常實做會將完全二元樹放置在 Array 中
節點的索引為 i（假設根節點的索引為0）則在它左子節點的索引會是 $2 * index + 1$，以及右子節點會是 $2 * index + 2$；而它的父節點（如果有）索引則為  $(index - 1) // 2$

## Insert

Insert 為把新節點插在樹的最後一格，在跟 Parent 確定是否需要交換，直到根節點

## Peek

Peek (刪除極值) 用樹的最後一格覆蓋樹根，在移除最後一格，在跟左右子節點確定是否需要交換，直到樹葉節點

## Heapify

Heapify 是將部分無序的堆調整為合法堆的操作。

Heapify 操作步驟
從根節點開始，與左右子節點比較。
與較小的子節點交換。
遞迴向下調整，直到滿足堆性質。

```cpp
template <class  T>
class MinHeap{
    std::deque<T> Arr;
    inline bool HeapEmpty(void){
        return Arr.size() == 0;
    }
    inline void Swap(size_t i, size_t j){
        T tmp = Arr.at(i);
        Arr[i] = Arr.at(j);
        Arr[j] = tmp;
    }
    inline size_t Parent(size_t i){
        return (i - 1) / 2;
    }
    inline size_t LeftChild(size_t i){
        return (i * 2) + 1;
    }
    inline size_t RightChild(size_t i){
        return (i * 2) + 2;
    }

public:
    long Find(T t){
        for(size_t i = 0; i < Arr.size(); ++i){
            if(t == Arr[i]){
                return (long)i;
            }
        }
        return -1;
    }
    void Insert(T t){
        size_t newNode, parent;

        newNode = Arr.size();
        Arr.push_back(t);
        while(newNode != 0){
            parent = Parent(newNode);
            if(Arr.at(parent) > t){
                Swap(parent, newNode);
                newNode = parent;
            }else{
                break;
            }
        }
    }

    T Peek(void){
        T min = Arr.at(0);
        size_t curNode = 0, ChildNode;
        Swap(0, Arr.size() - 1);
        Arr.pop_back();
        while(true){
            ChildNode = LeftChild(curNode);
            if(ChildNode >= Arr.size()){
                break;
            }
            if(Arr.at(curNode) > Arr.at(ChildNode)){
                Swap(curNode, ChildNode);
                curNode = ChildNode;
                continue;
            }
            ChildNode = RightChild(curNode);
            if(ChildNode >= Arr.size()){
                break;
            }
            if(Arr.at(curNode) > Arr.at(ChildNode)){
                Swap(curNode, ChildNode);
                curNode = ChildNode;
                continue;
            }
            break;
        }
        return min;
    }
};
```

優化目標
減少比較次數，相較教科書版本，可節省約 50%。

優化策略
由根節點開始，只比較左右子節點，不交換。
持續向下比較，直到找到應該放置的位置（即到達葉節點）。
從葉節點往上，找到適合放置根節點的最小值位置。

時間複雜度分析
第一階段（尋找下沉路徑）： O(log N) 次比較。
第二階段（上濾）： 通常 O(1) 次比較。
總比較次數： 約 log₂(N) + O(1)，相比標準版本減少 50%
當我們存取節點時，不希望重複計算 index * size
所以不存 index，而改存 i = index * size

- 傳統方式 

- 計算 parent index: $(index - 1) // 2$

直接存 node 指針，減少乘法運算
contanerof 檢查結構是否存在 nr ，不能保證 100％ 能動
