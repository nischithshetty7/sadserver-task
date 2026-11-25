# SadServers: The Command Line Murders

**marvellevel:** 0 | **Skills:** Linux, bash, grep, sed

## Goal
Find the murderer using Linux commands and save the name in `~/mysolution`. The scenario has a twist, so the accepted answer is different from the original game.

## Steps

### 1. Collect the clues
```
cd ~/clmystery/mystery
grep CLUE crimescene
```
The real clues: a tall male (at least 6'), a wallet with membership cards, and a witness named Annabel with blond spiky hair and a New Zealand accent.

### 2. Find the witness
```
grep Annabel people
sed -n 40p streets/Hart_Place
cat interviews/interview-47246024
sed -n 179p streets/Buckingham_Place
cat interviews/interview-699607
```
Ms. Sun had brown hair, so she was not the witness. Annabel Church saw a blue Honda with a plate starting with L337 and ending with 9.

### 3. Find the car owners
```
grep -A 6 "L337.*9" vehicles
```
Blue Hondas owned by people 6' or taller: Erika Owens, Joe Germuska, Jeremy Bowers, Jacqui Maher.

### 4. Check gender and memberships
```
grep -E "Erika Owens|Joe Germuska|Jeremy Bowers|Jacqui Maher" people
grep -E "Joe Germuska|Jeremy Bowers" memberships/*
```
Erika and Jacqui are women, so they were ruled out. Jeremy Bowers appeared in the club membership files.

### 5. Save and verify the answer
The twist meant the accepted answer was different, so I compared the checksum from the scenario page with the saved file:
```
echo "Joe Germuska" > ~/mysolution
md5sum ~/mysolution
```
The result matched the expected checksum `9bba101c7369f49ca890ea96aa242dd5`.

## What I learned from this task
- `grep` searches text, and `-A` shows lines after a match
- `sed -n 40p` prints one specific line
- `echo *` lists files when `ls` is not available
- Linux is case-sensitive: `Joe` and `joe` give different checksums
- `md5sum` checks that a file's content is exactly right
- Using Tab completion avoids typos in file names

## Screenshot
![Solved](solved.png)
