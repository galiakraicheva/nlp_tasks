# NLP Tasks: 

### Task 1: Websummarisation

**Write a Python script that loads an article from the internet and generates a summary and title using a large language model (LLM)**

The task consists of 2 parts: 1) To get the text from the Internet and 2) to summarise it. For the first part I do almost the same for all models.

For the second part, I try three combinations of models:

- [BART with no LangChain](https://github.com/galiakraicheva/nlp_tasks/blob/main/websummarisation/bart_websummarisation.ipynb): since it is the simplest model, I try different ways to truncate the text since BART only works with 1024 tokens. I try textwrap module with shorter and longer output and it performs realtively good in summarisation. However, it rases lots of warnings because the text truncating happens based on characters and not tokens and it is not guaranteed that the characters will meet the token requirements of the model. Since these warnings are annoying, I try to adjust the max_length dynamically. It works good for all the chuncks except for the last one which is normal since the last one is shorter. Then I try another way of chunking with tokens since the model doesn't work with characters but with tokens and again, it gave lots of warnings but that is also normal since the text has many short sentences and therefore, it is possible that it has shorter chuncks. Since the warnings are explainable and don't mess up the output, I don't pay too much attention to them for the models to follow (if they don't mess up the future results either). In terms of output, all the models worked well and the best seems to be the one with the longer summary.
- [LangChain and BART](https://github.com/galiakraicheva/nlp_tasks/blob/main/websummarisation/langchain_bart_summarisation.ipynb): First I try the LangChain syntax without chunking and with shorter text, then in the Revised code, I make the code more complex with chunking, longer output and add a title. The revised code gives a good summarisation, the first one is too simple and with no chunking, it doesn't perform well.
- [LlaMa](https://github.com/galiakraicheva/nlp_tasks/blob/main/websummarisation/llama_sumarisation.ipynb): Since the model is mentioned in the assignment, I try summarisation with it. I chose the smallest of the LlaMa 3.2 family so that it can run on my laptop fast enough. I did a code snippet without LangChain and with LangChain. Both worked well. Generating more than once gives a different output and in most cases, the output is a good summary and title but it can happen that there is a messed up part here or there. All of this seems normal to me because 1) it is possible to have different output due to the sampling technique of the model and not always picking the most probable token and 2) the model can make mistakes since it is the smallest of all. I have left an output with a mistake in the title but in general, from all the iterations that I did, the code snippets gave good summaries and titles. It may be interesting to see if I can fine-tune the model to give better results, like for example, to change the temperature or put constraints on the generated text. To know this, I need to run the model more times and try to find a pattern in the mistakes it gives. 

What should be next: if one has time or needs to really have a good and reliable model for summarisation, it is a good idea to see how one can evaluate the performance of the models. So far I have evaluated them by reading and desiding if they make sense but for a formal evaluation, I need to have a database of websites and good summaries to test if the generated summaries resemble the good reference summaries. For the creation of this database, I can use a stronger model like GPT-4 to summarise texts or do human summaries but this goes beyond the scope of the task. Good evaluation metrics would be ROUGE and BERTScore. 

### Task 2: Youtube Transcript Summarisation

**Extract and summarize the transcript of a YouTube video using YouTube’s API and an LLM.**

As before, the task consists of 2 parts: 1) get the transcript from the video; 2) summarise.

The task resembles the previous one and the summarisation part is the same as before. As for the first part I use youtube_transcript _api library in Python. I get the text and I break it into chunks to fit the model's maximum number of tokens. For a model, I have tried BART and it worked well for long text. For short text like song lyrics, I tried BART and t-5-base as well as additional preprocessing and what worked best was again BART with no additional text preprocessing. Here is the code and the explanations in a [Jupiter Notebook](https://github.com/galiakraicheva/nlp_tasks/tree/main/youtube_video_transcripts_summarisation). 

The short summaries are not ideal and if it was a real task, it would be a good idea to fine-tune a model to summarise song lyrics better. In reality, however, it is very unprobable that there will be a real-life task to summarise short texts and lyrics of music videos since they are usually so short that they don't need a summary. So the best model is the first one which should work well in a variety of transcripts. 


### Task 3: Multi-document summarisation

**Scrape multiple web pages on the same topic and generate a consolidated summary**

