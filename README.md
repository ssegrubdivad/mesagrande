# MesaGrande
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

* Burgess, D. _MesaGrande_ [Computer software]. Version 1.0. Saskatoon, Canada: University of Saskatchewan; 2023.

APA:

* Burgess, D. (2023). _MesaGrande_ (1.0) [Computer software]. University of Saskatchewan. http://github.com/ssegrubdivad/mesagrande

Chicago:

* Burgess, David. _MesaGrande_. V. 1.0. University of Saskatchewan. Python. 2023.

Harvard:

* Burgess, D. (2023) _MesaGrande_ (Version 1.0) [Computer program]. University of Saskatchewan, Saskatoon, Canada.

MLA:

* Burgess, David. _MesaGrande_. Version 1.0, University of Saskatchewan, 14 Jan. 2023.

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

**Call:** You may call this method in the ```step()``` method of an agent, as shown below; it calculates the spacial distance between two positions passed as arguments to the method:
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

**Potential Use:** This method may be useful to record the passing of information from one agent to another, but only where the other agent is considered a passive recipient (as, when calling this method, the other agent has no choice but to accept the incremementing of their variable ```var_name```).

**Call:** You may call this method in the ```step()``` method of an agent, as shown below; it increments the variable of another agent:
```python
step():
    self.increment_other_agent_var(other_agent, 'var_name')
```


### Decrement Other Agent Variable
This method takes two arguments: ```other_agent``` (as an object) and ```var_name``` (as a string). The method first checks if the other agent has a variable with the name of the given ```var_name``` using Python's ```hasattr()``` method. If the other agent does have the variable, it uses Python's ```setattr()``` method to decrement the value of the variable by 1. If the other agent does not have the variable, it prints a message saying that the agent does not have the variable.

**Potential Use:** This method may be useful to record the passing of information from one agent to another, but only where the other agent is considered a passive recipient (as, when calling this method, the other agent has no choice but to accept the decremementing of their variable ```var_name```).

**Call:** You may call this method in the ```step()``` method of an agent, as shown below; it decrements the variable of another agent:
```python
step():
    self.decrement_other_agent_var(other_agent, 'var_name')
```


### Change Other Agent Variable
This method takes three arguments: ```other_agent``` (as an object), ```var_name``` (as a string), and ```new_value``` (as any data type). The method first checks if the passed other agent has a variable with the name passed as ```var_name``` using Python's ```hasattr()``` method. If the other agent does have the variable, the method uses Python's ```setattr()``` method to change the value of the variable to the passed ```new_value```. If the other agent does not have the variable, the method prints a message saying that the agent does not have the variable.

**Potential Use:** This method may be useful to record the passing of information from one agent to another, but only where the other agent is considered a passive recipient (as, when calling this method, the other agent has no choice but to accept the new value of their variable ```var_name```).

**Call:** You may call this method in the ```step()``` method of an agent, as shown below; it changes the variable of another agent to any value you want:
```python
step():
    self.change_other_agent_var(other_agent, 'var_name', new_value)
```


### Update Agent Record
This method takes three arguments: ```other_agent``` (as an object), ```var_name``` (as a string), and ```new_value``` (as any data type). The method iterates over the list of agent_records and checks if the ```unique_id``` value of the record matches the given ```unique_id``` of the other agent. If it does, it updates the record with the new ```var_name``` and value. If it doesn't find a match, it appends a new record with the ```unique_id``` of the other agent, the ```var_name```, and value to the ```agent_records``` list.

**Potential Use:** This method may be useful to record the passing of information about other agents by the calling agent.

**NB:** Be sure to include the following attribute within the Agent's constructor method to initialize the ```self.agent_records``` iterable:
```python
def __init__(self, unique_id, model):
    super().__init__(unique_id, model)
    self.agent_records = [] # <— this line is required to be added
```

**NB:** The resulting self.agent_records iterable is formatted as follows:
```python
[[unique_id_x, ('var_name', new_value)],[unique_id_y, ('var_name', new_value)],[unique_id_z, ('var_name', new_value)]]
```

**Call:** You may call this method in the ```step()``` method of an agent, as shown below; it updates the record of another agent based on its ```unique_id```:
```python
step():
    self.update_agent_record(other_agent, 'var_name', new_value)
```


### Update Agent Record in Radius
The method takes four arguments: ```other_agent``` (as an object), ```radius``` (as an integer), ```var_name``` (as a string), and ```new_value``` (as any data type). The method returns ```None```. This method differs from the ```update_agent_record()``` method (of MesaGrande) in that it takes the radius argument.

The method first uses Mesa's grid's ```get_neighbors()``` method to collect all other agents within the given radius of the calling agent. A for loop is used to iterate through the list of agent records — that is, the ```self.agent_records``` — and checks for the record that has the same ```unique_id``` as the passed other agent. When it finds the record, it updates the variable name and value in the second dimension of the record.

**Potential Use:** This method gives each agent the ability to observe other agents (perhaps all other agents, perhaps a select group or a single other agent) one at a time within a step from a given distance (and no farther away), and then record information about the other agents in their own journal — the ```self.agent_records``` variable. These observations are updated each time the other agent is observed (that is, this method does not create a chronological record).

**NB:** Be sure to include the following within the Agent's constructor method to initialize the ```self.agent_records``` iterable:
```python
def __init__(self, unique_id, model):
    super().__init__(unique_id, model)
    self.agent_records = [] # <— this line is required to be added
````

NB: The resulting self.agent_records iterable is formatted as follows:
```python
[[unique_id_x, ('var_name', new_value)],[unique_id_y, ('var_name', new_value)],[unique_id_z, ('var_name', new_value)]]
```

**Call:** You may call this method in the ```step()``` method of an agent, as shown below; it updates the calling agent's records on another agent when that other agent is within a certain radius:
```python
step():
    self.update_agent_record_in_radius(other_agent, radius, 'var_name', new_value)
```

### Edit Other Agent's Variable
This method takes three arguments: ```other_agent``` (as an object), ```var_name``` (as a string), and ```new_value``` (as any data type). The method uses Python's ```hasattr()``` method to check if the other agent already has an attribute with the same name as the ```var_name``` passed to the method. If the other agent does, this method updates the value of the variable to the ```new_value``` passed to the method. If the attribute does not exist, it creates the variable and assigns the ```new_value``` passed to the method. In common use, it may be helpful to limit those other agents passed to this method such that they are within only a certain radius around the calling agent seeking to update the other agent's attribute's value. This could be done by using the ```choose_random_agent_var_value()``` method (of MesaGrande).

**Potential Use:** This method may be useful for situations when an agent requires the ability to (independent of the other agent) add and edit an attribute of that other agent, and which that other agent did not have a birth (when added to the grid). This situation might be considered analogous to infecting agents with some attribute, the severity of which could be changed by other agents, without the infected agent knowing that the infection has happened or that the severity has changed. Please be sure to read the NB caveat, below.

**NB:** When using this method, be aware that ```AttributeErrors``` may arise if these not handled appropriately. This will happen because the var_name variable is being referenced by the ```edit_other_agent_var()``` method (of MesaGrande) before the variable is created — Python assumes that variables will be defined before they are referenced. Consider implementing the following ```try/except/else``` statements to ensure such errors do not cause the simulation to fail:
```python
try other_agent.var_name:
except (AttributeError, TypeError):
    # do this when other_agent.var_name variable does not yet exist
    pass
else:
    # do this when other_agent.var_name variable exists
    pass
```

**Call:** You may call this method in the ```step()``` method of an agent, as shown below; it allows the colling agent to edits other agent's attributes:
```python
step():
    self.edit_other_agent_var(other_agent, 'var_name', new_value)
```


### Only I Edit Other Agent's Variable
This method takes three arguments: ```other_agent``` (as an object), ```var_name``` (as a string), and ```new_value``` (as any data type). The method uses Python's ```hasattr()``` method to check if the other agent already has an attribute with the same name as the ```var_name``` variable passed to this method. If it does, this method then checks to see if the calling agent is the same agent that originally created the attribute in the other agent. If it is, it updates the value of the variable to the ```new_value``` passed in this method. If the variable does not exist, this method creates the variable and assigns the new_value passed to this method along with the ```unique_id``` of the calling agent. This method differs from the ```edit_other_agent_var()``` method (of MesaGrande) in that it only permits the the calling agent that created the attribute in the other agent to edit it in the future. Using this method, calling agents can potentially create and control different attributes in different other agents. In common use, it may be helpful to limit those other agents passed to this method such that they are within only a certain radius around the calling agent. This could be done by using the ```choose_random_agent_var_value()``` method (of MesaGrande).

**Potential Use:** This method may be useful for situations when you want a calling agent to have the ability to (independent of another agent) add and edit an attribute of another agent that the other agent did not have a birth (that is, when added to the grid). This situation might be considered analogous to infecting agents with some attribute, the severity of which can only be changed by the original infecting agents, without the other agent knowing that the infection has happened or that the severity has changed. Please be sure to read the NB caveat, below.

**NB:** When using this method, be aware that ```AttributeErrors``` may arise if these not handled appropriately. This will happen because the var_name variable is being referenced by the ```only_I_edit_other_agent_var()``` method before the variable is created — Python assumes that variables will be defined before they are referenced. Consider implementing the following ```try/except/else``` statements to ensure such errors do not cause the simulation to fail:
```python
try other_agent.var_name: # could also be written try self.var_name:
except (AttributeError, TypeError):
    # do this when other_agent.var_name or self.var_name variable does not yet exist
    pass
else:
    # do this when other_agent.var_name or self.var_name variable exists
    pass
```

**Call:** You may call this method in the ```step()``` method of an agent, as shown below; it allows the calling agent to edit another agent's attributes — and only the calling agent for that particular attribute of that other agent:
```python
step():
    self.only_I_edit_other_agent_var(other_agent, 'var_name', new_value)
```


### Increment Self Attribute
This method takes three arguments: ```attribute_name``` (as a string and which represents the name of the attribute to be incremented), ```guard_attribute_name``` (as a string and which represents the name of the attribute that acts as a guard), and ```inc_value``` (as a float and which represents the value by which the attribute to be incremented will be incremented). The method returns ```None```.

This method first uses Python's ```getattr()``` method to retrieve the value of the ```guard_attribute_name```. If the value of the ```guard_attribute_name``` is ```False```, this method again uses Python's ```getattr()``` method to retrieve the current value of the ```attribute_name```. Following this, this method increments the current value of the ```attribute_name``` by the inc_value and next uses Python's ```setattr()``` method to update the ```attribute_name``` with the incremented value.

**Potential Use:** This method may be useful for situations when the value of some attribute of the agent should progressively increase only when another attribute of that agent is switched off.

**Call:** You may call this method in the ```step()``` method of an agent, as shown below; it increments an agent's attribute by the amount of the ```inc_value``` if a guard attribute is ```False```:
```python
step():
    self.increment_self_attribute('var_name', 'guard_var_name', inc_value)
```


### Decrement Self Attribute
This method takes three arguments: ```attribute_name``` (as a string and which represents the name of the attribute to be decremented), ```guard_attribute_name``` (as a string and which represents the name of the attribute that acts as a guard), and ```dec_value``` (as a float and which represents the value by which the attribute to be decremented will be decremented). The method returns ```None```.

This method first uses Python's ```getattr()``` method to retrieve the value of the ```guard_attribute_name```. If the value of the ```guard_attribute_name``` is ```False```, this method again uses Python's ```getattr()``` method to retrieve the current value of the ```attribute_name```. Following this, this method decrements the current value of the ```attribute_name``` by the ```dec_value``` and next uses Python's ```setattr()``` method to update the ```attribute_name``` with the decremented value.

**Potential Use:** This method may be useful for situations when the value of some attribute of the agent should progressively decrease only when another attribute of that agent is switched off.

**Call:** You may call this method in the ```step()``` method of an agent, as shown below; it decrements an agent's attribute by the amount of the ```dec_value``` if a guard attribute is ```False```:
```python
step():
    self.decrement_self_attribute('var_name', 'guard_var_name', dec_value)
```


### Move Toward Position
This method takes two arguments: ```x``` and ```y``` (which are integers representing the x and y coordinates of the position the calling agent should move towards). It returns ```None```.

This method first calculates the respective difference between the ```x``` and ```y``` coordinates of the calling agent's current position and the target position.

The method then checks if the difference between the ```x```s is greater than the difference between the ```y```s, if so it moves the agent one step closer to the target position in the x-direction. If not, it moves the agent one step closer to the target position in the y-direction.

The included ```move()``` helper method takes two arguments: ```dx``` and ```dy``` (as integers representing the change in position of the calling agent in the x and y direction). The ```move()``` helper method returns ```None```.

The ```move()``` helper method first calculates the new position of the agent based on its current position and the change in position passed as arguments. It then checks if the new position is occupied or not, if it is not occupied the ```move()``` helper method moves the agent to that position by calling Mesa's ```move_agent()``` method of the grid and passing the calling agent and the new position as arguments. If the new position is occupied, it iterates through a list of adjacent positions and checks if any of them are unoccupied. If an unoccupied position is found, it moves the agent to that position, otherwise it will not move the agent.

**Potential Use:** This method may be useful when agents are required to move to a certain location (perhaps for a given period of time) as directly as possible while still avoiding other agents.

**Call:** You may call this method in the ```step()``` method of an agent, as shown below; it moves the agent one space on the grid closer to a given position on the grid until it arrives at that position and stops or it encounters an obstacle in the path of the agent to the given position and attempts to move around the obstacle:
```python
step():
    self.move_toward_position(x, y)
```


### Move Randomly, Collision Increment
This method takes in three arguments: ```OtherAgentClass``` (a class of agents to check against for collision), ```var_name``` (as a string and which represents the attribute of the calling agent to increment if a collision occurs), and ```inc_value``` (as an integer and which represents the amount to increment ```var_name``` by if a collision occurs).

This method moves the calling agent randomly on the grid, then checks if the calling agent's new position is the same as the position of an agent of the class ```OtherAgentClass```. If it is, it increments the variable ```var_name``` by the amount of ```inc_value```.

**Potential Use:** This method may be useful when contact between agents of different types causes an incremental change in some attribute of one (or both, if the method is applied to the ```step()``` method of both agent types).

**Call:** You may call this method in the ```step()``` method of an agent, as shown below; it moves the calling agent randomly on the grid and when it collides with an agent of a different class, the attribute passed to the method is incremented by the value also passed:
```python
step():
    self.move_randomly_collision_increment(OtherAgentClass, 'var_name', inc_value)
```


### Move Randomly, Collision Decrement
This method takes in three arguments: ```OtherAgentClass``` (a class of agents to check against for collision), ```var_name``` (as a string and which represents the attribute of the calling agent to decrement if a collision occurs), and ```dec_value``` (as an integer and which represents the amount to decrement ```var_name``` by if a collision occurs).

This method moves the calling agent randomly on the grid, then checks if the calling agent's new position is the same as the position of an agent of the class ```OtherAgentClass```. If it is, it decrements the variable ```var_name``` by the amount of ```dec_value```.

**Potential Use:** This method may be useful when contact between agents of different types causes a decremental change in some attribute of one (or both, if the method is applied to the ```step()``` method of both agent types).

**Call:** You may call this method in the ```step()``` method of an agent, as shown below; it moves the calling agent randomly on the grid and when it collides with an agent of a different class, the attribute passed to the method is decremented by the value also passed:
```python
step():
    self.move_randomly_collision_decrement(OtherAgentClass, 'var_name', value)
```


### Move Between Positions
This method takes two arguments: ```pos1``` and ```pos2```, which are tuples of integers representing the x and y coordinates of the two positions on the grid that the agent should move between. It returns ```None```.

This method first checks if the ```self.move_toward_position_1``` attribute of the ```AgentGrande``` class (of MesaGrande) is ```True```. If it is (which it is by default), the method next checks if the calling agent's current position is not equal to ```pos1```. If it is not equal, the calling agent moves one step towards ```pos1```, using the ```move_toward()``` method (of MesaGrande). If the calling agent's current position is not not equal to (that is, equal to) ```pos1```, it sets the ```self.move_toward_position_1``` attribute of the ```AgentGrande``` class (of MesaGrande) to ```False```. If the ```self.move_toward_position_1``` attribute of the ```AgentGrande``` class (of MesaGrande) is found to be ```False```, the method next checks if the calling agent's current position is not equal to ```pos2```. If it is not equal, the calling agent moves one step toward ```pos2``` using the ```move_toward()``` method (of MesaGrande). If the calling agent's current position is not not equal to (that is, equal to) ```pos2```, it sets the ```self.move_toward_position_1``` attribute of the ```AgentGrande``` class (of MesaGrande) to ```True```.

This method should be called within the step() method of the Agent class to make the agent move back and forth between the two positions continuously — or until the code in the ```step()``` method programmatically stops calling this method.

**Potential Use:** This method may be useful when agents are required to move between two specific positions on the grid until this behaviour is no longer needed.

**NB:** If ```pos1``` and ```pos2``` do not both intersect a perfectly horizontal, vertical, or diagonal (45 degree) line, the calling agent's path from ```pos1``` to ```pos2``` may differ from that when it travels back from ```pos2``` to ```pos1```.

**NB:** This method relies on the ```self.move_toward_position_1``` attribute of the ```AgentGrande``` class. This attribute exists within the ```mesaGrande.py``` file. Be aware that this attribute name is consequentially reserved and cannot be used elsewhere within any other object of the simulation.

**Call:** You may call this method in the ```step()``` method of an agent, as shown below; it moves the agent one space on the grid towards pos1 and then towards pos2 alternatively once one of these endpoints has been reached:
```python
step():
    self.move_between_positions((pos1_x, pos1_y), (pos2_x, pos2_y))
```
