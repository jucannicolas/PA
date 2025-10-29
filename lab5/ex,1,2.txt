#include <stdio.h>
#include <stdlib.h>
typedef struct node
{
    int key;
    struct node *left;
    struct node *right;
} NodeT;
NodeT *insertNode( NodeT *root, int key )
{
    NodeT *p=(NodeT *)malloc(sizeof(NodeT));
    if(p==NULL) exit(1);
    if(root==NULL)
    {
        root=p;
        root->key=key;
        root->left=NULL;
        root->right=NULL;
        return root;
    }
    while(root!=NULL && root->key!=key)
    {
        if(key>root->key)
        {
            if(root->right==NULL)
            {
                root->right=p;
                p->key=key;
                p->right=NULL;
                p->left=NULL;
                return p;
            }
            else root=root->right;
        }
        else if(key<root->key)
        {
            if(root->left==NULL)
            {
                root->left=p;
                p->key=key;
                p->right=NULL;
                p->left=NULL;
                return p;
            }
            else root=root->left;
        }
    }
    return NULL;
}
void preordine(NodeT *p)
{
    if(p!=NULL)
    {
        printf("%d,",p->key);
        preordine(p->left);
        preordine(p->right);
    }
}
void inordine(NodeT *p)
{
    if(p!=NULL)
    {
        inordine(p->left);
        printf("%d ",p->key);
        inordine(p->right);
    }
}
NodeT * search(NodeT *root,int key)
{
    if(root==NULL) return NULL;
    if(root->key==key)
    {
        printf("DA");
        return root;
    }
    if(root->key>key) search(root->left,key);
    search(root->right,key);
}
int main()
{
    NodeT *root=insertNode(NULL,15);
    NodeT *p=insertNode(root,6);
    p=insertNode(root,18);
    p=insertNode(root,20);
    p=insertNode(root,17);
    p=insertNode(root,7);
    p=insertNode(root,13);
    p=insertNode(root,3);
    p=insertNode(root,2);
    p=insertNode(root,4);
    p=insertNode(root,9);
    preordine(root);
    printf("\n");
    inordine(root);
    printf("\n");
    p=search(root,7);
    if(p!=NULL) printf("DA");
    else printf("NU");
    return 0;
}
