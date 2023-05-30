# mesaGrande
*Quick-start behavioural methods for the Mesa module of Python.*

MesaGrande is a package of methods for use with the Mesa module in Python. Mesa supports the design and development of agent-based models (ABMs) that simulate the complexities of social interactions. These methods were designed, written, and tested by David Burgess (University of Saskatchewan), with acknowledgement (and equal parts frustration) attributed to OpenAI's ChatGPT. The below methods are contained within a custom Agent class (named AgentGrande) used with the Mesa module for Python designed by the members of Project Mesa. The included 20 methods have been designed to provide a quick-start means of implementing common, rudimentary, micro-social, -economic, and -health behaviours for agents of an Agent-Based Model (ABM). The methods rely on the existing design of the Agent class in the Mesa module.
Mesa Grande is a sub-division in Mesa.

**Usage**
----------

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

**Limitations and Assumptions**
----------

The methods assume that the ```MultiGrid``` class is used and that the grid (or lattice) is toroidal. Agent neighbourhoods are assumed to be Moore.

**Modified MIT License**
----------

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

**Included Methods**
----------

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

**Calculate Distance**

This method takes two positions as tuples of integers as its arguments and then calculates and returns as an integer the spacial distance from the first positional argument to the second positional argument.

Potential Use: This method may be useful as a helper method for other micro-behaviour methods, and it is used as such within other methods of MesaGrande.

Call: You may call this method from within the ```step()``` method of an agent, as shown below; it calculates the spacial distance between two positions passed as arguments to the method:
```python
step():
    self.calculate_distance(pos1, pos2)
```
