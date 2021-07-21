---
title: "[21.04.10] 알고리즘활용스터디 - HashTable [파트너님 문제]"
date: 2021-04-10 12:40:28 -0400
toc: true
toc_sticky: true
categories: Algorithm_Study
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
hash_table을 만드는데 아무래도 구조체가 편리해서 구조체 배열을 만들어서 해결해 봤다.

scanf로 참가한 선수의 수를 받고, 그 입력받은 수를 바탕으로 구조체 배열 participant(크기 N)와 completion(크기 N-1) 두개를 만든 후,
“몇 번째 참가한 선수의 이름을 입력하세요 : “
를 통해 참가한 선수 이름을 입력받아서 participant 구조체 배열에 넣는다.    
동일하게
“완주한 선수의 이름을 입력하세요:”
라는 문구로 완주한 선수 이름을 입력받아서 completion 구조체 배열에 넣는다.

participant는 hash_table에 insert하고, completion은 delete한다. 
마지막으로 최종 hash_table에 남은 이름을 return하는 solution함수를 정의해서 main함수에서 출력하면 끝!

## 내 코드
	#include <stdlib.h>
	#include <stdio.h>
	#include <string.h>
	#include<stdint.h>
	#include<stdbool.h>
	 
	#define MAX_NAME 21
	#define TABLE_SIZE 100001
	
	//받을 정보인 person을 struct 구조에 저장! name 그리고 external chaining 방식으로 collision을 handle하기 때문에 다음 연결된 person을 가리키는 포인터 next도 포함하고 있다.
	typedef struct person{
	    char name[MAX_NAME];
	    struct person *next;
	}person;
	
	//hash table 선언
	person * hash_table[TABLE_SIZE];
	
	//person의 name을 입력값으로 받아서 해시하고, 그 해시값을 반환하는 hash_with_name 함수를 정의했다.
	unsigned int hash_with_name(char *name){
	    int length = strnlen(name, MAX_NAME);
	    unsigned int hash_value = 0;
	    for (int i=0; i < length; i++){
	        hash_value += name[i];
	        hash_value = (hash_value * name[i]) % TABLE_SIZE; //random
	        
	    }
	    return hash_value;
	}
	
	
	//person 구조체의 포인터를 입력값으로 받아서 hash_table에 insert하는 함수이다.
	bool hash_table_insert(person *p){
	    if (p == NULL) return false;
	    int index = hash_with_name(p->name); //hash_with_names(p->name)를 통해 나온 값을 index로 사용!
	    p->next = hash_table[index]; //add the person to the front of the list
	    hash_table[index] = p;
	    return true;
	}
	
	//해시 테이블에서 우리가 찾는 값이 헤시테이블에 존재하는지를 알기 위해 name을 입력값으로 하는 hash_table_lookup_with_name 함수를 정의했다. 만약 있다면 "Found (입력된 name)." 존재하지 않는다면 "Not found"를 출력한다.
	void hash_table_lookup_with_name(char *name){
	    int index = hash_with_name(name);
	    person *tmp = hash_table[index];
	    while(tmp != NULL && strncmp(tmp->name, name, MAX_NAME)!=0){
	        tmp = tmp->next;
	    }
	    if (tmp == NULL)
	        printf("Not found!\n");
	    else
	        printf("Found %s.\n", tmp->name);
	}
	
	//해시테이블에서 우리가 원하는 값을 해시테이블에서 삭제하기 위해 name을 입력값으로 하는 hash_table_delete 함수를 정의했다.
	person *hash_table_delete(char *name){
	    int index = hash_with_name(name);
	    person *tmp = hash_table[index];
	    person *prev = NULL;
	    while(tmp != NULL && strncmp(tmp->name, name, MAX_NAME)!=0){
	        prev = tmp;
	        tmp = tmp->next;
	    }
	    if(tmp == NULL) return NULL; //We didn't find a match.
	    if(prev == NULL){
	        //the match that we should be deleting is the head
	        hash_table[index] = tmp->next;
	    }
	    else{
	        prev->next = tmp -> next;
	    }
	     return tmp;
	    }
	
	char * solution(){
	    char * sol = 0;
	    for(int i = 0; i<TABLE_SIZE;i++){
	        person *tmp = hash_table[i];
	        if(hash_table[i] != NULL){
	            sol = tmp->name;
	        }
	    }
	    return sol;
	}
		
	int main(){
	    int N;
	    scanf("%d",&N);
	    
	    person participant[N];
	    person completion[N-1];
	    
	    for(int i=0;i<N;i++){
	        printf("%d번째 참가한 선수의 이름을 입력하세요: ",i+1);
	        scanf("%s", participant[i].name);
	        hash_table_insert(&participant[i]);
	    }
	    
	    for(int j=0;j<N-1;j++){
	        printf("완주한 선수의 이름을 입력하세요: ");
	        scanf("%s", completion[j].name);
	        hash_table_delete(completion[j].name);
	    }
		
	    printf("완주하지 못한 선수는 %s입니다", solution());
		
	    return 0;
	}
	
<img width="384" alt="스크린샷 2021-04-13 오후 2 13 47" src="https://user-images.githubusercontent.com/63195670/114506359-a2ffb480-9c6c-11eb-8f70-099379acb4b6.png">
  
빌드 성공! 
