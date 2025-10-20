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

## Lesson 2
We are introduced to the notion of *state reducers*
1. We run a simple type dict with 1 node, and update the state by adding one, which is overwritten.
2. We run into a problem when we have branching nodes— since there is ambiguity as to which state to update while the graph attempts simultaneous updates (which isn't possible) and therefore we get an error.
3. With reducers, we specify how to perform updates, eliminating ambiguity. In our specific example, the overwriting is replaced by list concatenation and so the value at each node is just appended to a list and we don't have an error anymore.
4. We then look at custom reducers for specific use cases, wherein we define a function and then use that function as our reducer to fix an error **(see state-reducers.ipynb)**
5. We look at appending messages for context by using the add_messages reducer (using custom messages).
6. We also discuss re-writing (custom re-writing for experimenting) and removal of messages.


## Lesson 3
We open with reasons why we would need more control over schemas.
1. Then we use Private States for passing on states inside the langgraph nodes and the Overall State which is visible to the user.
2. We then define custom Input and Output states through user defined functions and then use it in our nodes. **(see multiple-schemas.ipynb)**
3. We can use this to restrict what is shown in inputs and outputs is the schema as per use case.

## Lesson 4
We define message as state (custom messages), pass them onto an LLM model and then visualize using langgraph.
1. We then move onto tackling long running conversations using reducers. So we define custom reducers to do so (for example, a reducer that deletes all but the last two messages in a conversation, this number could be changed as per need).
2. We take a look at LangSmith platform to see the workings.
3. We also use Trim Messages to limit token usage, and then open the LangSmith platform to see the runs.

