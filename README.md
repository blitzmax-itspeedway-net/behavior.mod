# Module bmx.behavior

A behavior system for BlitzMax allowing you to easily create and add AI to your entities.

**VERSION:** 2.0

# DEPENDENCIES
* [BlitzMax-NG](https://blitzmax.org/downloads/)

# MANUAL INSTALL USING GIT
**LINUX:**
```
    # mkdir -p ~/BlitzMax/mod/bmx.mod
    # cd ~/BlitzMax/mod/bmx.mod
    # git clone https://github.com/blitzmax-itspeedway-net/behavior.mod.git
    # cd behavior.mod
    # chmod +x compile.sh
    # ./compile.sh
```
**WINDOWS:**
```
    C:\> mkdir C:\BlitzMax\mod\bmx.mod
    C:\> cd /d C:\BlitzMax\mod\bmx.mod
    C:\> git https://github.com/blitzmax-itspeedway-net/behavior.mod.git
    C:\> cd behavior.mod
    C:\> compile.bat
```

# MANUAL INSTALL USING ZIP
* Create a folder in your BlitzMax/mod folder called "bmx.mod"
* Download ZIP file from GitHub and unzip it: You will have a folder called behavior.mod.
* Copy folder behavior.mod-main/behavior.mod to BlitzMax/mod/bmx.mod/
* Run the compile.sh or compile.bat file located in the lexer.mod folder to compile

# UPDATE USING GIT
**LINUX:**
```
    # cd ~/BlitzMax/mod/bmx.mod/behavior.mod
    # git pull
    # chmod +x compile.sh
    # ./compile.sh
```
**WINDOWS:**
```
    C:\> cd /d C:\BlitzMax\mod\bmx.mod\behavior.mod
    C:\> git pull
    C:\> compile.bat
```

# Importing the module
```
import bmx.behavior
```

# Using the Module

A Behavior tree is a way of adding decision making processes and actions to your entities without re-developing actions for each type of entity.

**Node**
A BTNode is the basic building block of a behavior tree and depending on the type of node, you can enable or disable it and add one or more children.
Functionality is provided by an exec() method that returns one of three values defined by the Enum type "BT": 

    BT.RUNNING      A node is still RUNNING and has yet to be a SUCCESS or FAILURE
    BT.SUCCESS      The node is in a SUCCESS state
    BT.FAILURE      Teh node is in a FAILURE state

**Composite**
    A Composite node has one or more children and generally is used to make decisions:

    Composites supplied by default include "BTSequence", "BTSelector", "BTForeach", "BTRandom" and "BTRoundRobin"
 
**Decorator**
    A Decorator is a node that has a single child and performs an action before passing control to that child.

    Coposites suppled by default are "BTInverter", "BTEnabler" and "BTDisabler"

**Leaf**

    A Leaf node is the functionality that you supply to perform some action within your game.

    A Leaf node might perform path calculation, move, shoot, animate or other action that your AI wishes to achieve.

# Composite Nodes

## BTSequence

    A Sequence is a logical AND that iterates each child and fails if any one of it's children return RUNNING or FAILURE
    Returns SUCCESS when all its children return SUCCESS.

## BTSelector

    A Selector is a logical OR that iterates each child until one returns SUCCESS or RUNNING
    Returns FAILURE when all its children return FAILURE.

## BTForeach

    As its name implies, each child is executed and the result is calculated afterwards.

    Returns SUCCESS if all children return SUCCESS
    Returns FAILURE is any one child returns FAILURE
    Otherwise returns RUNNING
 
## BTRoundRobin

    Executes the next child and returns its result.
    Returns FAILURE is there are no enabled children.

## BTRandom

    Selects an enabled child at random and returns its result.

# Decorator Nodes
    **NOTE**: Only the first child is used in a decorator; additonal ones (if added) are ignored. 

## BTInverter

    Reverses the result of a child.

    Returns SUCCESS if child returns FAILURE (or there is no child)
    Returns FAILURE if child returns SUCCESS
    Returns RUNNING if child returns RUNNING

## BTDisabler

    Disables a given node if child returns SUCCESS, enables that node if child returns FAILURE
    Returns SUCCESS if node state has changed
    Returns FAILURE if there are no children
    Returns RUNNING if child returns RUNNING
    

## BTEnabler

    Enables a given node if child returns SUCCESS, disables that node if child returns FAILURE
    Returns SUCCESS if node state has changed
    Returns FAILURE if there are no children
    Returns RUNNING if child returns RUNNING


