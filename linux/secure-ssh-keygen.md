# Secure SSH Keygen

*Monday, October 31st, 2023* by **devP**

Run the command for generating a SSH keypair of encryption type ED25519. Read more about the ED25519 [here](https://ed25519.cr.yp.to/).
`ssh-keygen -o -a 100 -t ed25519 -f ~/.ssh/file_name -C "your_description_here"`

**-o** for option
> Specify a key/value option.  These are specific to the operation that ssh-keygen has been requested to perform

**-a** for rounds
>When saving a private key, this option specifies the number
of KDF (key derivation function, currently bcrypt_pbkdf(3))
rounds used.  Higher numbers result in slower passphrase
verification and increased resistance to brute-force
password cracking (should the keys be stolen).  The default
is 16 rounds

**-t** for encryption type
>dsa | ecdsa | ecdsa-sk | ed25519 | ed25519-sk | rsa
Specifies the type of key to create

**-f** for filename
>Specifies the filename of the key file

**-C** for comment
> Provides a new comment

