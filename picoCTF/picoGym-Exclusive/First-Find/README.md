# First Find

## Description

Unzip this archive and find the file named 'uber-secret.txt'

## Approach

![Challenge Files](images/file.png)

After unzipping the `files.zip` we can see the file very obviously in the output

![Unzipped](images/unzip.png)

For the sake of the challenge I used `find` anyway with the command `find files/ -name "uber-text.txt"` which showed the path to the file

![find output](images/find.png)

Reading the file will give you the flag.
