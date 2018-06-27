// TIPS:
            // this is main code block for all C# console applications
            // you need to Build your solution each time you make changes to the code below or else it won't update
            // hitting the start button up top will run the application and this is where it starts reading
            
            // your second best friend besides Intellisense will be the debugger
            // if you select a line WITH code on it and hit F9, a break point will be insterted (it's a solid red circle; if it's a clear circle with a red outline, it means your code needs compiled and that line will be skipped over)
            // when you run your program next, the program will pause on that line of code. You can mouse over variables in the code that are on or above that line and you can see what its values are
            // THAT IS SO IMPORTANT. This is the best way to determine whether data is actually being stored like you want it to be. Become comfortable with this today.
            // hitting F10 will "step" to the next line aka will move one line below it that has code. This is the basic way to progress through the debugger. 
            // F5 will go to the next break point that you've set. If you didn't, it'll execute the rest of the code without stopping
            // Also, these "//" is how you make comments in the code. the application will just ignore whatever is typed there. Pretty self-explanatory
            // you can copy and paste all of the non-commented code into a new console project to see how short this is


            // Alright let's get started:
            // I explain everything that I'm doing here. This is program follows the requirements of the assignment EXCEPT user input validation. I think it's insane they're making you do TryParse or anything so I'm not including it. This is enough. Honestly if this isn't good enough for them they can fuck right off.

            // a while loop will keep the program running **while** all conditions are true (all conditions are going to be true until the user puts something in. more on that later)
            while (true)
            {
                // we need to get store the data that the user types in. So we need to declare aka create where that data can be stored
                // ints must have a name and must be assinged a value. 0 is usually what you choose when you don't have any preset data point

                string number1;
                string number2;
                
                // a bool is a true or false statement. The program will pass only if the user adds up the correct numbers. I've set the boolean "result" to true for now
                bool result = true;

                // Console.WriteLine is how you make text appear in the console and will be the only text on that line in the console. \n creates an extra line below it (for more space to read)
                Console.WriteLine("Good morning, programmer.\n");
                // Console.Write is the same thing except it doesn't create a new line after it
                Console.Write("Please enter a number: ");

                // Console.ReadLine() is how you get data from the user. This allows the user to type items into the program. All of that data comes in as a string.
                // for our purposes, let's say the user enters "543" into "number1". That info will now be stored there as long as the program is open

                number1 = Console.ReadLine();

                // repeat the process for the second number. The user enters "456" and will be stored in "number2"
                Console.Write("Please enter a second number: ");
                number2 = Console.ReadLine();

                // our first if/else statement. we want to determine whether the two numbers entered in match in length. IF they do (true), we execute the rest of the program code, ELSE (false) we make them redo it
                // in our example, number1 = 543 (which has a length of 3) and number2 = 456 (also a length of 3)
                if (number1.Length == number2.Length) // this is true.
                {
                    // we want to use the length of the numbers to determine how many times we go through the loop
                    // in our example, 3 will be stored for in the int "length"
                    int length = number1.ToString().Length;

                    // we want to put the totals in an array that we can loop through later (it's called a collection for that reason)
                    // NOTE: the length of an array must be defined when it's declared. the int[length] will make the array length be 3
                    int[] intarray = new int[length];

                    // now we need to pick each individual number out of the numbers the user put in
                    // Below is a common loop called a For loop. Here's the break down:
                    // int i = 0  ////// this is the number where the loop starts
                    // i < length ////// this is the limit for the loop. Since the length is determined by the user input, that's how many loops we'll make
                    // i++        ////// this is the increment. i++ simply means the loops increases i (the iternation) by one each time

                    for (int i = 0; i < length; i++)
                    {
                        // we need to isolate the first number in number1 and number2

                        // Let's break this down
                        // int.Parse() ///// since we're getting the first number out of the string variable "number1" and put it into the int variable "firstNumber", we'll need to convert it to an int. int.Parse does exactly that 
                        // number1.Substring(i,1) //// substring can pull individual characters out of strings. the "i" is the starting point in the string and the "1" is the number of characters we're going to pull characters out
                        // NOTE: Arrays place start from 0, not 1;
                        ////////////// for example, number1 = "543" and i = 2, then number1.Substring(i,1) would pull out "3" and place it into "firstNumber"
                        ////////////// another example, number1 = "543" and if i = 0, and if number1.Substring(i,2) would pull out "54"

                        int firstNumber = int.Parse(number1.Substring(i, 1));
                        int secondNumber = int.Parse(number2.Substring(i, 1));

                        // here we're totaling the numbers
                        
                        // so example if i = 0, then firstNumber = "5" and secondNumber = "4"
                        // total = 5 + 4;
                        // total = 9;
                        int total = firstNumber + secondNumber;

                        // every time you reach the end of a loop, all of the variables and data used will be reset unless they're saved to a variable or collection declared outside of it the scope (aka the curly brackets {} of the For loop)\
                        // so we're going to add the total to the array that we declared outside of the For loop. The [i] will put the total in the correct position within the array itself
                        intarray[i] = total;
                    }

                    // this part is tricky but needed
                    // we have a for loop nested (inside) a second for loop. notice that the iteration variables are different (the outer being "i" and the inner "j"). 
                    // what we're doing here is comparing each of the totals in the array with themselves. Here's an example of what's happening

                    // the following is how the logic works and is separate from our example (since our example will produce a correct response and the following will not):
                    // say we have an array that has [5, 8, 10]
                    // we want to compare 5 with 5, 5 with 8, 5 with 10 to see if they match
                    // then we want to see if 8 with 5, 8 with 8, 8 with 10, and so on
                    // the outer For loop (with "i") will be the 5; the inner For loop (with "j") will then compare each number with that 5.
                    // if at any point the numbers do not match (which will happen when 5 and 8 are compared, the "result" boolean will become false, thus determing the user's input was bad
                    // when it's finished, the "i" will increase by 1 and will go to the second position in the array (the 8 in this instance).
                    // we'll re-enter the "j" For loop again but comparing each number of the array with the number 8, and so on
                    // in our over example, the array is [9, 9, 9] so "result" will remain true

                    for (int i = 0; i < intarray.Length; i++)
                    {
                        for (int j = 0; j < intarray.Length; j++)
                        {
                            if (intarray[i] != intarray[j])
                            {
                                result = false;
                            }
                        }
                    }

                    // this is where we determine whether or not
                    // in our example, "result" stayed true and the program will therefore pass! cool beans
                    if (result == true)
                    {
                        Console.WriteLine("IT WORKED! GOOD JOB! Please any key to exit program...");
                        Console.ReadLine();
                        // Here's how we stop the program from running aka make the while loop become false. "break" exits the loop that it's placed in. This "break" it will exit the program entirely
                        break;
                    }
                    else
                    {
                        Console.WriteLine("This failed... Please any key to exit program...");
                        Console.ReadLine();
                        break;
                    }
                }
                //if the user entered numbers that were not equal in length, we would have them re-enter them
                else
                {
                    Console.WriteLine("Please enter two numbers that are of the same length. Enter any key to restart program...");
                    Console.ReadLine();
                    Console.Clear();
                }


                // That's it. This program will run and perform the task of comparing sets of numbers. 
                // I still think this is a lot for day 1 so please PLEASE look at each part of this and do research. 
            }