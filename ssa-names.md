# Social Security Administration given names

<https://www.ssa.gov/oact/babynames/limits.html>

> **National Data on the relative frequency of given names in the population of U.S. births where the individual has a Social Security Number**
> (Tabulated based on Social Security records as of March 2, 2025)
> 
> For each year of birth YYYY after 1879, we created a comma-delimited file called yobYYYY.txt. Each
> record in the individual annual files has the format "name,sex,number," where name is 2 to 15 characters,
> sex is M (male) or F (female) and "number" is the number of occurrences of the name. Each file is sorted
> first on sex and then on number of occurrences in descending order. When there is a tie on the number of
> occurrences, names are listed in alphabetical order. This sorting makes it easy to determine a name's rank.
> The first record for each sex has rank 1, the second record for each sex has rank 2, and so forth.
>
> To safeguard privacy, we restrict our list of names to those with at least 5 occurrences.


<tt>https://www.ssa.gov/oact/babynames/names.zip</tt>

```bash
wget http://www.ssa.gov/oact/babynames/names.zip
```

```console
URL transformed to HTTPS due to an HSTS policy
--2025-12-06 21:37:56--  https://www.ssa.gov/oact/babynames/names.zip
Resolving www.ssa.gov (www.ssa.gov)... 2600:141b:1c00:27::17ce:ac05, 2600:141b:1c00:27::17ce:ac1c, 23.222.17.206, ...
Connecting to www.ssa.gov (www.ssa.gov)|2600:141b:1c00:27::17ce:ac05|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 7726516 (7.4M) [application/zip]
Saving to: ‘names.zip’

names.zip                     100%[=================================================>]   7.37M  40.5MB/s    in 0.2s

2025-12-06 21:37:57 (40.5 MB/s) - ‘names.zip’ saved [7726516/7726516]
```


```bash
unzip -d ssa names.zip
```

```bash
cd ssa
head yob1990.txt
```

```console
Jessica,F,46486
Ashley,F,45560
Brittany,F,36537
Amanda,F,34413
Samantha,F,25868
Sarah,F,25825
Stephanie,F,24864
Jennifer,F,22236
Elizabeth,F,20749
Lauren,F,20507
```

```bash
tail yob1990.txt
```

```console
Zan,M,5
Zander,M,5
Zedekiah,M,5
Zephan,M,5
Zerick,M,5
Zeus,M,5
Ziyad,M,5
Zoilo,M,5
Zoran,M,5
Zvi,M,5
```

We and filter for F and M names using awk:

```console
ubuntu@histfile:~/ssa$ echo -e "1,M,2\n1,F,3"
1,M,2
1,F,3
```

```console
ubuntu@histfile:~/ssa$ echo -e "1,M,2\n1,F,3" | awk -F ',' '$2 == "F"'
1,F,3
```

```console
ubuntu@histfile:~/ssa$ echo -e "1,M,2\n1,F,3" | awk -F ',' '$2 == "M"'
1,M,2
```

```console
ubuntu@histfile:~/ssa$ awk -F ',' '$2 == "F"' yob1990.txt > yob1990F.txt
ubuntu@histfile:~/ssa$ awk -F ',' '$2 == "M"' yob1990.txt > yob1990M.txt
```

```console
ubuntu@histfile:~/ssa$ head yob1990F.txt | cut -d ',' -f 1,3
Jessica,46486
Ashley,45560
Brittany,36537
Amanda,34413
Samantha,25868
Sarah,25825
Stephanie,24864
Jennifer,22236
Elizabeth,20749
Lauren,20507
```

```console
ubuntu@histfile:~/ssa$ head yob1990M.txt | cut -d ',' -f 1,3
Michael,65318
Christopher,52359
Matthew,44822
Joshua,43233
Daniel,33831
David,33747
Andrew,33675
James,32357
Justin,30650
Joseph,30134
```

We can get names that were in top 20 in at least one year ("normal sounding names"), using NR with awk:

```console
ubuntu@histfile:~/ssa$ cat yob1990.txt | awk -F ',' 'NR <=20 && $2 =="F"'
Jessica,F,46486
Ashley,F,45560
Brittany,F,36537
Amanda,F,34413
Samantha,F,25868
Sarah,F,25825
Stephanie,F,24864
Jennifer,F,22236
Elizabeth,F,20749
Lauren,F,20507
Megan,F,20259
Emily,F,19368
Nicole,F,17953
Kayla,F,17538
Amber,F,15866
Rachel,F,15710
Courtney,F,15380
Danielle,F,14339
Heather,F,14220
Melissa,F,14000
```

Then using a Bash loop,

```bash
for file in $(ls yob*.txt); do awk -F ',' '$2 =="F"' $file |  awk 'NR <=20' | cut -d ',' -f 1; done | sort | uniq
```

There are 152 names that in some year's top 20 F names (piping to `wc -l`).


```bash
for file in $(ls yob*.txt); do awk -F ',' '$2 =="M"' $file |  awk 'NR <=20' | cut -d ',' -f 1; done | sort | uniq | wc -l
```

```console
94
```


Doing top 5 names,

```bash
for file in $(ls yob*.txt); do awk -F ',' '$2 =="F"' $file |  awk 'NR <=5' | cut -d ',' -f 1; done | sort | uniq
```

```console
Abigail
Alexis
Amanda
Amelia
Amy
Angela
Anna
Ashley
Ava
Barbara
Betty
Brittany
Carol
Charlotte
Deborah
Debra
Donna
Dorothy
Elizabeth
Emily
Emma
Hannah
Heather
Helen
Isabella
Jennifer
Jessica
Joan
Judith
Karen
Kimberly
Linda
Lisa
Madison
Margaret
Mary
Melissa
Mia
Michelle
Minnie
Olivia
Patricia
Ruth
Samantha
Sandra
Sarah
Shirley
Sophia
Susan
```

```bash
for file in $(ls yob*.txt); do awk -F ',' '$2 =="M"' $file |  awk 'NR <=5' | cut -d ',' -f 1; done | sort | uniq
```

```console
Alexander
Andrew
Charles
Christopher
Daniel
David
Elijah
Ethan
George
Jacob
James
Jason
Jayden
John
Joseph
Joshua
Liam
Logan
Mason
Matthew
Michael
Nicholas
Noah
Oliver
Richard
Robert
Theodore
Tyler
William
```

