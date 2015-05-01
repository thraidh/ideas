# Overview

This product is hard to put into a view words. It is basically a tool which fixes all that is wrong/sub-optimal
at my working place regarding organization and collaboration (like using 1000s of lists in sharepoint or excel and
hiding documents in even more sharepoint folders or shared drives). 

# Features

## Project Data

- have an overview page for each project
- contains important data about the project (name, important dates, etc)
- can contain subpages
- list of subprojects/project parts with completion state and latest progess info or "waiting-for"
- list of people involved and assigned roles and abilities
- list of roles with responsibilities and abilities
- personalized list of important documents (as everyone has a different focus)
- document search
- people roles can be active or inactive (project manager not needed when project is in operation, operators not needed during initial planning)

## Document Store

- store documents
- document search engine
- put tags on documents

## Infrastructure Projects

- allow the user to design a model for each OSI level
- associate model elements across levels
- integrate with external CMDBs
- provide APIs to provide a CMDB
- provide APIs to create network diagrams, firewall rules and other arbitrary documents from the model

## Project Templates/Cookbooks

- let the user describe steps and requirements which need to be done to complete a complex task
- this will result in a kind of requirement tree
- each node can have a description of the job to be done and necessary roles or abilities needed and approximate time
- each tree can be a template to be reused in a project
- in a project each node of a used can be modified, assigned to a person, marked as (partially) complete
- a node can be "waiting-for"
- if a node requires a role or ability, which is not present in the project, it needs to be added or is displayed as missing

## Personal Todo List

- display a list of all nodes which can be worked on by the user
- managers can assign priorities to projects or tasks
- display list of things to come, when the requirements are met
- display list of things which need my tasks to be completed
- order in a way that tasks are on top which need to be completed first or otherwise the project would be delayed
- register time spent on tasks

## Analysis tools

- Gantt charts (because management likes them)
- identify choke points (persons/roles which hold up progress)

## Page Builder

- a user can build pages
- these can by dynamic and updated by other users
- the data can be synced (rw) with data in documents, external data sources (DBs), APIs, CMDB model, ...
- data can be transformed and sent to pages, DBs, APIs, documents, per mail, etc
- example: a list with all things, a different list (subset) with things already rolled out, can be transformed to a percentage and displayed in a page



# Unsorted requirements


requirements
- central server to sync
- can work offline
- structure
  - customers (can have projects)
  - projects (can have task, can be for one or more customers)
  - tasks (has steps, is in one or more projects) (is actually the top-level construct)
  - steps (is in one (or more?) task, can depend on other steps in this or other tasks)
  - users (are invited to tasks and can then join and leave when they want)
  - roles (users are assigned to roles, so more than one user can perform a step)
- templates for tasks to setup a general structure
- active steps are displayed as TODO list to all users which SHOULD do them
- actually any user can complete any step to prevent lazy people to block everything
- blackboard per task
  - simple drawing capabilities (boxes, circles/ellipses, arrows/lines, text)
  - simple texts (wiki style, with links to graphics, documents)
  - documents with metadata and comments (e.g. "section B.3 contains the interesting stuff")
- documents are synced with local disk and central server
- document duplication is to be avoided
- steps can have estimated time
- steps can have a type
- calculated is: estimated/really used, really used/(end-start)
- with those we can more or less accurately calculate estimated completion per step type and user
- holiday plan
- "chess clock" and "manual" modes of entry of times spent on steps
- customers/projects/tasks/steps can have (and inherit)
  - COI/COI name/COI comment
  - priority/importance
- users can make their own priorities
- users can take several types per task
  - team: can do and see everything, are involved over the whole task
  - viewer: can see everything, but change nothing
- changing priorities displays projected shifts, broken deadlines, in other tasks
- maybe better only have hierarchical tasks, each inheriting customers, projects, COIs etc
  - a task is complete if all contained tasks are complete
  - each task in a network of dependent tasks can be in one or more super-tasks
  - every owner of a task can create sub-tasks and invite others to either the task or one or more subtasks
  - users can usually see only the current task and all its recursive sub-tasks
  - task owners
    - a newly created task is owned by the created, a newly created subtask is created by no-one
        - if a task is not explicitely owned, it is owned by the super-task owners
        - if someone is invited to a task and joins, he is added as owner
  - tasks can have public areas, which can be seen by super-task owners
- questions
  - questions are short(!) requests for information related to a task to any user
  - questions show up in the TODO list and must be answerable in with a limited number of characters and/or an
    unlimited amount of attached documents and with (very) little effort/time
  - if questions are not answerable with little effort or only with a long text, they are no questions and the
    requester should add an information-request-subtask and invite the answerer to complete that subtask

