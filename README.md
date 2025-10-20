Foundation: Introduction to Langgraph for MAT 496
# Module 1
## Lesson 1
We are introduced to the notion of an agent, which is the control flow (steps pre/post LLM call like tools, retrieval, etc) determined by an LLM.
There are many types of agents, depending on how much control you wanna give to the llm from router (lower control) to fully autonomous agents.

Langgraph aims to balance reliability with control with respect to the control flow in agents.  
We then go over what we will cover in all the modules of the course briefly.

## Lesson 2
We build a simple graph using langgraph. States,nodes and edges are discussed, and during the initializing of the graph, I changed the string with which a node state is updated and the probability with which we refer to a particular node.  
Then we move onto the visual aspect of the graph. Multiple graph invokes confirms our updated proportion is working and the presence of the updated string. **(see simple-graph.ipynb)**

## Lesson 3
Introduction to Langsmith Studio and its functionality which offers a more visually rich experience with a lot of useful features discussed briefly. No ipynb file associated.

## Lesson 4
We initialize a conversation with some human and AI messages then pass that context to a model to solicit a response (context changes to explore structure).
We then define a tool pass in a message that invokes said tools and then we use the messages as state in langgraph, defining reducers in the process **(see chain.ipynb for detailed discussions)**. Finally we invoke our graphs.

## Lesson 5
We add a tool to our router which, depending on the content of the messages will choose to either invoke or not invoke the tool. Not much to tweak with. **(see router.ipynb)**

## Lesson 6
We extend what we did in lesson 5 to a generic agent architecture by giving a ToolMessage back to the llm instead of the user. We then dicuss the structure of ReAct and then build and execute it. Again nothing significant to tweak, could've changes the tool function and aimessage prompt. **(see agent.ipynb)**

## Lesson 7
We again extend what we did in lesson 6 to introduce the concept of memory for our agent, which we demonstrate has no concept of memory on its own. We use persistence to address this problem, discussed in detail in agent-memory.ipynb. AGain nothing significant to tweak, can change the tools and context messages but nothing paradigm altering.

# Module 2
## Lesson 1
We begin with a quick recap of what we did in module 1 and the beginning of the code **(see state-schema.ipynb)** with user defined states and nodes, and invoking them as before.  
1. Then we discuss python data classes as an alternative way to type dict for establishing schema for our graph for versatility.
2. The problem with both these methods are that they don't enforce types at runtime, which means that invalid values don't produce errors.
3. So we use Pydantic, a powerful data validation library to address and solve this problem, and this time for invalid values we see an error.
4. We then integrate this with our langgraph agent and verify that invalid values cause an error, I have added an additional cell in the ipynb file to demonstrate valid and invalid values.