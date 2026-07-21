# Understanding Token Log Probabilities

## Objective
To understand how a GPT model assigns probabilities to each generated token by analyzing token-level log probabilities, probabilities, cumulative probabilities, and color codes.

## Model Used
- distilgpt2 (Hugging Face Transformers)

## Platform
- Google Colab

## Libraries Used
- Python
- Transformers
- Torch
- Math

## Features
- Accepts a prompt from the user.
- Generates a response using a GPT model.
- Retrieves the log probability of every generated token.
- Calculates the probability of each token.
- Computes cumulative probability.
- Assigns a color code (Green, Yellow, or Red) based on the token probability.

## Probability Color Codes
- **Green:** Probability ≥ 0.50 (High Confidence)
- **Yellow:** Probability ≥ 0.20 and < 0.50 (Medium Confidence)
- **Red:** Probability < 0.20 (Low Confidence)

## Sample Prompt
```
Artificial Intelligence is
```

## Output
The program displays:
- Token
- Log Probability
- Probability
- Cumulative Probability
- Color Code

## Conclusion
This assignment demonstrates how a GPT model predicts the next token by assigning probabilities to possible words. Log probabilities help measure the model's confidence, while cumulative probability shows the combined likelihood of the generated sequence. Color coding provides an easy way to visualize the confidence level of each generated token.
