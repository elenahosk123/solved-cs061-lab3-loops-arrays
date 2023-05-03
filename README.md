Download Link: https://assignmentchef.com/product/solved-cs061-lab3-loops-arrays
<br>
Today’s lab will introduce arrays: constructing and traversing them with both counter-controlled loops and (new) sentinel-controlled loops.

Our Destination This Week

<ol>

 <li>Lab 02 review</li>

 <li>Pseudo-ops revisited</li>

 <li>More indirection! Exercise 1</li>

 <li>Hurray for Arrays! ​ Exercises 2 – 3​</li>

 <li>More loopiness! Exercise 4  So do I know everything yet??</li>

</ol>

<strong>3    Processing data </strong>

Lab 02 review

If there is anything you don’t yet understand about the differences between <strong>LEA</strong>​  , ​ <strong>LD/ST</strong>​           , ​ <strong>LDI/STI</strong>​ , and​    <strong>LDR/STR</strong>​ – ask now!

<strong><em>Remember to always open the Text Window of your simpl LC-3 emulator!</em></strong>

<strong><u>Exercise 0</u> </strong>

Write a program that takes a single character from the keyboard, using Trap x20 (the GETC BIOS routine).

<strong><em><u>NOTE</u></em></strong>​<strong><em>: whenever you GETC, you must always immediately OUT, to echo the captured</em></strong>​ ​<strong><em>character </em></strong>​<em>– otherwise the user has no feedback to confirm what key they just typed (we call that “ghost typing”).</em> The ​<em><u>only</u></em>​ exception to this might be when capturing a password, when you don’t want to echo the characters for security reasons ​<em>(another approach is to echo every character with ‘*’)</em>​.

Using the simpl emulator, examine the contents of R0: you will see that LC3 stores each character as an 8-bit ascii code in the lower byte of a 16-bit word, setting the upper byte to 0 ​<em>(check an ascii table to confirm the code for the character you typed)</em>​.

<strong>3.1     Pseudo-ops revisited </strong>

All assembly languages have several “pseudo-ops” (i.e. assembler “directives” that instruct the assembler program how to set up the object code – just like the C++ compiler directives such as #include​).

If you have not done so already, review the ​<a href="https://docs.google.com/document/d/10Q1lFYmInYbrSKHdttUs4VRJAesdCmKGIpuk3nTxpG4/edit?usp=sharing">LC-3 Pseudo-ops summary</a><u>​</u> in the LC-3 Resources folder.

You encountered most of the LC3 pseudo ops already in lab 1:

.ORIG ​tells the assembler where to start loading the code <em>(</em>​ <em>usually x3000, except when we tell you otherwise)</em>​;

.END tells the assembler that there is no more code to assemble (like the ​ ‘}’​       ​ after main() in C++) .FILL stashes a single “hard-coded” value into a memory location; you can specify it as a decimal (​       #​ ​), hex (​x)​ , or ascii character (use ​’ ‘​, e.g. ​’a’​ or ​’
’​) and​ .STRINGZ​ creates a c-string, i.e. a null-terminated character array. You may use 
 inside a string to insert a newline at any point.

The last of the pseudo-ops we’ll need is .BLKW​         ​ <em>(</em>​ <em>“block words”)</em>​, which is a bit like .STRINGZ without any data: it tells the assembler to simply set aside <strong>n</strong>​ ​ memory locations for later use. It does not explicitly “zero out” the designated memory space, so there may be “junk values” in those locations if they have been used previously.

We’ll be using this pseudo-op in today’s exercises.

<u>Example</u>​:

ARRAY_1 .BLKW  #10 ; Reserves 10 memory locations, starting at address ARRAY_1 DEC_25    .FILL #25  ; stores the vale #25 at the memory address labelled DEC_25

; this will be located at the first address following ARRAY_1

<em>Figure 1: .BLKW Illustration </em>

<em>Note that even though the label DEC_25 immediately follows label ARRAY_1 in the code, its address is </em>

<h1>(address of ARRAY_1) + #10</h1>

<em>Note also that the ten memory locations are </em><u>​<em>not</em></u>​<em> guaranteed by the LC3 specs to be initialized to 0.</em>

<strong>3.2    More indirection!  </strong>

Exercise 1

Let’s take another look at Exercise 3 from last week.

At the time, we told you to hard code both remote addresses in the local data block – but this is not really very efficient ​<em>(suppose you had a dozen data values up there </em>…<em>) </em>

We know that the two data values are in contiguous memory locations (x4000 and x4001), so we ought to be able to just hard-code the first address and then use address arithmetic to get to the next.

So copy your <u>​Lab 2 Exercise 03</u>​ from last week into the lab03_ex1.asm file in your current directory, but this time use just a ​<em><u>single</u></em>​ pointer in the local data block. Call it DATA_PTR.

You know how to get the first data item from the remote location: how will you get the next? <em>Hint: LDI won’t work, because we don’t have a pointer to it in an accessible memory location. </em><strong>        </strong>

<strong>3.3    Hurray for Arrays!  </strong>

<strong> </strong>Exercise 2

The technique you just discovered ​<em>(if you didn’t, go back to exercise 1, and don’t join us here until you’ve figured it out!)</em>​ is a standard mechanism for constructing and traversing arrays – not just in LC3 programming, but in <u>​<em>all</em></u>​ languages.

So now write a program (lab03_ex2.asm) that builds and populates an array in the local data area:

<ul>

 <li>Use .BLKW to set up a blank array of 10 locations in the local data area.</li>

 <li>Then have the program prompt the user to enter exactly 10 characters from the keyboard, and populate that array with the characters as they are input</li>

</ul>

This will require a counter-controlled loop (DO-WHILE loop), which you should already know how to construct. <em>(</em>​ <em>Check </em><a href="https://drive.google.com/drive/folders/0B9AugYlANDZkVUtZajFkNUFBX0U?usp=sharing">​</a><a href="https://drive.google.com/drive/folders/0B9AugYlANDZkVUtZajFkNUFBX0U?usp=sharing"><em>here</em></a><a href="https://drive.google.com/drive/folders/0B9AugYlANDZkVUtZajFkNUFBX0U?usp=sharing">​</a> <em>if you need a refresher!) </em>

Test your program, inspecting the contents of the array in simpl after every character input. <em>(By the way: you should now understand one of the deep mysteries of C++ – why the number of elements in a static array variable </em><u>​<strong><em>must</em></strong></u>​<em> be known at compile time, and can’t be changed after that). </em>

Exercise 3

Now copy Exercise 02 into lab03_ex3.asm, and complete it by adding  another loop to traverse the array again, using your knowledge of i/o to <u>​<em>output</em></u><u>​</u> each stored character to the console, ​<u>one per line</u> (i.e. print a newline ‘
’ = ASCII x0A – <u>after each character</u>​          ).<u>​</u>

Your program will now be complete: it will accept exactly 10 characters from input, storing them one by one in an array, and then output the whole list to console.

<strong>3.4    More loopiness!  </strong>

<strong> </strong>Exercise 4

In the previous exercises, you were able to traverse the arrays because you knew up front how many elements were in them – in fact that number was hard-coded into the .BLKW pseudo-op.

Can you think of a way to create and/or traverse an array without knowing beforehand how many elements it will contain, and without using .BLKW?

Hint: think about the difference between counter &amp; sentinel control of loops.

Copy Exercise 3 into your lab03_ex4.asm file, and modify it as follows:

It must capture a sequence of characters as long as you like ​<em>(within reason – for now, let’s keep our tests to less than 100)</em>​, and decide when to stop.

The program will store each character as it is entered in an array starting at x4000 ​<em>(we will just assume for now that there is a vast amount of free memory up there)</em>​, and then output them to the console in a separate loop.

There are three separate problems to be solved here:

<ul>

 <li>How do I communicate to the program that I have finished input?</li>

</ul>

<em>Hint: what is the most common keyboard method of signaling “I’m done with this message” in, say, Facebook chat? </em>

<ul>

 <li>How do I build the array so that it “knows” where it stops?</li>

</ul>

<em>Hint: how does .STRINGZ do it? </em>

<ul>

 <li>How does the program know when to stop traversing the array for output? <em>See previous hint, and think PUTS! </em></li>

</ul>

Once you solve this problem you will have in your algorithmic toolkit a very powerful technique – <em><u>sentinel-controlled loops</u></em>​—that you will be using to manage i/o for the rest of the course.