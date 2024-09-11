# Rishikesh
Run the Pig Latin Scripts to find word count
-- Load the data from a text file
data = LOAD 'input.txt' USING PigStorage() AS (line:chararray);

-- Tokenize the lines into words
words = FOREACH data GENERATE FLATTEN(TOKENIZE(line)) AS word;

-- Group the words and count them
word_groups = GROUP words BY word;
word_counts = FOREACH word_groups GENERATE group AS word, COUNT(words) AS count;

-- Store the result in an output file
STORE word_counts INTO 'output' USING PigStorage(',');


