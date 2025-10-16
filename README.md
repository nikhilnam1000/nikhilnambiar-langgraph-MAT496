Foundation: Introduction to Langgraph for MAT 496
# Module 1
## Lesson 1
We are introduced to the notion of an agent, which is the control flow (steps pre/post LLM call like tools, retrieval, etc) determined by an LLM.
There are many types of agents, depending on how much control you wanna give to the llm from router (lower control) to fully autonomous agents.

Langgraph aims to balance reliability with control with respect to the control flow in agents.  
We then go over what we will cover in all the modules of the course briefly.

## Lesson 2
We build a simple graph using langgraph. States,nodes and edges are discussed, and during the initializing of the graph, I changed the string with which a node state is updated and the probability with which we refer to a particular node.  
Then we move onto the visual aspect of the graph. Multiple graph invokes confirms our updated proportion is working and the presence of the updated string.