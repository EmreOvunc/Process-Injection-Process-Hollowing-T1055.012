# Process-Injection-Process-Hollowing-T1055.012

Execution of the malicious code is masked under a legitimate process.

**Note**: I had to change 'original' source code to compile and execute, you can find both of them in this repository.

### Change Process:
Line #28 -> hollowed out:
```
CreateProcessA(NULL, (LPSTR)"c:\\windows\\syswow64\\notepad.exe", NULL, NULL, TRUE, CREATE_SUSPENDED, NULL, NULL, si, pi);
```

![notepad.exe](https://emreovunc.com/images/ProcessHollowing_01.png)

Line #41 -> executed inside the hollowed process:
```
HANDLE sourceFile = CreateFileA("C:\\windows\\syswow64\\calc.exe", GENERIC_READ, NULL, NULL, OPEN_ALWAYS, NULL, NULL);
```

![calc.exe](https://emreovunc.com/images/ProcessHollowing_02.png)

### Usage
```
cmd.exe /c %TMP%\ProcessHollowing.exe && timeout 5 && tasklist /svc | findstr /i calculator"
```

### Sources

https://attack.mitre.org/techniques/T1055/012/

https://ired.team/offensive-security/code-injection-process-injection/process-hollowing-and-pe-image-relocations
