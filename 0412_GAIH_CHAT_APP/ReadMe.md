# 📢 Global AI Bootcamp 2025 Hyderabad - 12 April 2025

## Date Time: 12-April-2025 at 09:00 AM IST

## Event URL: [https://www.meetup.com/global-ai-hyderabad/events/306095644](https://www.meetup.com/global-ai-hyderabad/events/306095644)



![Information | 100x100](./Documentation/Images/Information.PNG)

![Seat Belt | 100x100](./Documentation/Images/SeatBelt.PNG)


 
Session Title: Chat App - Azure OpenAI, Flask, React.js, and Tailwind CSS
---

### [ Introduction ]

1. Greeting & Session Overview:
   - "Good Morning, everyone! I'm Mucharla Sreelekha, and today, I'll guide you through the process of integrating Azure OpenAI into a Flask API—unlocking the power of  intelligent automation in your projects.”


        "Imagine a world where applications understand and respond to users just like a human assistant. Think of ChatGPT, but embedded seamlessly into your own       applications. Sounds exciting, right?"

   - “In the next few minutes, we’ll explore our project’s architecture, dive into the core code, and see a live demo where we send a sample prompt to our API.”

2. Session Objectives:  
   - Understand the system architecture behind a Flask API using Azure OpenAI.
   - Walk through the core code that powers the integration.
   - Live demo where we send a request and receive an AI-generated response. 


---

### [ Section 1: System Architecture Overview ]

1. The Architectural Diagram of the System :  

   - Visualizing the Flow:
      "Before we jump into the code, let’s first understand how the system works together. Let’s take a look at our architecture."

   - Components of Our System:
     1. Frontend (React UI) – The user interface (optional for today’s focus).
     2. Flask API (Backend Engine) – Handles client requests.
     3. Azure OpenAI Service – Processes requests and generates intelligent responses.
     4. Authentication & Logging (Optional Enhancements) – Ensuring security & monitoring. 

      ![Architectural Diagram | 100x100](./Documentation/Images/ArchitecturalDiagram.jpg)
     
  
2. Describing the Interaction Flow:  

    - How Everything Connects:
        "When a user inputs a prompt into our system, here’s what happens:"

         1. The React UI (or any client) sends a request to our Flask API.
         2. Flask processes the request and securely forwards it to Azure OpenAI.
         3. Azure OpenAI generates a response based on the provided input.
         4. Flask returns the AI-generated answer to the frontend.


    - Key Takeaway: This modular architecture makes our system scalable and easy to extend with security and logging mechanisms.


---

### [ Section 2: Code Walkthrough ]

1. Project Structure Overview:  
   - The directory layout:
     
               flask-react-aoai-completions/
               │── docs/
               │── src/
               │   ├── backend/
               │   │   ├── api/
               │   │   │   ├── home_routes.py
               │   │   │   ├── completions_routes.py
               │   │   ├── services/
               │   │   │   ├── azure_openai_service.py
               │   │   ├── utils/
               │   │   │   ├── env_config.py
               │   │   │   ├── error_handling.py
               │   │   │   ├── logging_config.py
               │   │   ├── app.py
               │── .env
               │── README.md
     

2. Flask API Initialization (app.py):  
   - “In app.py, we initialize our Flask application, configure logging, and register our blueprints. This is the entry point of our API.”
   - This function encapsulates the logic of communicating with Azure OpenAI and returning the complete response. 

3. Azure OpenAI Service (azure_openai_service.py): 

   -  Environment Variables Loading:
         We use the "os" module to load necessary credentials from environment variables:
              
               import os
               from openai import AzureOpenAI

               client = AzureOpenAI(
                  api_key=os.getenv("API_KEY"),
                  api_version=os.getenv("API_VERSION"),
                  azure_endpoint=os.getenv("ENDPOINT")
               )
               deployment_name = os.getenv("DEPLOYMENT_NAME")

         These include the API_KEY, ENDPOINT, DEPLOYMENT_NAME, and API_VERSION, which are essential for authenticating and connecting to the Azure OpenAI service.



   - Core Function – Azure OpenAI Call:

     
               def fetch_openai_response(prompt):
                  chat_prompt = [
                        {"role": "system", "content": "You are an AI assistant that helps people find information."},
                        {"role": "user", "content": prompt}
                  ]
                  try:
                        response = client.chat.completions.create(
                             model=deployment_name,
                             messages=chat_prompt,
                             max_tokens=800,
                             temperature=0.7,
                             top_p=0.95,
                             frequency_penalty=0,
                             presence_penalty=0,
                             stop=None,
                             stream=False
                        )
                        return response.choices[0].message.content
                  except Exception as e:
                        return f"Error: {str(e)}"

     
   - This function builds a chat prompt, sends it to the Azure OpenAI API, and returns the assistant’s response. It wraps the API interaction and error handling into a reusable, clean interface.

  
4. API Route for Completions (completions_routes.py):  
   
                @completions_api_bp.route("/completions", methods=["POST"])
                def generate_completion():
                    data = request.get_json()
                    prompt = data.get("prompt", "")
                    return Response(fetch_openai_response(prompt), content_type="text/plain")
     
   - This route handles POST requests to /completions. It extracts the prompt from the incoming JSON payload and returns the AI-generated response as plain text.

---

### [ Section 3: Live Demo ]

1. Start the Flask Server:  
   - “I’ll now start our Flask server by running python app.py.”
   - Show terminal output indicating the server is running on a specified port.

2. Test the API with PowerShell:  
   - “Let’s test the API using the following PowerShell command:”
     powershell
                Invoke-RestMethod -Uri "http://127.0.0.1:5009/api/completions" `
                                  -Method POST `
                                  -Headers @{"Content-Type"="application/json"} `
                                  -Body '{"prompt": "What is an Orange"}'
     
   - The resulting output :
         "An orange is a citrus fruit known for its sweet, tangy flavor and high vitamin C content."


   - “As you can see, the prompt is sent to our Flask API, which communicates with Azure OpenAI and returns the response.”



3. Key Points:  
   - Security: API keys and config are safely managed via environment variables.

  - Scalability: Though synchronous now, this setup provides a solid base for enhancements like streaming responses or frontend integration.

---

### [ Section 4: Q&A and Wrap-Up ]

1. Key Takeaways:  
   - “We explored how Flask interacts with Azure OpenAI to build an intelligent API.”
   - “We walked through the architecture, code structure, and API testing.”
   - “We successfully executed a live API call and received a response!”

2. Future Enhancements:  
   - “In future sessions, we’ll explore adding streaming support, a React frontend, and securing the API with Auth0.”
   - “This is just the beginning of building secure and intelligent AI applications.”

3. Open the Floor for Questions:  
   - “I’d now like to take any questions you might have about the architecture, code, or potential next steps.”

4. Closing:  
   - "The world is moving towards AI-powered applications, and today, you’ve taken a big step towards building one!"


"I hope this session has given you valuable insights into integrating Azure OpenAI with Flask. Feel free to reach out for questions, and let’s continue building intelligent solutions together!"

Thank you all for joining!!!

