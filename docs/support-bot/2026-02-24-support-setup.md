---
title: "Let's prepare for support"
---

<img src="./images/2026-02-24-bot.png" alt="js console" width="100" />

Building a support bot might seem trivial if you already have experience and know what to do. However, I decided to start by creating one myself before diving into the testing phase. You can find the code on GitHub:
[palapiessa/support-bot-sample](https://github.com/palapiessa/support-bot-sample)

The bot uses a set of e-commerce FAQs, initially sourced from Hugging Face:
[qgyd2021/e_commerce_customer_service](https://huggingface.co/datasets/qgyd2021/e_commerce_customer_service)

I reformatted the data and uploaded it back to Hugging Face here:
[palapiessa/e_commerce_customer_service_squad](https://huggingface.co/datasets/palapiessa/e_commerce_customer_service_squad)

When the bot CLI is launched for the first time, the data is loaded from the Hugging Face repo. The downloaded JSON is converted into a list of question-and-answer pairs and saved to a file. This file is then loaded, and a NumPy list of question embeddings is created. 

An embedding is a numeric vector representation of a sentence that captures its meaning, so semantically similar sentences end up close together and can be found with semantic search. This helps match the user’s question to the most relevant question in the FAQ list.   

The FAQ list initially contains 65 questions and answers, but a future post will cover generating more questions for the list.

<script src="https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.min.js"></script>
<script>mermaid.initialize({ startOnLoad: true });</script>

### Initial creation of FAQs and their embeddings
<div class="mermaid">
flowchart TD
    A["Start"] --> B["Request faq.json from Hugging Face"]
    B --> C["Load and parse faq.json"]
    C --> D["Extract questions"]
    D --> E["Create local questions list file"]
    E --> F["Initialize NumPy list for embeddings"]
    F --> G["Read next question from local list"]
    G --> H["Generate question embedding"]
    H --> I["Append embedding vector to NumPy list"]
    I --> J{"More questions?"}
    J -->|Yes| G
    J -->|No| K["Save/finalize embeddings list"]
    K --> L["Done"]
</div>



