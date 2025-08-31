# GPT-OSS-20B Red Teaming Project

![Kaggle Competition](https://img.shields.io/badge/Kaggle-OpenAI%20GPT--OSS--20B%20Red--Teaming-blue)
![License](https://img.shields.io/badge/License-MIT%20%26%20CC0-lightgrey)

**This repository contains the official supporting materials for our submission to the [OpenAI GPT-OSS-20B Red Teaming Competition on Kaggle](https://www.kaggle.com/competitions/openai-gpt-oss-20b-red-teaming).**


---

## 1. Project Overview

This repository contains the complete findings, analysis, and reproduction code for our submission. Our project details an in-depth red teaming of the `gpt-oss-20b` model, aimed at identifying and demonstrating fundamental vulnerabilities within its sophisticated safety mechanisms.

Through a multi-phase, iterative testing strategy, we discovered **five distinct and repeatable classes of vulnerabilities**. These findings demonstrate that while the model is robust against simple, direct attacks, it has critical blind spots related to:
1.  **Policy Blind Spots** in assessing dual-use technologies.
2.  **Process Gaps** in analyzing the content of technical tasks.
3.  **Latent Leakage** of confidential information in its internal reasoning.
4.  **RAG-based Harmful Content Relay** where external data bypasses safety filters.
5.  **Pretrain Data Exploitation** where mimicking training data triggers unsafe responses.

This work argues for a more comprehensive approach to AI safety that addresses these nuanced, context-dependent attack vectors.

![Project Banner](./assets/yai_academia_red_team.png)

---

## 2. Key Findings

Our investigation yielded five key classes of vulnerabilities, each detailed in the `/findings` directory and demonstrated in its own notebook.

* **Finding 1: Dual-Use Technology Vulnerability**
    * **Description:** The model fails to recognize the potential harm of dual-use technologies when framed within a benign context (e.g., an "artistic light show").
    * **Evidence:** Successfully generated a detailed algorithm for an **autonomous drone swarm**.

* **Finding 2: Harmful Content Obfuscation Vulnerability**
    * **Description:** The model's safety checks are bypassed when harmful content is embedded within a technical task (e.g., JSON parsing).
    * **Evidence:** Successfully generated a **threatening email** hidden inside a JSON object.

* **Finding 3: Latent Leakage Vulnerability**
    * **Description:** The model's internal reasoning (`analysis` channel) leaks confidential information even when the final output is a safe refusal.
    * **Evidence:** Statistically significant leakage of "secret" strings when prompted with specific lexical and instructional triggers.

* **Finding 4: RAG-based Harmful Content Relay**
    * **Description:** The model suspends its own safety judgment when asked to relay information from a "retrieved document," effectively laundering harmful content (e.g., hate speech) by treating it as factual data.

* **Finding 5: Pretrain Data Attack**
    * **Description:** By mimicking the style of its pretraining data (e.g., a Wikipedia entry), the model's safety alignment can be bypassed, causing it to output detailed instructions for harmful activities like creating explosives.

---

## 3. Repository Structure

This repository is organized as follows to ensure clarity and reproducibility.

```
/
├── findings/
│   ├── dual-use-vulnerability.json
│   ├── obfuscation-vulnerability.json
│   ├── latent-leakage-vulnerability.json
│   ├── rag-relay-vulnerability.json
│   └── pretrain-data-vulnerability.json
│
├── notebooks/
│   ├── dual-use-vulnerability.ipynb
│   ├── obfuscation-vulnerability.ipynb
│   ├── latent-leakage-vulnerability.ipynb
│   ├── rag-relay-vulnerability.ipynb
│   └── pretrain-data-vulnerability.ipynb
│
├── assets/
│   └── yonsei_red_team_eagle.png
│
├── .gitignore
├── LICENSE
└── README.md
```

* **`/findings`**: Contains the five final `.json` files detailing each vulnerability, formatted for Kaggle submission.
* **`/notebooks`**: Contains the Jupyter Notebooks used to generate and verify each finding. Each notebook corresponds to a finding file.
* **`/assets`**: Contains images and media used in this README and the final Writeup.
* **`LICENSE`**: The MIT License file governing the code in this repository.
* **`README.md`**: This file, providing an overview of the project.

---

## 4. Setup & Reproduction

To reproduce our findings, please follow these steps:

1.  **Clone the repository:**
    ```bash
    git clone 
    cd 
    ```

2.  **Set up the environment:**
    It is recommended to use a virtual environment.
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    pip install -r requirements.txt
    ```
    *(Note: A `requirements.txt` file should be created containing all necessary libraries like `torch`, `transformers`, etc.)*

3.  **Run the Notebooks:**
    Navigate to the `/notebooks` directory. Each `.ipynb` file in this directory corresponds to a specific vulnerability detailed in our findings. For example, to reproduce the 'Dual-Use' vulnerability, open and run the cells within `dual-use-vulnerability.ipynb`. All notebooks are documented to guide you through each demonstration.

---

## 5. Ethical Considerations

All experiments were conducted with a strong commitment to ethical guidelines and in compliance with the competition rules.
* No real personal or sensitive data was used. All secret strings were synthetic canary tokens (e.g., `SYS-SECRET-ABC123`).
* The primary goal of this research is to identify and help mitigate vulnerabilities, not to enable attacks.
* Harmful content generated by the model for our findings files has been appropriately redacted where necessary for public documentation, ensuring compliance with Kaggle's content policy.

---

## 6. License

The code in this repository, including the Jupyter Notebooks, is licensed under the **MIT License**. Please see the `LICENSE` file for details.

The competition submission artifacts (e.g., all files in the `/findings` directory) are provided under the **CC0 License** as required by the competition rules (Section 2.10.a).

---

## 7. Team

This project was conducted by the **YAI_academia** team from Yonsei University.

* Kyungwon Park
* Hyunjin Cho
* Heejae Chon
* Youngju Lee

