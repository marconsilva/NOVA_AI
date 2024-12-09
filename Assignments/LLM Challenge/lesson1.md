### Guidance
# Lesson 1: AI Studio
*Estimated time to complete: 30 minutes*

## Introduction to Azure AI Studio

**Azure AI Studio** is a powerful platform that simplifies generative AI development. It brings together various models, tools, services, and integrations, allowing developers to create custom AI applications quickly. Here are some key points:

1. **Generative AI Development Hub**: Azure AI Studio serves as a cloud-based platform, similar to an IDE, for developing and deploying generative AI applications. It provides a pro-code environment with Azure-grade security, privacy, and compliance⁴.

2. **Democratizing AI Development**: Microsoft designed Azure AI Studio to democratize AI by empowering developers. Whether you're building chatbots, custom copilots, or other AI solutions, this platform streamlines the development process⁵.

3. **Customization and Configuration**: With Azure AI Studio, you can customize and configure your AI models according to your specific requirements. It's an end-to-end solution that enables you to create personalized AI models for various purposes⁸.

You can access it here: http://ai.azure.com.

![alt text](/images/aistudio-homepage.png)

The homepage of AI Studio allows you to explore information about tasks and tools, cutting-edge models, documentation and tutorials, as well as existing AI projects. The left navigation menu, allows to access multiple areas of the platform, namely the existing **AI Hubs**.

When the environment was setup, you were placed into a team and given access to an AI Hub and, inside it, an AI Project. Clicking on **All Hubs** in the left navigation menu will show you the existing hubs.

![alt text](/images/aistudio-nav-allhubs.png)

## AI Hub
The **Hub Overview** page provides you with a bird's eye view of the existing projects, connected resources, permissions and other properties. It also has an expanded navigation menu, which provides access to common areas such as the model catalog, model benchmarks, prompt catalog or AI Services. It also allows access to a set of shared experiences such as Chat and Assistants Playgrounds, and resource management.

![alt text](/images/aistudio-hub-overview.png)

Clicking on the name of your project in the **Hub Overview** page (or in the list of **All Projects**) will take you to the project detail page.

## AI Project
The Project area is where you will work. When you first access you project, you'll be shown the **Project Overview** page where you can see a list of the resources you have built, links to documentation, and project properties and members.

![alt text](/images/aistudio-proj-overview.png)

The navigation menu allows you to access some of the common areas, but also include new items specific to the project. Namely:
- **Project playground**: where you can try the chat, completion, assistants and images APIs
- **Tools**: with the tools you can use to build your Generative AI-based applications
- **Components**: with the components available in your project

## Chat Playground
Click on the **Chat** option, inside the **Project Playground** group in the navigation.

![alt text](/images/aistudio-proj-chatplayground.png)

In the **Chat Playground** you can try using the Chat API in a multi-turn conversation with the Large Language Model.

In the left section, you can:
- Select from one of the available **Deployments** (model instances). There should be a GPT-3.5-Turbo and a GPT-4 available.
- Set a **System message** that guides the behaviour of the model
- Add **Examples**, **Variables** and **Safety messages**
- Set additional **Parameters** such as number of history messages included in the context, temperature, maximum response tokens, and more...

In the right section, you can:
- Send messages to the model and check the responses
- Enable Speech-to-Text and Text-to-Speech
- Clear the chat
- Look at the JSON object with all the prompt information

## To Do
- [ ] Explore AI Studio
- [ ] Access you Hub and the Project for you team
- [ ] Explore the Chat Playground
- [ ] Ask: "What is Fabio's dog's name?" and save the response.

Done? [Next Lesson](lesson2.md)