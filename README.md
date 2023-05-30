# mesaGrande
*Quick-start behavioural methods for the Mesa module of Python.*

MesaGrande is a package of methods for use with the Mesa module in Python. Mesa supports the design and development of agent-based models (ABMs) that simulate the complexities of social interactions. These methods were designed, written, and tested by David Burgess (University of Saskatchewan), with acknowledgement (and equal parts frustration) attributed to OpenAI's ChatGPT. The below methods are contained within a custom Agent class (named AgentGrande) used with the Mesa module for Python designed by the members of Project Mesa. The included 20 methods have been designed to provide a quick-start means of implementing common, rudimentary, micro-social, -economic, and -health behaviours for agents of an Agent-Based Model (ABM). The methods rely on the existing design of the Agent class in the Mesa module.
Mesa Grande is a sub-division in Mesa.


## Usage

1. Download (or copy and paste the content of) the mesaGrande.py file and place it in the same directory as your simulation's ```agent.py```, ```model.py```, and ```server.py``` files.
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


## Limitations and Assumptions

The methods assume that the ```MultiGrid``` class is used and that the grid (or lattice) is toroidal. Agent neighbourhoods are assumed to be Moore.


## Modified MIT License

Copyright (c) 2023 David Burgess, University of Saskatchewan

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

Any academic work (publication or presentation) or commercial usage resulting 
from the use of this Software must include a citation analogous to the following:

AMA:

* Burgess, D. MesaGrande [Computer software]. Version 1.0. Saskatoon, Canada: University of Saskatchewan; 2023.

APA:

* Burgess, D. (2023). MesaGrande (1.0) [Computer software]. University of Saskatchewan. http://github.com/ssegrubdivad/mesagrande

Chicago:

* Burgess, David. MesaGrande. V. 1.0. University of Saskatchewan. Python. 2023.

Harvard:

* Burgess, D. (2023) MesaGrande (Version 1.0) [Computer program]. University of Saskatchewan, Saskatoon, Canada.

MLA:

* Burgess, David. MesaGrande. Version 1.0, University of Saskatchewan, 14 Jan. 2023.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.


## Included Methods

* Calculate Distance
* Move Randomly 
* Move Away 
* Move Toward
* Choose Random Agent Variable Value
* Increment Other Agent Variable
* Decrement Other Agent Variable
* Change Other Agent Variable
* Update Agent Record
* Update Agent Record in Radius 
* Edit Other Agent's Variable
* Only I Edit Other Agent's Variable
* Increment Self Attribute
* Decrement Self Attribute
* Move Toward Position
* Move Randomly, Collision Increment
* Move Randomly, Collision Decrement
* Move Between Positions
* Interact with Random Other Agent
* Play Tag


### Calculate Distance

This method takes two positions as tuples of integers as its arguments and then calculates and returns as an integer the spacial distance from the first positional argument to the second positional argument.

**Potential Use:** This method may be useful as a helper method for other micro-behaviour methods, and it is used as such within other methods of MesaGrande.

**Call:** You may call this method from within the ```step()``` method of an agent, as shown below; it calculates the spacial distance between two positions passed as arguments to the method:
```python
step():
    self.calculate_distance(pos1, pos2)
```


### Move Randomly

This method uses the ```get_neighborhood()``` method of the MultiGrid class to retrieve all possible positions that are within a radius of 1 of the current position. It then chooses one of these positions randomly and uses the ```move_agent()``` method of the MultiGrid to move the agent to that position.

**Potential Use:** This method provides the most rudimentary behaviour for any agent and may be additionally helpful for testing purposes in early model and agent development.

**Call:** You may call this method in the ```step()``` method of an agent, as shown below; it moves the calling agent one step on the grid in a random direction away from the calling agent's current position:
```python
step():
    self.move_randomly()
```


### Move Away
This method takes a grid coordinate position (in the form of a tuple consisting of two integers) as its argument and calculates the distance between that position and the current position of the calling agent. It then checks if the calling agent is closer to the right or left side of the grid, or if it is closer to the top or bottom of the grid — it then moves the agent one step on the grid away from the target position.

**Potential Use:** This method may be useful for simulating avoidance behaviours among agents.

**Call:** You may call this method in the ```step()``` method of an agent, as shown below; it moves the calling agent one step on the grid away from the target position:
```python
step():
    self.move_away(target_pos)
```


### Move Toward
This method takes a grid coordinate position (in the form of a tuple consisting of two integers) as its argument and calculates the distance between that position and the current position of the calling agent. It then checks if the calling agent is closer to the right or left side of the grid, or if it is closer to the top or bottom of the grid — it then moves the agent one step on the grid closer to the target position.

**Potential Use:** This method may be useful for simulating attraction behaviours among agents.

**Call:** You may call this method in the ```step()``` method of an agent, as shown below; it moves the calling agent one step on the grid closer to the target position:
```python
step():
    self.move_toward(target_pos)
```


### Choose Random Agent Variable Value
This method takes four arguments: ```radius``` (as an integer), ```var_name``` (as a string), ```value``` (as any data type), and ```operator``` (one of the six valid operator types ['==', '<', '>', '<=', '>=', or '!=']). It uses the ```get_neighbors()``` method of Mesa's MultiGrid class to retrieve all other agents within the radius of the calling agent. It filters out those agents that are not objects, the calling agent itself, and those agents that do not have as their value for the ```var_name``` variable compliant with the given operator. The method returns a randomly chosen agent from the filtered list of possible agents. If there is no possible agent within the radius, this method returns None.

**Potential Use:** This method may be useful in instances when an agent needs to identify another agent with a specific attribute in advance of taking other actions.

**Call:** You may call this method in the ```step()``` method of an agent, as shown below; it will select an agent randomly based on an agent class and a particular variable value:
```python
step():
    self.choose_random_agent_variable_value(radius, 'var_name', var_value, 'operator_type')
```


### Increment Other Agent Variable
This method takes two arguments: ```other_agent``` (as an object) and ```var_name``` (as a string). The method first checks if the other agent has a variable with the name of the given ```var_name``` using Python's ```hasattr()``` method. If the other agent does have the variable, it uses Python's ```setattr()``` method to increment the value of the variable by 1. If the other agent does not have the variable, it prints a message saying that the agent does not have the variable.

**Potential Use:** This method may be useful to record the passing of information from one agent to another, but only where the other agent is considered a passive recipient (as, when calling this method, the other agent has no choice but to accept the incremementing of their variable var_name).

**Call:** You may call this method in the ```step()``` method of an agent, as shown below; it increments the variable of another agent:
```python
step():
    self.increment_other_agent_var(other_agent, 'var_name')
```
