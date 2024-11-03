# h2 Pubkey
https://terokarvinen.com/trust-to-blockchain/#h2-pubkey

x) Read and summarize (with some bullet points)

## € Schneier 2015: Applied Cryptography: Chapter 2 - Protocol Building Blocks, sections
https://learning.oreilly.com/library/view/applied-cryptography-protocols/9781119096726/10_chap02.html#chap02-sec005

2.5 Communications Using Public-Key Cryptography
- Public-key cryptography has two different keyes. One public and the other private.
- It is computationally hard to deduce the private key from the public key. Anyone with the public key can encrypt a message but not decrypt it.
- Public-Key algorithsm are not used to encrypt messages; they are used to encrypt keys.
- In most practical implementations public-key cryptography is used to secure and distribute session keys; those 	session keys are used with symmetric algorithms to secure message traffic. This is sometimes called a hybrid cryptosystem.

2.6 Digital Signatures
- There are several techniques of digital signature: Signing Documents with Symmetric Cryptosystems and an Arbitrator, Digital Signature Trees, Signing Documents with Public-Key Cryptography, Signing Documents and Timestamps,
  Signing Documents with Public-Key Cryptography and One-Way Hash Functions. 
- To maximise nonrepudiation of digital signatures is to have signed document timestamped  

2.7 Digital Signatures With Encryption
- By combining digital signatures with public-key cryptography, we develop a protocol that combines the security of encryption with the authenticity of digital signatures.
  Think of a letter from your mother: The signature provides proof of authorship and the envelope provides privacy.

2.8 Random And Pseudo-Random-Sequence Generation

Random-number generators are almost definitely not secure enough for cryptography, and probably not even very random. Most of them are embarrassingly bad.
Anything that is periodic is, by definition, predictable. And if something is predictable, it can't be random. A true random-number generator requires some random input; a computer can't provide that.
Every pseudo-random-sequence generator is going to produce  weird correlations and strange results if you use them in a certain way. And that's what a cryptanalyst will use to attack the system.
The output of a generator satisfying below three properties will be good enough for a one-time pad, key generation, and any other cryptographic applications that require a truly random sequence generator:
1. It looks random. This means that it passes all the statistical tests of randomness that we can find.
2. It is unpredictable. It must be computationally infeasible to predict what the next random bit will be, given complete knowledge of the algorithm or hardware generating the sequence and all of the previous bits in the stream.
3. It cannot be reliably reproduced. If you run the sequence generator twice with the exact same input (at least as exact as humanly possible), you will get two completely unrelated random sequences.


## € Rosenbaum 2019: Grokking Bitcoin
https://learning.oreilly.com/library/view/grokking-bitcoin/9781617294648/

Chapter 2. Cryptographic hash functions and digital signatures
https://learning.oreilly.com/library/view/grokking-bitcoin/9781617294648/OEBPS/Text/kindle_split_011.html
Digital signatures (8 sections, from "Typical use of digital signatures" to "Private key security")

A digital signature is a digital equivalent of a handwritten signature. The difference is that a handwritten signature is tied to a person, whereas a digital signature is tied to a random number called a private key. 
A key pair is created once. The same private key can be used several times to digitally sign stuff.
There are 3 steps: Prepartion by genrating a key pair, private and public. Signing with private key. Verifying the signature by using public key.
Private key security is very important. The owner of key has to make decisions against attackers choosing more secure and more inconvenient way or less secure and more convenient way: online-offline, cleartext-encrypted, whole key-split key.

## Karvinen 2023: PGP - Send Encrypted and Signed Message - gpg
https://terokarvinen.com/2023/pgp-encrypt-sign-verify/

Homework explained below on b) Messaging.

## a) Pubkey today. 
Explain how you have used public key cryptography today or yesterday, outside of this homework. 
In addition to naming the system, identify how different parties use keys in different steps of the system. (Answering this question likely requries finding sources on your own. This subtask does not require tests with a computer.)
I have used public key cryptography accessing bank services via web browser.
How keys are used:
- Earlier bank has ordered/crated SSL certificate to it's web page. 
- My laptop sends connection request to this bank web page.
- Because the web page is trustfull my laptop will send one-time key, which is crypted by puplic key of server of bank.
- Server of bank will decrypt the message by its private key and will have the one-time key of mine.
- The traffic between the workstation and the server during one session is handled using a one-time key.

## b) Messaging. 
Send an encrypted and signed message using PGP, then verify and decrypt it. (You can use folders to simulate users, or use two computers or two different OS users. Don't use Tero as a name of any party, unless that's your given name.)

https://terokarvinen.com/2023/pgp-encrypt-sign-verify/

I followed instructions:

I was able to generate Kati's Keypair (and installed required tools).

I was able to expor my pub key. 

I simulated Alice according instructions.
As Alice I was able to imp and verify Tero's key and see the trust.
But I had issues with "Tero needs Alices Public Key to Know IT's Her": I wasn't able to import alice.pub. Error: gpg: no valid OpenPGP data found. 
Tried to resolve the issue but didn't find resolution (killall also runned). 

Even I had unresolved issue I decided to test "Alice Sends a Secret Message"
I was able to create a message but encrypting and signing gives error: gpg: Note: '--sign' is not considered an option
Unfortunately I am not familiar with Linux. Thus I decided to stop thist task.


## c) Other tool. 
Encrypt a message using a tool other than PGP. Explain how different parties use different keys at different stages of operation. Evaluate the security of the tool you've chosen.

I used Whatsapp to encrypt a message.
When installing Whatsapp to my mobilephone Whatsapp creates public and private keys. Public key is shared with other users.
When I start a conversation Whatsapp changes public keays.
When I send a message Whatsapp encrypts message using public key of the receiver of the message.
Servers of Whatsapp act as brokers. They receive encypted message and deliver it to receiver.
Messages will be decrypted by privacy key of mobilephone of message receiver. WhatsApp uses end to end encryption so it is safe but WhatsApp account can be hijacked.
https://medium.com/@anoopnayak1/asymmetric-encryption-whatsapp-mechanism-79d1821e765c

## d) Eve and Mallory. 
In many crypto stories, Eve is a passive eavesdropper, listening on the wire. Mallory malliciously modifies the messages. 
Explain how PGP protects against Mallory and Eve. Be specific what features, which use of keys and which flags in the command are related to this protection. (This subtasks does not require tests with a computer)

Protection against Eve is encrypting message by public key of message receiver. Flag in the command is encrypt.
Protection against Mallory is digital signature and hash function . Sender of the massage sign message by private key of sender. 
Receiver can check it by public key of sender. Flag in the command is sign. 
Receiver can also check the integrity of the message using hash functions. Flag in the command is verify.

## f) Password management. 
Demonstrate use of a password manager. What kind of attacks take advantage of people not using password managers? (You can use any password manager, some examples include pass and KeePassXC.)
https://keepassxc.org/

Keepass downloaded and installed, database created and password set. Tested password generator.

If you don't use password manager most probably your passwords
- are not enough complicated 
- are saved somewhere where those are easy to steal 
- are similar or same kind of passwords to many places.
  
If password is not enough complicated it can be quessed.
If password is saved insecure way it can be stolen.
If same password is used for several places and it is leaked it can be used to other systems also.

## g) Refer to sources. 
Verify each homework report (this and the earlier ones) refers to sources. Every homework report should refer to this task page. 
It should also have references to any other source used, such as web pages, LLMs, man pages, other reports... References are mandatory, and must be present in every report. 
(This subtask does not need a report, you can just do it and write "Done." as the answer for this subtask.)

Done.



