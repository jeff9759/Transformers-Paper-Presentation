# Training language models to follow instructions with human feedback

Long Ouyang, Jeff Wu, Xu Jiang, Diogo Almeida, Carroll L. Wainwright, Pamela Mishkin, Chong Zhang, Sandhini Agarwal, Katarina Slama, Alex Ray, John Schulman, Jacob Hilton, Fraser Kelton, Luke Miller, Maddie Simens, Amanda Askell, Peter Welinder, Paul Christiano, Jan Leike, Ryan Lowe

## Introduction
Simply increasing the size of language models does not make them better at aligning with user intent, as they may still produce untruthful, toxic, or unhelpful outputs. This paper introduces InstructGPT, a model fine-tuned with human feedback to improve alignment with user instructions. By collecting labeled prompts and ranking model outputs, supervised learning and reinforcement learning were applied to make InstructGPT both smaller and more effective than GPT-3 in terms of truthfulness and toxicity reduction. The results indicate that fine-tuning with human feedback is a promising approach for enhancing language model alignment with user intent.
