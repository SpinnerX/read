# read
A small header-online library to make input in C++ sensible

Using cin >> to read in input from the keyboard is problematic for a few different reasons:
1) New programmers chain together multiple cin statements, leading to the inability to tell where an error occurred in the input
2) Cannot be combined with const
3) Cannot be combined with auto
4) Cannot be combined with cout statements
5) Cannot be used at the same time a variable is declared
6) Breaks if you mix and match cin >> statements with getlines

This short (~70LOC) header-only library provides four functions for reading from the standard input or from files. Here is an example of each of them in action:

```int x = read<int>();``` This reads an int from the keyboard and stores it in x. If the user types something not an int, it discard it and keeps reading until an int is read. Using cin, you'd need two lines to do this: ```int x; cin >> x;``` which is annoying and awkward.

```int age = read<int>("Please enter your age:\n");``` This will prompt the user to enter their age. If they don't type in a valid int, it will prompt them to do so again until the user successfully gives them an int.

```const double SIZE = read<double>();``` Because the input is something that can appear on the right hand side of an assignment operation, this opens up a lot of things that can't be done with cin, such as creating a variable and initializing it at the same time, as well as using input to initialize constants and combining with auto.

```auto x = read<char>();``` Reads a char from cin and returns it into x, whose type is deduced to be char by auto.

```const string NAME = readline("Please enter your name: ");``` Read is the equivalent to "cin >>". Readline is the equivalent of getline(cin,s), except it combines cleanly with read, whereas it is buggy to use cin >> and getline without being very careful with trailing newlines. This line here will prompt the user for their name and read until a newline, and then return the result in a string.

In addition to read and readline, there are two more functions also named read and readline that read from files instead of cin:

```ifstream ins("file.txt"); cout << read<int>(ins) << endl;``` The first line opens a file for reading, the second line directly outputs the first int found in that file. This would be awkward to write using cin and cout.

```string s = readline(ins);``` This reads a line of text from the file ins and stores the result in s. Like with the other readline, it plays nicely with read.

Testing the performance on a million ints, it appears to be equivalent to the old way, though this was not written with performance in mind. It was written to make input easier for new C++ programmers, who frequently get tripped up on input, especially when vetting their input for errors and when switching between >> and getline.
