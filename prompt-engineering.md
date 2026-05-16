# Prompt Engineering Interview — 9 Core Concepts


### 1. Zero-Shot & Few-Shot Prompting
No examples vs 1–5 examples in prompt
- Pros: Instant · Cons: Less precise
- Best for: Quick tasks

### 2. Chain-of-Thought (CoT)
"Think step-by-step" forcing
- Pros: Better reasoning · Cons: More tokens
- Best for: Math / logic

### 3. Tree-of-Thoughts (ToT) & Graph Reasoning
Multiple reasoning branches
- Pros: Complex problem solving · Cons: Compute heavy
- Best for: Planning

### 4. ReAct Prompting
Reason + Act in one prompt
- Pros: Agent-like behavior · Cons: Can loop
- Best for: Tool-using tasks

### 5. System Prompts & Role Prompting
"You are an expert…" — clear job title & rules
- Pros: Consistent tone · Cons: Overfitting to prompt
- Best for: Chatbots

### 6. Prompt Chaining & Pipelines
Break big task into sequential prompts
- Pros: Modular · Cons: More API calls
- Best for: Complex workflows

### 7. Prompt Optimization Techniques
Compression, automatic optimization tools
- Pros: Lower cost · Cons: Slight quality drop
- Best for: Production

### 8. Evaluation of Prompts
LLM-as-judge, A/B testing
- Pros: Data-driven · Cons: Subjective
- Best for: Iteration

### 9. Defensive Prompting
Guardrails inside the prompt
- Pros: Safer outputs · Cons: Longer prompts
- Best for: High-stakes use

### Quick Map
- Zero/Few-Shot → basics
- CoT → reasoning
- ToT → exploration
- ReAct → action
- System Prompts → consistency
- Chaining → modularity
- Optimization → efficiency
- Evaluation → quality
- Defensive → safety
