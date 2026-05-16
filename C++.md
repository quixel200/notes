
## Buffers

- cin - ignore leading whitespace, leave trailing \n 
- cout 
- cin.getline() - reads till \n but does not include \n
- cin.ignore(int n,char stop_char) - discard n characters or stop when stop_char is reached  

Stream classes are used to perform io and file operations 

ofstream - writing on files
ifstream - reading from files
fstream - both reading and writing 


```C++
ifstream myFile;
myFile.open(inFileName)
myFile >> cout;
```

```C++
ofstream myFile
myFile.open(inFileName)
myFile << cout << endl;
```


![[Pasted image 20260516170021.png]]