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
