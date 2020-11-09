# hashing_digital_signature
Commands for Hashing and generating Digital Signatures

# Generating hash:
md5sum Plaintext.txt

# Compiling hashing code
gcc hash_func.c -lcrypto

openssl enc -aes-128-cbc -in Plaintext.txt -K ABCDEF12345 -iv ABCDEF > Cipher.txt

openssl enc -d -aes-128-cbc -in Cipher.txt -K ABCDEF12345 -iv ABCDEF 

# Generate a detached signature:
openssl smime -binary -sign -in Plaintext.txt -signer PK.crt -inkey PK.key -outform pem -out file.p7b

# Dump signature contents:
openssl asn1parse -in file.p7b  -dump -i

====

# Generating digital-signature:

sha1sum Plaintext.txt | cut -d ' ' -f 1 > hash
openssl enc -aes-128-cbc -in hash -K ABCDEF12345 -iv ABCDEF > Signature.bin


# Verifying digital-signature:

sha1sum Plaintext.txt | cut -d ' ' -f 1 > hash_1
openssl enc -d -aes-128-cbc -in Signature.bin -K ABCDEF12345 -iv ABCDEF > hash_2

cat hash_1
cat hash_2

====


