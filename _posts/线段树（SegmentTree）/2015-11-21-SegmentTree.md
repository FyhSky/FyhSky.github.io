---
layout: post
title: "线段树"
date: 2015-11-21 18:00:00
comments: true
--- 
线段树
============

&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;线段树是一棵树，而且是二叉搜索树。它将一个区间划分成一些单元区间，每个单元区间对应线段树中的一个叶结点。

&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;主要应用：适用于和区间统计有关的问题，例如大数据的动态修改
及多次查询就比较适合使用这种树，效果比较好。

&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;性质：

&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; 1. 树中的每一个结点表示了一个区间[a,b]。a,b通常是整数。

&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; 2. 对于每一个非叶结点所表示的结点[a,b]，其左儿子表示的区间为

&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;   [a,(a+b)/2]，右儿子表示的区间为[(a+b)/2,b]。

 &#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;3. 同一层的节点所代表的区间，相互不会重叠。
 
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; 4. 叶子节点的区间是单位长度，不可再分。


&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;构造过程：

&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; 1. 构造节点node,对应的区间为[start,end]

&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; 2. 构造node的左孩子，对应的区间为[start,start + (end - start) / 2]

&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; 3. 构造node右孩子，对应的区间为[start + (end - start) / 2 + 1,end]

 
 &#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;线段树的构造过程就是二叉树递归的创建的过程，代码如下：
 
```
SegmentTreeNode* SegmentTree::GenerateTree(vector<int> &nums, int start, int end) {
    if(start > end) return nullptr;
    SegmentTreeNode *node = new SegmentTreeNode(start,end);
    if(start == end) {
        node->SetSum(nums[start]);
        return node;
    }
    int mid = start + (end - start) / 2;
    SegmentTreeNode *left = GenerateTree(nums,start,mid);
    SegmentTreeNode *right = GenerateTree(nums,mid+1,end);
    node->SetLeft(left);
    node->SetRight(right);
    node->SetSum(left->GetSum() + right->GetSum());
    return node;
}
```
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;其中SegmentTreeNode 以及 SegmentTree为自己定义的类，最后附上整个的代码。

```
#include <vector>
using namespace std;

class SegmentTreeNode {
public:
    SegmentTreeNode(int a, int b);
    int GetStart();
    int GetEnd();
    void SetSum(int sum);
    int GetSum();
    void SetLeft(SegmentTreeNode* left);
    SegmentTreeNode* GetLeft();
    void SetRight(SegmentTreeNode* right);
    SegmentTreeNode* GetRight();
    
private:
    int start, end, sum;
    SegmentTreeNode* left;
    SegmentTreeNode* right;

};


class SegmentTree {
public:
    void BuildTree(vector<int> &nums, int start, int end);
    SegmentTreeNode *GetRoot();
    int ModifyTree(int i, int val);
    int QueryTree(int i, int j);

private:
    SegmentTreeNode *GenerateTree(vector<int> &nums, int start, int end);
    int _ModifyTree(int i, int val,SegmentTreeNode *node);
    int _QueryTree(int i, int j,SegmentTreeNode *node);
    SegmentTreeNode *root;
};


SegmentTreeNode::SegmentTreeNode(int a, int b):start(a),
                                               end(b),
                                               sum(0),
                                               left(nullptr),
                                               right(nullptr) {
                                                   
                                                   
    
};

int SegmentTreeNode::GetStart() {
    return start;
}
int SegmentTreeNode::GetEnd() {
    return end;
}
void SegmentTreeNode::SetSum(int sum) {
    this->sum = sum;
}
int SegmentTreeNode::GetSum() {
    return sum;
}

void SegmentTreeNode::SetLeft(SegmentTreeNode* left) {
    this->left = left;
}
SegmentTreeNode* SegmentTreeNode::GetLeft() {
    return left;
}
void SegmentTreeNode::SetRight(SegmentTreeNode* right) {
    this->right = right;
}

SegmentTreeNode* SegmentTreeNode::GetRight() {
    return right;
}

void SegmentTree::BuildTree(vector<int> &nums, int start, int end) {
    root = GenerateTree(nums, start, end);
}

SegmentTreeNode* SegmentTree::GenerateTree(vector<int> &nums, int start, int end) {
    if(start > end) return nullptr;
    SegmentTreeNode *node = new SegmentTreeNode(start,end);
    if(start == end) {
        node->SetSum(nums[start]);
        return node;
    }
    int mid = start + (end - start) / 2;
    SegmentTreeNode *left = GenerateTree(nums,start,mid);
    SegmentTreeNode *right = GenerateTree(nums,mid+1,end);
    node->SetLeft(left);
    node->SetRight(right);
    node->SetSum(left->GetSum() + right->GetSum());
    return node;
}

int SegmentTree::ModifyTree(int i, int val) {
    return _ModifyTree(i, val, root);
}

int SegmentTree::QueryTree(int i, int j) {
    return _QueryTree(i, j, root);
}

int SegmentTree::_ModifyTree(int i, int val,SegmentTreeNode *node) {
    if(node == nullptr) return 0;
    int diff;
    if(node->GetStart() == i && node->GetEnd() == i) {
        diff = val - node->GetSum();
        node->SetSum(val);
        return diff;
    }
    int mid = (node->GetStart() + node->GetEnd()) / 2;
    if(i > mid) {
        diff = _ModifyTree(i,val,node->GetRight());
    } else {
        diff = _ModifyTree(i,val,node->GetLeft());
    }
    node->SetSum(node->GetSum() + diff);
    return diff;
}

int SegmentTree::_QueryTree(int i, int j,SegmentTreeNode *node) {
    if(node == nullptr) return 0;
    if(node->GetStart() == i && node->GetEnd() == j) return node->GetSum();
    int mid = (node->GetStart() + node->GetEnd()) / 2;
    if(i > mid) return _QueryTree(i,j,node->GetRight());
    if(j <= mid) return _QueryTree(i,j,node->GetLeft());
    return _QueryTree(i,mid,node->GetLeft()) + _QueryTree(mid+1,j,node->GetRight());
}
```
&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;利用此代码在https://leetcode.com上AC过了两道题目。

> Question 1: Given an integer array nums, find the sum of the elements
> between indices i and j (i ≤ j), inclusive.
> 
> Example: Given nums = [-2, 0, 3, -5, 2, -1]
> 
> sumRange(0, 2) -> 1 sumRange(2, 5) -> -1 sumRange(0, 5) -> -3 Note:
> You may assume that the array does not change. There are many calls to
> sumRange function.
> 
> Question 2: Given an integer array nums, find the sum of the elements
> between indices i and j (i ≤ j), inclusive.
> 
> The update(i, val) function modifies nums by updating the element at
> index i to val. Example: Given nums = [1, 3, 5]
> 
> sumRange(0, 2) -> 9 update(1, 2) sumRange(0, 2) -> 8 Note: The array
> is only modifiable by the update function. You may assume the number
> of calls to update and sumRange function is distributed evenly.

&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;源码的下载地址：https://github.com/FyhSky/SegmentTree