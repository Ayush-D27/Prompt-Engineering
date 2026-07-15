# Temperature Effect on GPT

## Objective
To generate responses using different temperature values using a GPT model and observe how the temperature parameter affects the generated output.

## Model Used
- distilgpt2 (Hugging Face Transformers)

## Platform
- Google Colab

## Libraries Used
- Python
- Transformers
- Torch

## Prompt
**Artificial Intelligence is**

## Temperature Values
- 0.2
- 0.7
- 1.2

## Observations

### Temperature = 0.2
- Generated a more focused and predictable response.
- Less randomness and higher consistency.

### Temperature = 0.7
- Produced a balanced response with moderate creativity.
- More detailed while maintaining coherence.

### Temperature = 1.2
- Generated a more creative and diverse response.
- Higher randomness with less predictable output.

## Conclusion
The temperature parameter controls the randomness of text generation. Lower temperature values produce more deterministic and consistent responses, while higher values generate more creative and varied outputs. The choice of temperature depends on the application, such as factual tasks, general conversation, or creative content generation.
