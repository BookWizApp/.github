# BookWizApp Automated_Book_summary_and_QA_generating_system
 
The project addresses the common reluctance
among people to read classic books. By providing
concise summaries and chatbot-like discussions,
the project aims to make classic literature more
accessible and appealing to a wider audience. It
targets individuals interested in exploring classic
texts, gaining insights into their content, and
engaging in meaningful conversations about the
ideas presented in the books.

<h3>Data Collection and Preparation</h3>

The project relies on several datasets to achieve its objectives.
The primary dataset is sourced from "Project Gutenberg,
" encompassing a comprehensive collection
of 70,000 classic books. This dataset serves as the testing data set, containing a diverse range of
classic texts that users can select from for engagement.
We used a Python script that searches for a book by name on the Project Gutenberg website, which
hosts a collection of free eBooks.
It uses web scraping techniques to find the best-matching book based on name similarity, retrieves the
download link for the plain text version of the book, and then attempts to retrieve and load the content
of the book using a custom “GutenbergLoader” class. If a matching book is found, it prints out the URL
and the loader object, otherwise, it indicates that no matching book was found.

<h3>Methodology</h3>

<h4>Used models</h4>

**"google/pegasus-cnn_dailymail"** - 
Pegasus is specifically designed for abstractive summarization that is more concise and creative
than extractive summaries. The maximum number of tokens this model can handle at a single time is
1023. The model is trained on a dataset of news articles and blog posts from the CNN/DailyMail
dataset. The dataset consists of over 2 million news articles and blog posts, which are about 1.6
billion words in total.

**“facebook/bart-large-cnn”** - 
BART is particularly effective when fine-tuned for text generation. This particular model has been
fine-tuned on CNN Daily Mail, a large collection of text-summary pairs. This model has a maximum
token limit of approximately 1024 tokens per input sequence. This means it can handle text inputs
with a combined token count of up to 1024 tokens.

**“all-MiniLM-L6-v2”** -
This is a sentence-transformers model: It maps sentences & and paragraphs to a 384 dimensional
dense vector space and can be used for tasks like clustering or semantic search. We used this
model to prepare vector databases and instructor embeddings.

**"TheBloke/Llama-2-13B-chat-GPTQ"** -
A text generation model is available on the Hugging Face platform. This LLM model can be used to
create a chatbot that gives accurate answers to the questions that the user is asking. Llama 2 was
pre-trained on 2 trillion tokens of data from publicly available sources. The fine-tuning data includes
publicly available instruction datasets, as well as over one million new human-annotated examples.
Neither the pretraining nor the fine-tuning datasets include Meta user data.

<h4>Method</h4>

**The BART Model:**
BART (Bidirectional and AutoRegressive Transformers) is a powerful language model developed by
Hugging Face that excels in text summarization. It's capable of understanding context, coherence,
and saliency in text. 

**LangChain's Approach:**
LangChain is a text-processing framework that leverages the BART model to create an efficient
summarization pipeline.

**The Map-Reduce Method:**
LangChain utilizes the Map-Reduce method, a distributed computing paradigm, to divide the
summarization task into smaller, manageable parts. This approach allows for parallel processing,
significantly reducing the time required for summarizing large documents.

**Map Phase:** LangChain's Map step divides the text into smaller chunks and sends them to the BART
model. Each chunk is independently summarized, generating intermediate summaries.

**Reduce Phase:** The intermediate summaries are then combined and refined in the Reduce phase. This
step ensures that the final summary is coherent, comprehensive, and well-structured.

------ 
**Prepare the vector Database with Instructor Embeddings**

We created a database using the Chroma library, where each document from the texts collection is
associated with its corresponding embedding from the embeddings collection. The resulting
database is saved in the directory specified by persist_directory. The purpose of this is to enable
efficient storage, retrieval, and manipulation of text documents along with their embeddings for
various analytical or information retrieval tasks.

**Create a chain with Llama 2 13B GPTQ LLM**

This initializes a quantized GPT-based chatbot model using the "Llama-2-13B-chat-GPTQ" variant. The
model is loaded along with a tokenizer, and various parameters are set to control its behavior and
execution environment. The quantization process aims to reduce the model's memory footprint while
maintaining its functionality.

**Using system prompts*

This defines a function “generate_prompt” that helps create a well-structured prompt for a
conversational AI system. It includes both the user's query and the system's predefined instructions to
guide the AI's response generation process. This approach ensures that the AI produces responses
that adhere to certain guidelines and ethical considerations.

<h3> Evaluation Metrics used </h3><br>
For the summarization model using "Bart" and "Pegasus," we plan to measure the
performance using a standard summarization evaluation metric called ROUGE:
ROUGE (Recall-Oriented Understudy for Gisting Evaluation): ROUGE measures the
overlap between generated summaries and reference summaries in terms of n-gram
matches and word sequences. We'll use ROUGE-1, ROUGE-2, and ROUGE-L
(longest common subsequence) scores to evaluate the quality of summaries.
<br><br>
For the Q&A section using LLMs like "Eluwa," evaluation might focus on qualitative
aspects such as the relevance of the responses to user queries, the coherence of the
generated text, and the ability to maintain context in ongoing conversations. These
aspects can be assessed through user feedback and interaction simulations.


