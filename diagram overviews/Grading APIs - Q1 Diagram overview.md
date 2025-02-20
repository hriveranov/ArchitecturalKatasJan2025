# Overview of Grading APIs for short answer questions Diagram

## Diagram
![image](../diagrams/Grading%20APIs%20-%20Q1%20Diagram.png)

## Overview of changes when compared to the original model

When compared to the original component model for the short answer grading APIs, our solution differs in a couple of key aspects. They can be summarized as follows:

1- Added an autograder that grades every short answer question. This does not mean that all of the grades that are outputted come from this autograder,but we decided to have the autograder grade every question that is graded by a human since this will provide us with valuable data to calibrate our model.

2- Changed the Aptitude Manual Capture service for a Task Scheduler service. This task scheduler will have several key functionalities. Among them are the functionalities that the Aptitude Manual Capture service had, along with deciding whether an answer should be graded by a human or the autograder service.

3- Added a Short Question Autograder service. We go into detail about how this service works in another diagram. For the purposes of this diagram, it can be seen as a black box that receives a message from a queue containing the keys to fetch the answer, the question and the parameters of the model, and outputs the results of running the model to a new DB we added: Aptitude Test Autograder DB.

4- Added the Auto Grade Commiter service. This service serves several key purposes. For one, it ensures that only grades for the answers that were marked by the Task Scheduler to be graded by the Autograder are persisted to the Aptitude Test Graded DB. In addition to this, it contains guardrails for the contents of the answer, ensuring that it gets retried a certain number of times if conditions like the schema of the answer aren't met, and eventually enqueues it to be graded by a human after the maximum number of retries is reached. It also delays the commiting of the grades to ensure that the test takers cannot easily tell if a human graded their answers by how long they took to grade. 

5- Turned the Candidate Status and Candidate Aptitute Notification services to pull services. They will periodically query the Aptitute Test Graded DB instead of being called by the manual grader.

