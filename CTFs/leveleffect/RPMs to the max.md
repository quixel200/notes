IP : HidRFCELORo7NzxFKwcOVQ==

key: Stemmatous

Decrypt function: 
```
public static string Read(string b64, string stringKey)    {        
string text;        
try{            
if (string.IsNullOrWhiteSpace(b64))            
{                
text = string.Empty; 
}            
else{                
text = StringDecrypt.FromBase64(StringDecrypt.Xor(StringDecrypt.FromBase64(b64), stringKey)); 
}        
}        
catch        
{            
text = b64;        
}        
return text;    
}
```

XOR:

```
public static string Xor(string input, string stringKey{        
StringBuilder stringBuilder = new StringBuilder();        
for (int i = 0; i < input.Length; i++)
{            
int num = (int)(input[i] ^ stringKey[i % stringKey.Length]);            
stringBuilder.AppendFormat({0}", char.ConvertFromUtf32(num));        
}        
return stringBuilder.ToString();    
}
```

![[Pasted image 20240707103236.png]]