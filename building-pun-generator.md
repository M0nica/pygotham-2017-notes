# Building a "Pun Generator" in Python

GitHub Repository for this talk [https://github.com/maxwell-schwartz/PUNchlineGenerator](https://github.com/maxwell-schwartz/PUNchlineGenerator)
 
 Scaffolding
 
 - user enters phrase
 - select scertain words (based on defined criteria)
 - find other words that sound like these (and other criteria)
 - replace words with similar sounding words
 - return to user
 - buffy the vampire slayor -> fluffy the vampire mayor

 Levenshtein Distance
 - method of measuring similarity between strings
 - based off of (charactver-level) edits
 - used for:
 	- 	autocorrect
	-  plagiarism detection
 	-  genomic sequence comparisons
- Looks at:
	- insertions
	- deletions
	- substitutions 	(insertion + deletions)
	- equal (substitutions) = cost = 0

The weight of cost for changes can be set to vary based on the type of change. 

Things get complicated easily when two words that are being compared are not the same length. As the cost will be higher than the actual minimum difference.

The solution to evaluate the difference in weight between words is the levenshtein distance algorithm


[FuzzyWuzzy](http://chairnerd.seatgeek.com/fuzzywuzzy-fuzzy-string-matching-in-python/) is a cool library for fuzzy string matching in Python [http://chairnerd.seatgeek.com/fuzzywuzzy-fuzzy-string-matching-in-python/](
http://chairnerd.seatgeek.com/fuzzywuzzy-fuzzy-string-matching-in-python/
)

In order to generate puns you have to look at more than just the actual letters due to phonetic differences between words.
ASCII options
- Arpabet Phonemes are unique combos of ASCII characters,

Need to compare phonetic similarities and the part of speech of the words. Want to replace words with the same part of speech.

