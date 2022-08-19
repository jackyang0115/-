# 线性表
## 顺序表
* 结构体&初始化
```c
//静态
#define MAXSIZE 100
typedef struct{
	ELEMENTTYPE data[MAXSIZE];
	int length;
}SqList;

int initList(SqList &L){
	L.length = 0;
	for(int i = 0;i < MAXSIZE;i++){
		L.data[i] = 0;
	}
	return 1;
}
```
```c
//动态
typedef struct{
	ELEMENTTYPE *data;
	int maxsize;
	int length;
}SqList;

int initList(SqList &L){
	L.maxsize = 100;
	L.length = 0;
	L.data = (ELEMENTTYPE *)malloc(sizeof(ELEMENTTYPE) * maxsize);
	if(L.data == NULL){
		return 0;
	}

	//忘记了！！！
	for(int i = 0;i < maxsize;i++){
		L.data[i] = 0;
	}

	return 1;
}

//动态增加
int dynamicIncrease(SqList &L){
	L.maxsize += 100;
	ELEMENTTYPE *p = L.data;//忘记了!!!
	L.data = (ELEMENTTYPE *)malloc(sizeof(ELEMENTTYPE) * maxsize);
	if(L.data == NULL){
		return 0;
	}
	for(int i = 0;i < length;i++){//如何防止脏数据？
		L.data[i] = p[i];//忘记如何操作指针偏移！！！
	}
	return 1;
}
```
* 增——插
```c
int insertList(SqList &L,int location,ELEMENTTYPE e){
	//不要忘记判合法&判满！！！
	if(location < 0 || location > length){
		return 0;
	}
	if(length == MAXSIZE){
		return 0;
	}
	
	for(int i = length - 1;i >= location;i--){
		L.data[i+1] = L.data[i];
	}
	L.data[location] = e;
	L.length++;//不要忘记！！！
}
```
* 删（按位删除）
```c
int deleteList(SqList &L,int location){
	//不要忘记判合法&判空！！！
	if(location < 0 || location >= length){
		return 0;
	}
	if(length == 0){
		return 0;
	}

	for(int i = location;i < length - 1;i++){
		L.data[i] = L.data[i+1];
	}
	L.length--;
	return 1;
}
```
* 查（按值+顺序 查找）
```c
int indexList(SqList &L,ELEMENTTYPE e){
	for(int i = 0;i < length;i++){
		if(L.data[i] == e){
			return i + 1;
		}
	}
	return 0;
}
```



## 链表
### 单向链表
* ==结构体&初始化==
```c
typedef struct LinkNode{
	ELEMENTTYPE data;
	struct LinkNode *next;//忘记了struct！！！
}LinkNode, *LinkList;

//带头结点
int initLinkList(LinkList &L){
	//分配空间
	L = (LinkNode *)malloc(sizeof(LinkNode));
	if(L == NULL){
		return 0;
	}
	//设置next
	L->next = NULL;
	return 1;
}

//不带头结点
int initLinkList(LinkList &L){
	//设置next
	L->next = NULL;
	return 1;
}
```
* 判空
```c
int isEmpty(LinkList &L){
	if(L->next == NULL){
		return 1;
	}
	return 0;
}

//简单写法
bool isEmpty(LinkList &L){
	return (L->next == NULL);
}
```
* ==增——插==
需要对地址进行操作时，使用指针；需要对内容进行操作时，使用引用。
```c
//前插法（在某结点的前面插入)（不能在最后面添加）
int insertLinkList(LinkList &L,int location,ELEMENTTYPE e){
	if(location < 1) return 0;//判定插入位置合法性
	LinkNode n;

	if(N == NULL) return 0;//判定被插结点是否为空，忘记了！！！
	//创建结点
	LinkNode p = (LinkNode)malloc(sizeof(LinkNode));
	if(p == NULL) return 0;
	//插入结点（先插入后面，再交换值）
	p->next = N->next;
	N->next = p;
	p->data = N->data;
	N->data = e;
}

//后插法（某结点的后面插入）（不能在最前面添加）
int insertLinkList(LinkList &L,int location,ELEMENTTYPE e){
	//创建结点
	LinkNode p = (LinkNode)malloc(sizeof(LinkNode));
	if(p == NULL) return 0;
	//插入结点
	p->next = N->next;
	N->next = p;
	p->data = e;
}
```

### 双向链表

### 循环单向链表

### 循环双向链表

### 静态链表
