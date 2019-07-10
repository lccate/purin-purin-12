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
静态链表具有一定的局限性，
