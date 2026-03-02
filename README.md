# Bandit Level 12 --> Level 13 Write-up
## Objectives:
The objective of this level is to obtain the password contained in the file  ` data.txt`  , 
which is a hexadecimal dump of a file that has been compressed several times.
## Methodology:
### Step 1: 
First, create a directory with this command:
```
mktemp -d
```
which gave me this result: 
```
/tmp/tmp.TjcslscyyN
```
### Step 2:
Copie the original file from the home directory:
```
cp ~/data.txt .
```
### Step 3: 
Converting the hexadecimal dump to binary using: 
```
xxd -r data.txt > data.bin
```
this create a a new file  ` data.bin `.
### Step 4:
I used the ` file `  command to determine if the file was compressed.
```
file data.bin
```
### Step 5: 
Decompressing gzip file
To do that, first rename the file with the extension we need:
```
mv data.bin data.gz
```
Now decompress with:
```
gunzip data.gz
```
### Step 6:
I used the command ` file data `  and saw that the file was compressed in bzip2 format.
So it needs to be renamed again:
```
mv data data.bz2
```
Now it can be decompressed with:
```
bunzip2 data.bz2
```
### Step 7:
Then, extract the tar file.
```
tar -xf data
```
We used the ` ls `  command and noticed that a new file was created: ` data5.bin `
### Step 8: 
Extracting tar archive with:
```
tar -xf data5.bin 
```
and this created:  ` data6.bin ` 
### Step 9:
Next, I used this command: 
```
file data6.bin
```
Then, as in previous steps, it is renamed and decompressed:
```
mv data6.bin data6.bz2
bunzip2 data6.bz2
```
Check with ` ls `  and we see that another file was created:  ` data6 `
### Step 10:
I checked the file and I extracted it:
```
tar -xf data6
```
This created:  ` data8.bin `
### Step 11:
I checked the file type whit:
```
file data8.bin
```
so I renamed and decompressed it:
```
mv data8.bin data8.gz
gunzip data8.gz
```
this created:  ` data8 `
### Step 12: 
I checked the file:
file data8
and I observed:
```
data8: ASCII text
```
Then I used the ` cat `  command to be able to view this file.
```
cat data8
```
And the password for the next level was found.
## Obstacles:
One of the obstacles was identifying the newly created files and the files that needed to be renamed and extracted, 
as well as repeating the steps until I found the password. When typing the commands, 
I mixed up the file names. Another mistake was using the wrong commands. 
Then, to correct the errors, I realized I had to follow a specific sequence until I finally solved the problem.
## Concepts learned
- Identifying file types using  ` file `
- Decompressing gzip files using  ` gunzip `
- Decompressing bzip2 files using  ` bunzip2 `
- Extracting tar archives using  ` tar -xf `
## Result:
I founded the password by converting the hexadecimal dump into binary repeatedly identifying and decompressing the files. 
This process demonstrated using the correct commands and order is important to extract hidden information.
