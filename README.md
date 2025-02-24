Download link :https://programming.engineering/product/group-project-music-recommender/


# Group-Project-Music-Recommender-
Group Project Music Recommender+
Overview

In this assignment, you will create a music recommender system similar to the one de-scribed in chapter 5 of the textbook, so read the chapter before reading the rest of this assignment. The learning objectives of this assignment are:

Practice with imperative programming (while-and for-loops) and mutable data types (lists and dictionaries).

Practice designing a program that combines several features and needs to be im-plemented using several functions.

Important:

Do exactly as instructed in this assignment to receive full marks.

All text in this document may be considered a requirement. At no point should your program crash.

If you would like to make your program do di erent things, go for it! But include a fancy-mode switch, like the ’debug’ variable in the tictactoe game (slide 15 of Lecture 9). Use it in your program so if it’s false, the program behaves exactly as it is shown in the spec document. If fancy-mode is true, then your program can do whatever cool stu you like. When you submit, make sure fancy-mode is switched o . Write a comment in Canvas to let the CAs know that you did something super cool so we can check it out.

Again, if it hasn’t been said enough already, make sure your program behaves EX-ACTLY as shown in the Example Interaction section of this document. There are two reasons the program should behave exactly as speci ed. First, it helps us grade more automatically (and hence consistently). Second, in real projects several people collaborate on di erent components; those components have to t together exactly or the application won’t work. So get used to following speci cations precisely. If you have any questions about this behavior, feel free to reach out to a CA to make sure you are implementing the print statements correctly :)

Of course, don’t cheat. This exercise has been used before so it wouldn’t be hard to nd solutions online. Unlike some of the previous exercises, this one is more involved so it is extremely unlikely you would come up with a solution very similar to someone else’s. So it’s very likely that cheating will be detected.

Notes and Suggestions

2

This is the most challenging assignment yet, so start early, and read the require-ments section of this document carefully. It provides exact speci cations that you must follow in order to receive full marks on this assignment. And read the text-book, which provides a lot of code that can help you, even though our version has a few extra features.

The requirements section is broken down into the exact functionality your assign-ment must provide, and the output which it must produce. However, you must decide on the implementation details yourself.

As this assignment is meant to help you focus on while loops, for loops, lists, and dictionaries, you should think about how you might use these tools for each task you complete. Reviewing your ideas and thinking about alternatives and improvements before proceeding with your plan can help you create better code.

Plan for unit testing: Early on, make notes on how to test the main functions. De ne the test cases so the functions can be tested separately, before combining them. These can be assert statements, print outs, pyunit tests, or whatever you feel most comfortable with, but remember to comment out these tests before submitting so that your program is able to be graded by the auto-grader.

Requirements

The Basics

Name your source le musicrecplus.py.

When the program starts, it loads the database from the le named musicrecplus.txt, if it exists. Otherwise it creates the le. The le stores the database using the fol-lowing format:

UserName : Artist1 , Artist2 , Artist3 ,…

Have a look at the sample database les provided with the assignment, and note the following.

The artist list must in sorted order, according to the Python comparison or-der for strings, and not have duplicates. Artist names are standardized using \title case”, i.e., capitalized (see the .title() function used in the textbook). For example, if the user entered artists \eminem”, \TMBG”, and \Kerkylas of Andros”, the program will convert those to \Eminem”, \Tmbg”, and \Kerky-las Of Andros”. So they will be stored in the le, and printed, in the converted form.

The lines of the le should be in order by user name, with no duplicate users.

The user’s name is allowed to end with the character $, which indicates that the user prefers their information to be kept private. This is called a private mode user and it will be discussed in some of the features described later. (But we aren’t going to implement anything that protects access to the database le by other programs.)

If the le musicrecplus.txt does not exist upon starting the program, create it.

3

Notice that no spaces should appear between commas and artist names or the colon and the last name of the user and the rst artist. Please follow this format very carefully and closely.

The user should be prompted for their name:

If the user is a new user (not already in the musicrecplus.txt le), they should be prompted to enter their initial preferences before they can move on to the menu.

If the user is not new, they should not be asked their pre erences and should immediately be shown the menu.

The user should be prompted for their name with the phrase

Enter your name ( put a $ symbol after your name ifyou wish your p r e f e r e n c e s to remain private ):

If the user adds a $ as the last character of their name, they are in private mode, which a ects the recommendations phase.

There should be a space after the colon in the prompt.

The Menu

The menu should display EXACTLY as follows:

Enter a letter to choose an

option :

e

– Enter p r e f e r e n c e s

r

– Get r e c o m m e n d a t i o n s

p

–

Show most popular artists

h

–

How popular isthe most

popular

m

–

Which user has the most

likes

q

–

Save andquit

When the menu prints, it should receive user input.

If no option is chosen, or an invalid option is chosen, the menu should reprint and request input until the user enters a valid option.

The main program should be structured as a while-loop that repeatedly o ers the user the choice to do one of the menu options. When he or she quits, it should halt after saving the le.

Functionality

Enter Preferences: The user enters their preferences (artists they like) one at a time, similar to the basic program in the textbook:

This will replace the preferences already saved in the database under that user.

The user should be prompted by:

Enter an artist that you like ( Enter to finish ):

The program should keep asking the user for preferences until the user enters the empty string (i.e. until they press enter).

After the user nishes entering preferences, the database should be updated imme-diately so that the other functions proceed using the new preferences. (In memory, not saved to a le.)

4

After the user nishes entering preferences, they should be returned to the menu, which should be awaiting their next choice. It should be the same after each of the operations (except Quit), so we won’t repeat this point below.

Get Recommendations: This option will also work similarly to the basic program in the textbook. However, it is a separate menu option and must follow these requirements:

The recommendations should come from the user with the most similarity to the current user.

But, if another client’s preferences are the same as, or a subset of, the user, then ignore that client’s preferences. In other words, the \best match” should be one that overlaps the most while also having at least one di erent artist to recommend.

If there is a tie for the best match, your program should just pick one (for example, the rst one it nds). (We will avoid testing what happens with ties.)

Users in private mode should be excluded from these calculations.

The recommendations should appear one per line.

Artists’ names should not be included more than once in a single list of recommen-dations.

The user should not be recommended any artists they already have entered a pref-erence for.

Recommendations should be sorted.

If there are no preferences available for recommendation, the user should be told:

No r e c o m m e n d a t i o n s a va il ab le at this time .

Show Most Popular Artist: Print the artists that are liked by the most users.

The top 3 artists should be printed, one per line, starting with the most popular.

Users in private mode should be excluded from these calculations.

If there are no artists found by this operation, display to the user

Sorry , no artists found .

If there are fewer than 3, print all of them.

If there is a tie for most popular, either choose one or print them all. (We won’t test for this situation.)

How Popular Is The Most Popular Artist: Print the number of likes the most popular artist received.

Print only the number. Do NOT print the artist!

Users in private mode should be excluded from these calculations.

If there are no artists found by this operation, display to the user

5

In the event of a tie, still only print this number once.

Note the similarity between this and ShowMostPopularArtists. Consider helper functions that help with the functionality of both of these functions at the same time.

Which User Likes The Most Artists: Print the full name(s) of the user(s) who like(s) the most artists.

Print only one user name per line, in sorted order.

If there are no artists found by this operation, display to the user

Sorry , no user found .

Users in private mode should be excluded from these calculations.

If there is a tie, you can pick one of the users, or print them all. (We won’t test for this situation.)

The current user should be included in this computation.

Save And Quit: When the user chooses to quit, the current database should be written to the musicrecplus.txt, replacing old contents (if any).

The name of the le saved to must be musicrecplus.txt.

You must save according to the le format described above.

If the le exists, overwrite the contents.

If the le does not exist, you should create it with the proper contents.

After this saving occurs, the program should exit (without crashing, of course).

Example Interactions

Example 1: Before this interaction, musicrecplus.txt does not exist. See example1.txt to see how the program should interact with the user. Make sure your program works exactly the same way! See musicrecplus_ex1.txt to see the musicrecplus.txt le after this interaction.

Example 2: See musicrecplus_ex2_a.txt to see what should be in musicrecplus.txt BEFORE executing this example. See example2.txt to see how the program should interact with the user. Make sure your program works exactly the same way! See musicrecplus_ex2_b.txt to see the musicrecplus.txt le after this interaction.

Extras

You’re welcome to add additional features, but your program is required to include at least these features, associated with the letters listed above. For extra credit, you can implement the following features:

Delete Preferences

6

This works similarly to Enter Preferences, the main di erence being that you are removing preferences from musicrecplus.txt instead of adding them. This will be \d” in the menu. To start, a list of the user’s current preferences should be listed so that the user knows what can be deleted. The details of this implementation are up to you. For example, you could number them and have the user choose a number, or you can just have them type out the name exactly as it is presented. You will receive the same credit either way. If you choose to implement this option, your Enter Preferences will need to be a little di erent. Instead of replacing the old preferences, it should add them to the existing list. (5pts)

Show Preferences:

Simply prints the current user’s preferences. This will be \s” in the menu. If implemented correctly, this should print the most up-to-date list, even if the user just entered new preferences and has not yet quit the program. (5pts)

Fixing the Get Recommendations Bug:

If you only have one user in the database and you try to get recommendations, you will run into an error since there are no users to compare to. Edit the Get Recommendations option to check for this, and present the user with your own error message that doesn’t crash the whole system and instead prints the menu again. (5pts)

This extra credit will allow you to exceed 100 points on this assignment and will act as additional points towards your overall homework grade. However, if adding these points would cause you to exceed 100 on your overall homework average, they cannot be counted, nor can they be put towards any other assignment category.
