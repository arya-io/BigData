Linux Teaser 1:

Implement a pipeline by writing down a single line linux command, where the end result of the pipeline is as given below
1) Output of the date command will be stored in a file fulldate.txt
2) The day part of the date output will be stored in a file today.txt

## First approach:
date > fulldate.txt && head -n 1 fulldate.txt | cut -d ' ' -f 1 > output.txt
![image](https://github.com/user-attachments/assets/0a6102ad-9466-4568-88f9-bcd0699cf24c)

This is a lengthy method

## Another solution:
date | cat > fulldate.txt && date +%a | cat > day.txt
![image](https://github.com/user-attachments/assets/7178396a-a8d0-46e3-a3db-331e728d0690)

Above is a little efficient method

## Efficient method:

date | tee fulldate.txt | xargs echo

![image](https://github.com/user-attachments/assets/923b1c97-7509-4a33-a645-86f1842d7faf)

What is tee? What is its working? Is it in a 'T' shape? What is its stdin and stdout? How does the input and output flow work here in accordance with the data? 

Tee got a input in the form of data (here, date), took its snapshot and passed it to its stdout.
tee  -  read  from standard input and write to standard output and
       files
q

for part 2 of the question, we need to split the output of date on the basis of spaces.
so we will get individual words. those individual words are known as fields and the first field is -f 1.

date | tee fulldate.txt | cut -d ' ' -f 1 > op.txt

![image](https://github.com/user-attachments/assets/8d21f143-6a05-4e89-a913-d7b36942a403)

---

Linux Teaser 2
-----------------------
1) What will be the output of this command
date | echo

Qa - Looking at the output, analyze and answer why you will get the output the way it is appearing.
Qb - What modification will you suggest so that the output of the date command can be echoed on the terminal?

We get no output after running: date | echo
![image](https://github.com/user-attachments/assets/b19c8834-8a7c-4ed3-a12d-dbfe541f948f)

Solution for Qa:

There are some commands which don't have stdin.
They only take command line arguments.

Every process has stdin, stdout, stderr, command line args.

Here, echo is a command which does not have stdin.

Solution for Qb:

date | xargs echo

What is xargs doing?
xargs - build and execute command lines from standard input
Takes a command line parameter as a command

![image](https://github.com/user-attachments/assets/e1f1c01f-1445-4a94-9740-2a1a6eab9e0c)

---

Linux Teaser 3
-----------------
remove all the files listed In filestodelete.txt

Note - 
1. Create 3 files del1.txt, del2.txt and del3.txt in your pwd (Use brace expdension)
2. Create a file filestodelete.txt having above file names on a single line with space as 
a delimiter character
3. delete the files by utilizing filestodelete.txt

Solution for 1:

touch del{1,2,3}.txt
touch del{1..3}.txt

We can use this for remove as well: rm del{1..3}.txt

![image](https://github.com/user-attachments/assets/6bec12ab-e8e7-4bb0-8f50-3d8b661930d4)

ls del*.txt
![image](https://github.com/user-attachments/assets/1d3cb994-8328-46d1-9ef1-2b745f381600)

ls del*.txt | tee filetodel.txt
cat filetodel.txt

![image](https://github.com/user-attachments/assets/a677ea3f-7fbb-4ed8-bdd3-64db8d284869)

We got all the files in multiple lines but we want them in a single line.

ls del*.txt | xargs echo > filetodel.txt
cat filetodel.txt

![image](https://github.com/user-attachments/assets/012028ec-d15e-4ceb-a211-506645f659cc)

Now delete them:

cat filetodel.txt | xargs rm

ls -lh

cat filetodel.txt

![image](https://github.com/user-attachments/assets/d2245c79-5cb7-4c2b-8a72-d11dfdacf5f6)

---

talentum@talentum-virtual-machine:~/test_teaser$ type echo
echo is a shell builtin
talentum@talentum-virtual-machine:~/test_teaser$ type ls
ls is aliased to `ls --color=auto'
talentum@talentum-virtual-machine:~/test_teaser$ type rm
rm is hashed (/bin/rm)

![image](https://github.com/user-attachments/assets/aebcf6fd-1147-4032-93a4-29d576ab3f6d)

---

Linux Teaser 4
-----------------
Create an alias calmagic, which will print 
1) a calendar month supplied from command line
2) A calendar 1 month before the command line supplied month
3) A calendar 1 month after the command line supplied month
in a file mymonths.txt in your home folder

For example 
If i am going to write a command
echo "12 2017" | calmagic
It should print the 11th month of 2017, 12th month of 2017 and 1st month of 2018 in a file mymonths.txt
Hint - 
1) Refer man cal
2) You need to put your alias in a file .bahs_aliases. and relaunch the terminal window
3) See how to create aliases in linux 
4) Try it on Ubuntu machine.

Solution:

talentum@talentum-virtual-machine:~/test_teaser$ cal
     April 2025       
Su Mo Tu We Th Fr Sa  
       1  2  3  4  5  
 6  7  8  9 10 11 12  
13 14 15 16 17 18 19  
20 21 22 23 24 25 26  
27 28 29 30  

![image](https://github.com/user-attachments/assets/c50334cb-2e13-4af4-9344-e7465be25a73)

talentum@talentum-virtual-machine:~/test_teaser$ cal 04 2002
     April 2002       
Su Mo Tu We Th Fr Sa  
    1  2  3  4  5  6  
 7  8  9 10 11 12 13  
14 15 16 17 18 19 20  
21 22 23 24 25 26 27  
28 29 30  

![image](https://github.com/user-attachments/assets/a9c69854-e474-47b7-86f1-c6938ea534ce)

talentum@talentum-virtual-machine:~/test_teaser$ cal 12 2024 -A 1 -B 1
   November 2024         December 2024          January 2025      
Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa  
                1  2   1  2  3  4  5  6  7            1  2  3  4  
 3  4  5  6  7  8  9   8  9 10 11 12 13 14   5  6  7  8  9 10 11  
10 11 12 13 14 15 16  15 16 17 18 19 20 21  12 13 14 15 16 17 18  
17 18 19 20 21 22 23  22 23 24 25 26 27 28  19 20 21 22 23 24 25  
24 25 26 27 28 29 30  29 30 31              26 27 28 29 30 31

![image](https://github.com/user-attachments/assets/427c341d-94c6-47de-9dd6-428bc15c405a)

cal 12 2024 -A 1 -B 1 > mymonths.txt

![image](https://github.com/user-attachments/assets/6d348ad3-a9f2-4bc1-ad17-414d077f59f0)
























