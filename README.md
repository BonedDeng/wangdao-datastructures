2021王道数据结构课后大题代码，使用Visual Studio编程。 考研时主要写的伪代码，记录一下自己将其代码数据结构的历程~  
 代码仅供个人研究，及交流学习使用。  

可不可以点个star呢~

已完结的章节：  
第二章 线性表  
第三章 栈和队列  
第五章 树与二叉树  
第六章 图  
第七章 查找  
第八章 排序  
  
全书更新完毕~  
好耶~   

PS:
第一章绪论与第四章串课后没有需要代码实现的题 

历时3个多月，把21版王道数据结构的课后代码题全部实现了一遍，一共96道题

![题目总数]96

 - 编程环境：Visual Studio 
 - 编程语言：C/C++

其中，每道题都是一个独立的cpp文件，可以独立运行。在树和图的章节，会有输入样例和对应的示例图。

cpp文件结构

 1. 建立要求的数据结构
 2. 题目说明
 3. 题目要求的代码
 4. 运行示例

以图章节的题目示例：

```cpp
#include <iostream>
#include <stack>
#include <queue>
#include <vector>
#include <algorithm>

using namespace std;

#pragma region 创建邻接表存储的有向图

#define MaxVertexNum 10   //图中顶点数目最大值
#define VertexType char
#define _for(i,a,b) for(int i=(a);i<(b);i++)

typedef struct ArcNode {    //边表结点
    int adjvex;             //该弧所指向的顶点的位置
    ArcNode* next;          //指向下一条弧的指针
}ArcNode;

typedef struct VNode {      //顶点表结点
    VertexType data;        //顶点信息
    ArcNode* first;         //指向第一条依附该顶点的弧的指针
}VNode, AdjList[MaxVertexNum];

typedef struct {
    AdjList vertices;       //领接表
    int vexnum, arcnum;     //图的顶点数和弧数
}ALGraph;                   //ALGraph是以邻接表存储的图类型


int LocateVex(ALGraph& G, VertexType x) {

    _for(i, 0, G.vexnum) {
        if (G.vertices[i].data == x)
            return i;
    }
    return -1;
}

void CreateALGraph(ALGraph& G) {

    cout << "输入顶点数和边数" << endl;
    cin >> G.vexnum >> G.arcnum;
    _for(i, 0, G.vexnum) {
        cout << "输入第" << i + 1 << "个顶点的信息" << endl;
        cin >> G.vertices[i].data;
        G.vertices[i].first = NULL;
    }
    _for(k, 0, G.arcnum) {
        VertexType e1, e2;
        cout << "输入第" << k + 1 << "条边（v1 -> v2）的顶点：" << endl;
        cin >> e1 >> e2;
        ArcNode* e = new ArcNode;
        if (!e) {
            cout << "内存申请失败！" << endl;
            exit(0);
        }

        int vi = LocateVex(G, e1);
        int vj = LocateVex(G, e2);

        e->adjvex = vj;                                 //这三步，类似于单链表的头插法
        e->next = G.vertices[vi].first;
        G.vertices[vi].first = e;
    }
}

#pragma endregion

//P254.9
//试说明利用DFS如何实现有向无环图拓扑排序

bool visited[MaxVertexNum];
int topo[MaxVertexNum];
int j = 0;

void DFS(ALGraph G, int i) {         

    ArcNode* p;
    visited[i] = true;              
    p = G.vertices[i].first;       
    while (p) {                    
        if (!visited[p->adjvex])    
            DFS(G, p->adjvex);
        p = p->next;
    }
    topo[j++] = i;
}

void DFSTraverse(ALGraph G) {

    memset(visited, false, sizeof(visited));      
    _for(i, 0, G.vexnum)
        if (!visited[i])
            DFS(G, i);                          
}

void Print_TopologicalSorting(ALGraph G) {
    for (int i = G.vexnum - 1; i >= 0; i--) {
        cout << G.vertices[topo[i]].data << " ";
    }
    cout << endl;
}


int main()
{
    ALGraph G;
    CreateALGraph(G);
    cout << "DFS求拓扑排序:" << endl;
    DFSTraverse(G);
    Print_TopologicalSorting(G);
    return 0;
}

/*
input:

6 7
a b c d e f
a b
a d
c e
c f
d b
e d
f f

有向图链接：https://s3.ax1x.com/2021/02/23/yLASpT.png

*/
```


emm也是记录一下考研那段时光的数据结构的过程，留个回忆~
希望一站成博

顺便点个star呗~

