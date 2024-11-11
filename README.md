# Training language models to follow instructions with human feedback

Long Ouyang, Jeff Wu, Xu Jiang, Diogo Almeida, Carroll L. Wainwright, Pamela Mishkin, Chong Zhang, Sandhini Agarwal, Katarina Slama, Alex Ray, John Schulman, Jacob Hilton, Fraser Kelton, Luke Miller, Maddie Simens, Amanda Askell, Peter Welinder, Paul Christiano, Jan Leike, Ryan Lowe

## Introduction
Simply increasing the size of language models does not make them better at aligning with user intent, as they may still produce untruthful, toxic, or unhelpful outputs. This paper introduces InstructGPT, a model fine-tuned with human feedback to improve alignment with user instructions. By collecting labeled prompts and ranking model outputs, supervised learning and reinforcement learning were applied to make InstructGPT both smaller and more effective than GPT-3 in terms of truthfulness and toxicity reduction. The results indicate that fine-tuning with human feedback is a promising approach for enhancing language model alignment with user intent.

## Problem Statement and Approach
**Problem Statement**: The core issue is that standard LLMs, while trained on extensive data, lack alignment with user intent, often producing outputs that don’t match user expectations. This is due to a mismatch between their training objective (predicting text) and the goal of following user instructions accurately.
**Approach**: The authors propose using Reinforcement Learning from Human Feedback (RLHF) to train LLMs. Specifically, they introduce InstructGPT, a version of GPT-3 fine-tuned with human preferences.

<img width="774" alt="Screenshot 2024-11-11 at 12 49 29 PM" src="https://github.com/user-attachments/assets/70557873-98e1-466e-a7b8-10e57a7e995f">

* InstructGPT outputs are consistently preferred over GPT-3, even when the model size is smaller; labelers rate InstructGPT as more reliable and better at following instructions.
* InstructGPT improves truthfulness significantly, halving hallucination rates compared to GPT-3, and performs better on tasks that require fidelity to the input.
* The model reduces toxicity in outputs by around 25% compared to GPT-3 but does not significantly improve on bias-related benchmarks.
* Performance regressions on some public NLP datasets (alignment tax) are minimized by modifying the reinforcement learning from human feed-back (RLHF) fine-tuning procedure with pretraining adjustments.
* InstructGPT generalizes well to held-out labelers and is preferred similarly by those who did not contribute to training, suggesting broader applicability.
* Public NLP datasets like FLAN and T0 don’t capture real-world API prompt needs well; InstructGPT outperforms them in preference tests for practical language tasks.
* InstructGPT can generalize to instructions outside its training scope, such as code-related prompts and some non-English instructions, showing flexibility with minimal direct supervision.
* While InstructGPT still makes mistakes (e.g., hedging too much or missing false premises), fine-tuning with human preferences significantly enhances model alignment and usability.

<img width="660" alt="Screenshot 2024-11-11 at 4 34 47 PM" src="https://github.com/user-attachments/assets/4e790e42-362a-4a22-bb78-2308c977e813">

<img width="649" alt="Screenshot 2024-11-11 at 4 33 45 PM" src="https://github.com/user-attachments/assets/11555283-1057-4bd4-9e63-33271d8db41b">


## Key Research Questions
**Question 1**: “Why might reinforcement learning from human feedback be more effective for alignment than simply scaling up model size?”

**Possible Answer**: Reinforcement learning from human feedback (RLHF) is more effective for alignment than merely scaling up model size because it directly optimizes the model’s behavior to align with specific user preferences and instructions, whereas scaling up model size does not inherently improve the model’s ability to follow user intent. Larger models, such as the 175B parameter GPT-3, can still generate untruthful, toxic, or unhelpful outputs due to the mismatch between the traditional language modeling objective (predicting the next word) and the goal of aligning with user instructions. By incorporating human feedback, RLHF fine-tunes models to prioritize outputs that are helpful, honest, and harmless, as judged by human labelers. This targeted approach results in the 1.3B parameter InstructGPT model being preferred by human evaluators over the much larger GPT-3, demonstrating that fine-tuning with human feedback is crucial for producing aligned, user-focused responses.
   
**Question 2**: “How does the InstructGPT approach help reduce toxic or biased outputs, and what are its limitations?”

**Possible Answer**: The InstructGPT approach helps reduce toxic outputs by using reinforcement learning from human feedback (RLHF), where labelers rate model outputs for appropriateness and respectfulness. This process incorporates human preferences directly into the training, encouraging the model to generate safer and more user-aligned responses. InstructGPT achieves a roughly 25% reduction in toxic outputs compared to GPT-3, particularly when explicitly instructed to be respectful.


## Architecture Overview







## Critical Analysis: What was overlooked by the authors?
* **Limitations**: The authors address only specific alignment goals (helpfulness, honesty, and harmlessness), but broader ethical implications and potential misuse are less explored. The human labelers’ demographic limitations (primarily English-speaking, specific cultural contexts) may bias the model’s behavior.
* **Areas for Further Development**: Exploring multilingual capabilities and performance in real-world, non-English settings could expand applicability. Additionally, adversarial testing could further assess model robustness against harmful prompts.
* **Disputes and Errors**: While RLHF is generally well-regarded, there’s debate on whether it creates an “alignment tax,” where alignment-focused models trade off raw performance on certain tasks.


## Impact and Importance
* **Shaping AI Alignment Research**: This work is pivotal in demonstrating RLHF’s potential for aligning LLMs with human intentions, setting a foundation for safer, more reliable AI applications.
* **Influence on Subsequent Models**: InstructGPT laid groundwork for models like ChatGPT, showing that RLHF can help models achieve high user satisfaction on open-ended tasks.
* **Broader AI Landscape**: By providing a feasible approach to align models with ethical guidelines, this work encourages more responsible AI development, impacting sectors like customer service, education, and content moderation.
