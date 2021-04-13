---
title: "[21.04.13] 알고리즘활용스터디 - HashTable [정리]"
date: 2021-04-13 03:20:28 -0400
categories: 알고리즘활용스터디
---

# HASH TABLE

Hash Table을 이해하기 위해서는 Linked List, Doubly Linked List, Array에 대한 기본 지식이 필요하다. 

Hash Table을 공부하고 관련 문제를 풀고 싶다면 위 자료구조들을 다시 학습하고, 구현까지 미리 해보는 것을 추천한다! 

-


우선, **엄청나게 많은 정보**가 서로 **Linked** 되어서 **Linked List에 저장**되어 있다고 가정해 보자.   
만약 여기서 우리가 **특정 정보를 찾고 싶을 때** 어떻게 해야 할까?    

처음 store되어 있는 정보부터 차례차례 Link를 따라가면서 내가 찾는 정보가 맞는지를 확인해야 한다.    
물론, 운이 좋아서 우리가 찾고 있는 정보가 앞쪽에 있을 수도 있겠지만, 운이 나빠서 맨 끝쪽에 있다면?    
정보 하나를 찾는데도 무지막지한 시간이 걸릴 것이다.   

이와 같은 Operation을 우리는 Linear Time Operation이라고 한다.    
또는 "Time Complexity is O(n) [Big O of n]" 즉, "시간 복잡도가 빅오n이다"라고 말하기도 한다.   
이는 우리가 찾고 싶은 정보를 찾는데 걸리는 시간은 정보의 양이 증가할수록 늘어나게 된다는 뜻이다.   

이 같은 문제를 해결하는 것이 HASH TABLE이다. HASH TABLE의 Time Complexity는 O(1)이다.     
즉 **정보의 양과 관계없이 constant**한 것!


-

지금까지 HASH TABLE의 장점과 사용하는 이유에 대해 간략히 살펴보았다.       
그렇다면 이제 HASH TABLE에 대해 본격적으로 알아보자.       
HASH TABLE은 형식적으로 본다면, Hash Function을 가진 Array라고 할 수 있다.   




어떤 정보 input이 있을 때, input을 Hash Function에 넣어서 나온 출력값을 Array에 저장하게 된다.    
예를 들어 우리가 어떤 사람에 관한 정보(그들의 이름, 나이..)를 저장하고, 그들의 **이름**으로 사람 정보를 찾고 싶다고 가정해 보자.   
그렇다면 **input은 사람의 이름**이 되고,  HASH TABLE은 이를 **Hash Function에 넣어서 나온 값을 index로 하여 배열에 저장**하는 것이다!    

여기서 잠깐! 우리가 HashFunction을 만들 때, 아무렇게나 만들면 안된다.     
좋은 Hash Function을 만들기 위해서는 아래 3가지 조건을 반드시 명심하자.

### 좋은 HASH FUNCTION을 만들 때 반드시 알아야 할 조건
	1. **같은 input은 반드시, 언제나 같은 output을 생성**해야 한다.
	2. function 자체가 너무 **느리면 안된다**. 
	3. 비교적 **랜덤한 값**을 출력해야 한다. -> Collision 최소화!


위 조건들 중 3번은 Collision을 최소화 하기 위해서이다.    
그렇다면 Collision은 무엇일까?

Collision은 충돌을 의미하는데, 다른 input 값이 같은 output을 출력할 때, 우리는 충돌이 일어났다고 말한다.    

정보의 내용이 많아지고 방대해질수록 충돌은 불가피하게 일어날 수 밖에 없다. 그렇기에 이러한 Collison이 일어나는 경우에도 HASH TABLE에 정보를 저장하기 위한 다양한 해결 방법이 존재한다.        
그중 하나는 Open-Addressing이고, 또 하나는 External-Chaining!    

Open-Addressing은 만약 어떤 input이 들어왔을 때 Hash Function 출력값의 index 배열값에 이미 어떤 정보가 존재한다면 (충돌이 일어난다면), 배열을 돌아보면서 빈 공간이 있는지 확인 후, 배열의 남아있는 빈공간에 그 정보를 할당하는 방법이다.    

아래는 Open-Addressing을 이용하여 간단한 HASHTABLE을 구현한 것이다.

### Delete한 값을 명시적으로 표시하지 않는 Open-Addressing을 이용한 HASHTABLE

	#include <stdlib.h>
	#include<stdio.h>
	#include<string.h>
	#include<stdint.h>
	#include<stdbool.h>
	
	#define MAX_NAME 256
	#define TABLE_SIZE 10
	
	typedef struct{
	    char name[MAX_NAME];
	    int age;
	    //...add other stuff later, maybe
	}person;
	
	person * hash_table[TABLE_SIZE];
	
	unsigned int hash(char *name){
	    int length = strnlen(name, MAX_NAME);//strnlen은 문자열과 문자열 길이의 맥스값을 넣어주어서 문자열의 길이가 맥스값을 넘으면 맥스값을 리턴하고 문자열의 길이가 맥스값을 안 넘으면 문자열의 길이를 리턴해준다.
	    
	    unsigned int hash_value = 0;
	    
	    for(int i=0; i < length; i++){
	        hash_value += name[i];
	        hash_value = (hash_value * name[i]) % TABLE_SIZE;
	    }
	    
	    return hash_value;
	}
	
	void init_hash_table(){
	    for(int i=0; i<TABLE_SIZE; i++){
	        hash_table[i] = NULL;
	    }
	    //table is empty
	}
	
	//The function that prints out the status of the table, so we can see what's going on.
	void print_table(){
	    printf("START\n");
	    for(int i=0; i<TABLE_SIZE; i++){
	        if(hash_table[i] == NULL){
	            printf("\t%i\t---\n",i); // if there is nothing, just print something that we can know it's empty
	        }
	        else{
	            printf("\t%i\t%s\n",i, hash_table[i]->name); //if there is something in the slot, we print it out.
	        }
	    }
	    printf("END\n");
	    printf("\n");
	}
	
	// A function that is going to insert a person into the table.
	//It will return true if we successfully insert a person, false if we don't.
	bool hash_table_insert(person *p){
	    if(p == NULL) return false; // Make sure that we don't accidently call this function with a NULL pointer!
	    int index = hash(p->name);
	    for(int i=0; i<TABLE_SIZE;i++){
	        int try = (i + index) % TABLE_SIZE;
	        if(hash_table[try] == NULL){ //If the hash_table[try] is empty, then we store the data in there.
	            hash_table[try] = p;
	            return true;
	        }
	    }
	    if(hash_table[index] != NULL){ //collision
	        return false;
	    }
	    hash_table[index] = p;
	    return true;
	}
	
	//This function find a person in the table by their name.
	person *hash_table_lookup(char *name){
	    int index = hash(name);
	    if(hash_table[index] != NULL && strncmp(hash_table[index]->name, name, TABLE_SIZE)== 0){
	        return hash_table[index];
	    }
	    else{
	        return NULL;
	    }
	}
	
	//This function deletes a person in the table.
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
	
	int main()
	{
	    //just to start with a clean state.
	    init_hash_table();
	    
	    print_table();
	    
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
	    
	    print_table();
	    
	    person *tmp = hash_table_lookup("Mpho");
	    if(tmp == NULL){
	        printf("Not found!\n");
	    }
	    else{
	        printf("Found %s.\n", tmp->name);
	    }
	    
	    tmp = hash_table_lookup("George");
	    if(tmp == NULL){
	        printf("Not found!\n");
	    }
	    else{
	        printf("Found %s.\n", tmp->name);
	    }
	    
	    hash_table_delete("Mpho");
	    
	    hash_table_delete("George"); //Nothing in the output because there is no George in the Table.
	    
	    tmp = hash_table_lookup("Mpho");
	    if(tmp == NULL){
	        printf("Not found!\n");
	    }
	    else{
	        printf("Found %s.\n", tmp->name);
	    }
	    
	    print_table();
	}


### Delete한 값을 명시적으로 표시하는 Open-Addressing을 이용한 HASHTABLE

	#include <stdlib.h>
	#include<stdio.h>
	#include<string.h>
	#include<stdint.h>
	#include<stdbool.h>
	
	#define MAX_NAME 256
	#define TABLE_SIZE 10
	#define DELETED_NODE (person*)(0xFFFFFFFFFFFFFFUL)
	
	typedef struct{
	    char name[MAX_NAME];
	    int age;
	    //...add other stuff later, maybe
	}person;
	
	person * hash_table[TABLE_SIZE];
	
	unsigned int hash(char *name){
	    int length = strnlen(name, MAX_NAME);//strnlen은 문자열과 문자열 길이의 맥스값을 넣어주어서 문자열의 길이가 맥스값을 넘으면 맥스값을 리턴하고 문자열의 길이가 맥스값을 안 넘으면 문자열의 길이를 리턴해준다.
	    
	    unsigned int hash_value = 0;
	    
	    for(int i=0; i < length; i++){
	        hash_value += name[i];
	        hash_value = (hash_value * name[i]) % TABLE_SIZE;
	    }
	    
	    return hash_value;
	}
	
	void init_hash_table(){
	    for(int i=0; i<TABLE_SIZE; i++){
	        hash_table[i] = NULL;
	    }
	    //table is empty
	}
	
	//The function that prints out the status of the table, so we can see what's going on.
	void print_table(){
	    printf("START\n");
	    for(int i=0; i<TABLE_SIZE; i++){
	        if(hash_table[i] == NULL){
	            printf("\t%i\t---\n",i); // if there is nothing, just print something that we can know it's empty
	        }
	        else if(hash_table[i] == DELETED_NODE){
	            printf("\t%i\t---<deleted>\n",i);
	        }
	        else
	        {
	            printf("\t%i\t%s\n",i, hash_table[i]->name); //if there is something in the slot, we print it out.
	        }
	    }
	    printf("END\n");
	    printf("\n");
	}
	
	// A function that is going to insert a person into the table.
	//It will return true if we successfully insert a person, false if we don't.
	bool hash_table_insert(person *p){
	    if(p == NULL) return false; // Make sure that we don't accidently call this function with a NULL pointer!
	    int index = hash(p->name);
	    for(int i=0; i<TABLE_SIZE;i++){
	        int try = (i + index) % TABLE_SIZE;
	        if(hash_table[try] == NULL || hash_table[try] == DELETED_NODE){ //If the hash_table[try] is empty, then we store the data in there.
	            hash_table[try] = p;
	            return true;
	        }
	    }
	    return false; //If the hash_table is full, then we failed to insert, return false.
	}
	
	//This function find a person in the table by their name.
	person *hash_table_lookup(char *name){
	    int index = hash(name);
	    for(int i = 0; i<TABLE_SIZE; i++){
	        int try = (index + i) % TABLE_SIZE;
	        if(hash_table[try] == NULL){
	            return false; //not here
	        }
	        if(hash_table[try] == DELETED_NODE) continue;
	        if(strncmp(hash_table[try]->name, name, TABLE_SIZE)== 0){
	            return hash_table[try];
	        }
	    }
	    return NULL;
	}
	
	//This function deletes a person in the table.
	person *hash_table_delete(char *name){
	    int index = hash(name);
	    for(int i = 0; i<TABLE_SIZE; i++){
	        int try = (index + i) % TABLE_SIZE;
	        if(hash_table[try] == NULL){
	            return NULL;
	        }
	        if(hash_table[try] == DELETED_NODE) continue;
	        if(strncmp(hash_table[try]->name, name, TABLE_SIZE)== 0){
	            person* tmp = hash_table[try];
	            hash_table[try] = DELETED_NODE;
	            return tmp;
	        }
	    }
	    return NULL;
	}
	
	int main()
	{
	    //just to start with a clean state.
	    init_hash_table();
	    
	    print_table();
	    
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
	    
	    print_table();
	    
	    person *tmp = hash_table_lookup("Mpho");
	    if(tmp == NULL){
	        printf("Not found!\n");
	    }
	    else{
	        printf("Found %s.\n", tmp->name);
	    }
	    
	    tmp = hash_table_lookup("George");
	    if(tmp == NULL){
	        printf("Not found!\n");
	    }
	    else{
	        printf("Found %s.\n", tmp->name);
	    }
	    
	    hash_table_delete("Mpho");
	    
	    tmp = hash_table_lookup("Mpho");
	    if(tmp == NULL){
	        printf("Not found!\n");
	    }
	    else{
	        printf("Found %s.\n", tmp->name);
	    }
	    
	    print_table();
	}


두번째로, External-Chaining은 많은 분들이 사용하는 방법이다.    
만약 어떤 input이 들어왔을 때 Hash Function 출력값의 index 배열값에 이미 어떤 정보가 존재한다면 (충돌이 일어난다면), 그냥 단순하게 linked list를 이용해서 ( 또는 doubly linked list를 이용해서) 이미 존재하던 값과 link 해주는 것이다.

아래는 External-Chaining을 이용하여 간단한 HASHTABLE을 구현한 것이다.

### External-Chaining을 이용한 HASHTABLE

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


이런 Collision이 많이 일어날수록 HASH TABLE은 더 복잡해지고 정보를 찾는 것도 느려질 수 있다.       
그렇기에 Collsion을 최소화할 수록 더 좋은 HASH FUNCTION이라고 할 수 있다.






