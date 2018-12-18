/* Linear Table On Sequence Structure */
#include <stdio.h>
#include <malloc.h>
#include <stdlib.h>

/*---------page 10 on textbook ---------*/
#define TRUE 1
#define FALSE 0
#define OK 1
#define ERROR 0
#define INFEASTABLE -1
#define OVERFLOW -2

typedef int status;
typedef struct
{
    int key;       //序号key
    char other;    //字符other
} ElemType;   //定义结构类型ElemType,包含序号key和字符other

/*-------page 22 on textbook -------*/
#define LIST_INIT_SIZE 100
#define LISTINCREMENT  10
typedef struct BiTNode
{
    ElemType data;    //结点数据域
    struct BiTNode *lchild, *rchild;  //结点指针域包含左孩子指针和右孩子指针
} BiTNode, *BiTreep;       //定义结点BiTNode，结点指针BiTreep

typedef struct
{
    BiTreep T;   //结点指针
    int length;   //二叉树长度
} BiTreepList;  //定义二叉树表来存储多个二叉树
static int dataNum=0;
status InitBiTree(BiTreep *T);
status DestroyBiTree(BiTreep *T);
status CreateBiTree(BiTreep *T,ElemType *data);
status ClearBiTree(BiTreep *T);
status BiTreeEmpty(BiTreep T);
status BiTreeDepth(BiTreep T);
char Root(BiTreep T);
char Value(BiTreep T, int e);
status Assign(BiTreep T, int e, char ch);
BiTNode* Parent(BiTreep T, int e);
BiTNode* LeftChild(BiTreep T, int e);
BiTNode* RightChild(BiTreep T, int e);
BiTNode* RightSibling(BiTreep T, int e);
BiTNode* LeftSibling(BiTreep T, int e);
BiTreep LocateNode(BiTreep T, int e);
status InsertChild(BiTreep T, BiTreep p, int LR, BiTreep c);
status DeleteChild(BiTreep T, BiTreep p, int LR);
status visit(ElemType data);
status PreOrderTraverse(BiTreep T, status (* visit)(ElemType data));
status InOrderTraverse(BiTreep T, status (* visit)(ElemType data));
status PostOrderTraverse(BiTreep T, status (* visit)(ElemType data));
status LevelOrderTraverse(BiTreep T, status (* visit)(ElemType data));
status Save(BiTreep T,FILE *fp);
status Load(BiTreep *T,FILE *fp);
status TreeDisplay(BiTreep T,int depth,status (* visit)(ElemType data));
status isKeyRepeat(BiTreep T);
int main()
{
    int n=2,k,num;
    printf("请输入你要操作的二叉树的个数:");
    do
    {
        scanf("%d",&n);
        if(n<1)      //判断n是否合法
            printf("个数有误!,请重新输入:");   //如果n不合法，提示重新输入
        fflush(stdin);    //清空缓冲区
    }
    while(n<1);
    BiTreepList L[n];                  //根据用户输入的n,创建n个二叉树的数组
    int op=1;                  //定义用户操作变量
    for(k=0; k<n; k++)
    {
        L[k].T=NULL;
        L[k].length=0;
    }
    num=0;
    while(op)
    {
        system("cls");
        printf("\n\n");

        printf("\t\t      Menu for Binary Tree On Chain Structure \n");
        printf("-------------------------------------------------------------------------------\n");
        printf("1.  InitBiTree           2.  DestroyBiTree\n");
        printf("3.  CreateBiTree         4.  ClearBiTree\n");
        printf("5.  BiTreeEmpty          6.  BiTreeDepth\n");
        printf("7.  Root                 8.  Value\n");
        printf("9.  Assign               10. Parent\n");
        printf("11. LeftChild            12. RightChild\n");
        printf("13. LeftSibling	         14. RightSibling\n");
        printf("15. InsertChild	         16. DeleteChild\n");
        printf("17. PreOrderTraverse     18. InOrderTraverse\n");
        printf("19. PostOrderTraverse    20. LevelOrderTraverse\n");
        printf("21. Choose(切换树)       22. Save(保存到文件中)\n");
        printf("23. Load(载入文件)       24. TreeDisplay(文件目录格式显示)\n");
        printf("0.  Exit\n");
        printf("----------------------------------------------------------------------------------\n");
        printf("请选择你的操作[0~24]:");
        scanf("%d",&op);
        switch(op)
        {
        case 1:
        {
            if(InitBiTree(&(L[num].T))==OK)
                printf("二叉树创建成功！\n");
            else
                printf("创建失败!\n");
            getchar();
            getchar();
            break;
        }
        case 2:
        {
            if (!L[num].T)
            {
                printf("二叉树不存在！");
                getchar();
                getchar();
                break;
            }
            if(DestroyBiTree(&L[num].T)==OK)
                printf("二叉树销毁成功！\n");
            else
                printf("二叉树销毁失败！\n");
            getchar();
            getchar();
            break;
        }
        case 3:
        {
            int i=0;
            if (!L[num].T)
            {
                printf("二叉树不存在！");
                getchar();
                getchar();
                break;
            }
            printf("请用前序方式构建二叉树，#表示空结点！@表示结束!\n");
            ElemType data[1000];
            dataNum=0;
            do
            {
                fflush(stdin);
                printf("请输入data:");
                scanf("%c",&data[i].other);
                if(data[i].other!='@'&&data[i].other!='#')
                {
                    getchar();
                    printf("请输入key:");
                    scanf("%d",&data[i].key);
                }
            }
            while(data[i++].other!='@'&&i<1000);
            if(CreateBiTree(&(L[num].T->lchild),&data[0])==OK)
            {
                if(isKeyRepeat(L[num].T->lchild)==TRUE)
                {
                    ClearBiTree(&(L[num].T->lchild));
                    printf("存在相同的key，创建失败！\n");
                }
                else
                    printf("二叉树构造成功！\n");
            }
            else
                printf("二叉树构造失败!\n");
            getchar();
            getchar();
            break;
        }
        case 4:
        {
            if (!L[num].T)
            {
                printf("二叉树不存在！");
                getchar();
                getchar();
                break;
            }
            if(ClearBiTree(&(L[num].T->lchild)) == OK)
                printf("二叉树清空成功！\n");
            else
                printf("二叉树清空失败！\n");
            getchar();
            getchar();
            break;
        }
        case 5:
        {
            if (!L[num].T)
            {
                printf("二叉树不存在！");
                getchar();
                getchar();
                break;
            }
            if(BiTreeEmpty(L[num].T->lchild) == OK)
                printf("二叉树为空树！\n");
            else
                printf("二叉树非空！\n");
            getchar();
            getchar();
            break;
        }
        case 6:
        {
            if (!L[num].T)
            {
                printf("二叉树不存在！");
                getchar();
                getchar();
                break;
            }
            if(BiTreeEmpty(L[num].T) == OK)
                printf("二叉树为空树！深度为0\n");
            else
                printf("二叉树的深度为%d\n", BiTreeDepth(L[num].T->lchild));
            getchar();
            getchar();
            break;
        }
        case 7:
        {
            if (!L[num].T)
            {
                printf("二叉树不存在！");
                getchar();
                getchar();
                break;
            }
            if(BiTreeEmpty(L[num].T->lchild) == OK)
            {
                printf("二叉树为空树！\n");
                getchar();
                getchar();
                break;
            }
            printf("二叉树的根为%c\n", Root(L[num].T->lchild));
            getchar();
            getchar();
            break;
        }
        case 8:
        {
            int e;
            char c;
            if (!L[num].T)
            {
                printf("二叉树不存在！");
                getchar();
                getchar();
                break;
            }
            printf("请输入你要查找的key:");
            scanf("%d", &e);
            c=Value(L[num].T->lchild,e);
            if ( c!= ERROR)
                printf("该key对应的data为：%c", c);
            else
                printf("该key不存在！");
            getchar();
            getchar();
            break;
        }
        case 9:
        {
            int e;
            char c;
            if (!L[num].T)
            {
                printf("二叉树不存在！");
                getchar();
                getchar();
                break;
            }
            printf("请输入你要查找的key:");
            scanf("%d", &e);
            getchar();
            printf("请输入你要重新赋值的data:");
            scanf("%c", &c);
            if (Assign(L[num].T->lchild, e, c)==OK)
                printf("修改成功！");
            else
                printf("该key不存在！");
            getchar();
            getchar();
            break;
        }
        case 10:
        {
            int e;
            BiTreep parent;
            if (!L[num].T)
            {
                printf("二叉树不存在！");
                getchar();
                getchar();
                break;
            }
            if(BiTreeEmpty(L[num].T->lchild) == OK)
            {
                printf("二叉树为空树！\n");
                getchar();
                getchar();
                break;
            }
            printf("请输入你要查找父母的key:");
            scanf("%d",&e);
            parent=Parent(L[num].T->lchild,e);
            if (parent)
            {
                printf("双亲对应的data为：%c\n双亲对应的key为：%d",parent->data.other,parent->data.key );
            }
            else
            {
                printf("双亲不存在！");
            }
            getchar();
            getchar();
            break;
        }
        case 11:
        {
            int e;
            BiTreep lchild;
            if (!L[num].T)
            {
                printf("二叉树不存在！");
                getchar();
                getchar();
                break;
            }
            printf("请输入你要查找左孩子的key:");
            scanf("%d", &e);
            lchild=LeftChild(L[num].T->lchild,e);
            if (lchild)
            {
                printf("左孩子对应的data为：%c\n左孩子对应的key为：%d",lchild->data.other,lchild->data.key);
            }
            else
                printf("左孩子不存在！");
            getchar();
            getchar();
            break;
        }
        case 12:
        {
            int e;
            BiTreep rchild;
            if (!L[num].T)
            {
                printf("二叉树不存在！");
                getchar();
                getchar();
                break;
            }
            printf("请输入你要查找右孩子的key:");
            scanf("%d", &e);
            rchild=RightChild(L[num].T->lchild,e);
            if (rchild)
                printf("右孩子对应的data为：%c\n右孩子对应的key为：%d",rchild->data.other,rchild->data.key);
            else
                printf("右孩子不存在！");
            getchar();
            getchar();
            break;
        }
        case 13:
        {
            int e;
            BiTreep lsibling;
            if (!L[num].T)
            {
                printf("二叉树不存在！");
                getchar();
                getchar();
                break;
            }
            printf("请输入你要查找左兄弟的key:");
            scanf("%d", &e);
            lsibling=LeftSibling(L[num].T->lchild,e);
            if (lsibling)
                printf("左兄弟对应的data为：%c\n左兄弟对应的key为：%d",lsibling->data.other,lsibling->data.key);
            else
                printf("左兄弟不存在！");
            getchar();
            getchar();
            break;
        }
        case 14:
        {
            int e;
            BiTreep rsibling;
            if (!L[num].T)
            {
                printf("二叉树不存在！");
                getchar();
                getchar();
                break;
            }
            printf("请输入你要查找右兄弟的key:");
            scanf("%d", &e);
            rsibling=RightSibling(L[num].T->lchild,e);
            if (rsibling)
                printf("右兄弟对应的data为：%c\n右兄弟对应的key为：%d", rsibling->data.other,rsibling->data.key);
            else
                printf("右兄弟不存在！");
            getchar();
            getchar();
            break;
        }
        case 15:
        {
            int e,LR;
            BiTreep T1,p;
            if (!L[num].T)
            {
                printf("二叉树不存在！");
                getchar();
                getchar();
                break;
            }
            printf("请输入你要插入位置的key: ");
            scanf("%d", &e);
            getchar();
            p = LocateNode(L[num].T->lchild,e);
            if (!p)
            {
                printf("该位置不存在!\n");
                getchar();
                getchar();
                break;
            }
            printf("请输入你想要插入的方向0或1，0表示左边，1表示右边: ");
            scanf("%d", &LR);
            fflush(stdin);
            int i;
            do
            {
                printf("请用前序方式构建要插入的二叉树(右子树为空)，#表示空结点！@表示结束!\n");
                ElemType data[1000];
                dataNum=0;
                i=0;
                do
                {
                    fflush(stdin);
                    printf("请输入data:");
                    scanf("%c",&(data[i].other));
                    if(data[i].other!='#'&&data[i].other!='@')
                    {
                        getchar();
                        printf("请输入key:");
                        scanf("%d",&data[i].key);
                    }
                }
                while(data[i++].other!='@'&&i<1000);
                CreateBiTree(&T1,data);
                if(!T1)
                    printf("树为空，请重新输入！\n");
                else if(T1->rchild)
                    printf("右子树不为空，请重新输入!\n");
            }
            while((!T1)||T1->rchild);
            if (InsertChild((L[num].T->lchild),p,LR,T1) == OK)
            {
                if(isKeyRepeat(L[num].T->lchild)==TRUE)
                {
                    ClearBiTree(&(L[num].T->lchild));
                    printf("存在相同的key，插入失败,已清空二叉树！\n");
                }
                else
                    printf("成功插入子树!");
                getchar();
                getchar();
            }
            else
            {
                printf("插入失败!");
                getchar();
                getchar();
            }
            break;
        }
        case 16:
        {
            int e,LR;
            BiTreep p;
            if (!L[num].T)
            {
                printf("二叉树不存在！");
                getchar();
                getchar();
                break;
            }
            printf("请输入你要删除位置的key: ");
            scanf("%d", &e);
            getchar();
            p=LocateNode(L[num].T->lchild,e);
            if (!p)
            {
                printf("该位置不存在!\n");
                getchar();
                getchar();
                break;
            }
            printf("请输入你想要删除的方向0或1，0表示左边，1表示右边: ");
            scanf("%d", &LR);
            getchar();
            if (DeleteChild(L[num].T->lchild,p, LR) == OK)
            {
                printf("成功删除子树!");
                getchar();
                getchar();
            }
            else
            {
                printf("删除失败!");
                getchar();
                getchar();
            }
            break;
        }
        case 17:
            if (!L[num].T)
            {
                printf("二叉树不存在！");
                getchar();
                getchar();
                break;
            }
            if(BiTreeEmpty(L[num].T->lchild) == OK)
            {
                printf("二叉树为空树！\n");
                getchar();
                getchar();
                break;
            }
            printf("该二叉树的前序遍历为：");
            PreOrderTraverse(L[num].T->lchild, visit);
            getchar();
            getchar();
            break;

        case 18:
            if (!L[num].T)
            {
                printf("二叉树不存在！");
                getchar();
                getchar();
                break;
            }
            if(BiTreeEmpty(L[num].T->lchild) == OK)
            {
                printf("二叉树为空树！\n");
                getchar();
                getchar();
                break;
            }
            printf("该二叉树的中序遍历为：");
            InOrderTraverse(L[num].T->lchild, visit);
            getchar();
            getchar();
            break;

        case 19:
            if (!L[num].T)
            {
                printf("二叉树不存在！");
                getchar();
                getchar();
                break;
            }
            if(BiTreeEmpty(L[num].T->lchild) == OK)
            {
                printf("二叉树为空树！\n");
                getchar();
                getchar();
                break;
            }
            printf("该二叉树的后序遍历为：");
            PostOrderTraverse(L[num].T->lchild, visit);
            getchar();
            getchar();
            break;

        case 20:
            if (!L[num].T)
            {
                printf("二叉树不存在！");
                getchar();
                getchar();
                break;
            }
            if(BiTreeEmpty(L[num].T->lchild) == OK)
            {
                printf("二叉树为空树！\n");
                getchar();
                getchar();
                break;
            }
            printf("该二叉树的层序遍历为：");
            LevelOrderTraverse(L[num].T->lchild, visit);
            getchar();
            getchar();
            break;

        case 21:
        {
            int k;
            printf("请输入要在第几个树操作（1~%d）: ",n);
            scanf("%d",&k);
            if(k<1||k>n)
            {
                printf("请选择正确范围！");
            }
            else
            {
                num=k-1;
                printf("切换成功！\n");
            }
            getchar();
            getchar();
            break;
        }
        case 22:
        {
            if (!L[num].T)
            {
                printf("二叉树不存在！");
                getchar();
                getchar();
                break;
            }
            if(BiTreeEmpty(L[num].T->lchild) == OK)
            {
                printf("二叉树为空树！\n");
                getchar();
                getchar();
                break;
            }
            char filename[100];
            FILE *fp;
            printf("请输入要保存的文件名: ");
            scanf("%s", filename);
            fp=fopen(filename,"w");
            if(!fp)
                printf("文件打开失败！\n");
            else
            {
                if(Save(L[num].T->lchild,fp)==OK)
                {
                    fprintf(fp,"@");
                    printf("文件保存成功！\n");
                }

                else
                    printf("文件保存失败！\n");
            }
            fclose(fp);
            getchar();
            getchar();
            break;
        }
        case 23:
        {
            if (!L[num].T)
            {
                printf("二叉树不存在！");
                getchar();
                getchar();
                break;
            }
            char filename[100];
            FILE *fp;
            printf("请输入要加载的文件名：");
            scanf("%s",filename);
            fp=fopen(filename,"r");
            if(!fp)
                printf("文件打开失败！\n");
            else
            {
                if(Load(&(L[num].T->lchild),fp)==OK)
                {
                    if(isKeyRepeat(L[num].T->lchild)==TRUE)
                    {
                        ClearBiTree(&(L[num].T->lchild));
                        printf("存在相同的key，加载失败,已清空二叉树！\n");
                    }
                    else
                        printf("文件加载成功！\n");
                }
                else
                    printf("文件加载失败！\n");
            }
            fclose(fp);
            getchar();
            break;
        }
        case 24:
        {
            if (!L[num].T)
            {
                printf("二叉树不存在！");
                getchar();
                getchar();
                break;
            }
            if(BiTreeEmpty(L[num].T->lchild) == OK)
            {
                printf("二叉树为空树！\n");
                getchar();
                getchar();
                break;
            }
            printf("该二叉树为:\n");
            TreeDisplay(L[num].T->lchild,1, visit);
            getchar();
            getchar();
            break;
        }
        case 0:
            break;
        }//end of switch
    }//end of while
}//end of main()
/*--------page 23 on textbook --------------------*/
/*
 * 函数名称: InitBiTreep
 * 初始条件：二叉树T不存在
 * 函数功能: 构造空树二叉树T
 * 返 回 值: status类型.
 */
status InitBiTree(BiTreep *T)
{
    *T = (BiTreep)malloc(sizeof(BiTNode));
    (*T)->lchild = NULL;
    (*T)->rchild = NULL;
    return OK;
}
/*
 * 函数名称: DestroyBiTree
 * 初始条件：二叉树T已存在
 * 函数功能: 销毁二叉树T
 * 返 回 值: status类型.
 */
status DestroyBiTree(BiTreep *T)
{
    if (*T)
    {
        if ((*T)->lchild)
            DestroyBiTree(&((*T)->lchild));
        if ((*T)->rchild)
            DestroyBiTree(&((*T)->rchild));
        free(*T);
        *T = NULL;
    }
    return OK;
}
/*
 * 函数名称: CreateBiTree
 * 初始条件：二叉树T已存在
 * 函数功能: 创建二叉树
 * 返 回 值: status类型.
 */
status CreateBiTree(BiTreep *T,ElemType *data)
{
    if(data[dataNum].other == '#'||data[dataNum].other=='@')
    {
        *T = NULL;
        if(data[dataNum].other == '#')
            dataNum++;
        return OK;
    }
    else
    {
        *T = (BiTreep)malloc(sizeof(BiTNode));
        if(!(*T))
            return ERROR;
        (*T)->data = data[dataNum];
        dataNum++;
        CreateBiTree(&((*T)->lchild),data);
        CreateBiTree(&((*T)->rchild),data);
    }
    return OK;
}
/*
 * 函数名称: ClearBiTree
 * 初始条件：二叉树T已存在
 * 函数功能: 构造二叉树
 * 返 回 值: status类型.
 */
status ClearBiTree(BiTreep *T)
{
   DestroyBiTree(T);
    return OK;
}
/*
 * 函数名称: BiTreeEmpty
 * 初始条件：二叉树T已存在
 * 函数功能: 若T为空二叉树则返回TRUE，否则返回FALSE
 * 返 回 值: status类型.
 */
status BiTreeEmpty(BiTreep T)
{
    if(!T)
        return OK;
    else
        return FALSE;
}
/*
 * 函数名称: BiTreeDepth
 * 初始条件：二叉树T已存在
 * 函数功能: 返回T的深度
 * 返 回 值: status类型.
 */
status BiTreeDepth(BiTreep T)
{
    int depth = 0;
    if(T)
    {
        int lchilddepth = BiTreeDepth(T->lchild);
        int rchilddepth = BiTreeDepth(T->rchild);
        depth = (lchilddepth>=rchilddepth?(lchilddepth+1):(rchilddepth+1));
    }
    return depth;
}
/*
 * 函数名称: Root
 * 初始条件：二叉树T已存在
 * 函数功能: 返回T的根
 * 返 回 值: char类型.
 */
char Root(BiTreep T)
{
    return T->data.other;
}
/*
 * 函数名称: Value
 * 初始条件：二叉树T已存在, e是T中的某个结点
 * 函数功能: 返回e的值
 * 返 回 值: char类型.
 */
char Value(BiTreep T, int e)
{
    if (!T)
        return ERROR;   //若二叉树为空，返回Error
    BiTreep st[1000], p;
    int top = 0;  //置空栈
    st[top++] = T;
    while (top)
    {
        p = st[--top]; //先序遍历，弹出栈顶元素
        if (p->data.key== e)
            return p->data.other;
        else
        {
            if(p->rchild!=NULL)
                st[top++] = p->rchild;
            if(p->lchild!=NULL)
                st[top++] = p->lchild;
        }
    }
    return ERROR;
}
/*
 * 函数名称: Assign
 * 初始条件：二叉树T已存在, e是T中的某个结点
 * 函数功能: 结点e赋值为value
 * 返 回 值: status类型.
 */
status Assign(BiTreep T, int e, char c)
{
    BiTreep p;
    p=LocateNode(T,e);
    if(!p)
        return ERROR;
    else
        p->data.other=c;
    return OK;
}

/*
 * 函数名称: Parent
 * 初始条件：二叉树T已存在, e是T中的某个结点
 * 函数功能: 若e是T的非根结点，则返回它的双亲结点指针，否则返回NULL
 * 返 回 值: BiTNode*类型.
 */
BiTreep Parent(BiTreep T, int e)
{
    BiTreep p;
    if (T)
    {
        if ((T->lchild&&T->lchild->data.key == e) ||(T->rchild&& T->rchild->data.key== e))
            return T;
        p = Parent(T->lchild, e);
        if (p)
            return p;
        p = Parent(T->rchild, e);
        if (p)
            return p;
    }
    return NULL;
}
/*
 * 函数名称: LeftChild
 * 初始条件：二叉树T已存在, e是T中的某个结点
 * 函数功能: 返回e的左孩子结点指针。若e无左孩子，则返回NULL
 * 返 回 值: BiTNode*类型.
 */
BiTNode* LeftChild(BiTreep T, int e)
{
    BiTreep lc;
    if (T)
    {
        if (T->data.key == e)
            return T->lchild;
        lc = LeftChild(T->lchild, e);
        if (lc )
            return lc;
        lc = LeftChild(T->rchild, e);
        if (lc)
            return lc;
    }
    return NULL;
}
/*
 * 函数名称: RightChild
 * 初始条件：二叉树T已存在, e是T中的某个结点
 * 函数功能: 返回e的右孩子结点指针。若e无右孩子，则返回NULL
 * 返 回 值: BiTNode*类型.
 */
BiTNode* RightChild(BiTreep T, int e)
{
    BiTreep rc;
    if (T)
    {
        if (T->data.key == e)
            return T->rchild;
        rc = RightChild(T->lchild, e);
        if (rc )
            return rc;
        rc = RightChild(T->rchild, e);
        if (rc )
            return rc;
    }
    return NULL;
}
/*
 * 函数名称: LeftSibling
 * 初始条件：二叉树T已存在, e是T中的某个结点
 * 函数功能: 返回e的左兄弟结点指针。若e是T的左孩子或者无左兄弟，则返回NULL
 * 返 回 值: BiTNode*类型.
 */
BiTNode* LeftSibling(BiTreep T, int e)
{
    BiTreep lsibling;
    if (T)
    {
        if (T->rchild&&T->rchild->data.key== e)
            return T->lchild;
        lsibling = LeftSibling(T->lchild, e);
        if (lsibling)
            return lsibling;
        lsibling = LeftSibling(T->rchild, e);
        if (lsibling)
            return lsibling;
    }
    return NULL;
}

/*
 * 函数名称: RightSibling
 * 初始条件：二叉树T已存在, e是T中的某个结点
 * 函数功能: 返回e的左兄弟结点指针。若e是T的左孩子或者无左兄弟，则返回NULL回e的右兄弟结点指针。若e是T的右孩子或者无有兄弟，则返回NULL
 * 返 回 值: BiTNode*类型.
 */
BiTNode* RightSibling(BiTreep T, int e)
{
    BiTreep rsibling;
    if (T)
    {
        if (T->lchild&&T->lchild->data.key == e)
            return T->rchild;
        rsibling = RightSibling(T->lchild, e);
        if (rsibling)
            return rsibling;
        rsibling = RightSibling(T->rchild, e);
        if (rsibling)
            return rsibling;
    }
    return NULL;
}
/*
 * 函数名称: LocateNode
 * 初始条件：二叉树T已存在, e是T中的某个结点
 * 函数功能: 返回e结点指针。若无e结点返回NULL
 * 返 回 值: BiTNode*类型.
 */
BiTreep LocateNode(BiTreep T, int e)
{
    BiTreep p;
    if(T)
    {
        if(T->data.key==e)
            return T;
        p=LocateNode(T->lchild,e);
        if(p)
            return p;
        p=LocateNode(T->rchild,e);
        if(p)
            return p;
    }
    return NULL;
}
/*
 * 函数名称: InsertChild
 * 初始条件：二叉树T存在，p指向T中的某个结点，LR为0或1
 * 函数功能: 根据LR为0或者1，插入c为T中p所指结点的左或右子树，p	所指结点的原有左子树或右子树则为c的右子树
 * 返 回 值: status类型.
 */
status InsertChild(BiTreep T, BiTreep p, int LR, BiTreep c)
{
    if (c->rchild)
    {
        printf("待插入二叉树的右子树不为空！");
        return ERROR;
    }
    if (LR == 0)
    {
        c->rchild = p->lchild;
        p->lchild = c;
    }
    else
    {
        c->rchild = p->rchild;
        p->rchild = c;
    }
    return OK;
}
/*
 * 函数名称: DeleteChild
 * 初始条件：二叉树T存在，p指向T中的某个结点，LR为0或1
 * 函数功能: 根据LR为0或者1，删除c为T中p所指结点的左或右子树
 * 返 回 值: status类型.
 */
status DeleteChild(BiTreep T, BiTreep p, int LR)
{
    BiTreep T1;
    if (LR == 0)
    {
        T1 = p->lchild;
        p->lchild = NULL;
        if(DestroyBiTree(&T1)==ERROR)
            return ERROR;
    }
    else
    {
        T1 = p->rchild;
        p->rchild = NULL;
        if (DestroyBiTree(&T1)==ERROR)
            return ERROR;
    }
    return OK;
}
/*
 * 函数名称: visit
 * 函数功能: 打印序号和字符
 * 返回值: status
 */
status visit(ElemType data)
{
    printf("%d:%c ",data.key,data.other);
    return OK;
}
/*
 * 函数名称: PreOrderTraverse
 * 初始条件：二叉树T已存在
 * 函数功能: 先序遍历T，对每个结点调用函数visit一次且一次，一旦调用失败，则操作失败
 * 返 回 值: status类型.
 */
status PreOrderTraverse(BiTreep T, status (* visit)(ElemType data))
{
    if(T)
    {
        if(visit(T->data))
            if(PreOrderTraverse(T->lchild, visit))
                if(PreOrderTraverse(T->rchild, visit))
                    return OK;
        return ERROR;
    }
    return OK;
}
/*
 * 函数名称: InOrderTraverse
 * 初始条件：二叉树T已存在
 * 函数功能: 中序遍历T，对每个结点调用函数visit一次且一次，一旦调用失败，则操作失败
 * 返 回 值: status类型.
 */
status InOrderTraverse(BiTreep T, status (* visit)(ElemType data))
{
    if(T)
    {
        if(InOrderTraverse(T->lchild, visit))
            if(visit(T->data))
                if(InOrderTraverse(T->rchild, visit))
                    return OK;
        return ERROR;
    }
    return OK;
}

/*
 * 函数名称: PostOrderTraverse
 * 初始条件：二叉树T已存在
 * 函数功能: 后序遍历T，对每个结点调用函数visit一次且一次，一旦调用失败，则操作失败
 * 返 回 值: status类型.
 */
status PostOrderTraverse(BiTreep T, status (* visit)(ElemType data))
{
    if(T)
    {
        if(PostOrderTraverse(T->lchild, visit))
            if(PostOrderTraverse(T->rchild, visit))
                if(visit(T->data))
                    return OK;
        return ERROR;
    }
    return OK;
}
/*
 * 函数名称: LevelOrderTraverse
 * 初始条件：二叉树T已存在
 * 函数功能: 层序遍历t，对每个结点调用函数visit一次且一次，一旦调用失败，则操作失败
 * 返 回 值: status类型.
 */
status LevelOrderTraverse(BiTreep T, status (* visit)(ElemType data))
{
    BiTreep queue[100],p;    //创建队列queue
    int rear=0,front=0,i;
    for(i=0; i<100; i++)
        queue[i]=NULL;
    queue[rear++]=T;       //T入队列
    while (queue[front])
    {
        p=queue[front++];    //离开队列
        if(visit(p->data))
        {
            if(p->lchild)
                queue[rear++]=p->lchild;
            if(p->rchild)
                queue[rear++]=p->rchild;
        }
    }
    return OK;
}
/*
 * 函数名称: Save
 * 初始条件：二叉树T已存在
 * 函数功能: 保存二叉树为文件
 * 返 回 值: status类型.
 */
status Save(BiTreep T,FILE *fp)
{
    if(T)
    {
        fprintf(fp,"%c %d ",T->data.other,T->data.key);
        if(Save(T->lchild,fp)!=OK)
            return ERROR;
        if(Save(T->rchild,fp)!=OK)
            return ERROR;
    }
    else
    {
        fprintf(fp,"# ");
    }
    return OK;
}

/*
 * 函数名称: Load
 * 函数功能: 从文件中读取二叉树
 * 返 回 值: status类型.
 */
status Load(BiTreep *T,FILE *fp)
{
    int i=0;
    char temp;
    ElemType data[1000];
    fflush(stdin);
    do
    {
        fscanf(fp,"%c",&data[i].other);
        if(data[i].other!='#'&&data[i].other!='@')
        {
            fscanf(fp,"%c",&temp);
            fscanf(fp,"%d",&data[i].key);
        }
        fscanf(fp,"%c",&temp);
    }
    while(data[i++].other!='@'&&i<1000);
    dataNum=0;
    if(CreateBiTree(T,&data[0])==OK)
        return OK;
    return ERROR;
}
/*
 * 函数名称: TreeDisplay
 * 初始条件：二叉树T已存在
 * 函数功能: 先序遍历T，并以OS资源管理器形式输出
 * 返 回 值: status类型.
 */
status TreeDisplay(BiTreep T,int depth,status (* visit)(ElemType data))
{
    if(!T)
    {
        printf("\n");
        return OK;
    }
    int i=0;
    for(; i<depth; i++)
        printf("   ");
    visit(T->data);
    printf("\n");
    if(T->lchild||T->rchild){
            TreeDisplay(T->lchild,depth+1,visit);
    TreeDisplay(T->rchild,depth+1,visit);
    }
    return OK;
}
/*
 * 函数名称: isKeyRepeat
 * 初始条件：二叉树T已存在
 * 函数功能: 如果二叉树中有相同的key返回TRUE，否则返回FALSE
 * 返 回 值: status类型.
 */
status isKeyRepeat(BiTreep T)
{
    if(T)
    {
        int flag[1000],top=1,i;
        BiTreep stack[100],p;    //创建栈
        for(i=0; i<100; i++)
            stack[i]=NULL;
        for(i=0; i<1000; i++)
            flag[i]=0;
        stack[top]=T;
        while (stack[top])
        {
            p=stack[top--];
            if(p->data.key<1000&&p->data.key>=0)
            {
                if(flag[p->data.key])
                    return TRUE;
                else
                {
                    flag[p->data.key]=1;
                    if(p->rchild)
                        stack[++top]=p->rchild;
                    if(p->lchild)
                        stack[++top]=p->lchild;

                }
            }
        }
        return FALSE;
    }
    return FALSE;
}
