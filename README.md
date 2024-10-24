# gradio_distilGPT2
This code is to create a web-based document-reading chatbot where users can upload a document and interact with it by asking questions
This code sets up a document-based chatbot using a small language model like DistilGPT-2 or GPT-2, combined with PDF and TXT file handling for providing context from uploaded files. It uses Gradio to create a web-based interface where users can interact with the model by uploading a file (either PDF or TXT) and entering prompts. Here's a breakdown of the key parts and the overall intention:

**Key Components:**
1. **Dependencies Installation:**
The required libraries (transformers, gradio, pdfplumber, and torch) are installed, which include the tools for working with language models, creating web interfaces, and extracting text from PDFs.

2. **Model and Tokenizer Setup:**
The code loads a small language model (like DistilGPT-2) and its corresponding tokenizer. This model is used to generate text responses based on the user's prompt and the content of the uploaded document. It uses GPU if available, falling back to CPU otherwise.

3. **Text Extraction from PDF and TXT:**
The pdfplumber library is used to extract text from PDF files, while simple reading and decoding are used for TXT files. These functions handle both file types and return an error if something goes wrong (like an unsupported file format or failure to extract text).

4. **Prompt Suggestions:**
The code includes a basic heuristic to generate prompt suggestions for the user based on keywords in the extracted text (e.g., if the text contains words like "chapter" or "conclusion"). These suggestions help guide the user to ask relevant questions.

5. **Chatbot Function:**
The core of the system is the chatbot_fn, which takes a user prompt and a file, extracts text from the file, and generates a response based on the model's output. To improve efficiency, tokenized inputs are cached so that the same content isn't re-tokenized multiple times.The chatbot history is updated with each interaction, storing both user inputs and model responses.

6. **Gradio Interface:**
Gradio is used to build a simple, shareable web interface. Users can:
- Upload a PDF or TXT file.
- Enter their message or prompt.
- Adjust the number of tokens for model responses using a slider.
- See the chat history in a text box, and view prompt suggestions dynamically based on the uploaded file content.
- The submit_button.click() is tied to the chatbot function, which processes user inputs and updates the interface accordingly.

7. **Caching and Performance Considerations:**
The code uses a caching mechanism for tokenized inputs to speed up the process by avoiding redundant tokenization.
The model generates responses with a configurable max_new_tokens, which controls the length of the chatbot's replies.

8. **Launching the Interface:**
The Gradio interface is launched with share=True, which means that a public link will be generated, allowing external users to test the chatbot.

**Overall Intention:**
The purpose of this code is to create a web-based document-reading chatbot where users can upload a document and interact with it by asking questions. The chatbot reads the content from the uploaded file, processes the text, and generates contextually relevant responses. This is useful for summarizing or discussing the contents of documents using a small language model.
