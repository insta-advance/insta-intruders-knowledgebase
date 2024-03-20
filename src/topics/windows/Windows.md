# Pentesting a Windows host

## Physical access

If you have physical access to a Windows machine with no BIOS password set or Bitlocker the NTFS filesystem can be accessed by livebooting Kali Linux into the machine.

A bootkit like [GrabAccess](https://github.com/Push3AX/GrabAccess) can potentially bypass Bitlocker if it is enabled, but no password is set, and boot with SYSTEM privileges (Windows superuser privileges). This will allow disabling Microsoft Defender and running any commands or tools as SYSTEM. A potential workflow is to use the bootkit to add a new Administrator account and then boot back into Windows normally and log with the newly created account.

## Stealing credentials

NTLM (New Technology LAN Manager) hashes are used in Windows authentication. Obtaining a NTLM has for a user potentially allows the cracking of the password for that user or impersonating that user using pass-the-hash attacks.

### Extracting credentials

Note that antiviruses such as Microsoft Defender will try to block different credential extraction methods.

A traditional method for extracting credentials is to use the [mimikatz](https://github.com/gentilkiwi/mimikatz) tool:

```
mimikatz "privilege::debug" "token::elevate" "sekurlsa::logonpasswords" "lsadump::lsa /inject" "lsadump::sam" "lsadump::cache" "sekurlsa::ekeys" "exit"
```

An alternative method is (as Administrator):

```
reg save HKLM\sam sam
reg save HKLM\system system
reg save HKLM\security security
```

Transferring the files created by the above commands to a Kali machine allows extracting the hashes using either `samdump2 system sam`
or `impacket-secretsdump -sam sam -security security -system system LOCAL`.

More information and tools for credential extraction is documented at [HackTricks](https://book.hacktricks.xyz/windows-hardening/stealing-credentials).

### Hash cracking

An obtained NTLM hash may be attempted to be cracked using John The Ripper and a wordlist in Kali:

```
echo "Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::" > hash.txt
john --FORMAT=NT --wordlist=<wordlist> hash.txt
```

Kali Linux has some built-in wordlists at `/usr/share/wordlists`.

Additional wordlists can be obtained from [https://weakpass.com/wordlist/](https://weakpass.com/wordlist/)

### Pass-the-hash

An obtained hash may be potentially used by pass-the-hash to authenticate to a remote system via SMB, MSRPC or RDP. A tool for this is for example [`impacket`](https://www.kali.org/tools/impacket-scripts/) in Kali. 




