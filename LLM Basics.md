# 📘 Notes: AI & LLM Basics

---

## 🔹 Learning Goals
- Learn tokens  
- Understand prompting strategies  
- Why LLMs hallucinate  
- How LangChain fits into AI application development  

---

## 🛠️ Mini Project
- **Prompt-only Q&A Bot**  

---

## 🎯 Topics Breakdown

### 1. Learn Tokens

#### Conceptual Overview
| Concept | Simple Explanation | Example |
|---------|--------------------|---------|
| **Token** | A small chunk of text that an LLM reads | Words, sub-words, or characters |
| **Why important** | LLMs don’t read sentences directly → they break text into tokens first | `"ChatGPT is great!"` → `[ "Chat", "G", "PT", " is", " great", "!" ]` |
| **Tokenization** | Process of splitting text into tokens | Different models tokenize differently (GPT vs BERT vs LLaMA) |
| **Token limit** | Maximum number of tokens per model (context window) | GPT-4o: ~128k tokens |
| **Token cost** | APIs charge per 1k tokens (input + output) | 1 token ≈ 4 chars → 1k tokens ≈ 750 words |

#### How Tokenization Works
| Section | Step / Point | Example / Note |
|---------|--------------|----------------|
| **Input text** | `"Rajinikanth is the superstar!"` | - |
| **Tokenizer splits** | `["Raj", "ini", "kanth", " is", " the", " superstar", "!"]` | - |
| **Model processes tokens** | Converts into IDs (numbers) | - |
| **Generation** | Predicts next token until stopping | - |

#### Why Tokens Matter
| Aspect | Key Point |
|--------|-----------|
| **Prompt length** | You can’t exceed the model’s context window |
| **Cost** | More tokens = higher API bill |
| **Control** | Explains weird splits (e.g., `"playing"` → `["play", "ing"]`) |
| **Streaming** | Models generate one token at a time |

#### Advanced Considerations
| Topic | Key Point | Why It Matters |
|-------|-----------|----------------|
| **Granularity** | Tokens are not always full words (sub-words, chars) | `"playing"` → `["play", "ing"]` |
| **Languages** | Some languages (Chinese, Tamil) require more tokens | Higher cost, context usage |
| **Whitespace & punctuation** | Spaces, commas, periods are tokens | Formatting increases cost |
| **Context Window** | Input + output tokens together count toward limit | 8k model: 7.5k input → only 500 output |
| **Truncation** | Longer than context → older tokens dropped | Risk of losing info |
| **Compression tricks** | Use shorter wording to save tokens | Reduces cost, frees space |
| **Embeddings** | Tokenization applies to embeddings too | Critical for RAG apps |
| **Streaming** | One token at a time | Enables real-time output |
| **Pricing** | Per 1k tokens (input + output separately) | Essential for cost planning |

---

### 2. Prompting Strategies

#### Core Strategies
| Strategy | Explanation | Example Prompt | Expected Behavior |
|----------|-------------|----------------|------------------|
| **Zero-shot** | Ask directly without examples | *“Translate ‘How are you?’ to French.”* | Model uses pre-trained knowledge |
| **Few-shot** | Provide examples to guide | *“Translate: ‘Good morning’ → ‘Bonjour’; ‘Thank you’ → ‘Merci’. Now: ‘How are you?’”* | Model follows pattern |
| **Chain-of-thought (CoT)** | Force reasoning step-by-step | *“If 3 apples, eat 1, how many left? Think step by step.”* | Explains reasoning → final answer |

#### Applied to Data Science
| Strategy | Explanation | Example Prompt | Expected Behavior |
|----------|-------------|----------------|------------------|
| **Zero-shot** | Direct classification | *“Classify: ‘The product was amazing!’”* | *Positive* |
| **Few-shot** | Guided classification | *“I love this → Positive; Worst experience → Negative; Now: ‘Not bad, but could be better’”* | *Neutral* |
| **Chain-of-thought** | Step-by-step reasoning | *“Store sold 120 shoes, 1/3 sneakers. How many sandals?”* | *Explains: 40 sneakers, 80 sandals* |
| **Zero-shot + CoT** | Direct with reasoning | *“Summarize this dataset step by step before a 2-line summary”* | Outline → Summary |
| **Few-shot + CoT** | Examples + reasoning | *“Convert English to SQL: ‘Count users’ → SELECT COUNT(*) FROM customers; Now: ‘Get total revenue.’ Think step by step.”* | SQL with reasoning |

---

### 3. Why LLMs Hallucinate

| Cause | Explanation | Example | Data Science Angle |
|-------|-------------|---------|--------------------|
| **Limits of training data** | Only “knows” patterns from training | Asked about 2025 dataset → makes it up | Like classifier on biased data |
| **Lack of grounding** | No fact-checking | Invents fake research title | Predictions without real-time DB |
| **Ambiguous prompts** | Vague → model guesses | “Tell me about Python” → language/animal | Bad feature engineering |
| **Overconfidence** | Doesn’t show uncertainty | Wrong SQL confidently | Regression w/o error bars |
| **No reasoning verification** | Skips steps | Wrong math result | Pipeline errors w/o validation |

---

### 4. Controlling Hallucinations

| Method | Explanation | Example | DS Angle |
|--------|-------------|---------|----------|
| **RAG** | Add external knowledge (docs, DBs, APIs) | *“Summarize this PDF”* → pulls from doc | Like feature augmentation |
| **Prompt engineering** | Write clear, unambiguous prompts | *“Explain Python (language) in 3 points”* | Like feature engineering |
| **Output validation** | Enforce structured formats | *Return JSON {“name”: str, “year”: int}* | Schema validation |
| **Chain-of-thought (CoT)** | Force step-by-step reasoning | *“56 ÷ 8 × 2. Show steps.”* | Logging intermediate steps |
| **Human-in-the-loop** | Human review for critical tasks | Analyst checks summary | Manual label validation |
| **Fine-tuning / domain adaptation** | Train on domain data | Medical bot trained on clinical notes | Transfer learning |
| **Confidence estimation** | Add thresholds/fallbacks | *If similarity < threshold → say ‘I don’t know’* | Probability thresholds |

---

## 📌 Summary
- **Tokens** = basic units of LLM processing (affect cost, performance, context).  
- **Prompting strategies** = zero-shot, few-shot, chain-of-thought, hybrids.  
- **Hallucinations** = caused by data limits, lack of grounding, ambiguity, overconfidence.  
- **Control hallucinations** = use RAG, better prompts, validation, reasoning, human checks, and fine-tuning.  

---
