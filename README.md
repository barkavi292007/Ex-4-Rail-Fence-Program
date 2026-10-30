# Ex-4 Rail-Fence-Program

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM
```

#include <stdio.h>
#include <string.h>

int main()
{
    char text[100], cipher[100], decrypt[100];
    int key, i, j, k = 0;

    printf("Enter plaintext: ");
    fgets(text, sizeof(text), stdin);
    text[strcspn(text, "\n")] = '\0';

    printf("Enter key: ");
    scanf("%d", &key);

    int len = strlen(text);
    char rail[key][len];

    for(i = 0; i < key; i++)
        for(j = 0; j < len; j++)
            rail[i][j] = '\n';

    int row = 0, dir = 1;

    for(i = 0; i < len; i++)
    {
        rail[row][i] = text[i];

        if(row == 0)
            dir = 1;
        else if(row == key - 1)
            dir = -1;

        row += dir;
    }

    for(i = 0; i < key; i++)
        for(j = 0; j < len; j++)
            if(rail[i][j] != '\n')
                cipher[k++] = rail[i][j];

    cipher[k] = '\0';

    printf("\nEncrypted text: %s", cipher);

    k = 0;
    row = 0;
    dir = 1;

    for(i = 0; i < len; i++)
    {
        rail[row][i] = '*';

        if(row == 0)
            dir = 1;
        else if(row == key - 1)
            dir = -1;

        row += dir;
    }

    for(i = 0; i < key; i++)
        for(j = 0; j < len; j++)
            if(rail[i][j] == '*')
                rail[i][j] = cipher[k++];

    row = 0;
    dir = 1;

    for(i = 0; i < len; i++)
    {
        decrypt[i] = rail[row][i];

        if(row == 0)
            dir = 1;
        else if(row == key - 1)
            dir = -1;

        row += dir;
    }

    decrypt[len] = '\0';

    printf("\nDecrypted text: %s\n", decrypt);

    return 0;
}

```
# OUTPUT
<img width="922" height="327" alt="image" src="https://github.com/user-attachments/assets/6f852531-f896-4672-8760-a4dd380be6ce" />


# RESULT
Thus, the Rail Fence Cipher program was successfully executed, and both encrypted and decrypted texts were obtained.
