# Training language models to follow instructions with human feedback

Long Ouyang, Jeff Wu, Xu Jiang, Diogo Almeida, Carroll L. Wainwright, Pamela Mishkin, Chong Zhang, Sandhini Agarwal, Katarina Slama, Alex Ray, John Schulman, Jacob Hilton, Fraser Kelton, Luke Miller, Maddie Simens, Amanda Askell, Peter Welinder, Paul Christiano, Jan Leike, Ryan Lowe

## Introduction
Simply increasing the size of language models does not make them better at aligning with user intent, as they may still produce untruthful, toxic, or unhelpful outputs. This paper introduces InstructGPT, a model fine-tuned with human feedback to improve alignment with user instructions. By collecting labeled prompts and ranking model outputs, supervised learning and reinforcement learning were applied to make InstructGPT both smaller and more effective than GPT-3 in terms of truthfulness and toxicity reduction. The results indicate that fine-tuning with human feedback is a promising approach for enhancing language model alignment with user intent.

## Problem Statement and Approach
**Problem Statement**: The core issue is that standard LLMs, while trained on extensive data, lack alignment with user intent, often producing outputs that don’t match user expectations. This is due to a mismatch between their training objective (predicting text) and the goal of following user instructions accurately.
**Approach**: The authors propose using Reinforcement Learning from Human Feedback (RLHF) to train LLMs. Specifically, they introduce InstructGPT, a version of GPT-3 fine-tuned with human preferences.

<img width="774" alt="Screenshot 2024-11-11 at 12 49 29 PM" src="https://github.com/user-attachments/assets/70557873-98e1-466e-a7b8-10e57a7e995f">

## Results

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

**Possible Answer**: Reinforcement learning from human feedback (RLHF) is more effective for alignment than merely scaling up model size because **it directly optimizes the model’s behavior to align with specific user preferences and instructions, whereas scaling up model size does not inherently improve the model’s ability to follow user intent**. Larger models, such as the 175B parameter GPT-3, can still generate untruthful, toxic, or unhelpful outputs due to the mismatch between the traditional language modeling objective (predicting the next word) and the goal of aligning with user instructions. By incorporating human feedback, RLHF fine-tunes models to prioritize outputs that are helpful, honest, and harmless, as judged by human labelers. This targeted approach results in the 1.3B parameter InstructGPT model being preferred by human evaluators over the much larger GPT-3, demonstrating that fine-tuning with human feedback is crucial for producing aligned, user-focused responses.
   
**Question 2**: “How does the InstructGPT approach help reduce toxic or biased outputs, and what are its limitations?”

**Possible Answer**: **The InstructGPT approach helps reduce toxic outputs by using reinforcement learning from human feedback (RLHF), where labelers rate model outputs for appropriateness and respectfulness.** This process incorporates human preferences directly into the training, encouraging the model to generate safer and more user-aligned responses. InstructGPT achieves a roughly 25% reduction in toxic outputs compared to GPT-3, particularly when explicitly instructed to be respectful.


## Architecture Overview

**Formal Pseudocode**

<img width="557" alt="Screenshot 2024-11-11 at 4 49 02 PM" src="https://github.com/user-attachments/assets/5530b798-902b-4224-a38f-33e6f48b97e8">

In the pseudocode provided, the purpose of the list C is to store the intermediate values required to compute the binomial coefficient  C(n, r)  (also known as “n choose r”) using a dynamic programming approach. The list C is initialized with r + 1 elements, all set to 0, except for C[0], which is set to 1. This initialization allows C to store the values of binomial coefficients up to the rth position as the computation progresses. The code iterates from 1 to n (inclusive) to compute the coefficients. For each i, the inner loop iterates backwards from j = min(i, r) down to 1. At each step, C[j] is updated to be the sum of C[j] and C[j - 1], effectively building the values of the binomial coefficients for n rows of Pascal’s Triangle. The final value, C[r], holds the computed binomial coefficient  C(n, r) .

**Why This Approach?**

The list C serves as a memory-efficient storage to calculate the binomial coefficient iteratively without the need for recursion or computing factorials, which can be computationally intensive. By storing only the required elements of Pascal’s Triangle, this approach avoids recalculating values and minimizes memory usage.

**How It Differs from Previous Models or Approaches?**

Traditional approaches for calculating binomial coefficients might use recursive formulas, factorials, or full Pascal’s Triangle generation. However, this dynamic programming method optimizes both time and space by calculating only the necessary values up to C[r] for a given n, making it efficient for large values of n and r. This is particularly useful in scenarios where repeated calculations of binomial coefficients are needed, as it avoids redundant calculations.

## Critical Analysis: What was overlooked by the authors?
* **Limitations**: The authors address only specific alignment goals (helpfulness, honesty, and harmlessness), but broader ethical implications and potential misuse are less explored. The human labelers’ demographic limitations (primarily English-speaking, specific cultural contexts) may bias the model’s behavior.
* **Areas for Further Development**: Exploring multilingual capabilities and performance in real-world, non-English settings could expand applicability. Additionally, adversarial testing could further assess model robustness against harmful prompts.
* **Disputes and Errors**: While RLHF is generally well-regarded, there’s debate on whether it creates an “alignment tax,” where alignment-focused models trade off raw performance on certain tasks.


## Impact and Importance
* **Shaping AI Alignment Research**: This work is pivotal in demonstrating RLHF’s potential for aligning LLMs with human intentions, setting a foundation for safer, more reliable AI applications.
* **Influence on Subsequent Models**: InstructGPT laid groundwork for models like ChatGPT, showing that RLHF can help models achieve high user satisfaction on open-ended tasks.
* **Broader AI Landscape**: By providing a feasible approach to align models with ethical guidelines, this work encourages more responsible AI development, impacting sectors like customer service, education, and content moderation.

## Resource Links
1. Original Paper: Training language models to follow instructions with human feedback (https://arxiv.org/abs/2203.02155)
2. Related Paper: Imitating Interactive Intelligence (https://arxiv.org/abs/2012.05672)
3. A General Language Assistant as a Laboratory for Alignment (https://arxiv.org/abs/2112.00861)
4. Language (Technology) is Power: A Critical Survey of "Bias" in NLP (https://arxiv.org/abs/2005.14050)
5. Truth, lies, and automation (https://cset.georgetown.edu/wp-content/uploads/CSET-Truth-Lies-and-Automation.pdf)

## Citation
Ouyang, L., Wu, J., Jiang, X., Almeida, D., Wainwright, C. L., Mishkin, P., Zhang, C., Agarwal, S., Slama, K., Ray, A., Schulman, J., Hilton, J., Kelton, F., Miller, L., Simens, M., Askell, A., Welinder, P., Christiano, P., Leike, J., & Lowe, R. (2022). Training language models to follow instructions with human feedback. arXiv. https://arxiv.org/abs/2203.02155


