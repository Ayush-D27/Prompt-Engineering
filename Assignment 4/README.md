# Assignment 4: Comparing a Base Model and a Fine-tuned Model

## Objective
The objective of this assignment is to compare the outputs of a **pre-trained (base) language model** and a **fine-tuned (instruction-tuned) language model** using the same prompts. This comparison helps analyze how fine-tuning improves a model's ability to understand and follow user instructions.

---

## Models Used

### Base Model
- **Model:** DistilGPT-2
- **Hugging Face:** `distilgpt2`
- **Type:** Pre-trained Language Model

### Fine-tuned Model
- **Model:** Qwen2.5-0.5B-Instruct
- **Hugging Face:** `Qwen/Qwen2.5-0.5B-Instruct`
- **Type:** Instruction Fine-tuned Language Model

---

## Prompts Used

1. **Explain Artificial Intelligence in about 100 words.**
2. **List five advantages of cloud computing.**

The same prompts were provided to both models to compare their responses.

---

## Comparison of Models

| Feature | Base Model (DistilGPT-2) | Fine-tuned Model (Qwen2.5-0.5B-Instruct) |
|---------|---------------------------|------------------------------------------|
| Model Type | Pre-trained | Instruction Fine-tuned |
| Instruction Following | Moderate | Excellent |
| Response Quality | General text generation | More accurate and informative |
| Response Structure | Less organized | Well-structured and coherent |
| Clarity | Moderate | High |
| Accuracy | Moderate | High |
| Readability | Average | Excellent |
| Overall Performance | Good | Better |

---

## Observations

### Prompt 1: Explain Artificial Intelligence
- **Base Model:** Generated a general continuation of text but did not fully focus on the requested explanation.
- **Fine-tuned Model:** Produced a clear, accurate, and well-structured explanation by effectively following the instruction.

### Prompt 2: List Five Advantages of Cloud Computing
- **Base Model:** Generated less organized content and may miss important points.
- **Fine-tuned Model:** Produced a clear and structured list of relevant advantages.

---

## Conclusion

The comparison demonstrates that the **fine-tuned model performs significantly better than the base model** for instruction-based tasks. It generates responses that are more accurate, organized, relevant, and easier to understand. Fine-tuning enhances the model's ability to interpret user prompts and produce high-quality outputs, making it more effective for practical natural language processing applications.
