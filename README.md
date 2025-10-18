#SLM Paper - Initial Sketch

## Thoughts

1. Why is deepseek underperforming ? 
2. Has the model been fine tuned or wikll fine tuning perform better ? 
3. Does longer solution correlate to good solve ? 
4. Are thinking models generally udnerperforming ? 
5. Does deepseek lack a proper parser in the pipeline ? 
6. Why do we need Semantic Consistency here ? 
7. What if we implement Langchnain Sequential chain ? 

## 1

- Use phi-14b dataset with their exact methods to reproduce the results

## 2

- Test to see if deepseek having the same issue

## 3

- Try to parse deepseek differently

## 4

- Try Agentic method combining thinking and coding models

## 5

- Use distilled models of LLMs ?

## 6

- Try Error correction by recursive method ?

# Work done till now :

1. Reproduced the results (Phi - 14B - 1 Language) 
2. Trying Changin Prompt for Deepseek —( Worsens Score) 
3. Trying to utilize thinking models to prune syntax errors after generating (WIP)
