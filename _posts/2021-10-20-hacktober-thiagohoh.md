---
layout: post
title:  A first linux module
date:   2021-10-20 19:00:00 -0300
author: Thiago Alexsander
github: thiagohoh
---


As we all know this year is the 8th edition of the **Hacktoberfest**.
Just in case you are new to this whole thing, Hacktoberfest is a **Celebration** of open source code run by DigitalOcean.

To participate is simple, submit 4 Pull Requests to any participating GitHub or GitLab repository/projects, and if you do there are some rewards you can get like a T-shirt or you can plant a tree.
🌲🌴👕


So this year i was a **little** busy, so i decided to take it easy, and doing some research to find some cool repositorys/projects, i found the perfect one:
 [FunnyAlgorithms](https://github.com/ReciHub/FunnyAlgorithms), and as they say "A repository with a bunch of funny algorithms, beginners friendly". So this was a great opportunity to revisit some old code that and rewrite and share them with others.

Well the hardest part was to think of a funny algotithm, that wasn't there yet...
So i kind ~~cheated~~ used the term funny in a very loose way. I mean, isn't it funny how different a code looks when it's written to be a kernel module??? I thought so, too.

The code is a simple module that when loaded display all running taks on the terminal. I know, i know it's kinda simple, but in a cool way is also very beginner friendly if you are new to Linux kernel.

So let's get to the code, and how some things are a little different.


The first thing right off the bat is that you can add module macros used for licenses and descriptions.

```C
MODULE_LICENSE("GPL");
MODULE_AUTHOR("Thiago");
MODULE_DESCRIPTION("Display all tasks in terminal.");
MODULE_VERSION("0.2");
```
The most common license for linux kernel is the GPL or GPL v2, those macros are in some way self explanatory, and you can even have other macros like:

```C
 MODULE_SUPPORTED_DEVICE() 
 ```

 The next thing is a function to print thing on the terminal and to do that we need the terminal struct.

 ```C
 static void print_string(char *message) //Recieves a message to be written 
    struct tty_struct *my_tty; //Terminal struct
 ```
 And to be able to use the current terminal we call

```C
my_tty = get_current_tty();
```
 And of course we need to verify if the terminal is not **null**.
 The my_tty->driver holds terminal functions, one of them is **write** that can be used to write strings to it.

```C
 (my_tty->driver->ops->write) (my_tty, "\015\012", 2);
 (my_tty->driver->ops->write) (my_tty, message, strlen(message));
 ```
The first parameter tells which terminal to write to.
The second parameter is a pointer to a string.
The third which is the lenght of that string.

Another thing to consider is the inclusion of \015\012, the way the terminal was built a simple \n would not work correctly. Becausa of this we need to have a carriage return and a line feed \015\012 in ASCII.

The next two functions are the __init and __exit Macros
```C
static int __init print_string_init(void)
```
Here we print a nice little message on dmsg using printk, all printk messages are printed to the kernel log buffer. Below it there is for each that run through all tasks in our taks_list, and for each task we call print_string with the task name.  
```C
printk(KERN_INFO "Displaying all tasks\n");// Prints this message on dmesg
	for_each_process(task_list){ // For each process running
		print_string(task_list->comm); //Display task name.
```

The __exit macro just prints a message on printk as well, and with that we conclude our linux module.
Of course there is so much more that could be done or explained, but for our first kernel module i think it's ok.

The **PR** was successfully merged and closed and can be found [PR](https://github.com/ReciHub/FunnyAlgorithms/pull/865). I hope this help someone to learn more about how linux modules are made, and if you want to know more or go in more details i highly recommend [The Linux Kernel Module Programming Guide](https://sysprog21.github.io/lkmpg/).

And if you want to get your hands on T-shirt consider visiting [Hacktoberfest website](https://hacktoberfest.digitalocean.com/) and participate as well.