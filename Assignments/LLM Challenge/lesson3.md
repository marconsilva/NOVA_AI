### Guidance
# Lesson 3: Prompt Flow
*Estimated time to complete: 30 minutes*

## Introduction to Prompt Flow

**Azure Machine Learning Prompt Flow** is a suite of development tools designed to streamline the end-to-end development cycle of AI applications powered by Large Language Models (LLMs). Whether you're a developer, data scientist, researcher, or hobbyist, Prompt Flow simplifies the process of building LLM-based applications. Here are some key features:

1. **Visualized Graphs**: Create executable flows that link LLMs, prompts, and Python tools through a visualized graph.
2. **Collaboration**: Debug, share, and iterate your flows with ease through team collaboration.
3. **Prompt Variants**: Create and evaluate multiple prompt variants for iterative refinement.
4. **Enterprise Readiness**: Streamline prompt engineering from development to deployment and monitoring.

With Azure Machine Learning Prompt Flow, you can prototype, experiment, and deploy LLM-based AI applications efficiently. Get started today and experience the power of streamlined development!

Learn more:
- [Azure Machine Learning Prompt Flow Documentation](https://microsoft.github.io/promptflow/index.html)
- [Try out more Prompt Flow examples](https://microsoft.github.io/promptflow/tutorials/index.html)

## Creating a new Flow

To access **Prompt Flow**, you can use the left navigation when inside you Project. The welcome page list the existing flows and allows you to create new ones, by pressing the **+ Create** button in the top of the screen.

When creating a new flow, you can select from three base types:
- **Standard flow**: a simple flow meant to be run end-to-end.
- **Chat flow**: a flow meant to be used for multi-turn chat, with history support.
- **Evaluation flow**: a flow meant to be used to evaluate specific metrics of other flows.

Alternatively, you can create a flow based on a template from the gallery of samples. These are more complex flows meant for specific scenarios, such as Q&A on your data or chat with Wikipedia.

## Variants in Prompt Flow

A **variant** refers to a specific version of a tool node within Prompt Flow, characterized by distinct settings. Currently, variants are supported only in the **Large Language Model (LLM)** tool. Here's how they work:

1. **LLM Tool Variants**: When working with LLMs, you can create different variants of the same node, each with unique prompt content or connection settings. For instance:
   - **Variant 0**: Summary generation with a high temperature setting (e.g., `Temperature = 1`).
   - **Variant 1**: Summary generation with a slightly lower temperature (e.g., `Temperature = 0.7`).
   - **Variant 2**: Asking for the main point of an article with high temperature.
   - **Variant 3**: Asking for the main point of an article with a lower temperature.

2. **Benefits of Using Variants**:
   - **Quality Enhancement**: By experimenting with multiple prompt variants and configurations, you can identify the optimal combination that produces high-quality content aligned with your needs.
   - **Time Savings**: Even minor prompt modifications can yield significantly different results. Variants allow you to manage historical versions of your LLM nodes, facilitating updates without forgetting previous iterations.
   - **Productivity Boost**: Streamline the optimization process by creating and managing multiple variations, achieving improved results in less time.
   - **Easy Comparison**: Effortlessly compare results from different variants side by side, enabling data-driven decisions.

## To Do
- [ ] Create a chat with Wikipedia flow
- [ ] Create a Q&A on Your Data flow
- [ ] Create variants of the prompt and test them

Want to go back? [Previous Lesson](lesson2.md)