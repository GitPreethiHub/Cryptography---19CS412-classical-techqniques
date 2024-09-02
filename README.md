# Cryptography---19CS412-classical-techqniques

# Caeser Cipher
Caeser Cipher using with different key values

# AIM:

To develop a simple C program to implement Caeser Cipher.

## DESIGN STEPS:

### Step 1:

Design of Caeser Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
```
#include <stdio.h>
#include <ctype.h>

void caesar_cipher(char *text, int shift, int encrypt) {
    int i;

    for (i = 0; text[i] != '\0'; i++) {
        if (isalpha(text[i])) {
            char base = isupper(text[i]) ? 'A' : 'a';
            text[i] = (char)((text[i] - base + (encrypt ? shift : -shift)) % 26 + base);
        }
    }
}

int main() {
    char text[100];
    int shift;

    printf("Enter the text: ");
    fgets(text, 100, stdin);

    printf("Enter the shift value: ");
    scanf("%d", &shift);

    caesar_cipher(text, shift, 1); // Encrypt

    printf("Encrypted text: %s\n", text);

    caesar_cipher(text, shift, 0); // Decrypt

    printf("Decrypted text: %s\n", text);

    return 0;
}
```
## OUTPUT:
![image](https://github.com/user-attachments/assets/c185920e-a40d-4456-9d55-f06ae55b6a9a)

## RESULT:
The program is executed successfully

---------------------------------

# PlayFair Cipher
Playfair Cipher using with different key values

# AIM:

To develop a simple C program to implement PlayFair Cipher.

## DESIGN STEPS:

### Step 1:

Design of PlayFair Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
 ```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

#define SIZE 5

void prepareKeyMatrix(char key[], char keyMatrix[SIZE][SIZE]) {
    int used[26] = {0};
    int i, j, k = 0;

    used['J' - 'A'] = 1;

    for (i = 0; key[i] != '\0'; i++) {
        char currentChar = toupper(key[i]);
        if (!used[currentChar - 'A']) {
            keyMatrix[k / SIZE][k % SIZE] = currentChar;
            used[currentChar - 'A'] = 1;
            k++;
        }
    }

    for (i = 0; i < 26; i++) {
        if (!used[i]) {
            keyMatrix[k / SIZE][k % SIZE] = 'A' + i;
            k++;
        }
    }
}

void printKeyMatrix(char keyMatrix[SIZE][SIZE]) {
    printf("Key Matrix:\n");
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            printf("%c ", keyMatrix[i][j]);
        }
        printf("\n");
    }
}

void findPosition(char keyMatrix[SIZE][SIZE], char letter, int *row, int *col) {
    if (letter == 'J') letter = 'I';
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            if (keyMatrix[i][j] == letter) {
                *row = i;
                *col = j;
                return;
            }
        }
    }
}

void encrypt(char text[], char keyMatrix[SIZE][SIZE], char encryptedText[]) {
    int i, row1, col1, row2, col2;
    char first, second;
    int length = strlen(text);

    for (i = 0; i < length; i += 2) {
        first = toupper(text[i]);
        second = (i + 1 < length) ? toupper(text[i + 1]) : 'X';

        findPosition(keyMatrix, first, &row1, &col1);
        findPosition(keyMatrix, second, &row2, &col2);

        if (row1 == row2) {
            encryptedText[i] = keyMatrix[row1][(col1 + 1) % SIZE];
            encryptedText[i + 1] = keyMatrix[row2][(col2 + 1) % SIZE];
        } else if (col1 == col2) {
            encryptedText[i] = keyMatrix[(row1 + 1) % SIZE][col1];
            encryptedText[i + 1] = keyMatrix[(row2 + 1) % SIZE][col2];
        } else {
            encryptedText[i] = keyMatrix[row1][col2];
            encryptedText[i + 1] = keyMatrix[row2][col1];
        }
    }
    encryptedText[length] = '\0';
}

void decrypt(char text[], char keyMatrix[SIZE][SIZE], char decryptedText[]) {
    int i, row1, col1, row2, col2;
    char first, second;
    int length = strlen(text);

    for (i = 0; i < length; i += 2) {
        first = toupper(text[i]);
        second = (i + 1 < length) ? toupper(text[i + 1]) : 'X';

        findPosition(keyMatrix, first, &row1, &col1);
        findPosition(keyMatrix, second, &row2, &col2);

        if (row1 == row2) {
            decryptedText[i] = keyMatrix[row1][(col1 - 1 + SIZE) % SIZE];
            decryptedText[i + 1] = keyMatrix[row2][(col2 - 1 + SIZE) % SIZE];
        } else if (col1 == col2) {
            decryptedText[i] = keyMatrix[(row1 - 1 + SIZE) % SIZE][col1];
            decryptedText[i + 1] = keyMatrix[(row2 - 1 + SIZE) % SIZE][col2];
        } else {
            decryptedText[i] = keyMatrix[row1][col2];
            decryptedText[i + 1] = keyMatrix[row2][col1];
        }
    }
    decryptedText[length] = '\0';
}

int main() {
    char key[100], text[100], keyMatrix[SIZE][SIZE], encryptedText[100], decryptedText[100];

    printf("Enter the keyword: ");
    fgets(key, sizeof(key), stdin);
    key[strcspn(key, "\n")] = '\0';

    printf("Enter the plaintext: ");
    fgets(text, sizeof(text), stdin);
    text[strcspn(text, "\n")] = '\0';

    if (strlen(text) % 2 != 0) {
        strcat(text, "X");
    }

    prepareKeyMatrix(key, keyMatrix);
    printKeyMatrix(keyMatrix);

    printf("Plaintext: %s\n", text);

    encrypt(text, keyMatrix, encryptedText);
    printf("Encrypted Text: %s\n", encryptedText);

    decrypt(encryptedText, keyMatrix, decryptedText);
    printf("Decrypted Text: %s\n", decryptedText);

    return 0;
}
```
## OUTPUT:
![image](https://github.com/user-attachments/assets/90d37a24-2459-4ca7-93c5-3bfd0d74360b)

## RESULT:
The program is executed successfully

---------------------------


# Hill Cipher
Hill Cipher using with different key values

# AIM:

To develop a simple C program to implement Hill Cipher.

## DESIGN STEPS:

### Step 1:

Design of Hill Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>  // Include the necessary header for toupper()

int keymat[3][3] = { { 1, 2, 1 }, { 2, 3, 2 }, { 2, 2, 1 } };
int invkeymat[3][3] = { { -1, 0, 1 }, { 2, -1, 0 }, { -2, 2, -1 } };
char key[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

void encode(char a, char b, char c, char ret[4]) {
    int x, y, z;
    int posa = (int) a - 65;
    int posb = (int) b - 65;
    int posc = (int) c - 65;
    
    x = posa * keymat[0][0] + posb * keymat[1][0] + posc * keymat[2][0];
    y = posa * keymat[0][1] + posb * keymat[1][1] + posc * keymat[2][1];
    z = posa * keymat[0][2] + posb * keymat[1][2] + posc * keymat[2][2];
    
    ret[0] = key[(x % 26 + 26) % 26];
    ret[1] = key[(y % 26 + 26) % 26];
    ret[2] = key[(z % 26 + 26) % 26];
    ret[3] = '\0';
}

void decode(char a, char b, char c, char ret[4]) {
    int x, y, z;
    int posa = (int) a - 65;
    int posb = (int) b - 65;
    int posc = (int) c - 65;
    
    x = posa * invkeymat[0][0] + posb * invkeymat[1][0] + posc * invkeymat[2][0];
    y = posa * invkeymat[0][1] + posb * invkeymat[1][1] + posc * invkeymat[2][1];
    z = posa * invkeymat[0][2] + posb * invkeymat[1][2] + posc * invkeymat[2][2];
    
    ret[0] = key[(x % 26 + 26) % 26];
    ret[1] = key[(y % 26 + 26) % 26];
    ret[2] = key[(z % 26 + 26) % 26];
    ret[3] = '\0';
}

int main() {
    char msg[1000];
    char enc[1000] = "";
    char dec[1000] = "";
    int n;
    
    strcpy(msg, "SecurityLaboratory");
    printf("Simulation of Hill Cipher\n");
    printf("Input message : %s\n", msg);
    
    for (int i = 0; i < strlen(msg); i++) {
        msg[i] = toupper(msg[i]);
    }
    
    // Remove spaces
    n = strlen(msg) % 3;
    
    // Append padding text X
    if (n != 0) {
        for (int i = 1; i <= (3 - n); i++) {
            strcat(msg, "X");
        }
    }
    
    printf("Padded message : %s\n", msg);
    
    for (int i = 0; i < strlen(msg); i += 3) {
        char a = msg[i];
        char b = msg[i + 1];
        char c = msg[i + 2];
        char ret[4];
        encode(a, b, c, ret);
        strcat(enc, ret);
    }
    
    printf("Encoded message : %s\n", enc);
    
    for (int i = 0; i < strlen(enc); i += 3) {
        char a = enc[i];
        char b = enc[i + 1];
        char c = enc[i + 2];
        char ret[4];
        decode(a, b, c, ret);
        strcat(dec, ret);
    }
    
    printf("Decoded message : %s\n", dec);
    
    return 0;
}
```
## OUTPUT:
![Screenshot 2024-08-30 at 14-20-37 Online C Compiler - Programiz](https://github.com/user-attachments/assets/a73fd00a-f5c4-42e2-92af-57252233a223)

## RESULT:
The program is executed successfully

-------------------------------------------------


# Vigenere Cipher
Vigenere Cipher using with different key values

# AIM:

To develop a simple C program to implement Vigenere Cipher.

## DESIGN STEPS:

### Step 1:

Design of Vigenere Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
```
#include <stdio.h>
#include <string.h>

// Function to perform Vigenere encryption
void vigenereEncrypt(char *text, const char *key) {
    int textLen = strlen(text);
    int keyLen = strlen(key);

    for (int i = 0; i < textLen; i++) {
        char c = text[i];
        if (c >= 'A' && c <= 'Z') {
            // Encrypt uppercase letters
            text[i] = ((c - 'A' + key[i % keyLen] - 'A') % 26) + 'A';
        } else if (c >= 'a' && c <= 'z') {
            // Encrypt lowercase letters
            text[i] = ((c - 'a' + key[i % keyLen] - 'A') % 26) + 'a';
        }
    }
}

// Function to perform Vigenere decryption
void vigenereDecrypt(char *text, const char *key) {
    int textLen = strlen(text);
    int keyLen = strlen(key);

    for (int i = 0; i < textLen; i++) {
        char c = text[i];
        if (c >= 'A' && c <= 'Z') {
            // Decrypt uppercase letters
            text[i] = ((c - 'A' - (key[i % keyLen] - 'A') + 26) % 26) + 'A';
        } else if (c >= 'a' && c <= 'z') {
            // Decrypt lowercase letters
            text[i] = ((c - 'a' - (key[i % keyLen] - 'A') + 26) % 26) + 'a';
        }
    }
}

int main() {
    const char *key = "KEY";  // Replace with your desired key
    char message[] = "This is a secret message.";  // Replace with your message

    // Encrypt the message
    vigenereEncrypt(message, key);
    printf("Encrypted Message: %s\n", message);

    // Decrypt the message back to the original
    vigenereDecrypt(message, key);
    printf("Decrypted Message: %s\n", message);

    return 0;
}
```
## OUTPUT:
![Screenshot 2024-08-30 at 14-24-43 Online C Compiler - Programiz](https://github.com/user-attachments/assets/30296f10-323e-412e-9184-03790ac25c00)

## RESULT:
The program is executed successfully

-----------------------------------------------------------------------















# Rail Fence Cipher
Rail Fence Cipher using with different key values

# AIM:

To develop a simple C program to implement Rail Fence Cipher.

## DESIGN STEPS:

### Step 1:

Design of Rail Fence Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
```
#include<stdio.h>
#include<string.h>
#include<stdlib.h>
main()
{
int i,j,len,rails,count,code[100][1000];
 char str[1000];
 printf("Enter a Secret Message\n");
 gets(str);
 len=strlen(str);
printf("Enter number of rails\n");
scanf("%d",&rails);
for(i=0;i<rails;i++)
{
 for(j=0;j<len;j++)
 {
 code[i][j]=0;
 }
}
count=0;
j=0;
while(j<len)
{
if(count%2==0)
{
for(i=0;i<rails;i++)
{
 //strcpy(code[i][j],str[j]);
 code[i][j]=(int)str[j]; 
 j++;
}
}
else
{
for(i=rails-2;i>0;i--)
{
 code[i][j]=(int)str[j];
j++;
} 
} 
count++;
}
for(i=0;i<rails;i++)
{
for(j=0;j<len;j++)
{
 if(code[i][j]!=0)
 printf("%c",code[i][j]);
}
}
printf("\n");
}
```
## OUTPUT:
![Screenshot 2024-08-30 at 14-35-37 Online C Compiler - online editor](https://github.com/user-attachments/assets/829b97f5-957d-40d4-9ec5-5aa7f23228f8)

## RESULT:
The program is executed successfully
