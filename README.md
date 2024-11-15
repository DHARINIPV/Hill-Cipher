# Hill Cipher
Hill Cipher using with different key values

## AIM:
To develop a simple C program to implement Hill Cipher.

## DESIGN STEPS:
Step 1:
Design of Hill Cipher algorithnm

Step 2:
Implementation using C or pyhton code

Step 3:
Testing algorithm with different key values. ALGORITHM DESCRIPTION: The Hill cipher is a substitution cipher invented by Lester S. Hill in 1929. Each letter is represented by a number modulo 26. To encrypt a message, each block of n letters is multiplied by an invertible n × n matrix, again modulus 26. To decrypt the message, each block is multiplied by the inverse of the matrix used for encryption. The matrix used for encryption is the cipher key, and it should be chosen randomly from the set of invertible n × n matrices (modulo 26). The cipher can, be adapted to an alphabet with any number of letters. All arithmetic just needs to be done modulo the number of letters instead of modulo 26.

## PROGRAM:
```c
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int keymat[3][3] = {
    { 1, 2, 1 },
    { 2, 3, 2 },
    { 2, 2, 1 }
};

int invkeymat[3][3] = {
    { -1, 0, 1 },
    { 2, -1, 0 },
    { -2, 2, -1 }
};

char key[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

// Function to encode a triplet of characters
void encode(char a, char b, char c, char *ret) {
    int x, y, z;
    int posa = (int)a - 65;
    int posb = (int)b - 65;
    int posc = (int)c - 65;

    x = (posa * keymat[0][0] + posb * keymat[1][0] + posc * keymat[2][0]) % 26;
    y = (posa * keymat[0][1] + posb * keymat[1][1] + posc * keymat[2][1]) % 26;
    z = (posa * keymat[0][2] + posb * keymat[1][2] + posc * keymat[2][2]) % 26;

    if (x < 0) x += 26;
    if (y < 0) y += 26;
    if (z < 0) z += 26;

    ret[0] = key[x];
    ret[1] = key[y];
    ret[2] = key[z];
    ret[3] = '\0';
}

// Function to decode a triplet of characters
void decode(char a, char b, char c, char *ret) {
    int x, y, z;
    int posa = (int)a - 65;
    int posb = (int)b - 65;
    int posc = (int)c - 65;

    x = (posa * invkeymat[0][0] + posb * invkeymat[1][0] + posc * invkeymat[2][0]) % 26;
    y = (posa * invkeymat[0][1] + posb * invkeymat[1][1] + posc * invkeymat[2][1]) % 26;
    z = (posa * invkeymat[0][2] + posb * invkeymat[1][2] + posc * invkeymat[2][2]) % 26;

    if (x < 0) x += 26;
    if (y < 0) y += 26;
    if (z < 0) z += 26;

    ret[0] = key[x];
    ret[1] = key[y];
    ret[2] = key[z];
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

    // Convert message to uppercase
    for (int i = 0; i < strlen(msg); i++) {
        msg[i] = toupper(msg[i]);
    }

    // Calculate padding needed
    n = strlen(msg) % 3;
    if (n != 0) {
        for (int i = 1; i <= (3 - n); i++) {
            strcat(msg, "X"); // Pad with 'X' to make length a multiple of 3
        }
    }
    printf("Padded message : %s\n", msg);

    // Encrypt the message
    char triplet[4];
    for (int i = 0; i < strlen(msg); i += 3) {
        encode(msg[i], msg[i + 1], msg[i + 2], triplet);
        strcat(enc, triplet);
    }
    printf("Encrypted message : %s\n", enc);

    // Decrypt the message
    for (int i = 0; i < strlen(enc); i += 3) {
        decode(enc[i], enc[i + 1], enc[i + 2], triplet);
        strcat(dec, triplet);
    }
    printf("Decoded message : %s\n", dec);

    return 0;
}
```

## OUTPUT:
![image](https://github.com/user-attachments/assets/272598d4-a3a7-430b-b8cb-9aca3644f011)


## RESULT:
The program is executed successfully
