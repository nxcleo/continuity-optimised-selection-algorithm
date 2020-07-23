# continuity-optimised-selection-algorithm
Finding ways of splitting a set of units while maximising continuity 
The algorithm has many uses and I found it useful in optimising room selection when booking across time to maximise continuity and minimise moving from room to room.
Here it is used to break up the unspaced string into words with a dictionary.
![image](https://github.com/nxcleo/continuity-optimised-selection-algorithm/blob/master/splitting.png)
 
The dynamic programming approach uses 2 lists of length len(message), representing a row from the table above. As only the previous row is required and not the entire table, only 2 of these lists are required (named current and previous). At the start, previous is set to default value of 0s.
Each cell is a list that holds two values, first being the length of the word currently matched with, and the second being the index of where the next word would start.
For each word in the dictionary, the algorithm completes 2 passes through the current list. 
1.	Find matches with current word. For each character in the message, the algorithm would check if the given word could be made starting from said character. If it is possible, the cells matching would be set to the appropriate values (length of word and index of the next cell after the word).
2.	Merging the current row with the previous row. This is done with sections, a section is a range in the current or previous list where the words extend over each other and words are mutually exclusive. i.e. the following previous current list pair would be split into sections as so:
 
![image](https://github.com/nxcleo/continuity-optimised-selection-algorithm/blob/master/segments.png)
If in a section the previous has higher matched character count, it would replace the section in current. Tie is broken by the section with less words as longer words are preferred. 
The final word is pieced together by following the indexes of next word in the list, adding a space after each word and dealing with the zeros which means no match.

Time complexity: O(kNM)
        for every word in the dictionary (N):
            iterate through letters in the unspaced message twice,
            first pass(k):
                check if the string is equal to the current word (M)
            second pass: combine with the results of previous word(2k)    
    

Space complexity: O(k + NM)
requires NM to store the dictionary words
requires two lists of length k, each element is a list of size 2. did not use a table as only the previous row was required.
