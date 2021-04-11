---
title: "[21.04.09] 알고리즘활용스터디 - HashTable [내 문제]"
date: 2021-04-09 02:37:28 -0400
categories: 알고리즘활용스터디
---

# HashTable [내 문제]

	#include <stdlib.h>
	#include <stdio.h>
	#include <string.h>
	#include<stdint.h>
	#include<stdbool.h>
	 
	#define MAX_NAME 256
	#define TABLE_SIZE 10
	
	//받을 정보인 person을 struct 구조에 저장! name과 age, 그리고 external chaining 방식으로 collision을 handle하기 때문에 다음 연결된 person을 가리키는 포인터 next도 포함하고 있다.
	typedef struct person{
	    char name[MAX_NAME];
	    int age;
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
	
	//그리고 name으로 해시한 해시테이블을 깔끔하게 출력하기 위해 print_table_with_name()함수를 정의했다.
	void print_table_with_name(){
	    printf("Start\n");
	    for (int i=0; i < TABLE_SIZE; i++){
	        if (hash_table[i] == NULL){
	            printf("\t%i\t--\n", i);
	        }
	        else{
	            printf("\t%i\t",i);
	            person *tmp = hash_table[i];
	            while(tmp != NULL){
	                printf("%s - ", tmp->name);
	                tmp = tmp->next;
	        }
	            printf("\n");
	        }
	}
	    printf("End\n");
	    printf("\n");
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
	
	//해시테이블에서 우리가 원하는 값을 해시테이블에서 삭제하기 위해 name을 입력값으로 하는 hash_table_delete_with_name 함수를 정의했다.
	person *hash_table_delete_with_name(char *name){
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
	
	int main(){
	    
	    print_table_with_name();
	    
	    person jacob = {.name="Jacob", .age = 256};
	    person kate = {.name ="Kate", .age= 27};
	    person mpho = {.name ="Mpho", .age= 14};
	    person sarah = {.name ="Sarah", .age= 54};
	    person edna = {.name ="Edna", .age= 15};
	    person maren = {.name ="Maren", .age= 25};
	    person eliza = {.name ="Eliza", .age= 34};
	    person robert = {.name ="Robert", .age= 1};
	    person jane = {.name ="Jane", .age= 75};
	    
	    hash_table_insert(&jacob);
	    hash_table_insert(&kate);
	    hash_table_insert(&mpho);
	    hash_table_insert(&sarah);
	    hash_table_insert(&edna);
	    hash_table_insert(&robert);
	    hash_table_insert(&jane);
	    hash_table_insert(&maren);
	    hash_table_insert(&eliza);
	    print_table_with_name();
	    
	    hash_table_lookup_with_name("Mpho");
	    
	    hash_table_lookup_with_name("George");
	    
	    hash_table_delete_with_name("Mpho");
	    
	    hash_table_lookup_with_name("Mpho");
	
	    print_table_with_name();
	
	    return 0;
	}

 위 **name**을 기준으로 만든, 해시테이블 이용 함수를 참고하여 이번에는 **age**를 기준으로 헤시테이블 이용 함수들을 만들어보자.

아래는 대략의 구조이다. (함수의 내용만 채우면 된다.)

	#include <stdlib.h>
	#include <stdio.h>
	#include <string.h>
	#include<stdint.h>
	#include<stdbool.h>
	 
	#define MAX_NAME 256
	#define TABLE_SIZE 10
	
	//받을 정보인 person을 struct 구조에 저장! name과 age, 그리고 external chaining 방식으로 collision을 handle하기 때문에 다음 연결된 person을 가리키는 포인터 next도 포함하고 있다.
	typedef struct person{
	    char name[MAX_NAME];
	    int age;
	    struct person *next;
	}person;
	
	//hash table 선언
	person * hash_table[TABLE_SIZE];
	
	//person의 age을 입력값으로 받아서 해시하고, 그 해시값을 반환하는 hash_with_age 함수를 정의해보자. 해시값은 간단하게 age를 TABLE_SIZE로 나눈 값으로 정한다.
	unsigned int hash_with_age(int age){
	   
	}
	
	//age로 해시한 해시테이블을 깔끔하게 출력하기 위해 print_table_with_age()함수를 정의해보자.
	void print_table_with_age(){
	   
	}
	
	//person 구조체의 포인터를 입력값으로 받아서 hash_table에 insert하는 함수이다.
	bool hash_table_insert(person *p){
	    if (p == NULL) return false;
	    int index = hash_with_age(p->age); //이번에는 hash_with_age(n->age)를 통해 나온 값을 index로 사용!
	    p->next = hash_table[index]; //add the person to the front of the list
	    hash_table[index] = p;
	    return true;
	}
	
	//해시 테이블에서 우리가 찾는 값이 헤시테이블에 존재하는지를 알기 위해 age를 입력값으로 하는 hash_table_lookup_with_age 함수를 정의하자. 만약 있다면 "Found (입력된 age)." 존재하지 않는다면 "Not found"를 출력한다.
	void hash_table_lookup_with_age(int age){
	   
	}
	
	//해시테이블에서 우리가 원하는 값을 해시테이블에서 삭제하기 위해 age를 입력값으로 하는 hash_table_delete_with_age 함수를 정의하자.
	person *hash_table_delete_with_age(int age){
	   	    }
	
	int main(){
	    
	    print_table_with_age();
	    
	    person jacob = {.name="Jacob", .age = 256};
	    person kate = {.name ="Kate", .age= 27};
	    person mpho = {.name ="Mpho", .age= 14};
	    person sarah = {.name ="Sarah", .age= 54};
	    person edna = {.name ="Edna", .age= 15};
	    person maren = {.name ="Maren", .age= 25};
	    person eliza = {.name ="Eliza", .age= 34};
	    person robert = {.name ="Robert", .age= 1};
	    person jane = {.name ="Jane", .age= 75};
	    
	    hash_table_insert(&jacob);
	    hash_table_insert(&kate);
	    hash_table_insert(&mpho);
	    hash_table_insert(&sarah);
	    hash_table_insert(&edna);
	    hash_table_insert(&robert);
	    hash_table_insert(&jane);
	    hash_table_insert(&maren);
	    hash_table_insert(&eliza);
	    
	    print_table_with_age();
	    
	    hash_table_lookup_with_age(14);
	    
	    
	    hash_table_lookup_with_age(78);
	    
	    hash_table_delete_with_age(14);
	    
	    hash_table_lookup_with_age(14);
	
	    print_table_with_age();
	
	    return 0;
	}
	

# 코드 완성본
	#include <stdlib.h>
	#include <stdio.h>
	#include <string.h>
	#include<stdint.h>
	#include<stdbool.h>
	 
	#define MAX_NAME 256
	#define TABLE_SIZE 10
	
	//받을 정보인 person을 struct 구조에 저장! name과 age, 그리고 external chaining 방식으로 collision을 handle하기 때문에 다음 연결된 person을 가리키는 포인터 next도 포함하고 있다.
	typedef struct person{
	    char name[MAX_NAME];
	    int age;
	    struct person *next;
	}person;
	
	//hash table 선언
	person * hash_table[TABLE_SIZE];
	
	//person의 age을 입력값으로 받아서 해시하고, 그 해시값을 반환하는 hash_with_age 함수를 정의해보자. 해시값은 간단하게 age를 TABLE_SIZE로 나눈 값으로 정한다.
	unsigned int hash_with_age(int age){
	    unsigned int hash_value = 0;
	        hash_value = age;
	        hash_value %= TABLE_SIZE; //random
	    return hash_value;
	}
	
	//age로 해시한 해시테이블을 깔끔하게 출력하기 위해 print_table_with_age()함수를 정의해보자.
	void print_table_with_age(){
	    printf("Start\n");
	    for (int i=0; i < TABLE_SIZE; i++){
	        if (hash_table[i] == NULL){
	            printf("\t%i\t--\n", i);
	        }
	        else{
	            printf("\t%i\t",i);
	            person *tmp = hash_table[i];
	            while(tmp != NULL){
	                printf("%d - ", tmp->age);
	                tmp = tmp->next;
	        }
	            printf("\n");
	        }
	}
	    printf("End\n");
	    printf("\n");
	}
	
	//person 구조체의 포인터를 입력값으로 받아서 hash_table에 insert하는 함수이다.
	bool hash_table_insert(person *p){
	    if (p == NULL) return false;
	    int index = hash_with_age(p->age); //이번에는 hash_with_age(n->age)를 통해 나온 값을 index로 사용!
	    p->next = hash_table[index]; //add the person to the front of the list
	    hash_table[index] = p;
	    return true;
	}
	
	//해시 테이블에서 우리가 찾는 값이 헤시테이블에 존재하는지를 알기 위해 age를 입력값으로 하는 hash_table_lookup_with_age 함수를 정의하자. 만약 있다면 "Found (입력된 age)." 존재하지 않는다면 "Not found"를 출력한다.
	void hash_table_lookup_with_age(int age){
	    int index = hash_with_age(age);
	    person *tmp = hash_table[index];
	    while(tmp != NULL && tmp->age != age){
	        tmp = tmp->next;
	    }
	    if (tmp == NULL)
	        printf("Not found!\n");
	    else
	        printf("Found %d.\n", tmp->age);
	}
	
	//해시테이블에서 우리가 원하는 값을 해시테이블에서 삭제하기 위해 age를 입력값으로 하는 hash_table_delete_with_age 함수를 정의하자.
	person *hash_table_delete_with_age(int age){
	    int index = hash_with_age(age);
	    person *tmp = hash_table[index];
	    person *prev = NULL;
	    while(tmp != NULL && tmp->age != age){
	        prev = tmp;
	        tmp = tmp->next;
	    }
	    if(prev == NULL){
	        //the match that we should be deleting is the head
	        hash_table[index] = tmp->next;
	    }
	    if(tmp == NULL) return NULL; //We didn't find a match.
	    else{
	        prev->next = tmp -> next;
	    }
	     return tmp;
	    }
	
	int main(){
	    
	    print_table_with_age();
	    
	    person jacob = {.name="Jacob", .age = 256};
	    person kate = {.name ="Kate", .age= 27};
	    person mpho = {.name ="Mpho", .age= 14};
	    person sarah = {.name ="Sarah", .age= 54};
	    person edna = {.name ="Edna", .age= 15};
	    person maren = {.name ="Maren", .age= 25};
	    person eliza = {.name ="Eliza", .age= 34};
	    person robert = {.name ="Robert", .age= 1};
	    person jane = {.name ="Jane", .age= 75};
	    
	    hash_table_insert(&jacob);
	    hash_table_insert(&kate);
	    hash_table_insert(&mpho);
	    hash_table_insert(&sarah);
	    hash_table_insert(&edna);
	    hash_table_insert(&robert);
	    hash_table_insert(&jane);
	    hash_table_insert(&maren);
	    hash_table_insert(&eliza);
	    
	    print_table_with_age();
	    
	    hash_table_lookup_with_age(14);
	    
	    
	    hash_table_lookup_with_age(78);
	    
	    hash_table_delete_with_age(14);
	    
	    hash_table_lookup_with_age(14);
	
	    print_table_with_age();
	
	    return 0;
	}
	
	
