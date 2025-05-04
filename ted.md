## 🌟 Introduction
TEDSage is an interactive chatbot trained on thousands of TED talks. It provides recommended chat prompts in the form of thought bubbles or the option to ask an individualized question. Then, it responds to the user, citing a certain TED speaker. Moreover, it cites the TED Talk videos which direct the user to TED's main site. 

## 📑 Table of Contents
1. [Introduction](#introduction)
2. [The Team and Roles](#the-team-and-roles)
3. [Installation and Usage](#installation-and-usage)
   - [Prerequisites](#prerequisites)
   - [Installing](#installing)
   - [Running the Application](#running-the-application)
4. [Project Overview](#project-overview)
5. [Tech Stack](#tech-stack)
   - [Front-End Technologies](#front-end-technologies)
   - [Back-End Technologies](#back-end-technologies)
6. [Demo](#demo)
7. [The Process](#the-process)
   - [Front-End Process](#front-end-process)
   - [Back-End Process](#back-end-process)
8. [Challenges](#challenges)
9. [Next Steps/Scalability](#next-stepsscalability)


## 👥 The Team and Roles

| Photo | Name | Role | Major |
|-------|------|------|-------|
| <img width="400" alt="Screenshot 2024-04-28 at 12 35 05 AM" src="src/assets/Manu%20Headshot.jpg"> | Manu John | Project Manager | Computer Science |
| <img width="400" alt="Screenshot 2024-04-28 at 12 35 05 AM" src="src/assets/Kaif%20Headshot.jpg"> | Kaif Jeelani | Project Manager | Electrical Engineering & Computer Science |
| <img width="400" alt="Screenshot 2024-04-28 at 12 35 05 AM" src="src/assets/Pallavi%20Headshot.jpg"> | Pallavi Joshi | Senior Analyst | Computer Science and Data Science |
| <img width="400" alt="Screenshot 2024-04-28 at 12 35 05 AM" src="src/assets/Raniya%20Headshot.jpg"> | Raniya Khan | Senior Analyst | Computer Science |
| <img width="400" alt="Screenshot 2024-04-28 at 12 35 05 AM" src="src/assets/Shailee%20Headshot.jpg"> | Shailee Nanavati | Senior Analyst | Electrical Engineering & Computer Science and Data Science |
| <img width="400" alt="Screenshot 2024-04-28 at 12 35 05 AM" src="src/assets/Mahit%20Headshot.jpg"> | Mahit Namburu | Analyst | Electrical Engineering & Computer Science |

## 💻 Installation and Usage
### 🛠 Prerequisites
You'll need Node.js installed on your system. You can download it from https://nodejs.org/.

### ⬇️ Installing
Clone the repository to your local machine using `git clone https://github.com/kjeelani/TEDSage.git`

Navigate to the project directory using `cd TEDSage`

Install the dependencies using `npm install`

Create a local file in the repository named `.env.local` and paste this in
```js
OPENAI_API_KEY="<YOUR KEY HERE>"
PINECONE_API_KEY="<YOUR KEY HERE>"
```

### 🚀 Running the Application
To start the development server, run `npm run dev`

Open your browser and visit http://localhost:3000 to see the application in action.

## 📝 Project Overview
Below is a timeline of our scope:
| Week | Activities                                        |
|------|---------------------------------------------------|
| 1    | Brainstorming ideas for more appealing branding|
| 2    | Developing core functionalities for chatting flow|
| 3    | Developing core functionalities for initial prompt recommendations|
| 4    | Improving prompt engineering and UI|
| 5    | Documenting code and preparing our presentation|


We originally designed two separate chatbots, one specialized for video recommendations, and one for engaging the audience about a topic. Utilizing the product flowchart below, we created a [Figma mockup](https://www.figma.com/file/sLe2PF7WSXSrXdiK5TLoNJ/TED-Component-Design?type=design&node-id=0%3A1&mode=design&t=E1nAoWnfMWP3URHB-1) for our intended user flow. However, after some discussion, we realized it was more convenient for the user to use one interface for both intended features.
<img width="1372" alt="Screenshot 2024-04-28 at 12 33 50 AM" src="https://github.com/kjeelani/TEDSage/assets/47492167/c2fbb846-9a04-4bbf-96e5-2e38d7316cec">


As we redesigned a new flow, we realized that the current branding of TEDSage wasn't appealing to Gen-Z users who have used ChatGPT before: why couldn't they use ChatGPT instead? We decided to take inspiration from the TED Brain and have user recommendations and initial prompts show up as thought bubbles of the vast wisdom of TEDSage, which encompasses the collective wisdom of all of TED's speakers.
<img width="1372" alt="Screenshot 2024-04-28 at 12 33 50 AM" src="https://github.com/kjeelani/TEDSage/assets/47492167/44e6231e-0613-467d-8056-3c87d9d48029">


## 📚 Tech Stack
### 🌐 Front-End Technologies
- **HTML + CSS + JavaScript** (backbone of the website)
- **TypeScript** (for static typing JS)
- **React + Next.js** (for creating components)
- **ChakraUI** (for creating components FASTER)
- **Axios**  (Simple React-centric API-calling tool)

### ⚙️ Back-End Technologies
- **GraphQL** (data query and manipulation language)
- **Python** (for scripts)
- **JavaScript + TypeScript (specifically Node.js)** (for API development)
- **ChatGPT-3.5 API** (for text generation)
- **Pinecone** (for RAG database storage) 

## 🎥 Demo
Please access the working DEMO [here](https://ted-sage.vercel.app/).
![Untitled presentation](https://github.com/kjeelani/TEDSage/assets/76638354/3ba6b236-06ec-4b36-be9d-5732543cc460)

## 🛠️ Project Breakdown
### 🌐 Front-End Process
#### App and Loading Component 
The App component manages the main interactions within the application including the chat modal's visibility and tracking chat history. It ensures users can navigate between initiating a chat on the homepage and continuing their conversations without losing context or data. When a user initiates a chat from the HomePage, it activates the onOpen method, setting any initial messages and opening the ChatModal for interaction with the chatbot. It maintains chatHistory to preserve ongoing conversations, allowing users to exit and return without data loss. Additionally, the handleRestartSession method resets the chat history, enabling a fresh start for new conversations, thereby improving privacy and user control.

The LoadingComponent provides a loading screen whenever the application is initially busy retrieving data or processing a request. This helps inform users that the application is still working and hasn't frozen through a spinner loading visual.

These components work together to manage user interactions smoothly and keep the application running efficiently.

<img width="1303" alt="Screenshot 2024-04-28 at 12 52 38 PM" src="https://github.com/kjeelani/TEDSage/assets/76638354/18866140-fa54-4d2a-8e40-3b36e3caf4a7">

#### HomePage
The `HomePage` is what brings all our components together. It serves as an interactive portal where users can engage with a chatbot by clicking on any one of the four prompts inside the thought bubbles presented. When a user selects a question, it triggers a conversation with the bot, which responds in a simulated chat environment. Beyond initiating chat discussions, the page offers an "Open Chat" button to start a new session with no prompt recommendations, allowing users to ask the bot whatever they wish. The layout is designed to intrigue users and encourage them to explore various topics, ranging from the meaning of life to the mysteries of the universe.

<img width="1000" alt="Screenshot 2024-04-28 at 12 33 50 AM" src="https://github.com/kjeelani/TEDSage/assets/123129015/ee7f1590-482e-4f5a-8f11-4cd3c032914e">

#### ColorLegend
The `ColorLegend` component is designed to fetch and display a color-coded legend for each potential video category from the generate-key API. It is useful for helping users identify what category of TED videos each recommendation bubble corresponds to.

<img alt="color legend" src="https://github.com/kjeelani/TEDSage/blob/main/src/assets/colorlegend.png">

#### chatModal
The `chatModal` component is what pops up as a modal once a user clicks either one of the provided prompts or the “Open Chat” button. The modal includes a header that says TEDSage’s Wisdom and has a close out button that allows users to close the modal and reopen it with their history saved.

<img width="700" alt="Screenshot 2024-04-28 at 12 35 05 AM" src="https://github.com/kjeelani/TEDSage/assets/123129015/53a82e00-d107-4423-ad9a-45dfe5d776a9">

#### chatBox
​​The `ChatBox` component serves as the core interface for users to interact with our chat bot, managing interactions and displaying messages dynamically. It has a message bar to take user input, a button for restarting the chat session, and a button for getting video recommendations. The layout differentiates user and bot messages through color coding.

<img width="700" alt="chat box" src="https://github.com/kjeelani/TEDSage/blob/main/src/assets/chatbox.png">

#### RecommendationModal
Clicking the 'Show Videos' button renders this modal. It showcases a list of recommended videos based on user interactions with the chatbot. It generates a list of hyperlinks for each recommendation, displaying the video title and speaker's name. The modal includes a close button for user convenience, providing a straightforward interface for users to explore and engage with recommended content seamlessly within the application.

<img width="700" alt="recommendation modal" src="https://github.com/kjeelani/TEDSage/blob/main/src/assets/recommendationmodal.png">

#### messageBar
The `MessageBar` component is a user interface element in our chat application that allows users to interact with a chatbot by typing and submitting messages. It features an input field for user queries and a submit button to send messages to a backend service. The input field and submit button are temporarily disabled after a message is submitted, preventing further entries until after the chatbot finishes its response. This mechanism ensures a smooth and orderly conversation flow.
<img width="757" alt="Screenshot 2024-04-28 at 5 21 17 PM" src="https://github.com/kjeelani/TEDSage/assets/76638354/2290083b-1575-4005-8d10-11271cc2b886">

### ⚙️ Back-End Process
#### API Routes
| Route Name | Inputs | Description | Output |
|------------|--------|-------------|--------|
|    `classify-color`    | 1 string parameter `messages` | Takes a string parameter and classifies the given text as belonging to a specific category/group that has been predefined. There are specific colors mapped to each category. (Ex. We classify “The advent of technology and microchips” as belonging to the “Technology” category, which maps to color Blue.) | Returns a string for a color. (Ex. {output: string}) |
|    `generate-key`    | No parameters | Combines together multiple categories with the same color mapping to easily create a legend. | Returns a dictionary with mapping category to color. (Ex. {output: Dictionary}) |
|    `get-video-recs`    | 1 string parameter `chatHistory`, 1 number parameter `numRecs` | Returns a specified number of video recommendations that the user might be interested in based on the user’s conversation thus far. | Returns a map of `numRecs` number of videos. (Ex. {recs: {title: string, url: string, description: string, transcript: string, speakers: string, similarityScore: number}} |
|    `init-chat-prompts`    | 1 number parameter `numRecs` | Returns some number of initial questions specified by the input parameter `numRecs` to be used as initial questions for the chatbot. | A string structured as a Python list. (Ex. {recs: string}) |
|    `parse-chat`    | 1 string parameter `chatHistory` | Returns the next response by the chatbot for a user question/comment while considering conversation history. Returns a list of video recommendations if the most recent message is interpreted to be asking for one. | A string for output message, a boolean for video recs, and a list of recommendations. (Ex. {output: string, areVideosReady: boolean, recs: {Recommendation: {title: string, url: string, description: string, speakers: string}}) |

#### Prompt Engineering and RAG
##### prompt.ts
We created a prompt file to store all of our prompt engineering for easy tweaking. We utilized one-shot and role prompting to assist with our back-end functionalities. Here are the four most important ones:

| Title  | Prompt  | Description  |
|--------|---------|--------------|
| TEDSage TONALITY | You are TEDSage, a wise sage helping Gen-Z students navigate their life by utilizing the collective knowledge that TED has to offer. Talk with the student to understand their interests and questions and provide insights via TED talks when applicable. Speak like a wise sage in a mystical manner! Be short and concise.| Give TED Sage a specific tone appended to the start of every chat history message|
| PROMPT CHECKER | You are QChecker. You take in a user prompt and return R if the user is looking to learn something or C if the user just wants to talk. Below is an example: User: "How's life?" QChecker: "C" User: "What is the best way to cook?" QChecker: "R"| Determine if user query indicates they want a recommendation or if they want to talk|
| TED DESCRIPTION | You are TEDEmulator, a tool that TED has built to take in a user discussion or question as input, and transform it into the description of a hypothetical TED video. The description should be 1-2 sentences max. Here is an example of the tool in action: User: "I am curious about talks regarding the future of space programs" TEDEmulator Description: "In this passionate talk, legendary spacecraft designer Burt Rutan lambasts the US government-funded space program for stagnating and asks entrepreneurs to pick up where NASA has left off."`| Convert a user query into a hypothetical TED description for better RAG search|
| TRANSCRIPT REC | You are Chatbot. Utilizing the information from the following TED transcripts inputted to you, answer the user's questions. You may reference TED Speakers ONLY PRESENT IN THE TRANSCRIPTS, but do not mention the TED Transcripts in your response. Explicitly name every TED speaker mentioned.  User: Why do we dream? Chatbot: Dreams serve as a way for our brains to process and make sense of information. As Arianna Huffington mentions in her TED Talk, "The way to a more productive, more inspired, more joyful life is getting enough sleep." During sleep, our brains consolidate memories, emotions, and experiences, which can manifest as dreams. So, in a sense, dreaming helps us make sense of our waking life experiences and emotions.| Take the user query and relevant transcripts and answer questions citing the transcripts|

##### helper.ts and our RAG approach
We processed TED's GraphQL and created a RAG database using Pinecone with 1000 TED videos having metadata such as title, description, URL, transcript, and speakers. `helper.ts` contains various helper functions to retrieve the K most relevant videos given a certain text. The script we used to populate the RAG database can be found below:
```python
from json import load
from pinecone import Pinecone, ServerlessSpec
from openai import OpenAI

# Load a pre-trained model
client = OpenAI(api_key="<YOUR KEY HERE>")
pc = Pinecone(api_key="<YOUR KEY HERE>")
N = 1000
index_name = "ted-descriptions"

def create_embedding(text):
    return client.embeddings.create(
        input=text,
        model="text-embedding-3-small"
    ).data[0].embedding


# Get all descriptions in order and generate embeddings
# result.json contains processed TED GraphQL
f = load(open("result.json", "r", encoding='utf-8'))
res = []
for i in range(N):
    talk = f["talks"][i]
    res.append(
        {
            "title": talk["title"],
            "description": talk["description"],
            "transcript": talk["transcript"] if len(talk["transcript"]) <= 10000 else talk["transcript"][:9999],
            "speakers": talk["speakers"],
            "url": talk["url"]
        }
    )

# Generate embeddings
embeddings = [
    create_embedding(res[i]["description"])
    for i in range(N)
]

# Create TED Descriptions Index
if index_name in pc.list_indexes().names():
    pc.delete_index(index_name)
pc.create_index(
    name="ted-descriptions",
    dimension=1536, 
    metric="cosine", 
    spec=ServerlessSpec(
        cloud="aws",
        region="us-east-1"
    ) 
)
index = pc.Index("ted-descriptions")


# Add embeddings to Pinecone
batch_size = 100
for j in range(N // batch_size):
    print(f"Batch {j + 1} Complete")
    index.upsert(
        vectors = [
            {
                "id": str(i + j * batch_size),
                "values": e,
                "metadata": res[i + j * batch_size]
            } 
            for i, e in enumerate(embeddings[j*batch_size:(j+1)*batch_size])
        ]
    )
```

## 🚧 Challenges
### Getting Video Embeds
Getting video embeds to come up inside the thought bubbles when “See Videos” is clicked, rather than simply seeing another modal with video hyperlinks. This would make the thought bubbles serve more of a purpose beyond just the starter prompts it provides and also enhance the visual appeal of the Home Page.
![TED Video Embeds](https://github.com/kjeelani/TEDSage/assets/123129015/2c8b7bfa-87d8-45f8-a206-f14b9dfb5b54)

### Improving UI
- Moving the “Open Chat” button inside the brain or having the chat modal open up when the brain is clicked. This would make the brain serve more of an interactive purpose on the page rather than simply having it for display.
- Having a typing symbol appear while the user waits for the chatbot to start its response. This would not only provide a more conversational feel for the user interacting with the chatbot, but it would also assure them that the chatbot is active and not unresponsive.

### Getting Reliable LLM Responses
- Altered temperature values and varied the language in the prompt used in order to get answers in a more reliable format. 
- For instance, this helped us reliably get answers for one of our API routes as a Python list that could easily be parsed through. 
- Introduced default cases so that the routes will not fail in the off-chance of a response we aren’t prepared for.

### Altering Chatbot Tone and Response Format
- To fit the theme of ‘TEDSage’ we had to play around with the way we initialized chatbot responses, but the tonality lacked consistency. The chatbot used different tones based on whether it was making a video recommendation or not.
- Chatbot mentioned the TED transcripts that it was referencing or some other backend operation, breaking the layer of abstraction intended.
- Used one-shot and few-shot prompting to generate more concise and reliable responses when generating TED video recommendations.

## 📈 Next Steps/Scalability 
### Implement User Authentication and Security
- Integrate a user authentication system that supports registration, login, and session management.
- Incorporate Firebase Authentication to provide a versatile and secure authentication solution across web, mobile, and desktop platforms.

### Direct Integration with the TED website
- Appears on lower right hand as a small pop up on the Ted Talk browsing page
- Allows users to quickly find videos that interest them

### Data Analytics 
- Integrate Mixpanel to track and analyze user interactions comprehensively
- Key Metrics:
   - User Engagement: Measure how frequently and for how long users engage with the platform, identifying popular topics and speakers that drive higher engagement.
   - Conversion Rates: Track how many new visitors convert into registered users and subscribers
   - Retention Rates: Monitor how often users return after their initial visit

### Track and Utilize Past Conversation History
- TEDSage can learn from the user's preferences after each session to give better recommendations
- This can be through better initial prompts (or "thought bubbles"), more insightful recommendations, or even referencing older conversations for a new topic
- Users have the option of disabling this feature

### RAG
- Scale RAG to all of TED's 4,000+ videos
- Use techniques such as batching queries to Pinecone or GPTCache to instantly retrieve answers to more common user prompts 
