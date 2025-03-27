#include <stdio.h>
#include <stdlib.h>
typedef struct noeud{
    int valeur;
    struct noeud *suiv;
}noeud;

noeud *cree(int val){
    noeud *Nvnoeud;
     Nvnoeud=(noeud *)malloc(sizeof(noeud));
     Nvnoeud->valeur=val;
     Nvnoeud->suiv=NULL;
     return Nvnoeud;
}

noeud *ajoutdebut(noeud*debut,int val){
    noeud *Nvnoeud;
    Nvnoeud=cree(val);
    Nvnoeud->valeur=val;
    Nvnoeud->suiv=NULL;
    if(debut!=NULL){
         Nvnoeud->suiv=debut;
         debut=Nvnoeud;
    }
    return debut;
}
noeud *ajoutfin(noeud *debut,int val){
    noeud *Nvnoeud, *ptr;
    Nvnoeud=cree(val);
    Nvnoeud->valeur=val;
    Nvnoeud->suiv=NULL;
    if(debut==NULL){
        debut=Nvnoeud;
    }
    ptr=debut;
        while(ptr->suiv!=NULL){
           ptr = ptr->suiv;
        }
    ptr->suiv=Nvnoeud;
    return debut;
    }
 noeud *suppressionD(noeud *debut){
     if(debut==NULL){
        printf("la liste deja vide.");
        return NULL;
     }
     noeud *tmp=debut;
     debut->suiv;
     free(tmp);
     return debut;
 }

  noeud *suppressionF(noeud *debut){
      if(debut==NULL){
        printf("la liste deja vide.");
        return NULL;
      }
      noeud *ptr=debut;
      if(ptr->suiv==NULL){
        free(ptr);
        return NULL;
      }
      while(ptr->suiv->suiv!=NULL){
        ptr=ptr->suiv;
        }
        free(ptr->suiv);
        ptr->suiv=NULL;

      return debut;
  }

  noeud *suppressionP(noeud *debut,int pos){
      noeud *ptr, *temp;
      ptr=debut;
      if(debut==NULL){
        printf("la liste vide");
        return NULL;
      }
      int size = taille(debut);
      if(pos<1||pos>size){
        printf("la postion est invalide");
        return debut;
      }
      if(pos==1){
        debut=debut->suiv;
        free(ptr);
        return debut;
      }
      int i;
      for(i=1;i<pos;i++){
        ptr=ptr->suiv;
      }
      temp=ptr->suiv;
      ptr->suiv=temp->suiv;
      free(temp);
      return debut;
  }

 int taille(noeud *debut){
     int tl=0;
     noeud *ptr=debut;
     while(ptr!=NULL){
        ptr=ptr->suiv;
        tl++;
     }
     return tl;
 }

 void*rechercher(noeud *debut,int val){
     noeud *ptr=debut;
     while(ptr!=NULL){
        if(ptr->valeur==val)
            return ptr;
        ptr=ptr->suiv;
     }
 }
void affichage (noeud *debut){
    noeud *tmp =debut;
    if(debut==NULL){
    printf("la liste vide");
    }
    else{
        while(tmp!=NULL){
            printf("la valeur est : %d .\n",tmp->valeur);
            tmp=tmp->suiv;
        }
    }
}

noeud* insertion(noeud* debut, int pos, int valeur){
    int size=taille(debut);
    noeud* Nvnoeud=cree(valeur);
    if(pos<1 || pos>size+1){
        printf("position introuvable!");
    }
    if(pos == 1){
        Nvnoeud->suiv = debut;
        debut = Nvnoeud;
        return debut;
    }else{
   noeud* tmp= debut;
    for (int i= 0;tmp !=NULL && i < pos-1; i++)
        {
        tmp= tmp->suiv;
        }
    Nvnoeud->suiv = tmp->suiv;
    tmp->suiv = Nvnoeud;
    }
    return debut;
}

noeud* modifierD(noeud *debut , int val){
     noeud* Nvnoeud=cree(val);
     Nvnoeud->valeur=val;
     Nvnoeud->suiv=NULL;
     if(debut!=NULL)
        Nvnoeud->suiv=debut;
     debut=Nvnoeud;
     return debut;
}

noeud* modifierF(noeud *debut , int val){
    if(debut==NULL){
        printf("liste vide");
        return NULL;
    }
    noeud *ptr=debut;
    while(ptr->suiv!=NULL){
        ptr=ptr->suiv;
    }
     ptr->valeur=val;
     return debut;
}

noeud* modifierP(noeud *debut , int val,int pos){
if(debut==NULL){
    printf("la liste vide");
    return NULL;
}
int tl=taille(debut);
  if(pos<1 || pos>tl){
    printf("la position invalide");
    return debut;
  }
   noeud *ptr=debut;
   int i;
   for(i=1;i<pos;i++){
    ptr=ptr->suiv;
    ptr->valeur=val;
   }
   return debut;
}

int main()
{
    noeud *debut =NULL;
    noeud *P = cree(10);
    noeud *B = cree(550);
    noeud *T = cree(100);

    printf("l'adresse de debut est %p . \n",debut);
    printf("l'adresse de P est %p . \n",P);
    printf("l'adresse de B est %p . \n",B);
    printf("l'adresse de T est %p . \n",T);

    debut=P;
    P->suiv=B;
    B->suiv=T;
    T->suiv=NULL;

    printf("l'adresse de debut est %p . \n",debut);
    printf("l'adresse de P est %p . \n",P);
    printf("l'adresse de B est %p . \n",B);
    printf("l'adresse de T est %p . \n",T);

    printf("ajout debut:\n");
    debut= ajoutdebut(debut,90);
    affichage(debut);

   printf("la taille de la liste est %d .\n",taille(debut));

    printf("ajout fin :\n");
   debut = ajoutfin(debut, 200);
   affichage(debut);

    printf("suppression debut:\n");
    debut = suppressionD(debut);
    affichage(debut);

    printf("suppression fin:\n");
    debut = suppressionF(debut);
    affichage(debut);

    printf("suppression a une position:\n");
    debut = suppressionP(debut,3);
    affichage(debut);

    printf("\ninserer valeur a la position 2 :\n");
    debut = insertion(debut, 2, 80);
    affichage(debut);

    printf("modifier debut:\n");
    debut = modifierD(debut, 10);
    affichage(debut);

    printf("modifier fin:\n");
    debut = modifierF(debut, 700);
    affichage(debut);

    printf("modifier a position 2:\n");
    debut = modifierP(debut, 600, 2);
    affichage(debut);


    printf("rechercher la valeur 20:\n");
    noeud* resultat = rechercher(debut, 20);

    return 0;
}
