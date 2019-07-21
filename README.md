# 链表和指针
静态链表的使用：  
```
typedef Struct Stu
{
  int id;  //数据域
  char name[100];
  struct Stu *next;  //指针域
}Stu;

int main()
{
  //初始化三个结构体对象，这三个结构体之间并无联系
  Stu S1 = {1, "mike",NULL};
  Stu S2 = {2, "mik",NULL};
  Stu S3 = {3, "mi",NULL};
  
  //将三个结构体对象做成链表的形式
  s1.next = &s2;
  s2.next = &s3;
  s3.next = NULL;
  
  //打印内容，先创建结点p，然后结点p不断后移，直到为空
  Stu *p = &s1;
  
  while (p != NULL)
  {
    printf("id = %d,name = %s\n",p->id,p->name);
    //结点后移
    p = p->next;
  }
}
```
静态链表具有一定的局限性，不如动态链表灵活，接下来使用malloc对动态链表分配空间:  
（1）建立链表：创建结构体结点，编写函数SlistCreat，建立带有头结点的单向链表,链表的头结点地址由函数返回  
```
typedef struct Node
{
  int id; 
  struct Node *next;
}Node;

//创建头结点
//链表头结点地址由函数返回
Node *SlistCreat()
{
  Node *head = NULL;
  //头结点作为标志，不存储有效数据,因此赋值为-1，head->next为空
  head = (Node*)malloc(sizeof(Node));
  
  if(head == NULL)
  {
    return NULL;
  }
  
  head->id = -1;
  head->next = NULL;
  
  Node *pCur = head;
  Node *pNew = NULL;
  
  int data;
  
  while(1)
  {
    printf("请输入数据：")；
    scanf("%d", &data);
    if(data==-1)
    {
      break;//跳出while循环
    }
    
    //新结点动态分配空间，如果分配不成功则continue，继续while循环
    pNew = (Node*)malloc(sizeof(Node));
    if(pNew == NULL)
    {
      continue;
    }
    //给pNew成员赋值
    pNew->id = data;
    pNew->next = NULL;
    
    //链表建立关系
    //pCur的下一个结点指向pNew
    //pNew的下一个结点指向NULL
    //pCur指向pNew
    pCur->next = pNew;
    pNew->next = NULL;
    pCur = pNew;
  }
  return head;
}

```
（2）遍历链表：  
```
int SlistPrint()
{
  if(head = NULL)
  {
    return -1;
  }
  
  //取出第一个有效结点（头结点的next）
  Node *pCur = head->next;
  
  while(pCur =!NULL)
  {
    printf("%d", pCur->data);
    pCur = pCur->next;
  }
}
```
（3）向链表中插入结点:  
在值为x的结点前插入y，如果x不存在则插在表尾  
```
int NodeInsert(Node *head, int x, int y)
{
  if(head == NULL)
  {
    return -1;
  }
  Node *pPre = head;
  Node *pCur = head->next;
  
  while(pCur != NULL)
  {
    if(pCur->id == x)  //找到了匹配结点
    {
      break；
    }
    
    //没找到匹配点继续遍历
    pPre = pCur;
    pCur = pCur->next;
    
    //遍历到最后会出现两种结果
    //1；找到了匹配的结点，pCur为最后一个结点，pPre为倒数第二个结点
    //2：没找到匹配的结点，pPre为最后一个结点，pCur指向空
    
    //给新结点动态分配空间
    Node *pNew = (Node *)malloc(sizeof(Node));
    if (pNew == NULL)
    {
      return -2; //遍历完了没有找到，则返回-2
    }
    
    //给pNew的成员变量赋值
    pNew->id = y;
    pNew->next = NULL;
    
    //插入指定位置
    pPre->next = pNew;
    pNew->next = pCur;
  }
}
```
注：c++中经常会看到return 0，-1，-2，这个要看编辑者的意图，一般0表示正确结束，其他数字代表不同的错误  
