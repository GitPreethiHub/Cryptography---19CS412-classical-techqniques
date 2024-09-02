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
#include <ctype.h>

int keymat[3][3] = {{1, 2, 1}, {2, 3, 2}, {2, 2, 1}};
int invkeymat[3][3] = {{-1, 0, 1}, {2, -1, 0}, {-2, 2, -1}};
char key[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

void encode(char a, char b, char c, char *ret) {
    int x = (a - 65) * keymat[0][0] + (b - 65) * keymat[1][0] + (c - 65) * keymat[2][0];
    int y = (a - 65) * keymat[0][1] + (b - 65) * keymat[1][1] + (c - 65) * keymat[2][1];
    int z = (a - 65) * keymat[0][2] + (b - 65) * keymat[1][2] + (c - 65) * keymat[2][2];
    ret[0] = key[x % 26];
    ret[1] = key[y % 26];
    ret[2] = key[z % 26];
    ret[3] = '\0';
}

void decode(char a, char b, char c, char *ret) {
    int x = (a - 65) * invkeymat[0][0] + (b - 65) * invkeymat[1][0] + (c - 65) * invkeymat[2][0];
    int y = (a - 65) * invkeymat[0][1] + (b - 65) * invkeymat[1][1] + (c - 65) * invkeymat[2][1];
    int z = (a - 65) * invkeymat[0][2] + (b - 65) * invkeymat[1][2] + (c - 65) * invkeymat[2][2];
    ret[0] = key[(x % 26 + 26) % 26];
    ret[1] = key[(y % 26 + 26) % 26];
    ret[2] = key[(z % 26 + 26) % 26];
    ret[3] = '\0';
}

int main() {
    char msg[1000], enc[1000] = "", dec[1000] = "", temp[4];
    
    printf("Enter the plaintext: ");
    fgets(msg, sizeof(msg), stdin);
    msg[strcspn(msg, "\n")] = '\0';
    
    for (int i = 0; i < strlen(msg); i++) {
        msg[i] = toupper(msg[i]);
    }

    int original_len = strlen(msg); 

    int n = original_len % 3;
    if (n != 0) {
        for (int i = 0; i < 3 - n; i++) {
            strcat(msg, "X");
        }
    }

    printf("Padded message: %s\n", msg); 

    for (int i = 0; i < strlen(msg); i += 3) {
        encode(msg[i], msg[i + 1], msg[i + 2], temp);
        strcat(enc, temp);
    }

    for (int i = 0; i < strlen(enc); i += 3) {
        decode(enc[i], enc[i + 1], enc[i + 2], temp);
        strcat(dec, temp);
    }

    dec[original_len] = '\0'; 

    printf("Encoded message: %s\n", enc);
    printf("Decoded message: %s\n", dec);
    
    return 0;
}

```
## OUTPUT:
![image](https://github.com/user-attachments/assets/eb57c27c-30d1-437b-b5a5-0f68ab431a07)

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
#include <ctype.h>

void vigenere_encrypt(const char *plaintext, const char *key, char *encrypted) {
    int pt_len = strlen(plaintext);
    int key_len = strlen(key);
    int i, j;

    for (i = 0, j = 0; i < pt_len; i++) {
        if (isalpha(plaintext[i])) {
            char pt_char = toupper(plaintext[i]);
            char key_char = toupper(key[j % key_len]);
            encrypted[i] = ((pt_char - 'A') + (key_char - 'A')) % 26 + 'A';
            j++;
        } else {
            encrypted[i] = plaintext[i];
        }
    }
    encrypted[pt_len] = '\0';
}

void vigenere_decrypt(const char *encrypted, const char *key, char *decrypted) {
    int enc_len = strlen(encrypted);
    int key_len = strlen(key);
    int i, j;

    for (i = 0, j = 0; i < enc_len; i++) {
        if (isalpha(encrypted[i])) {
            char enc_char = toupper(encrypted[i]);
            char key_char = toupper(key[j % key_len]);
            decrypted[i] = ((enc_char - 'A') - (key_char - 'A') + 26) % 26 + 'A';
            j++;
        } else {
            decrypted[i] = encrypted[i];
        }
    }
    decrypted[enc_len] = '\0';
}

int main() {
    char plaintext[1000], key[1000], encrypted[1000], decrypted[1000];

    printf("Enter the plaintext: ");
    fgets(plaintext, sizeof(plaintext), stdin);
    plaintext[strcspn(plaintext, "\n")] = '\0';

    printf("Enter the key: ");
    fgets(key, sizeof(key), stdin);
    key[strcspn(key, "\n")] = '\0';

    vigenere_encrypt(plaintext, key, encrypted);
    printf("Encrypted message: %s\n", encrypted);

    vigenere_decrypt(encrypted, key, decrypted);
    printf("Decoded message: %s\n", decrypted);

    return 0;
}

```
## OUTPUT:
![image](https://github.com/user-attachments/assets/53a3d8c9-de62-447b-9814-7f79d778c02e)

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
