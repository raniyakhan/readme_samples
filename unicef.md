## 🌟 Introduction
This project focuses on improving the Learning Passport platform by implementing a course recommendation system designed to enhance navigation and accessibility for educators and students. This web application was built with Azure using TypeScript and Node.js as a proof of concept for how we can use Microsoft Community Training's REST API to query for content, format this content into a prompt to TogetherAI, and display its recommendations in LearningPassport through course descriptions. By streamlining how users discover relevant learning materials, the system aims to support more effective teaching and learning experiences. Its focus on affordability and adaptability ensures that the solution can be scaled to diverse educational environments, aligning with UNICEF’s mission to make quality education accessible globally. 

## 👥 The Team and Roles

| Photo                                                                                                           | Name           | Role             | Major                                                         |
|-----------------------------------------------------------------------------------------------------------------|----------------|------------------|---------------------------------------------------------------|
| <img src="https://github.com/user-attachments/assets/2b818185-24d9-46f0-b7ee-ebe188772b91" width="150"/>        | Shailee Nanavati | Project Manager  | Electrical Engineering & Computer Science and Data Science    |
| <img src="https://github.com/user-attachments/assets/0725ee9e-1931-4ce9-bfb1-30624c1b9267" width="150"/>        | Raniya Khan       | Project Manager  | Applied Mathematics and Computer Science                      |
| <img src="https://github.com/user-attachments/assets/ca2e1dca-e806-4470-bcec-e633cc706e06" width="150"/>        | Kinton Duong      | Senior Analyst   | Computer Science and Data Science                             |
| <img src="https://github.com/user-attachments/assets/27b8e6fc-cfa7-4f12-93d8-4d8af84b05a3" width="150"/>        | Mahit Namburu     | Senior Analyst   | Electrical Engineering & Computer Science                     |
| <img src="https://github.com/user-attachments/assets/3dae189e-3bd8-4830-ac7a-3fbf025b1afd" width="150"/>        | Ava Shah          | Senior Analyst   | Industrial Engineering & Operations Research                  |
| <img src="https://github.com/user-attachments/assets/34abd5e1-e68a-49eb-a7de-164c8e015aad" width="150"/>        | Angad Bhargav     | Analyst          | Electrical Engineering & Computer Science                     |
| <img src="https://github.com/user-attachments/assets/ee77df3c-11c0-49f0-bf9e-748b9352befe" width="150"/>        | Jaansi Parsa      | Analyst          | Electrical Engineering & Computer Science and Business Administration |


### 🛠 Prerequisites
You’ll need the following installed on your system:
- **VSCode**
- **Node.js**
- **npm**
- **Azure Functions Extension**
- **.NET SDK**
- A properly configured `.env` file with the following settings:

### ⬇️ Installing

1. **Install Node.js and npm**  
   - Ensure Node.js is installed on your local system via [Node.js official website](https://nodejs.org/en).  
   - Install the required npm dependencies by running the following command in the terminal:  
     ```bash
     npm install
     ```

2. **Install the Azure Functions Extension**  
   - Open the Extensions Marketplace in VSCode.  
   - Search for "Azure Functions" and install it.  
   - To install Core Tools globally into Azure Functions, run:  
     ```bash
     npm install -g azure-functions-core-tools@4
     ```

3. **Install the .NET SDK**  
   - Download and install the .NET SDK from [Microsoft .NET](https://dotnet.microsoft.com/en-us/download).

4. **Set up an `.env` file**  
   - Create a file named `.env` and add the following configuration:
     ```env
     # The `Requestverificationtoken` header sent in specialized requests like `EditCourse`. Use DevTools to find.
     LP_REQUEST_VERIFICATION_TOKEN=""

     # The `Cookie` header sent in admin requests when authenticated. Use DevTools to find.
     LP_ADMIN_COOKIE=""

     # The `Cookie` header sent in image requests when authenticated. Use DevTools to find.
     LP_IMAGE_COOKIE=""

     # The URL to the LP instance you're querying from. In our case:
     LP_URL="https://global.learningpassport.unicef.org"

     # TogetherAI API Key. Create one here: https://www.together.ai/
     TOGETHER_API_KEY=""
     ```
### Running the Application

Run the application by first running:

```bash
npm run build
```

Then, start the application with:

```bash
npm start
```

This will open a local server running the Azure Function at:

```bash
http://localhost:7071
```

Alternatively, you can run the application through the Azure Functions Extension in VSCode by selecting **Start Function App**.



## 📚 Tech Stack

- **Node.js**: Used for writing and deploying the Azure Function, interacting with the LP Instance and LLM model, generating and managing HTML files, and pushing the results back to the LP instance API.

- **Azure**: Azure Functions are used to push changes onto Learning Passport based on a manual trigger without needing to access or modify LP’s underlying infrastructure.

- **Together AI**: Together AI is used to generate course recommendations based on a given current course and list of courses.

## 📝 Project Overview

### LLM and TogetherAI Overview

#### Models Tried

| **Model/Platform**     | **Description**                                                                                                                                           | **Strengths**                                                                                     | **Limitations**                                                                                   |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| **Gemini AI**           | Designed for deep contextual understanding and reasoning across domains. It analyzes course descriptions, focusing on keywords and structure to recommend the next course. | - Deep contextual understanding<br>- Cross-domain reasoning                                      | - Slower<br>- Less specialized for tasks like course categorization and recommendation          |
| **Flan-T5**             | A fine-tuned text-to-text model that excels at instruction-following tasks, making it ideal for structured tasks like summarization.                     | - Versatile and powerful for structured tasks<br>- Excellent at following instructions           | - Less effective in dynamic, multi-domain scenarios                                              |
| **🌟 TogetherAI** (**Chosen Platform**) | Provides tools and infrastructure for developing, fine-tuning, and deploying generative AI models, supporting a range of AI applications. **Selected for its flexibility, scalability, and minimal cost.** | - Fast, scalable inference on open-source models<br>- Allows for customization using proprietary data<br>- Minimal cost | - No significant drawbacks!       |

---
## 🔗 API Routes

This project utilizes API endpoints to fetch, process, and recommend courses using data from Microsoft Community Training’s REST API and TogetherAI’s recommendation system.

The main API endpoint provided is `/api/update-course`, which, given an inputted course, will add a lesson containing recommendations to other courses. This endpoint depends on two helper API endpoints: `/api/recommend` and `/api/upload`.

| Route Name             | Inputs                                                                                       | Description                                                                                                                                                                                                                 | Output                                                                                                          |
|------------------------|----------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| `POST: /api/update-course` | - `courseId`: the ID of the course to add a "Recommended" lesson to.                                                       | Combines the functionalities of `/api/recommend` and `/api/upload`. Fetches and filters relevant courses using the LP API, generates recommendations, formats them as HTML, and uploads the HTML as a lesson to the course. | Adds a lesson containing the recommendations to the specified course and publishes it.                         |
| `POST: /api/recommend`     | - `courseId`: the course ID for which recommendations are to be made. <br> - `categoriesAndCourses`: list of courses and categories in the format returned by the LP API endpoint. | Formats information from `categoriesAndCourses` into a concise JSON object containing relevant course data, then uses TogetherAI’s JSON mode to generate recommendations for the provided `courseId`.                           | Returns a list of recommended course IDs. (Ex. `{courseIds: [Number]}`)                                        |
| `POST: /api/upload`        | - `courseId`: the ID of the course to add a "Recommended" lesson to. <br> - `html`: the raw HTML content for the new lesson.                                       | Uploads a new lesson to the specified course using the provided HTML content. Requests a SAS token for secure upload, uploads the file, and publishes the lesson to the course.                                              | Adds the lesson to the specified course and publishes it.                                                      |

## 🎬 Demo!

## 🛠️ The Process

### Front-End Process
**Quick CSS Overview and Creative Direction**  
We used CSS to display each course’s information efficiently, highlighting the most important details with a clear design hierarchy:
- The course title is displayed in **bold**.
- The course description is truncated to 3 lines to avoid distracting from other details.
- Additional details such as the number of lessons, and type of course are also provided.

![image](https://github.com/user-attachments/assets/2b58aed5-71ee-482a-ad8e-6eb4b123b1b7)


---

### Back-End Process

#### **LLM Selection**
We aimed to select a model that was both free (or as close to free as possible) and produced good results. To evaluate the options, we created prompts to test:
- Categorizing courses (by age, topic, etc.).
- Recommending courses (based on a list of existing courses and one current course).
- Providing reasoning for recommendations.
- Generating recommendations in HTML format.

**Evaluation of Models**:
- **Gemini**: Offered a free-tier, performed well for creating recommendations and providing reasoning, but lacked categorization optimization.
- **Flan T5**: Free, but generated poor recommendations and struggled with categorization tasks.
- **OpenAI**: Produced the best recommendations and categorization results but was more expensive.
- **Together.ai (with Mistral)**: Provided strong recommendations, excellent categorization, and was completely free.

**Scoring Table**:
| Model       | Price | Recommendation | Categorization |
|-------------|-------|----------------|----------------|
| Gemini      | 3     | 2              | 3              |
| OpenAI      | 4     | 1              | 1              |
| Flan T5     | 2     | 4              | 4              |
| Together.ai | 1     | 3              | 2              |

**Decision**:  
Together.ai and OpenAI had the best scores, but given our priority on price, we selected **Together.ai** as the LLM for this project.

---

### API Changes
Previously, the API added course recommendations directly to the course description.  
- **Update**: Recommendations are now inserted as a **new lesson** at the end of the course for better structure and organization.

## 🚀 Deployment

### **Using GitHub Actions**
To deploy our Azure Function, we utilized **GitHub Actions** for a streamlined and efficient deployment process.

#### **Why GitHub Actions?**
- GitHub Actions allows us to control deployment updates in a repeatable manner, known as **continuous deployment**.
- It enables us to automate the deployment process with minimal manual intervention.

#### **Integration with Azure**
1. Configured GitHub Actions to trigger deployment upon every push to the `main` branch, ensuring functions are updated instantly.
2. Used a YAML configuration file located in `.github/workflows/` to define the deployment workflow.

#### **Streamlined Workflow**
- Directly connected our Azure accounts to GitHub, reducing configuration complexity and saving time.
- Leveraged GitHub Secrets for storing sensitive portions of the Azure Function configuration:
  - **Encrypted settings** were used to ensure the deployment process remains secure.

This integration made the deployment process more efficient and secure, while maintaining flexibility for updates and changes.

## 🚧 Challenges

### **Authentication with Microsoft LearningPassport**
- One challenge was determining the best authentication method: whether to use a **cookie** or an **authorization header**.
- Sorting out this issue required testing and understanding how different authentication methods would impact security and integration.

---

### **Azure Function**
- Initially, we faced uncertainty about how to configure the Azure Function with the existing application.
- Ensuring compatibility with the larger system when deployed was a significant concern.
- **Scalability**: We needed to ensure the function could handle variable workloads without compromising performance or reliability.

---

### **Evaluating and Comparing Different LLMs**
- Measuring the response quality of each LLM was difficult due to the lack of quantitative evaluation methods.
- To address this, we ranked LLM options based on:
  - **Price**
  - **Recommendation quality**
  - **Ability to categorize**
- We tested these models using various prompts, altering the given list of courses and/or current course to see how their effectiveness changed based on:
  - **Age level**
  - **Title**
  - **Description**

This approach helped us identify the most cost-effective and high-performing LLM for our needs.

## 📈 Next Steps/Scalability

- **Exploring Paid LLM Options**:  
  If UNICEF is willing to invest more in an LLM, paid options like **GPT-4** or **Anthropic** could deliver better recommendation results and improved scalability as the user base grows.

- **Incorporating User Data**:  
  Currently, course recommendations are based only on the name and description of the current course. In the future, recommendations could be personalized by incorporating user-specific information, such as:
  - Course history
  - Learning goals
  - Age

- **Using a Vector Database and RAG**:  
  Leveraging a **vector database** with **Retrieval-Augmented Generation (RAG)** could help generate more accurate and context-aware recommendations.

- **Fine-Tuning Together.AI**:  
  If Together.AI continues to be used, it could be fine-tuned to better align with the specific task of providing accurate and effective course recommendations.
