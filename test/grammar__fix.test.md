### Fix grammar issues

```timeout
30000
```

```file:input.txt
One of the most important issue is the lack of parking spaces at the local mall.
If you don’t mind, I’d prefer leave early tomorrow.
Do you have a few minutes to discuss about this project?
Although I’ve known him for a while, I still can’t believe how much stubborn he is.
Would you like to take part of this activity?
```

```execute
cat input.txt | aux4 grammar fix
```

```expect
One of the most important issues is the lack of parking spaces at the local mall.
If you don't mind, I'd prefer to leave early tomorrow.
Do you have a few minutes to discuss this project?
Although I've known him for a while, I still can't believe how stubborn he is.
Would you like to take part in this activity?
```

### Fix grammar issues and save to file

```timeout
30000
```

```afterAll
rm -f output.txt
```

```file:input2.txt
She don't like going to the gym on weekends.
The team are working hardly to meet the deadline.
```

```execute
cat input2.txt | aux4 grammar fix --save output.txt && cat output.txt
```

```expect
She doesn't like going to the gym on weekends.
The team is working hard to meet the deadline.
She doesn't like going to the gym on weekends.
The team is working hard to meet the deadline.
```
