# ue4study
UnrealEngine 4 study

## Pak file encrypt and signed

Pak file is UnrealEngine game resources package file.<br/>

In newer UE4 version, encryption only for ini files in game package file.<br/>

You need set encrypt ini files = true and compress package file.<br/>

### 4.15 AES Key and Signed Key set

In UE4 4.15, AES Key can config in game project ini file.<br/>

Dont need UE4 source code and modify AES.h. It is very good for binary version.<br/>

Source code location:<br/>

Engine/Source/Programs/UnrealPak/Private/UnrealPak.cpp<br/>

Configuration:<br/>
1. In your game project folder "Config" folder, create Encryption.ini file for current games.
1. Or in your UE4 Engine \'s folder "Config", create Encryption.ini file for all games.
1. INI file need include "Core.Encryption" section.
1. In Core.Encryption section add config item: SignPak=true for sign pak file.
1. In Core.Encryption section add config item: EncryptPak=true for encrypt ini file in pak file.
1. In Core.Encryption section add config item: rsa.publicexp=0xNNNNNNNN for RSA Public Exp
1. In Core.Encryption section add config item: rsa.privateexp=0xNNNNNNNN for RSA private Exp
1. In Core.Encryption section add config item: rsa.modulus=0xNNNNNNNN for RSA modulus
1. In Core.Encryption section add config item: aes.key="32characters" for AES key must more than 32 characters
<br/>
INI file example:<br/>

````
[Core.Encryption]
SignPak=true
EncryptPak=true
; RSA Signed Key's
rsa.publicexp=0x10001
rsa.privateexp=0x163c4b9641234567890c897ee0a577d6b07240909bdfd768c72d8ea8cc025bb1
rsa.modulus=0xb22e3a1512345678906e4fe505c13163c2d57968e4cbe124e5b8b843e91a8c55
; AES Key must more than 32 characters
aes.key="12345678876543211234567887654321"
````
