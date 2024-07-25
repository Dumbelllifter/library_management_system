#include <stdio.h>
#include <string.h>

#define MAX 30
#define MAX_BOOK 100

typedef struct {
    char title[MAX];
    char genre[MAX];
    char author[MAX];
    char status[MAX/2];
    int id;
} book;

book Book1 = {"Book One", "Genre", "Author", "Avaiable", 0};
book Book2 = {"Book Two", "Genre", "Author", "Available", 1};
book Book3 = {"Book Three", "Genre", "Author", "Available", 2};


void add_book(book client_list[], int *client_list_size, const char *title) {
    if(client_list_size >= MAX_BOOK) {
        printf("The list is full");
        return;
    }
    strncpy(client_list[*client_list_size].title, title, MAX - 1);
    client_list[*client_list_size].title[MAX - 1] = '\0';
    strcpy(client_list[*client_list_size].status, "available");
    client_list[*client_list_size].id = *client_list_size + 1; 

    (*client_list_size)++;
    printf("Book '%s' added to the client's list.\n", title);
}

void remove_book(book client_list[], int *client_list_size, const char *title) {
    int i, j;

    if (*client_list_size == 0) {
        printf("There are no books in the list!\n");
        return;
    }

    for (i = 0; i < *client_list_size; i++) {
        if (strcmp(client_list[i].title, title) == 0) {
            for (j = i; j < *client_list_size - 1; j++) {
                client_list[j] = client_list[j + 1];
            }

            (*client_list_size)--;
            printf("Book '%s' has been removed from the list.\n", title);
            return;
        }
    }

    printf("Book '%s' not found in the list.\n", title);
}



void client_choice_handler(int choice_number, int client_list) {
    switch(choice_number) {
        case 1:
            printf("Enter the book name:\n");
            char book_name[MAX];
            scanf("%s", &book_name);
            // Gotta complete
            break;
        case 2:
            if(client_list < 1) {
                printf("What book would you like to add to your list?\n");
                // Code to handle adding a book goes here
            } else {
                int client_choice_two;
                printf("1 - Add a book.\n2 - Remove a book.\n");
                scanf("%d", &client_choice_two);
                switch(client_choice_two) {
                    case 1:
                        printf("Enter a book name to add:\n");
                        // Code to handle adding a book goes here
                        break;
                    case 2:
                        if(client_list == 1) {
                            printf("Removing book from your list!\n");
                            // Code to handle removing the only book goes here
                        } else {
                            char client_remove[MAX];
                            printf("What book would you like to remove?\n");
                            scanf("%s", client_remove); 
                        }
                        break;
                    default:
                        printf("Invalid input!\n");
                        break;
                }
            }
            break;
        default:
            printf("Invalid input!\n");
            break;
    }
}

int main() {
    int client_choice;
    int client_list_quantity = 0;

    printf("Hi! You can begin by choosing an option:\n1 - Search for author or book.\n2 - Add or remove a book from your list.\n");
    scanf("%d", &client_choice);

    client_choice_handler(client_choice, client_list_quantity);

    return 0;
}