## Python codes for Bioinformatics:

#### 1. Create a code to compare two DNA sequences and calculate the percentage of resemblance:
```py
seq1 = "ACCGTCT"
seq2 = "ACCATCA"

# Initiate required variables for counting:
matches = 0
missmatches = 0
baseseq2 = 0 # Index of seq2

for base in seq1:
    if seq2[baseseq2] == base:  # If sequence2[base position changing from 0 to the length of seq1]
                                # is the same as base in sequence1...
        matches+=1                # increment matches
        baseseq2+=1                  # increment seq2 index
    else:                       # If not the same...
        missmatches+=1            # increment missmatches
        baseseq2+=1                  # increment seq2 index

# Calculate the percentage of resemblance:
total = (matches*100)/(matches+missmatches)

# Output:
print(f"""Matches: {matches}
Missmatches: {missmatches} 
Calculation: {"{:.2f}".format(total)}%""")  # The expression {:.2f}".format(x) 
                                            # limits float output to two decimal points
```

Results:
```
    Matches: 5
    Missmatches: 2 
    Calculation: 71.43%
```

The previous would work well for sequences of the same length. However, if the seq1 is longer than the seq2 we get an error:
```
    IndexError: string index out of range
```

This happens when the program tries to index seq2 further than it can reach the seq2 length.<br>
Therefore, if we modify the code to make the iteration with the length of the shortest sequence it should be:
```py
seq1 = "ACCGTCTAATTTAC"
seq2 = "ACCATCAAAA"

# Calculate longest sequence (for sequences of different lengths 
#                             to iterate using the shorter one):
# Initialize variables:
shortestseq = seq1
otherseq = seq2

# Compare lengths and reassign variables if needed:
if len(seq1) > len(seq2):
    shortestseq = seq2
    otherseq = seq1
```

> NOTE! It's important to change the variable names in the rest of the code:
>- `seq1 > shortestseq`
>- `seq2 > otherseq`
>```
>for base in shortestseq:
>    if otherseq[baseseq2] == base:
>```

#### 2. Turn the previous into two functions and the seq1 and seq2 are given by the user:
Function to calculate the longest sequence:
```py
def longestseq (sequence1, sequence2):
    """Calculate longest sequence (for sequences of different lengths
                                    to iterate using the shorter one)
    Args:
        sequence1: Sequence number 1 
        sequence2: Senquence number 2
    
    Returns:
        shortestseq: the shorter sequence
        otherseq: the longer sequence
    """

    # Initialize variables:
    shortestseq = sequence1
    otherseq = sequence2

    # Compare lengths:
    if len(sequence1) > len(sequence2):
        shortestseq = sequence2
        otherseq = sequence1

    return shortestseq, otherseq
```

Function to calculate the resemblance:
```py
def resemblanceCalc (seq1, seq2):
    """Calculate the percentage of resemblance between the two sequences
    
    Args: sequences 1 and 2.

    Returns: Results of calculation.
    """

    # Use the function created previously to obtain sequences by length
    shortestsequence, othersequence = longestseq(seq1, seq2)   

    # Initiate required variables for counting:
    matches = 0
    missmatches = 0
    baseseq2 = 0 # Index of seq2

    for base in shortestsequence:
        if othersequence[baseseq2] == base:  
            matches+=1                
            baseseq2+=1                 

        else:                       
            missmatches+=1           
            baseseq2+=1              

    # Calculate the percentage of resemblance:
    total = (matches*100)/(matches+missmatches)

    # Output:
    print(
f"""Matches: {matches}
Missmatches: {missmatches} 
Calculation: {"{:.2f}".format(total)}%""")  # The expression {:.2f}".format(x) 
                                            # limits float output to two decimal points
```

Change `seq1` and `seq2` for the user input and use the `resemblanceCalc` function with the sequences as parameters:
```py
seq1 = input("Enter the first sequence to compare: ")
seq2 = input("Enter the second sequence to compare: ")

resemblanceCalc(seq1, seq2)
```

Results:
```
    Enter the first sequence to compare: ACCGTCTAATTTAC
    Enter the second sequence to compare: ACCATCAAAA
    Matches: 7
    Missmatches: 3 
    Calculation: 70.00%
```

#### 2. Turn the previous into a function inside the DNA class:
```py

```