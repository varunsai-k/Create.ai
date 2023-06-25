<h1 align='center'>Create<b style="color: MediumBlue;">.</b>ai</h1>
<p>Create<b style="color: MediumBlue;">.</b>ai is an AI-powered content creation tool that can help you level up your YouTube channel. With Create.ai, you can generate high-quality content in minutes, including titles, descriptions, scripts, and even entire videos.Whether you're a beginner or a seasoned YouTuber, Create.ai can help you take your channel to the next level.</p>
<br>


<img src="https://binus.ac.id/malang/communication/wp-content/uploads/sites/3/2021/05/1.jpg" style="width:1000px;height:500px;" class="center">


<br>
<p><b>Create</b><b style="color: MediumBlue;">.</b><b>ai</b> uses langchain to integrate large language model to input data source.<b style="color: black;">🦜️🔗 LangChain</b> is a framework for developing applications powered by language models.For Using Langchain and integrating large language models from OpenAI we need to set up an OpenAI environment.</p>

<h3>Setting Up Environment</h3>

<p>An environment variable is a variable that is set on your operating system, rather than within your application. It consists of a name and value.We recommend that you set the name of the variable to OPENAI_API_KEY. By keeping this variable name consistent across your team, you can commit and share your code without the risk of exposing your API key.</p>

<code class="prettify" style="color: Purple;">import os <br> os.environ['OPENAI_API_KEY']='your openai key here'</code>

<h3>LLMs</h3>

<p>The basic building block of LangChain is the LLM, which takes in text and generates more text.we're building an application that generates title, script, description based on content. In order to do this, we need to initialize an OpenAI model wrapper. In this case, since we want the outputs to be MORE random, we'll initialize our model with a HIGH temperature.</p>

<code class="prettify" style="color: Purple;">from langchain.llms import OpenAI
  <br> llm = OpenAI(temperature=0.9)</code>

<h3>Prompt templates</h3>

<p>Most LLM applications do not pass user input directly into to an LLM. Usually they will add the user input to a larger piece of text, called a prompt template, that provides additional context on the specific task at hand. I used different prompt templates for title generation, script generation etc. Prompt templates provides best experience so that the users can just only pass the content they are intrested to create. based on the content the prompt templates takes it as input and generates title for youtube video.Now video script is generated based on the title generated bt title template. In this prompt templates work in different ways.</p>

<code class="prettify" style="color: Purple;">from langchain.prompts import PromptTemplate
<br> title_template = PromptTemplate(input_variables = ['topic'], template='write me a youtube video title about {topic}')</code>

<p>Similarly, other templates are defined based on the title generated by title template as input. </p>

<h3>Chains</h3>

<p>Chains give us a way to link (or chain) together multiple primitives, like models, prompts, and other chains.</p>

<code class="prettify" style="color: Purple;">prompt=input('enter your prompt here') 
<br> from langchain.chains import LLMChain 
<br> title_chain = LLMChain(llm=llm, prompt=title_template)<br> title_chain.run(prompt)
</code>

<p>Similarly, we are creating chains for different templates.</p>

<h3>Memory</h3>

<p>The chains and agents we've looked at so far have been stateless, but for many applications it's necessary to reference past interactions.The Memory module gives you a way to maintain application state. The base Memory interface is simple: it lets you update state given the latest run inputs and outputs and it lets you modify the next input using the stored state.</p>

<code class="prettify" style="color: Purple;">title_memory = ConversationBufferMemory(input_key='topic', memory_key='chat_history')
<br> title_chain = LLMChain(llm=llm, prompt=title_template, verbose=True, output_key='title', memory=title_memory)
<br> title = title_chain.run(prompt)
</code>

<h3>WikipediaAPIWrapper</h3>

<p>This wrapper will use the Wikipedia API to conduct searches and fetch page summaries. Using wikipedia api wrapper, we can save the search results and we can also able to know the research made by model on different wiki pages. </p>

<code class="prettify" style="color: Purple;">wiki = WikipediaAPIWrapper()
<br> wiki_research = wiki.run(prompt)</code>
<br><br><br>

<div align="middle">
    <video src="creativity.mp4" width="80%" controls autoplay/>
</div>
