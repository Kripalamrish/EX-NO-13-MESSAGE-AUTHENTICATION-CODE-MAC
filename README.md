# EX-NO-13-MESSAGE-AUTHENTICATION-CODE-MAC

## AIM:
To implement MESSAGE AUTHENTICATION CODE(MAC)

## ALGORITHM:

1. Message Authentication Code (MAC) is a cryptographic technique used to verify the integrity and authenticity of a message by using a secret key.

2. Initialization:
   - Choose a cryptographic hash function \( H \) (e.g., SHA-256) and a secret key \( K \).
   - The message \( M \) to be authenticated is input along with the secret key \( K \).

3. MAC Generation:
   - Compute the MAC by applying the hash function to the combination of the message \( M \) and the secret key \( K \): 
     \[
     \text{MAC}(M, K) = H(K || M)
     \]
     where \( || \) denotes concatenation of \( K \) and \( M \).

4. Verification:
   - The recipient, who knows the secret key \( K \), computes the MAC using the received message \( M \) and the same hash function.
   - The recipient compares the computed MAC with the received MAC. If they match, the message is authentic and unchanged.

5. Security: The security of the MAC relies on the secret key \( K \) and the strength of the hash function \( H \), ensuring that an attacker cannot forge a valid MAC without knowledge of the key.

## Program:
```
#include <stdio.h>
#include <string.h>

/* Simple hash function */
int generateHash(char str[])
{
    int i;
    int hash = 0;

    for(i = 0; str[i] != '\0'; i++)
    {
        hash = hash + str[i];
    }

    return hash;
}

int main()
{
    char message[100];
    char secretKey[100];
    char combined[200];

    int macSender;
    int macReceiver;

    printf("Enter Message: ");
    fgets(message, sizeof(message), stdin);

    printf("Enter Secret Key: ");
    fgets(secretKey, sizeof(secretKey), stdin);

    /* Remove newline characters */
    message[strcspn(message, "\n")] = '\0';
    secretKey[strcspn(secretKey, "\n")] = '\0';

    /* Combine Key and Message */
    strcpy(combined, secretKey);
    strcat(combined, message);

    /* MAC Generation */
    macSender = generateHash(combined);

    printf("\nGenerated MAC: %d\n", macSender);

    /* Receiver Side Verification */
    macReceiver = generateHash(combined);

    printf("Receiver Computed MAC: %d\n", macReceiver);

    if(macSender == macReceiver)
    {
        printf("\nMessage is Authentic and Unchanged.\n");
    }
    else
    {
        printf("\nMessage Authentication Failed.\n");
    }

    return 0;
}
```


## Output:

<img width="1684" height="1000" alt="image" src="https://github.com/user-attachments/assets/2091c6ef-2efa-4475-9c0b-8269e6a42a21" />

## Result:
The program is executed successfully.
