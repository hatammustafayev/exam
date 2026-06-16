1)Caesar Decrypt
def solution(k: int, text: str) -> str:
    s = ""

    for c in text:
        if 'a' <= c <= 'z':
            s += chr(ord('a') + (ord(c) - ord('a') - k) % 26)
        elif 'A' <= c <= 'Z':
            s += chr(ord('A') + (ord(c) - ord('A') - k) % 26)
        else:
            s += c

    return s

















2)Caesar Encrypt
def solution(k: int, text: str) -> str:
    s = ""

    for c in text:
        if 'a' <= c <= 'z':
            s += chr(ord('a') + (ord(c) - ord('a') + k) % 26)
        elif 'A' <= c <= 'Z':
            s += chr(ord('A') + (ord(c) - ord('A') + k) % 26)
        else:
            s += c

    return s

 3)Caesar Brute Force with Crib
 def solution(ct: str, crib: str) -> str:
    for k in range(26):
        s = ""
        for c in ct:
            if 'a' <= c <= 'z':
                s += chr((ord(c)-97-k)%26+97)
            elif 'A' <= c <= 'Z':
                s += chr((ord(c)-65-k)%26+65)
            else:
                s += c

        if crib.lower() in s.lower():
            return s

    return ""


4)Recover Caesar Shift
def solution(pt: str, ct: str) -> int:
    return (ord(ct[0].upper()) - ord(pt[0].upper())) % 26


5)Byte-Range Caesar 
def solution(k: int, hex_data: str) -> str:
 	data = bytes.fromhex(hex_data)
 	return bytes((b - k) % 256 for b in data).decode()

6)One-Time Pad Decrypt
def solution(hex_ct: str, hex_key: str) -> str:
    ct = bytes.fromhex(hex_ct)
    key = bytes.fromhex(hex_key)
 	return bytes(a ^ b for a, b in zip(ct, key)).decode()

7)One-Time Pad Encrypt
def solution(pt: str, hex_key: str) -> str:
    p = pt.encode()
    key = bytes.fromhex(hex_key)
    return bytes(a ^ b for a, b in zip(p, key)).hex()

8)Recover the One-Time Pad
def solution(pt: str, hex_ct: str) -> str:

    p = pt.encode()
    ct = bytes.fromhex(hex_ct)
    return bytes(a ^ b for a, b in zip(p, ct)).hex()

9)Break Single-byte XOR
def solution(hex_ct: str) -> str:
    b = bytes.fromhex(hex_ct)
    best, best_s = "", -1
    for k in range(256):
        p = bytes(x ^ k for x in b)
        if any(c < 32 and c not in (10, 13) for c in p):
            continue
        s = sum(c in b" etaoinshrdluETAOINSHRDLU" for c in p)
        if s > best_s:
            best_s = s
            best = p
    return best.decode()

10)Repeating-Key XOR Decrypt
def solution(key: str, hex_ct: str) -> str:

    k = key.encode()
    ct = bytes.fromhex(hex_ct)
    return bytes(b ^ k[i % len(k)] for i, b in enumerate(ct)).decode()

11)Repeating-Key XOR Encrypt 
def solution(key: str, pt: str) -> str:
    k = key.encode()
    p = pt.encode()
    return bytes(b ^ k[i % len(k)] for i, b in enumerate(p)).hex()

12)Recover XOR Key from Known Prefix
def solution(hex_ct: str, prefix: str) -> str:
    ct = bytes.fromhex(hex_ct)
    pref = prefix.encode()
    return bytes(ct[i] ^ pref[i] for i in range(len(pref))).decode()
