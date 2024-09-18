#include<stdio.h>
#include<stdlib.h>
#include<string.h>
int ID=0;
typedef struct phone{
    int id;
    char customerName[50];
    char contactNo[15];
    struct phone* next;
    
}phone;

phone* insert(phone**head,char* name,char* num){
    phone* temp=(phone*)malloc(sizeof(phone));
     ID++;
    temp ->id=ID;
    strcpy(temp->customerName,name);
    strcpy(temp->contactNo,num);
    temp->next=NULL;
    if(*head==NULL){
        *head=temp;
        return *head;
    }
   else if((*head)->next==NULL){
        (*head)->next=temp;
        return* head;
    }
    else{
        phone* curr=*head;
        while(curr->next!=NULL){
            curr=curr->next;
        }
        curr->next=temp;
    }
    return *head;
};
phone * deleteById(phone**head,int ID){
    phone*temp=*head;
    phone* curr;
    while(temp->id!=ID){
        curr=temp;
        temp=temp->next;
    }
    if(temp==NULL){
        printf("This ID does not exist in the Directory\n");
        return*head;
    }
    else{
    curr->next=temp->next;
    temp->next=NULL;
    free(temp);
    temp=NULL;
    return*head;
    }
};
phone* traverse(phone*head){
    int count=0;
    phone*temp=head;
    while(temp){
        printf("%d   ",temp->id);
       printf("%s   ",temp->contactNo);
       printf("%s   \n",temp->customerName);
        count++;
        temp=temp->next;
    }
    printf("\nThere are total of %d Contacts in the Directory\n",count);
};
int main(){
    int data,choice;
phone* head=NULL;

while(1){
    printf("Enter the Directory Operation you want to persom\n");
printf("1->Inserting a contact\n");
printf("2->Deleting a Contact by Id\n");
printf("3->Printing the Entire telephone Directory\n");
scanf("%d",&choice);
switch(choice){
    case 1 :
    char name[50];
    char num[10];
    printf("Enter the customer name : \n");
    scanf("%s",name);
    printf("Enter the contact Numebr : \n");
    scanf("%s",num);
    insert(&head,name,num);
    break;
    
    case 2:
    printf("Enter the id to be deleted :\n");
    scanf("%d",data);
    deleteById(&head,data);
    break;
    
    case 3:
    printf("Printing all the Contacts : \n");
    traverse(head);
    break;
    
    case 4:
    exit(1);
    
    default:
    printf("Wrong choice\n");
}
}
}
