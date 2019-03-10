# Supermarket
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
struct lista_produse_supermarket
{
    char* nume;
    char* categorie;
    int pret;
    int cantitate;
    int stoc;
    struct lista_produse_supermarket* next;
};
typedef struct lista_produse_supermarket lista1;
struct lista_cumparaturi
{

    char* nume;
    char* categorie;
    int cantitate;
    struct lista_cumparaturi* next;
};
typedef struct lista_cumparaturi lista2;
struct lista_produse_cumparate
{

    char* nume;
    char* categorie;
    int cantitate;
    struct lista_produse_cumparate* next;
};
typedef struct lista_produse_cumparate lista3;
struct arb
{
    int cantitate;
    struct arb *left, *right;
};
typedef struct arb Node;
lista2* init2(lista2 *cap2)
{
	cap2=NULL;
	return cap2;
}
lista3* init3(lista3 *cap3)
{
	cap3=NULL;
	return cap3;
}
lista1* init1(lista1 *cap1)
{
	cap1=NULL;
	return cap1;
}

lista2* adFata(lista2 *cap, char nm[], char cat[], int cant)
{
	lista2 *temp;
	temp=(lista2*)malloc(sizeof(lista2));
	temp->nume=(char*)malloc(sizeof(char)*20);
	temp->categorie=(char*)malloc((sizeof(char)*20));
    strcpy(temp->nume, nm);
    strcpy(temp->categorie, cat);
    temp->cantitate=cant;


	if (cap==NULL)
	{
		temp->next=NULL;
		cap=temp;
	}
	else
	{
		temp->next=cap;
		cap=temp;
	}
	return cap;
}
lista2* stergeVal(lista2 *cap2, char inf[])
{
	lista2 *temp2, *aux2;
	if (cap2==NULL)
		printf("\nLista este vida\n");
	else
		if(strcmp(cap2->nume,inf)==0)
		{
			temp2=cap2;
			cap2=cap2->next;
			free(temp2);
		}
		else
			if(cap2->next==NULL)
				printf("\nValoarea de sters nu se afla in lista\n");
			else
			{
				temp2=cap2;
				aux2=temp2->next;
				while((aux2!=NULL)&&(strcmp(aux2->nume,inf)!=0))
				{
                    aux2=aux2->next;
					temp2=temp2->next;
				}
				if(aux2!=NULL)
				{
					temp2->next=aux2->next;
						free(aux2);
				}
			}
	return cap2;
}
lista3* adSpate3(lista3 *cap3, char tempnm[], char categorie[], int cantitate)
{
	lista3 *temp, *aux;
	temp=(lista3*)malloc(sizeof(lista3));
	temp->nume=(char*)malloc(sizeof(char)*20);
	temp->categorie=(char*)malloc((sizeof(char)*20));
    strcpy(temp->nume, tempnm);
    strcpy(temp->categorie, categorie);
    temp->cantitate=cantitate;

	if (cap3==NULL)
	{
		temp->next=NULL;
		cap3=temp;
	}
	else
	{
		aux=cap3;
		while(aux->next!=NULL)
			aux=aux->next;
		aux->next=temp;
		temp->next=NULL;
	}
    return cap3;
}
lista2* adSpate2(lista2 *cap2, char nm2[], char cat2[], int cant2)
{
	lista2 *temp, *aux;
	temp=(lista2*)malloc(sizeof(lista2));
	temp->nume=(char*)malloc(sizeof(char)*20);
	temp->categorie=(char*)malloc((sizeof(char)*20));
    strcpy(temp->nume, nm2);
    strcpy(temp->categorie, cat2);
    temp->cantitate=cant2;

	if (cap2==NULL)
	{
		temp->next=NULL;
		cap2=temp;
	}
	else
	{
		aux=cap2;
		while(aux->next!=NULL)
			aux=aux->next;
		aux->next=temp;
		temp->next=NULL;
	}
    return cap2;
}
lista1* adSpate1(lista1 *cap1, char nm1[], char cat1[],int pr, int cant1, int st)
{
	lista1 *temp, *aux;
	temp=(lista1*)malloc(sizeof(lista1));
	temp->nume=(char*)malloc(sizeof(char)*20);
	temp->categorie=(char*)malloc((sizeof(char)*20));
    strcpy(temp->nume, nm1);
    strcpy(temp->categorie, cat1);
    temp->cantitate=cant1;
    temp->pret=pr;
    temp->stoc=st;

	if (cap1==NULL)
	{
		temp->next=NULL;
		cap1=temp;
	}
	else
	{
		aux=cap1;
		while(aux->next!=NULL)
			aux=aux->next;
		aux->next=temp;
		temp->next=NULL;
	}
return cap1;
}
void afisList2(lista2 *cap2, FILE *f4)
{	

	lista2 *aux;
	aux=cap2;
	while (aux!=NULL)
	{
        fprintf(f4,"%s ", aux->nume);
        fprintf(f4,"%s ", aux->categorie);
        fprintf(f4,"%d\n",aux->cantitate);
		aux=aux->next;
	}
	fprintf(f4,"\n");

}
void afisList3(lista3 *cap3, FILE *f4)
{	
	lista3 *aux;
	aux=cap3;
	while (aux!=NULL)
	{
        fprintf(f4,"%s ", aux->nume);
        fprintf(f4,"%s ", aux->categorie);
        fprintf(f4,"%d\n",aux->cantitate);
		aux=aux->next;
	}
	fprintf(f4,"\n");
}
void afisList1(lista1 *cap1, FILE *f4)
{

	lista1 *aux;
	aux=cap1;
	while (aux!=NULL)
	{
        fprintf(f4,"%s ", aux->nume);
        fprintf(f4,"%s ", aux->categorie);
        fprintf(f4,"%d ", aux->pret);
        fprintf(f4,"%d ", aux->cantitate);
        fprintf(f4,"%d\n", aux->stoc);
		aux=aux->next;
	}
	fprintf(f4,"\n");
}
Node* creare_arbore(int N,int cantitati[],int i)
{
    if(N>0)
    {
        Node *root=(Node*)malloc(sizeof(Node));
        root->cantitate=cantitati[i];
        root->left=creare_arbore(N/2,cantitati,i+1);
        root->right=creare_arbore(N-1-N/2,cantitati,i+3);
        return root;

    }
    else return NULL;
}
void preorder(Node*root, FILE *f4)
{
    if(root)
    {
        fprintf(f4,"%d ",root->cantitate);
        preorder(root->left,f4);
        preorder(root->right,f4);
    }
}
int cautare_pret_apropiat(lista1 *cap1, char nume[20])
{
    lista1* aux;
    aux=(lista1*)malloc(sizeof(lista1));
    aux->nume=(char*)malloc(sizeof(char)*20);
    aux->categorie=(char*)malloc((sizeof(char)*20));
    char categorie[20];
    int k=0, pret, i, next, prev, a[20], temp, pret_cautat, j;
    aux=cap1;
    while(aux!=NULL)
    {
        if(strcmp(nume,aux->nume)==0)
        {
            strcpy(categorie,aux->categorie);
            pret=aux->pret;
        }   
        aux=aux->next;
    }
    //printf("%s\n",categorie);
    aux=cap1;
    while(aux!=NULL)
    {
        if(strcmp(categorie,aux->categorie)==0)
        {
            a[k]=aux->pret;
            k++;
        }
        //printf("%s\n",aux->categorie);
        aux=aux->next;
    }
    for(i=0;i<k-1;i++)
    {
        for(j=1;j<k;j++)
        {
            if(a[i]>a[j])
            {
                temp=a[i];
                a[i]=a[j];
                a[j]=temp;
            }
        }
    }
    for(i=0;i<k;i++)
    {   
       // printf("%d vector\n",a[i]);
        if (a[i]==pret)
        {
            next=a[i+1];
            prev=a[i-1];
        }
        else continue;
    }
    //printf("%d aici",pret);
    if(a[0]==pret)
        pret_cautat=a[1];

    else    if(a[k-1]==pret)
            pret_cautat=a[k-2];
    else    if(abs(pret-next) == abs(pret-prev))
        pret_cautat=prev;

    else    if(abs(pret-next) < abs(pret-prev))
        pret_cautat=next;
    else
        pret_cautat=prev;
    //printf("%d cautat\n",pret_cautat);
    return pret_cautat; 
}
int cmpfunc (const void * a, const void * b) {
   return ( *(int*)a - *(int*)b );
}
void bubble_sort(int vector[], int n)
{
  int i, j, temp;
 
  for (i= 0 ; i < ( n - 1 ); i++)
  {
    for (j = 0 ; j < n - i - 1; j++)
    {
      if (vector[j] > vector[j+1])
      {
        temp=vector[j];
        vector[j]=vector[j+1];
        vector[j+1]=temp;
      }
    }
  }
}
int main(int argc, char *argv[])
{

    FILE *f1, *f2, *f3, *f4;
    lista3 *cap3, *p3;
    lista2 *cap2, *auxil2, *p2;
    lista1 *cap1, *auxil, *p1, *auxil4;
    int i, n,cant2 , cant1, st, pr, c1, c2, c3, c4, c5, c6, buget,pret_produs, cantitate, cantitate_buna;
    int pretul_minim, cantitate_ramasa;
    int k=0, cantitati[20],j;
    char nm2[20], cat2[20];
    char nm1[20], cat1[20], inf[20];
    char tempnm[20], categorie[20];
    char str1[20], str2[20], str3[20];
    Node* root;
    root=(Node*)malloc(sizeof(Node));
    f4=fopen(argv[4],"w");
    if(f4==NULL)
        printf("Fisierul nu a putut fi deschis!");
    f3=fopen(argv[3],"r");
    if(f3==NULL)
        printf("Fisierul nu a putut fi deschis!");
    fscanf(f3,"%d",&c1);
    fscanf(f3,"%d",&c2);
    fscanf(f3,"%d",&c3);
    fscanf(f3,"%d",&c4);
    fscanf(f3,"%d",&c5);
    fscanf(f3,"%d",&c6);
    fscanf(f3,"%d",&buget);
    fclose(f3);
    f2=fopen(argv[2],"r");
    if(f2==NULL)
        printf("Fisierul nu a putut fi deschis!");
    cap1=NULL;
    cap2=NULL;
    cap3=NULL;
    fscanf(f2,"%d",&n);
    for(i=0;i<n;i++)
    {
        fscanf(f2,"%s", nm2);
        fscanf(f2,"%s", cat2);
        fscanf(f2,"%d", &cant2);
        cap2=adSpate2(cap2, nm2, cat2, cant2);
    }
    fclose(f2);
    f1=fopen(argv[1],"r");
    if(f1==NULL)
        printf("Fisierul nu a putut fi deschis!");
    fscanf(f1,"%d",&n);
    for(i=0;i<n;i++)
    {
        fscanf(f1,"%s", nm1);
        fscanf(f1,"%s", cat1);
        fscanf(f1,"%d", &pr);
        fscanf(f1,"%d", &cant1);
        fscanf(f1,"%d", &st);
        cap1=adSpate1(cap1, nm1, cat1,pr, cant1, st);
    }
    fclose(f1);
	if(c1==1 && c2==0)
    {
        afisList2(cap2,f4);
    }
    if(c2==1)
    {
    auxil=cap1;
    while(auxil!=NULL)
    {
        if(auxil->stoc==0)
        {
            strcpy(inf,auxil->nume);
            cap2=stergeVal(cap2, inf);
        }
        auxil=auxil->next;
    }
	afisList2(cap2,f4);
    }
    auxil2=cap2;
if(c3==1 && c4==0)
{
    while(buget>0 && auxil2 != NULL)
    {
        auxil2=cap2;
        while(auxil2!=NULL)
        {
            strcpy(tempnm,auxil2->nume);
            auxil=cap1;
            while(auxil!=NULL)
            {
                if(strcmp(auxil->nume,tempnm)==0)
                {
                    strcpy(categorie,auxil->categorie);
                    if((auxil2->cantitate)>(auxil->cantitate))
                    {
                        cantitate=auxil->cantitate;
                        //cantitate_de_cumparat=auxil2->cantitate-auxil->cantitate;
                        for(i=1;i<=cantitate;i++)
                        {
                            pret_produs=i*(auxil->pret);
                            if(buget-pret_produs<0)
                                break;
                            else
                                cantitate_buna=i;
                        }
                        buget=buget-(cantitate_buna)*(auxil->pret);
                    }
                    else
                    {
                        cantitate=auxil2->cantitate;
                        for(i=1;i<=cantitate;i++)
                        {
                            pret_produs=i*(auxil->pret);
                            if(buget-pret_produs<0)
                            break;
                            else
                            cantitate_buna=i;
                        }
                        buget=buget-(cantitate_buna)*(auxil->pret);
                    }
                }
                    auxil=auxil->next;
            }
            if(buget<0)
            {
                    break;
            }
            else
            {
                cap3=adSpate3(cap3,tempnm,categorie,cantitate_buna);
                auxil2=auxil2->next;
            }
        }
    }
    afisList3(cap3,f4);
}
fclose(f4);
/*auxil2=cap2;
auxil2=(lista2*)malloc(sizeof(lista2));
auxil2->nume=(char*)malloc(sizeof(char)*20);
auxil2->categorie=(char*)malloc((sizeof(char)*20));*/
int ok;
if(c3==0 && c4==1)
{

    f4=fopen(argv[4],"w");
    if(f4==NULL)
        printf("fisierul nu a putut fi deschis");
        auxil2=cap2;
        while(auxil2!=NULL)
        {
            strcpy(tempnm,auxil2->nume);
            auxil=cap1;
            while(auxil!=NULL)
            {
                if(strcmp(auxil->nume,tempnm)==0)
                {
                    strcpy(categorie,auxil->categorie);
                    if((auxil2->cantitate)>(auxil->cantitate))
                    {
                            cantitate=auxil->cantitate;
                            cantitate_ramasa=auxil2->cantitate-auxil->cantitate;
                            pretul_minim=cautare_pret_apropiat(cap1,tempnm);
                            auxil4=cap1;
                            while(auxil4!=NULL)
                            {
                                if(pretul_minim==auxil4->pret && strcmp(auxil4->categorie,categorie)==0 && strcmp(auxil4->nume,tempnm)!=0)
                                {
                                    strcpy(str2,auxil4->nume);
                                }
                                auxil4=auxil4->next;
                            }
                            strcpy(str3,auxil->nume);
                    }
                    else
                    {
                        cantitate=auxil2->cantitate;
                        strcpy(str1,tempnm);
                    }
                     auxil=auxil->next;
                    ok=1;
                }
                else if(strcmp(auxil->nume,tempnm)!=0)
                        auxil=auxil->next;
            }
        if(strcmp(str1,auxil2->nume)==0)
        {

                cap3=adSpate3(cap3,str1,categorie,cantitate);
                auxil2->cantitate=(auxil2->cantitate)-cantitate;
                auxil2=auxil2->next;
        }
        else if(strcmp(str1,auxil2->nume)!=0 && ok==1)
        {

                cap3=adSpate3(cap3,str3,categorie,cantitate);
                cap3=adSpate3(cap3,str2,categorie,cantitate_ramasa);
                auxil2->cantitate=(auxil2->cantitate)-cantitate-cantitate_ramasa;
                auxil2=auxil2->next;
                
        }
        else
            auxil2=auxil2->next;
        }
    afisList2(cap2,f4);
    afisList3(cap3,f4);
    fclose(f4);

}
if(c5==1)
{
    f4=fopen(argv[4],"a");
    p3=(lista3*)malloc(sizeof(lista3));
    p3=cap3;
    while(p3!=NULL)
    {
        cantitati[k]=p3->cantitate;
        k++;
        p3=p3->next;
    }
    bubble_sort(cantitati,k);
    root=creare_arbore(k,cantitati,0);
    preorder(root,f4);
    fclose(f4);
}
if(c6==1)
{
    f4=fopen(argv[4],"a");
    int b[20], o=0,q=1, c[20],m;
    lista1*temp1;
    temp1=cap1;
    while(temp1!=NULL)
    {
        b[o]=temp1->pret;
        o++;
        temp1=temp1->next;
    }
    /*for(i=0;i<o;i++)
        fprintf(f4,"%d\n",b[i]);*/
    for(i=1;i<o;i++)
    {
        m=0;
        for(j=0;j<i;j++)
            {
                if((b[i]<b[j]))
                {
                    m++;
                }
                else
                {
                    m=0;

                }

            }
                c[q]=m;
                q++;
    }
    c[0]=0;
    for(i=0;i<q;i++)
    {
        fprintf(f4,"%d ",c[i]);
    }
}

    for(p1=cap1; p1!=NULL; p1=p1->next)
    {
        free(p1);
    }
    for(p2=cap2; p2!=NULL; p2=p2->next)
    {
        free(p2);   
    }
    for(p3=cap3; p3!=NULL; p3=p3->next)
    {
        free(p3);
    }
    return 0;
}


