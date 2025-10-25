# Setting up `pass` UNIX password manager

*Thursday, October 23rd, 2025* by **devP**

***More about `pass`: https://www.passwordstore.org/***

**Install `pass`**

`sudo apt install pass`

You need to set up GPG keys first before using `pass`. Here's how to create a password in `pass`:

**Check if you have GPG keys**

`gpg --list-keys`

If you see no keys, you need to create one first.

**Create a GPG key (if you don't have one)**

`gpg --full-generate-key`

Follow the prompts:
- Key type: 1 (RSA and RSA)
- Key size: 4096
- Expiration: 0 (never expires, or choose your preference)
- Enter your name and email
- Set a passphrase (you'll use this to unlock your password store)

**Initialize pass with your GPG key**

`gpg --list-keys`

Copy your GPG key ID (the long string after pub), then:

`pass init "your-email@example.com"`

Or use the key ID directly:

`pass init YOUR_GPG_KEY_ID`

**Now insert your Ansible Vault password**

`pass insert "Ansible Vault Password"`

Enter your password when prompted.

**(Optional) Retrieve the password**

This will display the password in your terminal

`pass show " Password"`