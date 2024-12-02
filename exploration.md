# Target:
Receive natural language input from a patient and extract taget data.
- User feedback: How will missing information be recognized and how will clarifications be prompted?
- Prompt generation: How will prompts be generated? Tailored for specific info required?
- What will the underlying structure of the data be?
- How will privacy regulations be addressed? Dealing with sensative user data

# Project Objectives
- Increase efficiency of onboarding process
- Convert NL input to structured data to support downstream uses
- Ensure security and integrity of patient data

# NLP Objectives:
- (Named) Entity and Intent Recognition: 
    - Identify entities from user input and associate them with data targets (patient name and location, symptoms, medications, insurance info, etc.)
    - Request clarifications on entities with ambiguity
    - Associate unknown entities with general concepts, refine assications via clarifications
- Contextual Awareness: 
    - Context between prompts and responses should be retained throughout the conversation
    - If a user's identity is known: incorporate known information about the user (from past conversations, medical history)
- Sentiment Analysis: 
    - *Determine the overall sentiment or emotion from the user's inputs and react accordingly*
    - Enhances the ability of the chatbot to provide a user-tailored experience 
- Data Validation:
    - Ensure the consistency and integrity of information by requesting clarification for conflicting data points

# Things to keep in mind:
* Multi-lingual support? Translation?
* Ensure chatbot has proper medical knowledge-base
* Extensions of the model: used in conjunction with OCR or audio transcription to improve experience for specific userbases (visual impairments, geriatric patients, etc.)

# Structured Data Target
- Heirarchical? Relational?
- What kinds of data are required? Optional?
- How will missing data be addressed? A form might not let you submit without certain required fields, how will the chatbot handle this?

# NLP Implementation:
1. Intent and Entity Recognition
    - Model Selection: 
        - pre-trained GPT models, with healthcare fine tuning
        - [BioBERT](https://arxiv.org/abs/1901.08746) (BERT trained on biomedical text)
        - [MedNER](https://dl.acm.org/doi/10.1145/3678178)
    - Intent Definition: define set of intents the model should recognize
    - Entity Definition: define a set of entity classes to train the model to recognize
    - Training Data:
        - NL inputs associated with intent class(es) and entities
2. Contextual Awareness
    - Stateful Converstaion Model: track previous exchanges
        - State variables: relevant medical info, location data, etc.
    - Task-Oriented Dialogue: [DiagGPT](https://arxiv.org/html/2308.08043v4) ensamble LLM approach to enhance topic-oriented tasks
    - Memory: both short-term (intra-conversation) and long-term (inter-conversation)
3. Sentiment Analysis
    - Sentiment and emotion recognition
        - VADER model for sentiment analysis
    - Incorporate emotions and sentiments into conversational state to enhance user-personalization
4. Evaluation
    - [Task-oriented evaluation](https://arxiv.org/abs/2312.13871)
    - [ToolSandbox](https://arxiv.org/html/2408.04682v1)