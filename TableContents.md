# Table of Contents

## Introduction
Last year I learned about hardware hacking and was looking for a way to get into the practice. I stumbled across this wonderful [article](https://trustedsec.com/blog/hacking-the-my-arcade-contra-pocket-player-part-i) which demonstrated how to pull Flash data from the MyArcade Contra Console. The article ended with a promise of a part 2, that would demonstrate how to install game ROMs onto the MyArcade Contra console. However, given the fact that the article was written in December of 2021 and (at the time of working on this project) it was 2023, I assumed that part 2 would never come. So for the next year I messed arround with the MyArcade Contra console with two goals in mind:

1. Load separate ROMs onto the console
2. Compile and load my own programs onto the console

After a year of work I have met these goals and am writing this article in the hope that anyone with similar aspirations can use this as a fallback if they get stuck. 

## The Basics
1. Reading the Flash Memory
2. Modifying the Flash Memory
3. Enabling UART
4. Connecting to UART

## Advanced
1. Compiling for the Console
2. SDL2 modifications
3. Adding ROMs