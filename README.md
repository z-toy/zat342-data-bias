# zat342-data-bias

The goal of this assignment was to explore the concept of bias through querying an existing natural language processing model — specifically, the Perspective API released by Google Jigsaw. For this assignment, I examined a dataset of internet comments and their scores and also formulated my own queries and using the Perspective API client to score the toxicity of each comment.

After exploring the sample dataset and parsing through it, I used the first 200 toxic comments and their Perspective API toxicity calulcation to determine a threshold for whether a comment will be considered toxic or not. Because the average score for toxic comments was about 0.70, I chose this to be our threshold for the model. Given the Perspective API's documentation, this would indicate that a comment is considered toxic when 7/10 people indicate it as so. Per the documentation's recommendations, "For social science researchers using Perspective to study harassment, we recommend experimenting with thresholds of 0.7 or 0.9, similar to typical moderation use cases."

Hypothesis: the Perspective API will fail if we incorrectly spell common swear words.

For the hypothesis testing step, I chose to create a test score function that allowed me to input a sample comment and output the toxicity score. To test my hypothesis, I first inputted a mean comment with a common toxic word and generated its toxicity score. Then, I inputted that same mean comment but slightly misspelled the toxic word.

The results of my testing showed that, for all 12 of my samples, my hypothesis was to some extent correct: the Perspective API will fail if we incorrectly spell common swear words. For example, the word "stupid" generated a toxic score of 0.78 while "stoopid" generated a score of 0.66. In this case, the Perspective API scored "stupid" above the threshold for toxic, while its counterpart, "stoopid", was scored below the threshold and would be deemed not toxic.

While not every test showed this difference in toxicity when it comes to the threshold (that is, sometimes even the misspelled comments scored above 0.70), the slightly misspelled toxic comments were consistently lower in every test. The findings suggest that the Perspective API could be biased towards only common curse words (i.e. non-slang versions) and begins to be less effective at spotting and scoring toxic comments when toxic words are slightly misspelled, shortened, or in a slang version.

As for my theories about why I got these results, I think that a possible reason could be that slang versions of curse words are more difficult to identify since new slang is always circulating and changing. When it comes to solving this problem, if there were some way to identify if a word sounded similar to a curse word (ex. "hoe" vs "ho"), then this issue could be resolved. Additionally, I think it is difficult for Perspective to identify when a curse word is slightly misspelled; however, if there were a way to use something like spell-check to help find common errors in curse words than the toxic words could be detected more effectively.
