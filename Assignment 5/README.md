# Exploring the Gemini API Generation Parameters

## Problem Statement

To explore and understand different generation parameters of the Gemini API and observe how they affect the generated response.

## Objective

The objective of this assignment is to understand important Gemini API generation parameters such as **Temperature, topP, topK, maxOutputTokens, stopSequences, responseLogprobs/logprobs, and Streaming**.

---

## Generation Parameters

### 1. Temperature

**What it does:**
Temperature controls the randomness or creativity of the model's response.

* Low temperature → More predictable and consistent responses.
* High temperature → More varied and creative responses.

---

### 2. topP

**What it does:**
topP controls the range of likely tokens considered by the model based on their cumulative probability.

* Lower topP → Fewer possible choices.
* Higher topP → More possible choices.

---

### 3. topK

**What it does:**
topK limits the model to the **K most likely tokens** when generating each next token.

Example:

```python
top_k = 5
```

This means the model considers the 5 most likely tokens.

---

### 4. maxOutputTokens

**What it does:**
maxOutputTokens sets the maximum number of tokens that the model can generate.

The following values were tested:

```python
max_output_tokens = 20
max_output_tokens = 50
max_output_tokens = 100
```

* 20 → Short response
* 50 → Longer response
* 100 → More space for generating the response

---

### 5. stopSequences

**What it does:**
stopSequences tells the model to stop generating when a specified sequence is reached.

Example:

```python
stop_sequences = ["END"]
```

When the model generates the specified stop sequence, generation stops.

---

### 6. responseLogprobs / logprobs

**What it does:**
These parameters provide information about the likelihood of the generated tokens.

Example:

```python
response_logprobs = True
logprobs = 5
```

Here, `response_logprobs` enables log-probability information, while `logprobs = 5` requests information about the top 5 candidate tokens.

---

### 7. Streaming

**What it does:**
Streaming returns the model's response in small parts while it is being generated instead of waiting for the complete response.

**Without streaming:**

```text
Request → Complete response
```

**With streaming:**

```text
Request → Part 1 → Part 2 → Part 3 → Complete response
```

---

## Summary Table

| Parameter                   | Purpose                                               |
| --------------------------- | ----------------------------------------------------- |
| Temperature                 | Controls randomness and creativity                    |
| topP                        | Controls token selection using cumulative probability |
| topK                        | Limits the number of likely token choices             |
| maxOutputTokens             | Sets the maximum output length                        |
| stopSequences               | Specifies when generation should stop                 |
| responseLogprobs / logprobs | Provides token likelihood information                 |
| Streaming                   | Returns the response progressively                    |

## Conclusion

The Gemini API provides several generation parameters that give developers control over the model's output. Temperature controls randomness, topP and topK control token selection, maxOutputTokens controls response length, stopSequences controls when generation ends, logprobs provide token probability information, and streaming allows responses to be received progressively.
