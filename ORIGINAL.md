# Overview

This would be a project that will aim to help with interviews by doing a conversational discussion with the user.

## Folder Structure

There would be a "memories/" folder in the route which will store the information gathered from the interview. It is managed by a "manage-memory" subagent who updates the memory files.

## Agents

**Interview Planner** Will ask the user for his latest CV and the Job Description he is preparing for. Then will create a plan that he will be handing over to the manage-memory subagent who will update the overall plan to add which topics are new topics that are not in the overall plan yet.

## Subagents

**manage-memory** will try to keep track of what topics still needs to be done, and have been planned. This will use the "OpenAI/GPT-6 Luna Pro" model
