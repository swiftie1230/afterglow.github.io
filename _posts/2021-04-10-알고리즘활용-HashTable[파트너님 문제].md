---
title: "[21.04.10] 알고리즘활용스터디 - HashTable [파트너님 문제]"
date: 2021-04-10 12:40:28 -0400
categories: 알고리즘활용스터디
---

# HashTable [파트너님 문제]

코딩테스트 연습-해시-[완주하지 못한 선수] 문제이다.

## 문제 설명

수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.

마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

## 제한사항
마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다. 

completion의 길이는 participant의 길이보다 1 작습니다.  

참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.

참가자 중에는 동명이인이 있을 수 있습니다. 

## 입출력 예시
<img width="279" alt="스크린샷 2021-04-10 오후 12 39 58" src="https://user-images.githubusercontent.com/63195670/114257285-ebfc0280-99f9-11eb-9fd9-877ab2a1da32.png">

 
## 내 코드 설명
두개의 배열을 받고 완주하지 못한 선수의 이름을 return하는 함수인 solution 함수를 만들기 위해 시도했지만 자꾸 오류가 떴다.        
C언어로는 확실히 구현이 어려운 문제인 것 같다. ㅜㅜ

그래서 HashTable을 만들고, 배열 participant의 값들을 `hash_table_insert` 함수에, completion의 값들을 `hash_table_delete` 함수에 각각 넣은 후, hashtable에 남아있는 이름을 출력하는 식으로 문제를 바꾸어 풀어보았다.
	
	#include<stdio.h>
	#include<string.h>
	#include<stdbool.h>
	
	#define TABLE_SIZE 100001 //문제에서 참가 선수가 100000명 이하라고 했으므로
	#define MAX_NAME 21 //참가자의 이름이 20개 이하라고 했으므로
	
	//person 구조체에 이름을 저장
	typedef struct person{
	    char name[MAX_NAME];
	}person;
	
	//person을 반환값으로 하는 hash_table 선언
	person * hash_table[TABLE_SIZE];
	
	//hash 함수 정의! 
	unsigned int hash(char *name){
	    int length = strnlen(name, MAX_NAME);
	    unsigned int hash_value = 0;
	    for (int i=0; i < length; i++){
	        hash_value += name[i];
	        hash_value = (hash_value * name[i]) % TABLE_SIZE; //random
	        
	    }
	    return hash_value;
	}
	
	//insert 함수 정의!
	bool hash_table_insert(person *p){
	    if (p == NULL) return false;
	    int index = hash(p->name);
	    hash_table[index] = p;
	    return true;
	}
	
	//delete 함수 정의!
	person *hash_table_delete(char *name){
	    int index = hash(name);
	    if(hash_table[index] != NULL && strncmp(hash_table[index]->name, name, TABLE_SIZE)== 0){
	        person *tmp = hash_table[index];
	        hash_table[index] = NULL;
	        return tmp; //return the pointer that we saved to the caller, so the caller can free the pointer
	    }
	    else{
	        return NULL;
	    }
	}
	
	//hash_table에 남아있는 값을 출력하는 solution함수 정의!
	void solution(){
	    for(int i = 0; i<TABLE_SIZE;i++){
	        person *tmp = hash_table[i];
	        if(hash_table[i] != NULL){
	            printf("완주하지 못한 선수는 %s입니다.\n", tmp->name);
	        }
	    }
	    return;
	}
	
	int main(){
	    //값들 입력
	    person marina = {.name="marina"};
	    person josipa = {.name ="josipa"};
	    person nikola = {.name ="nikola"};
	    person vinko = {.name ="vinko"};
	    person filipa = {.name ="filipa"};
	    
	    hash_table_insert(&marina);
	    hash_table_insert(&josipa);
	    hash_table_insert(&nikola);
	    hash_table_insert(&filipa);
	    hash_table_insert(&vinko);
	    
	    hash_table_delete("marina");
	    hash_table_delete("josipa");
	    hash_table_delete("nikola");
	    hash_table_delete("filipa");
	    
	    //solution함수를 돌린다.
	    solution();
	}
	
	빌드 성공! 
