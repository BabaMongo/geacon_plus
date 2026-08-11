geacon_plus Golang implementation of CobaltStrike stageless HTTP(S)/DNS beacon, supports Windows/Linux/macOS.
Thanks to brother @H4de5 for Windows code support. Secondary development ideas: CobaltStrike beacon secondary development guide DNS beacon implementation details: CS DNS beacon secondary development guide
Disclaimer Please fully read and agree to the following before using this project. This project is only for learning the CobaltStrike protocol and testing related technical methods. Do not use it for any illegal purposes. Strictly prohibited from using this project to attack computer information systems. Consequences are borne by the user.
Sister project geacon_pro has high attack potential and risk of abuse, so it has been made private and is no longer public. This project has not synced the later anti-detection features from the pro version and is only for learning CS beacon design.
Features
	•	Cross-platform: can execute simple commands on Linux and macOS (macOS untested, theoretical)
	•	Tested on local Windows 7/10, WinServer 2012 and Ubuntu 22.04
	•	Experimental DNS beacon, tested on CS 4.0 and 4.3
Most prefer higher versions, so 4.1+ compatibility was added. Set Support41Plus in config/config.go to choose 4.0 or 4.1+.
Usage Based on darkr4y/geacon. See original project for details. Partial c2profile support for encoding and padding. Project uses classic jquery.profile. Compile with -ldflags "-H windowsgui -s -w" to reduce size and hide console. go-strip can also remove symbols (may not work on newer Go).
c2profile Partial support: encoding and prepend/append for server/client data. Supported encodings: base64, base64url, netbios, netbiosu, mask. DNS supports custom domain prefix.
File management mv, cp, mkdir, rm, upload, download, fileBrowse Returns data in standard format, supports CS GUI interaction.
Process management listProcess and kill, supports GUI interaction.
Command execution shell, run, execute. Uses local shell. Windows uses CreateProcess.
Process injection Windows only. Reflective DLL injection (simple inject + spawn+inject). Supports screenshot, portscan, netview and other CS RDI tasks. Remote thread injection can be detected, so option to patch ExitProcess to ExitThread and inject into self instead of spawn+inject (configurable).
Token related Tried runas, make token, steal token. steal token works. runas has mysterious error. make token is weird: LOGON32_LOGON_BATCH always password error; LOGON32_LOGON_NEW_CREDENTIALS accepts anything but returned token unusable (maybe only for network?).
Post-exploitation Supports in-memory PowerShell module loading, reflective DLL injection or Go in-memory C# execution.
DNS beacon Edit dns config in config/config.go: domain and nameserver IP/port (non-53 allowed). Configure matching DNS listener. Domain must be .example.com. (leading and trailing dots required). Domain prefix config added in c2profile.go (default; change for custom profiles).
TODO Moved to issues.
References mai1zhi2/SharpBeacon darkr4y/geacon WBGlIl/ReBeacon_Src
