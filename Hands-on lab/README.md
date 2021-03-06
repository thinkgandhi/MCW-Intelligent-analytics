# Intelligent analytics hands-on lab

AdventureWorks Travel specializes in building software solutions for the hospitality industry. Their latest product is an enterprise mobile/social chat product called Concierge+ (aka ConciergePlus). The mobile web app enables guests to easily stay in touch with the concierge and other guests, enabling greater personalization and improving their experience during their stay. Sentiment analysis is performed on top of chat messages as they occur, enabling hotel operators to keep tabs on guest sentiments in real-time.

## Contents

- [Abstract](#abstract)
- [Solution architecture](#solution-architecture)
- [Requirements](#requirements)
- [Before the Hands-on Lab](#before-the-hands-on-lab)
- [Hands-on Lab](#hands-on-lab)
- [After the Hands-on Lab](#after-the-hands-on-lab)

## Abstract

This hands-on lab is designed to provide exposure to many of Microsoft's transformative line of business applications built using Microsoft advanced analytics. The goal is to show an end-to-end solution, leveraging many of these technologies, but not necessarily doing work in every component possible.

## Solution architecture

Below is a diagram of the solution architecture you will build in this lab. Please study this carefully so you understand the whole of the solution as you are working on the various components.

![This is the high-level overview diagram of the end-to-end solution.](../Whiteboard%20design%20session/media/high-level-overview.png 'High-level overview diagram')

Messages are sent from browsers running within laptop or mobile clients via Web Sockets to an endpoint running in an **Azure Web App**. Instead of typing a chat message, end users can leverage the speech to text functionality of the **Speech API** to type the chat message for them- in this scenario the Speech API is invoked directly from the web page running in a client device. Chat messages received by the Web App are sent to an **Event Hub** where they are temporarily stored. An **Azure Function** picks up the chat messages and applies sentiment analysis to the message text (using the **Text Analytics API**), as well as contextual understanding (using **LUIS**). The function forwards the chat message to an Event Hub used to store messages for archival purposes, and to a **Service Bus Topic** which is used to deliver the message to the intended recipients. A **Stream Analytics** Job provides a simple mechanism for pulling the chat messages from the second Event Hub and writing them both to **Azure Cosmos DB** for archival and to **Power BI** for visualization of sentiment in real-time as well as trending sentiment. An indexer runs atop Cosmos DB that updates the **Azure Search** index which provides full text search capability. Messages in the Service Bus Topic are pulled by Subscriptions created in the Web App and running on behalf of each client device connected by Web Sockets. When the Subscription receives a message, it is pushed via Web Sockets down to the browser-based app and displayed in a web page. **Bot Services** hosts a bot created using QnA maker, which automatically answers simple questions asked by site visitors.

## Requirements

- Microsoft Azure subscription must be pay-as-you-go or MSDN
  - Trial subscriptions will not work

## Before the Hands-on Lab

Before attending the hands-on lab workshop, you should set up your environment for use in the rest of the hands-on lab.

You should follow all the steps provided in the [Before the Hands-on Lab](./Before%20the%20HOL%20-%20Intelligent%20analytics.md) section to prepare your environment before attending the hands-on lab. Failure to complete the Before the Hands-on Lab setup may result in an inability to complete the lab with in the time allowed.

## Hands-on Lab

Select the guide you are using to complete the Hands-on lab below.

- [Step-by-step guide](./HOL%20step-by-step%20Intelligent%20analytics.md)
  - Provides detailed, step-by-step instructions for completing the lab.
- [Unguided](./HOL%20unguided%20-%20Intelligent%20analytics.md)
  - This guide provides minimal instruction, and assumes a high-level of knowledge about the technologies used in this lab. This should typically only be used if you are doing this as part of a group or hackathon.
