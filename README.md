# aquaq_challange
Coding puzzles from https://challenges.aquaq.co.uk/

## Found these while looking for some additional challenges that look like the Advent of Code challenges. These are a little different and are not from a person using Python by default, but pretty good. I will put a little about each challenge here

* 0 - What's a numpad? - You will generate a message from the input using the old texting/phone input method. I agree with the low difficulty rating listed on this one
* 1 - Rose by any other name - Change a string into an RGB hex color. I didn't know browsers would do that. Neat
* 2 - One is all you need - Remove some bad sections of data. Since the input is short, lots of ways to do this. I probably should have tried to come up with a regex, but just flipped the remaining list a bunch to search in reverse.
* 3 - Short walks - Move square by square until out of instructions. Similar to the easier map walks in Advent of Code
* 4 - This is good co-primen - There are not too many numbers and they are not too large, so a brute force method of doing this one works fine. I stopped there, but could see this with a much larger list with much larger numbers as a later day of Advent of code. Assuming there is a faster prime math way to resolve this
* 5 - Snake eyes - We need to rotate two dice a number of times as given by the input. Again, brute force is fine, and it's not too bad
* 6 - Let me count the ways - Find how many ways you can sum a number. Since we only count the sum of three numbers and the number is not too big we can do this with a two deep nested for, so not too bad.
* 7 - What is best in life? - You are scoring a ping pong tourney using the ELO chess scoring method. The only trouble here was getting the correct order in the (Rb-Ra) part. It was fun to read the Wiki page on chess scoring as I didn't know how they did that. The 400 and 20 constants can also be changed to fit your application and seem to be the middle tier constants used for chess
* 8 - Cron Flakes - Here you run through a daily routine of eating cereal and shopping for groceries. I think this would have a much easier rating except that the instructions have to be read very carefully. I needed to see that milk expires on the fifth day, after you use it and carefully do that part. Also, I needed to note that you are on your first shopping trip of the day when you give your answer, not the second shopping trip of the day (yes, you shop twice a day)
* 9 - Big Data? - Not for Python. Since Python automatically handles very large integers, this is trivial and should be rated 1.6 for Python users
* 10 - Troll Toll - Again, if you use Python and allow yourself the use of NetworkX this is probably a 2.5 level of difficulty. It is a fun one to do and I loved the phrase "how much to get Diddy his fiddy" and after the 2024 accusations, one asks, "What is the fifty for? ;-)"
* 11 - Boxed In - This one was medium hard only as it again requires a careful read and recall of the instructions. Remember you are looking for "total, contiguous tiles needed" not the count of overlapping tiles and not including sections outside the main one with overlaps
* 12 - A Day In The Lift - One needs to read the example very carefully here to get the correct intention. After that, not too bad and in-line with the posted difficulty. Reminds me of the state machine type problems in Advent of Code
* 13 - O RLE? - Count the recurring substring after possibly trimming the front and/or back of the string. Then sum the count for each line. This was not too bad to do brute force by finding all substrings and counting all the consecutive repeats, but it is a bit slow at an average of a couple seconds per line and about 1-2 minutes to get the answer. Each line is independent, so one could run each (or several) in parallel to speed things up if needed
* 14 - That's a bingo - Given a board, play each game until you win and sum the number of draws needed to win all games. Finishes quickly, so nothing tricky needed, but takes a bit of code to get a solution. Easy to understand what the challenge was looking for, which was nice
* 15 - word wore mare maze - You are supposed to change a word to another word, only changing one letter, until you arrive at a target word. After thinking a bit, I figured that I could use NetworkX again (the challenge actually says 'paths+graphs' so maybe it should have been obvious). That's true, but the trouble is in making the network quickly. I made it slowly by removing one word from the list of words given and comparing to all others to see if it was different by exactly one letter. If so, add an edge to the network between those two words. Keep doing this until the word list empties. This works, but takes over 30 minutes to create the network. I will make another version of this one to run faster and update. Until then...
  - The -2 version first breaks up the words into lists of the same length. This makes the comparison list shorter and we don't have to test for the same length in our function to find if the words are one character different. This version finishes in <10 minutes, so over a 3x speed up
  - The -3 version uses the same breakup, but uses numpy on the ord values to find all the one-off words faster. This takes about 75 seconds, so we are at at least a 25x speed up, but I was really hoping for 100x
  - For the -4 version I moved the conversion to integers while reading in the file and used a shorter np.uint8 type, but only gained a couple seconds. I tried to get numpy to work with blas at more than 2 threads on Windows, but totally failed to do anything other than use up a few hours of life. I did update the numpy part to only go over the part of the matrix that had not already been compared, and that got me to about 37 seconds. I'm going to give myself credit for a 50x speedup and call it a day
* 16 - Keming - I assume the name is a joke on a tight kern of 'r' and 'n' turning into an 'm'. You need to count spaces after doing kerning on a series of ascii art letters. Took some thinking and some code, but ran after minimum debugging and only took a couple seconds straight away
* 17 - The Beautiful Shame - You need to find which team had the largest number of days from a game with a score of 0 to a scoring game. I was trying to make this too hard, but still would give it a 4.0 even after thinking of a straight forward way to do it. It also had a read error where I had to force an encoding with the read() function
* 18 - Emit time - Find how many seconds away is the nearest palindromic time and sum those. There is probably a cleaner way to do this or to use a time module, but it ran in <10 seconds, so good enough and not too difficult
* 19 - It's alive - Find how many cells are alive after each game-of-life and sum them up. This was not too difficult, but was slow to run. The first version took 2491 seconds and was basic Python
  - The -2 version used NumPy and the SciPy convolution2d function. It ran ~8x faster, but still was not using all the CPU cores, similar to the puzzle 15 attempts. Using WinPython did not help as it also seems locked to 2 CPUs via used libraries
* 20 - Blackjack - Play consecutive games of blackjack with the input and count up the number of wins. Just had to remember the "all bust" condition check and then it was pretty straightforward and ran quick
* 21 - Clean Sweep - Find the vacuum path that collects the most dust. I would have given this another point of difficulty, but part of that was me not noticing that the vacuum width was 5 and not the 3 in the example. Still, it has to use a negative value path or be changed to a positive one and the cost has to be moved from node to edge (if you use NetworkX) and you have to group cells in the cost. Seemed worth a 5.0 to me
  - The -2 version was so that I could use the Dijkstra collection of NetworkX functions (which need positive edge costs) before I realized my width error. However, still useful as you can use a list of sources with one of the Dijkstra functions, which improves the runtime from about 5.1 seconds to about 0.7 seconds
* 22 - Veni Vidi Vitavi - First, puzzle name decoding. I'm going to trust the Chat GPT result here; "Veni Vidi Vici" is attributed to Caesar (makes sense as the puzzle text refers to the Caesar cipher) and means "I came, I saw, I conquered". The puzzle name means "I came, I saw, I avoided", which is like me using the roman module to make this challenge super easy, which matches the listed difficulty. You convert numbers to roman numerals, then convert each character of that to an integer starting with A=1 and sum those
* 23 - Fair Play - Use the Playfair cipher to decrypt the message. Pretty easy to follow the given encryption instructions and make a decryption function. Difficulty rating seems correct. Chat GPT says the decrypted phrase comes from a season five episode of The Simpsons
* 24 - Huff and Puff - Use Huffman encoding to get a compression scheme and use it to decode the message. So it was not hugely difficult, but was complicated in a couple ways: my first idea to use a heapq didn't work, because this is not supposed to be a balanced tree, so I needed to move to a tree class. Then, I tried to use a reasonable sort to keep the unprocessed parts in order, but the level of the name needed to be considered, so I needed to move to an insert with some conditions. So it ended up getting a little long and took some time, but will it prove to be tied as the "most difficult". There was also no runtime issue and it finished quick
* 25 - S'morse - Use Morse code to decipher the message. There were a few steps involved and it took some code, so I would have given it a 4.2 vs the 3.6 it got, but maybe those still going through the list at this point are better coders on average. I could have also cleaned this up a bit
* 26 - Typo Theft - This one was interesting for an unexpected reason. The numbers at the end of the input are very large. If this were Advent of Code in a later puzzle, this would indicate that just incrementing the number and checking the digits used would never work and you have to find some better search pattern for the answer. So I did that and first tried a bad approach of looking for the first valid swap the current, least significant digit with all the more significant ones. Unfortunately, this worked on the examples. Next, I came up with testing each of an increasing set of insignificant digits with the next digit and added an example to catch my error in my test input. This worked, but given the possibly tricky example set, I thought it was worth a 6.0 difficulty which is a lot more than the voted 4.5. However, what if the incrementing approach actually works?
  - In the -2 version, I try an easy incrementing version and it works in reasonable time. So I think that a bunch of folks did it the easy way and probably voted it about 3.5. A different input set could have made this a good bit harder
* 27 - Snake Eater - Find all connected words and sum all computed word values. I decided to feed the input into a network with NetworkX using (y, x) tuples as node names and the letter as a node value. Then I could look for the ends of the snakes by looking for the nodes with only one edge. After that, I could grab an end node, and look for the other end node that had a path to it. When I had the list of paths then I just needed to walk them and compute the word values. I think it was worth at least another point and, again,  I assume only better coders are left in the challenge set to give it a rating
* 28 - Hall of Mirrors - Find the encryption for the given string with the given hall-of-mirrors maze. After some minor fixing from test to actual input, it's pretty easy and I agree with the listed difficulty. I just made and walked the grid for each letter
* 29 - On the up and up - Find numbers with non-decreasing digits. Since this was rated so easy, I just tried the brute force way first and it worked. It took about five minutes and I tried up to 1M first to make sure I wouldn't have to wait too long. There should be a way to calculate this by digit position and if the target number would have had a couple more zeros, it would have forced this. Especially if using Python loops was your other option
* 30 - Take away a face up card and flip any next to it. Count up possible, winning starting positions. My first attempt was running way to slow to finish, but that was pretty much expected, so I moved to an attempt to cache the possible winning combinations that I had seen before. That had a bit of a false start because I did not set the size to none and the lru_cache library has a max size default of 128. After that was fixed, it was faster, but still was not finishing and was using up all the memory in the system with several of the longest lines still to go. So I moved to a true/false representation and re-wrote everything. This time it worked in less than five minutes.
  - v2 in the last rewrite, I noticed an error in the previous implementation. So I fixed that and reran the character based version. It ran in less than two minutes, so it was not required to move to the true/false method, just to code it correctly with the cache.
* 31 - Brandless Combination Cubes - Currently waiting to be finished on the home computer
* 32 - In Parenthesis - Find the number of lines that have balanced braces. This was pretty straight forward and I only needed to remember to check if any opening braces are left at the end of the line