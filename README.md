# SGPool
Lottery random numbers generators with algorithm rules.

The algorithms such as Mod10, Odd Even sequence, Sum, Contains (and the variants), Exclude Draw will determine the output numbers. For example if you want the output number to have sum in range of 140 to 200, use `-SUM 140 200`, and  if you want to select 5 numbers out from a series of numbers use `-CONTAINOR 2,3,5,8,9,10,17,20,24,32,39,41,48 5` which 1 more number is any number and if you combine both switches it will generate numbers with the sum to be in 140 to 200 which 5 numbers are gotten from that sequence. 

The numbers being output is a lot but combining different algorithm will result in lesser numbers. Example, we can add another algorithm of adding all numbers together which reaches single digit of 6, `-ONLYMOD 6`. By using these algorithms and doing elimination, numbers generated are lesser but with lesser winning rate.

Above example resulting in
```
SGPool toto math -ALLCOMB -SUM 140 200 -CONTAINOR 2,3,5,8,9,10,17,20,24,32,39,41,48 5 -ONLYMOD 6 -input TotoResult.csv -output 3755.txt
```

## Requirement
1. After having `SGPool` file downloaded from bin folder
2. You will need the latest toto result data by running the program using command line with below switches
```
SGPool toto download TotoResult.csv
```
3. The process takes a lot of time which requires internet connection, console will not print any information during the time, after it finishes the file TotoResult.csv will exist which will be used to generate lottery numbers
4. When the software rerun the same statement with same filename, the file will be appended with missing result and will not redownload previous downloaded result

## Usage
```
SGPool toto math [algorithm switches...] [ending switches...]
```
For usage of the program starts running it in Console (Command Prompt) with `SGPool toto math` switches, the switches then accept Algorithm Switches such as `-ALLCOMB` to generate all possible random numbers filter with other algorithm switches, then it will follow with Ending Switches 

### Ending Switches
`-INPUT [Filename]` for accepting input file containing draw history which is required by some algorithms
`-OUTPUT [DrawNo].txt` switch is used to output to file beside the console (optional)
`-WITHOUTONE` which is used to filter out ball 1 from the numbers generated (optional).

## Algorithm Switches

### `-ALLCOMB`
This switch must be the first switch to be pass to the program following by algorithm rules, this switch means that the program will generate all possible 6 permutations of number between 1-49.

### `-MOD10 [MaxDraw]`
Mod10 means that it will sum up a set of number, for example :1,2,3,4,5,6 which sum to 21 and reduce it to single digit, which means 2+1=3 which is single digit, so mod10 of that set of number is 3. This switch is used with [MaxDraw] for example 3, which means it will exclude Mod10 from last 3 draws, for example last 3 draws result in Mod10 of 2,5, and 7, then the number generated with this `-MOD10 3` switch will get only set of number that generates to Mod10 of 1,3,4,6,8, or 9.

This switch need an input file that contains last [MaxDraw] lottery result, which uses ```-INPUT [Filename]``` switch such as ```-INPUT TotoResult.csv```
  
### `-ONLYMOD [Number]`
ONLYMOD means that it will only generate set of numbers which sum up to Mod10 of [Number].
  
### `-ODDEVEN [MaxDraw]`
OddEven means that based on 6 numbers generated it will sort the number followed by determining the Odd and Even of the number, if Even it is 0, Odd is 1. So 1,2,3,4,5,6 result in 1,0,1,0,1,0.
  
Then pass with [MaxDraw] 3, it will exclude set of numbers that generated to the OddEven of the last 3 draws.

This switch need an input file that contains last [MaxDraw] lottery result, which uses ```-INPUT [Filename]``` switch such as ```-INPUT TotoResult.csv```

### `-ONLYODDEVEN [Sequence]`
It will generate number that has the OddEven of the OddEven [Sequence]

### `-EXCLUDEDRAW [MaxDraw] [AmountTolerate]`
It will exclude numbers that is drawn from the last [MaxDraw] draws, if however it contains only maximum of [AmountTolerate] same numbers from those draws, the set of number will still be generated, the number will not be generated when it exceed the tolerable amount.
  
For Example last 3 draws are "1,2,3,4,5,6", "7,8,9,10,11,12", "13,14,15,16,17,18" then if the [AmountTolerate] is 0, it will generate only number starts with 19-49 permutation, if it is for example 2, it will allow 2 same balls from those balls.

This switch need an input file that contains last [MaxDraw] lottery result, which uses ```-INPUT [Filename]``` switch such as ```-INPUT TotoResult.csv```

### `-CONTAINOR [Sequence] [MinAmount]`
ContainOr will generate set of numbers from [Sequence] of balls and show sets that only has [MinAmount] of those balls.
  
For Example [Sequence] is "1,2,3,4,5,6,7,8,9,10,11,12" and [MinAmount] is 5. So it will Generate number "1,2,3,4,5,X" or "2,3,4,5,6,X" etc where the remaining X is any numbers.
  
### `-CONTAINAND [Sequence]`
ContainAnd will generate set of numbers that must contains all the numbers in the [Sequence].

For Example [Sequence] is "12,17,21" so the set generated will contains "12,17,21,X,Y,Z" which means it will only generate numbers which contains the sequence plus some remaining other numbers.

### `-NOTCONTAIN [Sequence]`
NotContain will skip any set of numbers containing any of the number in the [Sequence].

For Example [Sequence] is "1,49", so the set generated will not contain ball 1 and ball 49.

### `-FILTERTEN [Number]`
Numbers in range of 1-49 start with 0-9, 11-19, 20-29, 30-39, 40-49 which means there are 5 maximum division, if FilterTen is pass with 5, number in the group of all division will be shown and will not show set of numbers that skip division range for example 10-19. FilterTen works with minimum if it is pass with 3, minimum 3 of the division will be shown. 

### `-ONLYTEN [Number]`
Same with FILTERTEN but it will only show numbers that has exact [Number] of division.

### `-SUM [Min] [Max]`
Only show numbers which sum to have value in between [Min] and [Max]
