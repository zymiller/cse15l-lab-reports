# Lab report 2

## Part 1

The main method in my code that is called to add these new strings is the `if (url.getPath().contains("/add-message"))` portion of my code.
This part will basically see if the URI I put in includes the /add-messages part of the URI that we determined we needed for this function to work.
Afterwards it breaks up the input by taking what comes after `?s=` and putting it into a string array. Then all I did was add some code that 
takes the new added word, and then transfers it to a string ArrayList to then be put onto the homepage. Specifically in this request, 
because `?s=` is followed by `Hola`, I then add Hola into storedWords.

The main method again is the `if (url.getPath().contains("/add-message"))` and everything else follows the exact same process as before. The only
difference this time around is that instead of Hola, a `Hello` is in front of the `?s=` portion of the URI. This means `paraneters[1]` will be Hello,
and thus will be added to storedWords.


## Part 2
![Failure inducing input](bug-input.png)
