---
platform: Codeforces
difficulty: "1300"
date: 2026-01-29
---
# Solution
- C
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define TABLE_SIZE 150001

// Node structure in the linked list (For collision handling)
typedef struct Node {
    char value[33];
    int count;
    struct Node* next;
}Node;

// Hash table strcucture
typedef struct HashTable {
    Node* buckets[TABLE_SIZE];
} HashTable;
HashTable myTable;

// The hash function
int hashFunction(char* str){
    int length = strlen(str);
    unsigned int ascii = 0;
    for (int i = 0; i < length; i++){
        char character = str[i];
        ascii *= 31;
        ascii += character;
    }
    return ascii % TABLE_SIZE;
}
  
// Initalize the Hash Table
void init_table(HashTable* ht){
    for (int i = 0; i < TABLE_SIZE; i++){
        ht->buckets[i] = NULL;
    }
}

// Create a new Node
Node* createNode(const char* value){
    Node* newNode = (Node*)malloc(sizeof(Node));
    if (newNode == NULL)return NULL;  
    memset(newNode->value, 0, sizeof(newNode->value));
    strncpy(newNode->value, value, 32);
    newNode->value[32] = '\0';
    newNode->count = 1;
    newNode->next = NULL;
    return newNode;
}

// register a user function : it contains both insert an item and search
void registerUser(HashTable* ht, char* name){
    unsigned int index = hashFunction(name);
    Node* current = ht->buckets[index];
    while (current != NULL){
        if (strcmp(current->value, name) == 0){
            printf("%s%d\n", current->value, current->count);  
            current->count++;
            return;
        }
        current = current->next;
    }
    printf("OK\n");
    Node* newNode = createNode(name);
    newNode->next = ht->buckets[index];
    ht->buckets[index] = newNode;
}

int main(){
    int n;
    char name[100];
    scanf("%d", &n);
    init_table(&myTable);
    for (int i = 0; i < n; i++){
        scanf("%s", name);
        registerUser(&myTable, name);
    }
    return 0;
}
```

- Learned so much about `Hash Tables` really advise you to watch this video to learn about them : [Understand hash tables](https://youtu.be/KyUTuwz_b7Q?si=4TfuCGGCLY7s-IpL)
