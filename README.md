## EX. NO:2 IMPLEMENTATION OF PLAYFAIR CIPHER

## DATE: 20-03-2025 

## AIM:
 

 

To write a python program to implement the Playfair Substitution technique.

## DESCRIPTION:

The Playfair cipher starts with creating a key table. The key table is a 5×5 grid of letters that will act as the key for encrypting your plaintext. Each of the 25 letters must be unique and one letter of the alphabet is omitted from the table (as there are 25 spots and 26 letters in the alphabet).

To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. The two letters of the diagram are considered as the opposite corners of a rectangle in the key table. Note the relative position of the corners of this rectangle. Then apply the following 4 rules, in order, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of corners of the rectangle defined by the original pair.
## EXAMPLE:
![image](https://github.com/Hemamanigandan/EX-NO-2-/assets/149653568/e6858d4f-b122-42ba-acdb-db18ec2e9675)

 

## ALGORITHM:

STEP-1: Read the plain text from the user.
STEP-2: Read the keyword from the user.
STEP-3: Arrange the keyword without duplicates in a 5*5 matrix in the row order and fill the remaining cells with missed out letters in alphabetical order. Note that ‘i’ and ‘j’ takes the same cell.
STEP-4: Group the plain text in pairs and match the corresponding corner letters by forming a rectangular grid.
STEP-5: Display the obtained cipher text.




## Program:
```c
def generate_key_square(key):
    key = key.replace(' ', '').upper().replace('J', 'I')
    key_square = []
    used_chars = set()

    for char in key:
        if char not in used_chars and char.isalpha():
            key_square.append(char)
            used_chars.add(char)

    for char in 'ABCDEFGHIKLMNOPQRSTUVWXYZ':
        if char not in used_chars:
            key_square.append(char)

    matrix = [key_square[i:i + 5] for i in range(0, 25, 5)]
    print("Key Square:")
    for row in matrix:
        print(' '.join(row))
    return matrix

def find_position(matrix, char):
    for i in range(5):
        for j in range(5):
            if matrix[i][j] == char:
                return i, j

def playfair_encrypt_pair(ch1, ch2, key_square):
    row1, col1 = find_position(key_square, ch1)
    row2, col2 = find_position(key_square, ch2)

    if row1 == row2:
        return key_square[row1][(col1 + 1) % 5] + key_square[row2][(col2 + 1) % 5]
    elif col1 == col2:
        return key_square[(row1 + 1) % 5][col1] + key_square[(row2 + 1) % 5][col2]
    else:
        return key_square[row1][col2] + key_square[row2][col1]

def playfair_decrypt_pair(ch1, ch2, key_square):
    row1, col1 = find_position(key_square, ch1)
    row2, col2 = find_position(key_square, ch2)

    if row1 == row2:
        return key_square[row1][(col1 - 1) % 5] + key_square[row2][(col2 - 1) % 5]
    elif col1 == col2:
        return key_square[(row1 - 1) % 5][col1] + key_square[(row2 - 1) % 5][col2]
    else:
        return key_square[row1][col2] + key_square[row2][col1]

def playfair_encrypt(text, key):
    key_square = generate_key_square(key)
    text = text.replace(' ', '').upper().replace('J', 'I')
    formatted_text = ''
    i = 0

    while i < len(text):
        ch1 = text[i]
        ch2 = text[i + 1] if i + 1 < len(text) else 'X'

        if ch1 == ch2:
            formatted_text += ch1 + 'X'
            i += 1
        else:
            formatted_text += ch1 + ch2
            i += 2

    if len(formatted_text) % 2 != 0:
        formatted_text += 'X'

    cipher_text = ''
    for i in range(0, len(formatted_text), 2):
        cipher_text += playfair_encrypt_pair(formatted_text[i], formatted_text[i + 1], key_square)

    return cipher_text

def playfair_decrypt(text, key):
    key_square = generate_key_square(key)
    decrypted_text = ''

    for i in range(0, len(text), 2):
        decrypted_text += playfair_decrypt_pair(text[i], text[i + 1], key_square)

    return decrypted_text.replace('X', '')

def main():
    key = input("Enter key: ")
    text = input("Enter the plain text: ")

    encrypted_text = playfair_encrypt(text, key)
    print(f"\nEntered text: {text}\nCipher Text: {encrypted_text}")

    decrypted_text = playfair_decrypt(encrypted_text, key)
    print(f"Decrypted Text: {decrypted_text}")

if __name__ == "__main__":
    main()


```





## Output:
![image](https://github.com/user-attachments/assets/fcb2defa-11e9-426c-bf06-ac5538c73bd7)


## Result:
Thus, the Playfair Cipher Substitution algorithm is implemented using python programming and executed successfully.
