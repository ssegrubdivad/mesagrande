# mesagrande
*Quick-start behavioural methods for the Mesa module of Python.*

MesaGrande is a package of methods for use with the Mesa module in Python. Mesa supports the design and development of agent-based models (ABMs) that simulate the complexities of social interactions. These methods were designed, written, and tested by David Burgess (University of Saskatchewan), with acknowledgement (and equal parts frustration) attributed to OpenAI's ChatGPT. The below methods are contained within a custom Agent class (named AgentGrande) used with the Mesa module for Python designed by the members of Project Mesa. The included 20 methods have been designed to provide a quick-start means of implementing common, rudimentary, micro-social, -economic, and -health behaviours for agents of an Agent-Based Model (ABM). The methods rely on the existing design of the Agent class in the Mesa module.
Mesa Grande is a sub-division in Mesa.

**Usage:**
1. Download (or copy and paste the content of) the mesaGrande.py file and place it in the same directory as your simulation's agent.py, model.py, and server.py files.
2. Within the agent.py file, ensure the following import line is included:
```python & mesa
from mesaGrande import AgentGrande
```
3. Pass the AgentGrande class to your agent class when declared:
```python & mesa
class MyAgent(AgentGrande):
  ...
```
4. All of the methods included may now be used within your simulation.

**Limitations and Assumptions:**
The methods assume that the MultiGrid class is used and that the grid (or lattice) is toroidal. Agent neighbourhoods are assumed to be Moore.
