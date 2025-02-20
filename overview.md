# AI Architectural Katas 2025

## Overview

Our team developed a solution to automate the grading of both Aptitude Test short answers as well as the Case Study architecture submission. The system allows to fully automate grading of both exams, provided certain conditions are met.

Let us start with the Aptitude Test (the Case Study solution is similar).

We define a service that takes in a question and an answer. Autograding goes as follows:

1. The answer goes through Guardrails to check for prompt injection, harmful language, etc. In case the Guardrails fail, the automatic grading of the answer fails.
2. Otherwise, the service pulls a question-tailored prompt template. Such prompt instructs an LLM how to grade said question. These instructions also define different dimensions that the question should be graded with, as opposed to just a single grade. The service builds a prompt by filling in the template with the answer.
3. The service calls an LLM, and the LLM returns  a vector of numbers that represent scores of the different dimensions that the answer is graded against, plus a feedback string.
4. Additionally, there is a regression model that takes as input the vector with the dimensions' scores and produces a final grade for the answer. The purpose of breaking down the final grade computation this way is so that the system can calibrate the regression model to mimic the human grades, as opposed to having an LLM produce a final grade directly, which is harder to calibrate.
5. The service is adjusting this regression model weights using human-graded answers via an Active Learning algorithm. Notice we don't require humans to grade using these dimensions explicitly. They can continue producing the final grade only. The calibration model will learn how to map the different dimensions into the human grade.
6. Finally, the feedback also goes through Guardrails to filter harmful content.

Notice that for the solution to work, there are several pre-conditions that must be met:
- Experts need to define, per exam question, the dimensions that the question should be graded with.
- Before the automated grader service can take on grading of a given question, there must be some human-graded samples of the question so that the calibration model can be fine-tuned.

In our design, we require an admin expert, via the Aptitude Test Maintenance Service, to manually enable the system to automatically grade a question after checking that the model is calibrated enough to the human grade.

Also, for every question, there is a random subset of answers that remains being graded by humans (and the auto grader shadow-grades as well), so that the model can continously calibrate itself with recent data.


We model the auto-grading of a Case Study similarly. We acknowledge that a Case Study is more complicated to grade than a short answer. Therefore, in order to enable auto-grading, we require a change in the way a Case Study is graded by humans. Concretely, we require each case study to be broken down into a collection of independent, narrowly-scoped questions. Each question that a case study is broken down into is then treated the same as a short-answer question from the Aptitude Test, and the architecture submission is treated as the answer to that question.