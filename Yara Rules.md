
## Sample 1

```
rule sample1
{
	strings:
		$codesection = "code"
		$file = "CreateFile"
		$password = "PASSWORD"
		$hidden = "HIDDEN"	
	condition:
		$codesection and $file and $password and $hidden 
}
```

## Sample 2

```
rule sample2
{
	strings:
		$dll1 = "MPR.dll"
		$dll2 = "WINMM.dll"
		$get_connection = "WNetGetConnection"
		$khatra = "TRAv3$"
	condition:
		$dll1 and $dll2 and $get_connection and $khatra
}
```

## Sample 3

```
rule sample3
{
	strings:
		$keylogger = "keylogger"
		$cmd_path = "C:\\WINDOWS\\cmd.html"
		$keystate = "GetKeyState"
	condition:
		$keylogger and $cmd_path and $keystate
}
```

## Sample 4

```
rule sample4
{
	strings:
		$call = "CallWindowProc"
		$vb_path = "C:\\Program Files\\Microsoft Visual Studio\\VB98\\VB6.OLB"
		$regex_cmd = /Command[0-9]{1,4}/ ascii wide
	condition:
		$call and $vb_path and $regex_cmd
}
```

## Sample 5

```
rule sample5
{
	strings:
		$code_section = ".code"
		$cmd = "GetCommandLine"
		$thread = "ResumeThread" base64 wide ascii 
		$write_memory = "WriteProcessMemory" base64 wide ascii
	condition:
		$code_section and $cmd and $thread and $write_memory
	
}
```