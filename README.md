# trabalho

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include "trabalho.h"

void cria(Lista *L){
  L->ini = NULL;
  L->fim = NULL;
}

void cadastrar(Lista *L, char *nome, int *erro){
  no *p = (no *)malloc(sizeof(no));
  no *aux = L->ini;
  int ordnome = -1;
  
  if(p == NULL){
    *erro = 1;
    return;
  } else {
    strcpy(p->nome,nome);
    if(L->ini == NULL){
      L->ini = p;
      L->fim = p;
      p->prox = NULL;
      p->ant = NULL;
      return;
    } else {
      while(ordnome < 0){
	ordnome = strcmp(aux->nome,p->nome);
	if(ordnome > 0){
	  break;
	}
	if(aux->prox == NULL){
	  //ordnome = 1;
	  break;
	}
	aux = aux->prox;
      }

      
      if(ordnome == 0){
      	*erro = 2;
      	return;
      } else {
	//ordnome = 0;
	if(aux->prox == NULL && aux->ant == NULL){
	  p->ant = aux;
	  p->prox = NULL;
	  L->fim = p;
	  aux->prox = p;
	  return;
	} else if(aux->prox == NULL && aux->ant != NULL){
	  ordnome = strcmp(aux->ant->nome,p->nome);
	  if((strcmp(aux->ant->nome,p->nome) < 0) && (strcmp(aux->nome,p->nome) > 0)){
	    p->prox = aux;
	    p->ant = aux->ant;
	    aux->ant = p;
	    (aux->ant)->prox = p;
	    return;
	  } else {
	    p->prox = NULL;
	    aux->prox = p;
	    p->ant = aux;
	    return;
	  }
	}
      }
    }
  }
}

void listaprodutos(Lista *L){
  no *p = L->ini;

  if(p == NULL){
    printf("Nenhum produto cadastrado.\n");
  } else {
    while(p != NULL){
      printf("%s\n", p->nome);
      p = p->prox;
    }
  }
}
