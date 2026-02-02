# Commit Messages

### Why commit messages are important

When you are applying for jobs, employers will 
look through your projects on GitHub and they will look through your commit history.

Having a good commit message history will
allow you (or other developers working on your code) to quickly see what changes were made and why.
     
This is useful if a bug is found in the code that needs to be fixed!
     
Having a good commit message history will also be helpful if you come back to a project you were working on after stepping away from it for a while.

You likely won't remember your thought process and changes made when initially writing out the code.

### Bad vs. Good Commits

When it comes to writing commits, it is
crucial to know how to write them effectively. Here's an example of a bad commit message: <br>
`fix a bug`
     
Even though it describes what you did, the message is to vague, which leaves the other developers on your team confused.
     
A good commit message will explain the "why" behind your changes.
     
In other words, a commit message describes what problem your changes solve and how it solves them.
     
Effective commits consist of two separate parts: a subject, and a body:
     
Subject - a brief summary of the change you made to the project

"This is the change I made to the codebase"

Body - a concise yet clear description of what you did

"Describe the problem your commit solves and how"

Now that we learned the secret to creating a good commit message, let's try and fix the commit message from earlier:

"Add missing link and alt text to the company's logo

Screen readers won't read the images to users with disabilities without this information."

Now, developers can gain a better understanding of this commit message because it does the following:

1. Provides a subject that specifies your code's action (e.g., "Add missing link and alt text to the company's logo").

2. Contains a body that provides a concise yet clear description of why the commit needed to be made (e.g., "Screen readers won't read the images to users with disabilities without this information.").

3. Separates the subject from the body with a new/blank line. This is a best practice we highly recommend following. It makes commit messages easier for other developers to read.

> Some teams of developers might have their own convention for commit messages in specific formats. However, they still follow the same principles as this lesson outlined.


### When to Commit

A good way to view a commit is like a
"snapshot" of your code at the moment that it was made. That version of your code up to that point will be saved for you to revert back or to look back at.
     
When writing code, it's considered best practice to commit every time you have a meaningful change in the code. This will create a timeline of your progress and show that your finished code didn't appear out of nowhere.
     
In other words, make a commit if you get a piece of code you are working on to function like you want it to, fix a typo, or fix a bug. 

As you gain experience, you will develop a better feel for what should be committed!
     
There will come a time when you are working on a project and you FINALLY get something just right (this would be a good time to commit!), and then maybe 30 seconds to a few days later it breaks.
     
You have no idea what you changed, everything looks to be the same, and you don't remember editing that line, but alas, it isn't working how you want it anymore.
     
You'd be able to go back through your commit history and either revert your code back to the last commit you made when you first got that part working or go back and see what your code looked like at that point in time.


### Knowledge Check 
1. What are two benefits of having well-written commit messages and a good commit history?

(a) You are able to track and identify which function does not work / what parts were edited by you, (b) Context is provided properly from the commit message and the developer easily understands it
     
2. How many characters should the subject line of your commit message be?

Should at least be less than or equal to 72 characters.
