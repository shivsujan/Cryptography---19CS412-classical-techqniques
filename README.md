# Cryptography---19CS412-classical-techqniques
# Caeser Cipher
Caeser Cipher using with different key values

# AIM:

To encrypt and decrypt the given message by using Ceaser Cipher encryption algorithm.


## DESIGN STEPS:

### Step 1:

Design of Caeser Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

1.	In Ceaser Cipher each letter in the plaintext is replaced by a letter some fixed number of positions down the alphabet.
2.	For example, with a left shift of 3, D would be replaced by A, E would become B, and so on.
3.	The encryption can also be represented using modular arithmetic by first transforming the letters into numbers, according to the   
    scheme, A = 0, B = 1, Z = 25.
4.	Encryption of a letter x by a shift n can be described mathematically as,
                       En(x) = (x + n) mod26
5.	Decryption is performed similarly,
                       Dn (x)=(x - n) mod26


## PROGRAM:
CaearCipher.
```
 #include<stdio.h>
 #include <string.h>
 #include<conio.h>
 #include <ctype.h>
 int main()
 {
 char plain[10], cipher[10];
 int key,i,length;
 int result;
 printf("\n Enter the plain text:");
 scanf("%s", plain);
 printf("\n Enter the key value:");
 scanf("%d", &key);
 printf("\n \n PLAIN TEXt: %s",plain);
 printf("\n \n ENCRYPTED TEXT: ");
 for(i = 0, length = strlen(plain); i < length; i++)
 {
    cipher[i]=plain[i] + key;
    if (isupper(plain[i]) && (cipher[i] > 'Z'))
    cipher[i] = cipher[i] - 26;
    if (islower(plain[i]) && (cipher[i] > 'z'))
    cipher[i] = cipher[i] - 26;
    printf("%c", cipher[i]);
 }
 printf("\n \n AFTER DECRYPTION : ");
 for(i=0;i<length;i++)
 {
    plain[i]=cipher[i]-key;
    if(isupper(cipher[i])&&(plain[i]<'A'))
    plain[i]=plain[i]+26;
    if(islower(cipher[i])&&(plain[i]<'a'))
    plain[i]=plain[i]+26;
    printf("%c",plain[i]);
 }
OUTPUT:
 The program is executed successfully
 return 0;
 }
```
## OUTPUT:
OUTPUT:
Simulating Caesar Cipher

![Screenshot 2024-09-02 123258](https://github.com/user-attachments/assets/ff023845-7261-48c5-8b1b-e368702a2e9b)

## RESULT:
The program is executed successfully

---------------------------------

# PlayFair Cipher
Playfair Cipher using with different key values

# AIM:

To implement a program to encrypt a plain text and decrypt a cipher text using play fair Cipher substitution technique.

 
## DESIGN STEPS:

### Step 1:

Design of PlayFair Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

ALGORITHM DESCRIPTION:
The Playfair cipher uses a 5 by 5 table containing a key word or phrase. To generate the key table, first fill the spaces in the table with the letters of the keyword, then fill the remaining spaces with the rest of the letters of the alphabet in order (usually omitting "Q" to reduce the alphabet to fit; other versions put both "I" and "J" in the same space). The key can be written in the top rows of the table, from left to right, or in some other pattern, such as a spiral beginning in the upper-left-hand corner and ending in the centre.
The keyword together with the conventions for filling in the 5 by 5 table constitutes the cipher key. To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. Then apply the following 4 rules, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter. Encrypt the new pair and continue. Some   
   variants of Playfair use "Q" instead of "X", but any letter, itself uncommon as a repeated pair, will do.
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively (wrapping 
   around to the left side of the row if a letter in the original pair was on the right side of the row).
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively (wrapping around 
   to the top side of the column if a letter in the original pair was on the bottom side of the column).
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of 
   corners of the rectangle defined by the original pair. The order is important – the first letter of the encrypted pair is the one that 
    lies on the same row as the first letter of the plaintext pair.
To decrypt, use the INVERSE (opposite) of the last 3 rules, and the 1st as-is (dropping any extra "X"s, or "Q"s that do not make sense in the final message when finished).


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
    
    x = posa * invkeymat[0][0] + posb * invkeymat[1][0] + posc * 
invkeymat[2][0];
    y = posa * invkeymat[0][1] + posb * invkeymat[1][1] + posc * 
invkeymat[2][1];
    z = posa * invkeymat[0][2] + posb * invkeymat[1][2] + posc * 
invkeymat[2][2];
    
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
    
    strcpy(msg, "sujan");
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
Output:

![Screenshot 2024-09-02 124311](https://github.com/user-attachments/assets/b21f083c-531d-472d-b80c-6d42fa4724b5)

![Screenshot 2024-09-02 124612](https://github.com/user-attachments/assets/d15e65a7-7319-4b8a-97fe-d5401201a958)

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
ALGORITHM DESCRIPTION:
The Hill cipher is a substitution cipher invented by Lester S. Hill in 1929. Each letter is represented by a number modulo 26. To encrypt a message, each block of n letters is multiplied by an invertible n × n matrix, again modulus 26.
To decrypt the message, each block is multiplied by the inverse of the matrix used for encryption. The matrix used for encryption is the cipher key, and it should be chosen randomly from the set of invertible n × n matrices (modulo 26).
The cipher can, be adapted to an alphabet with any number of letters. All arithmetic just needs to be done modulo the number of letters instead of modulo 26.


## PROGRAM:
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int keymat[3][3] = { { 1, 2, 1 }, { 2, 3, 2 }, { 2, 2, 1 } };
int invkeymat[3][3] = { { -1, 0, 1 }, { 2, -1, 0 }, { -2, 2, -1 } };
char key[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

// Function to encode a triplet of characters
void encode(char a, char b, char c, char ret[]) {
    int x, y, z;
    int posa = (int)a - 65;
    int posb = (int)b - 65;
    int posc = (int)c - 65;

    x = posa * keymat[0][0] + posb * keymat[1][0] + posc * keymat[2][0];
    y = posa * keymat[0][1] + posb * keymat[1][1] + posc * keymat[2][1];
    z = posa * keymat[0][2] + posb * keymat[1][2] + posc * keymat[2][2];

    ret[0] = key[x % 26];
    ret[1] = key[y % 26];
    ret[2] = key[z % 26];
    ret[3] = '\0';
}

// Function to decode a triplet of characters
void decode(char a, char b, char c, char ret[]) {
    int x, y, z;
    int posa = (int)a - 65;
    int posb = (int)b - 65;
    int posc = (int)c - 65;

    x = posa * invkeymat[0][0] + posb * invkeymat[1][0] + posc * invkeymat[2][0];
    y = posa * invkeymat[0][1] + posb * invkeymat[1][1] + posc * invkeymat[2][1];
    z = posa * invkeymat[0][2] + posb * invkeymat[1][2] + posc * invkeymat[2][2];

    ret[0] = key[(x % 26 < 0) ? (26 + x % 26) : (x % 26)];
    ret[1] = key[(y % 26 < 0) ? (26 + y % 26) : (y % 26)];
    ret[2] = key[(z % 26 < 0) ? (26 + z % 26) : (z % 26)];
    ret[3] = '\0';
}

int main() {
    char msg[1000];
    char enc[1000] = "";
    char dec[1000] = "";
    int n;

    strcpy(msg, "SUJAN");
    printf("Input message : %s\n", msg);

    // Convert the input message to uppercase
    for (int i = 0; i < strlen(msg); i++) {
        msg[i] = toupper(msg[i]);
    }

    // Remove spaces
    n = strlen(msg) % 3;

    // Append padding text 'X' if necessary
    if (n != 0) {
        for (int i = 1; i <= (3 - n); i++) {
            strcat(msg, "X");
        }
    }

    printf("Padded message : %s\n", msg);

    // Encode the message
    for (int i = 0; i < strlen(msg); i += 3) {
        char a = msg[i];
        char b = msg[i + 1];
        char c = msg[i + 2];
        char encoded[4];
        encode(a, b, c, encoded);
        strcat(enc, encoded);
    }

    printf("Encoded message : %s\n", enc);

    // Decode the message
    for (int i = 0; i < strlen(enc); i += 3) {
        char a = enc[i];
        char b = enc[i + 1];
        char c = enc[i + 2];
        char decoded[4];
        decode(a, b, c, decoded);
        strcat(dec, decoded);
    }

    printf("Decoded message : %s\n", dec);
    return 0;
}
```
## OUTPUT:
OUTPUT:
Simulating Hill Cipher

![Screenshot 2024-09-02 091155](https://github.com/user-attachments/assets/b0b7106d-335a-4cc5-a478-6e1bad56cae9)

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
ALGORITHM DESCRIPTION:
The Vigenere cipher is a method of encrypting alphabetic text by using a series of different Caesar ciphers based on the letters of a keyword. It is a simple form of polyalphabetic substitution.To encrypt, a table of alphabets can be used, termed a Vigenere square, or Vigenere table. It consists of the alphabet written out 26 times in different rows, each alphabet shifted cyclically to the left compared to the previous alphabet, corresponding to the 26 possible Caesar ciphers. At different points in the encryption process, the cipher uses a different alphabet from one of the rows used. The alphabet at each point depends on a repeating keyword.



## PROGRAM:
```
#include <stdio.h>
#include <stdlib.h>  // For exit() function
#include <ctype.h>   // For toupper() function
#include <string.h>  // For strlen() function

void encipher();
void decipher();

int main() {
    int choice;
    while (1) {
        printf("\n1. Encrypt Text");
        printf("\n2. Decrypt Text");
        printf("\n3. Exit");
        printf("\n\nEnter Your Choice: ");
        scanf("%d", &choice);

        if (choice == 3)
            exit(0);
        else if (choice == 1)
            encipher();
        else if (choice == 2)
            decipher();
        else
            printf("Please Enter a Valid Option.\n");
    }
    return 0;  // Added return statement for the main function
}

void encipher() {
    unsigned int i, j;
    char input[50], key[10];

    printf("\n\nEnter Plain Text: ");
    scanf("%s", input);  // Removed newline for better input handling

    printf("Enter Key Value: ");
    scanf("%s", key);

    printf("Resultant Cipher Text: ");
    for (i = 0, j = 0; i < strlen(input); i++, j++) {
        if (j >= strlen(key)) {
            j = 0;
        }
        printf("%c", 65 + (((toupper(input[i]) - 65) + (toupper(key[j]) - 65)) % 26));
    }
    printf("\n");  // Added newline for output formatting
}

void decipher() {
    unsigned int i, j;
    char input[50], key[10];
    int value;

    printf("\n\nEnter Cipher Text: ");
    scanf("%s", input);  // Removed newline for better input handling

    printf("Enter the Key Value: ");
    scanf("%s", key);

    printf("Resultant Plain Text: ");
    for (i = 0, j = 0; i < strlen(input); i++, j++) {
        if (j >= strlen(key)) {
            j = 0;
        }

        // Calculate the decrypted character value
        value = (toupper(input[i]) - 65) - (toupper(key[j]) - 65);
        if (value < 0) {
            value += 26;  // Correct for negative values in circular shift
        }
        printf("%c", 65 + (value % 26));
    }
    printf("\n");  // Added newline for output formatting
}

```

## OUTPUT:
OUTPUT :

Simulating Vigenere Cipher

![Screenshot 2024-09-02 130735](https://github.com/user-attachments/assets/4e3a15cd-8af4-44d0-b3df-8166382ea2c9)

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
ALGORITHM DESCRIPTION:
In the rail fence cipher, the plaintext is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

## PROGRAM:
```
 #include <stdio.h>
 #include <string.h>
 void encryptRailFence(char *text, int key, char *cipherText) {
    int len = strlen(text);
    int row, col, direction;
    char rail[key][len];
    // Initializing the rail matrix with null characters
    for (row = 0; row < key; row++)
        for (col = 0; col < len; col++)
            rail[row][col] = '\n';
    // Placing characters in the rail matrix in a zig-zag manner
    row = 0;
    direction = 1; // 1 for down, -1 for up
    for (col = 0; col < len; col++) {
        rail[row][col] = text[col];
        if (row == 0)
            direction = 1;
        else if (row == key - 1)
            direction = -1;
        row += direction;
    }
    // Reading the matrix row-wise to get the cipher text
    int index = 0;
    for (row = 0; row < key; row++) {
        for (col = 0; col < len; col++) {
            if (rail[row][col] != '\n') {
                cipherText[index++] = rail[row][col];
            }
        }
    }
    cipherText[index] = '\0';
 }
 void decryptRailFence(char *cipherText, int key, char *plainText) {
    int len = strlen(cipherText);
    int row, col, direction;
    char rail[key][len];
    // Initializing the rail matrix with null characters
    for (row = 0; row < key; row++)
        for (col = 0; col < len; col++)
            rail[row][col] = '\n';
    // Marking the places in the rail matrix where the cipher text 
characters will go
    row = 0;
    direction = 1; // 1 for down, -1 for up
    for (col = 0; col < len; col++) {
        rail[row][col] = '*';
        if (row == 0)
            direction = 1;
        else if (row == key - 1)
            direction = -1;
        row += direction;
    }
    // Filling the rail matrix with the cipher text characters
    int index = 0;
    for (row = 0; row < key; row++) {
        for (col = 0; col < len; col++) {
            if (rail[row][col] == '*' && index < len) {
                rail[row][col] = cipherText[index++];
            }
        }
    }
    // Reading the matrix in a zig-zag manner to get the plain text
    row = 0;
    direction = 1; // 1 for down, -1 for up
    for (col = 0; col < len; col++) {
        plainText[col] = rail[row][col];
        if (row == 0)
            direction = 1;
        else if (row == key - 1)
            direction = -1;
        row += direction;
    }
    plainText[len] = '\0';
 }
 int main() {
    char text[100], cipherText[100], plainText[100];
    int key;
    // Input the plain text
    printf("Enter the plain text: ");
    gets(text);
    // Input the key (number of rails)
    printf("Enter the key (number of rails): ");
    scanf("%d", &key);
    // Encrypt the plain text
    encryptRailFence(text, key, cipherText);
    printf("Encrypted Text: %s\n", cipherText);
OUTPUT:
 The program is executed successfully
    // Decrypt the cipher text
    decryptRailFence(cipherText, key, plainText);
    printf("Decrypted Text: %s\n", plainText);
    return 0;
 }
```
## OUTPUT:
OUTPUT:

![Screenshot 2024-09-02 131032](https://github.com/user-attachments/assets/fec4d6eb-cc46-43ee-9dc2-b6de62d08cad)


## RESULT:
The program is executed successfully
