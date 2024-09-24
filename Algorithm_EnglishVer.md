# Algorithm

## Divide And Rule

In my view, DivideAndRule is a method which can make a very big problem divide into pieces of small and same questions.
Always, these small questions have the same mode, if you understand what this mode actually is, then, the solution of this problem is easy to get.
For example, here is a classic problem about Divide and Rule --- Hanoi Tower.

```
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <cmath>
using namespace std;
void Hanoi(int n, char first, char second, char third);
int main(void) {
   int n;

   cin >> n;

   cout << pow(2, n) - 1 << "\n";

   Hanoi(n, 'A', 'C', 'B');

    return 0;
}

void Hanoi(int n, char first, char second, char third) {
    if(n == 0) {
        return;
    }
    else {
        Hanoi(n - 1, first, third, second);
        cout << first << "->" << second << "\n";
        Hanoi(n - 1, third, second, first);
    }
}
```
Trough this example, you can clearly understand how the Divide and Rule run.
The Recursion use this method usually, and recusion is also used on Graph and Tree.
Though this part seems easy to understand, it always hard to edit the Recursive boundary and Recurive condition. Those are most improtant in Recusion.

## Tree
Tree is one of the hardest parts to learn in Algoritim.

I won't introduce the concepts of Tree one by one, those mostly repeat in Discrete mathematics. So, there only list some concepts of Binary tree.

Since I'm a Chinese, I study with the profile with Chinse for the most part. I will try my best to describe these concepts with my understanding in English.

### The difference of Binary Tree and Normal Tree
1.Every node have two childs most.

2.The lchild and rchild have sequence, they cann't be upside down.

### Storage Structure of Binary Tree
#### Sequential Storage
This way to store the Binay Tree utilize the arry.
```
typedef struct {
    int data;
    int lchild;
    int rchild;
} BNode[MAXSIZE];
```

### Chain Storage
This way to store the Binary Tree utilize the Binary linked list.
```
typedef struct BNode{
    int data;
    struct BNode lchild;
    struct BNode rchild;
}BNode, Bitree;
```

### Pre-order traversal
### Mid-order traversal
### Post-order traversal
These three methods is amostly same, so we disguss together.

They all use the recusion to implemente.

The code as follow:
```
void preOrder(int root) {
    if (root == -1) {
        return;
    }
    pre.push_back(root);
    preOrder(nodes[root].l);
    preOrder(nodes[root].r);
}

void Midorder(int root) {
    if(root == -1) {
        return;
    }
    else {
        Midorder(node[root].l);
        pre.push_back(root);
        Midorder(node[root].r);
    }
}

void Postorder(int root) {
    if(root == -1) {
        return;
    }
    else {
        Postorder(node[root].l);
        Postorder(node[root].r);
        pre.push_back(root);
    }
}
```

### Layer-order traversal
This method to traversal use queue to implementation.

Why? Well, if you just push every node into the vector you define, then you will forget one thing: the layers!

What as said above ignore every node is itself's root node, since it only  push itself and it's left child and right child into the vector, and using the recusion to contine. It didn't pay attention to one layer' s nodes of the Tree is next layer's roots. Then, The trouble it makes is that the output will be like the Pre-order traversal or others, because it use recusion which can't distinguish nodes's relationship.

So, how to use queue to solve this problem? First, Let's make clear that the function of queue in this situation. The queue's property is "First in First out", so, we can utilize it to push the root node's left child into the vector first. What different with the wrong way is, it push the root and it's childs at once, but only output the head of queue at next loop. It means, at next loop, we will push next node and it' s childs, and only output the head of queue, namely, the upper layer' s rchild, then, the nodes is placed layer by layer throuth queue with the queue's property of delaying to output.

The code as follow:
```
#include <iostream>
#include <string>
#include <vector>
#include <map>
#include <stack>
#include <queue>
#define MAXLIM 50
using namespace std;


struct Node {
    int l, r;
}node[MAXLIM];

vector<int> pre;

void Layorder(int root, int n);
int main(void) {
    int n;
    cin >> n;
    
    for(int i = 0; i < n; i++) {
        cin >> node[i].l >> node[i].r;
    }
    Layorder(0, n);
    for(int i = 0; i < (int)pre.size(); i++) {
        cout << pre[i];
        if(i < (int)pre.size() - 1) {
            cout << " ";
        }
    }
    return 0;
}

void Layorder(int root, int n) {
    queue<int> q;
    q.push(root);
    while (!q.empty()) {
        int current = q.front();
        q.pop();
        pre.push_back(current);
        if(node[current].l != -1)
            q.push(node[current].l);
        if(node[current].r != -1)
            q.push(node[current].r);
    }
}
```
### The Height and Depth of Binary Tree
