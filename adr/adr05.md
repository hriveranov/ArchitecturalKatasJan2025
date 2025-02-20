# The model evaluations won't be used until its accuracy has been evaluated.
Accuracy of the evaluation is defined in this context as: how a human would evaluate

## Status
Proposed

## Context
Defining accuracy in the context of evaluating the answers is not a small task, since
there isn't a concrete answer: there may be as many answers as people taking the test,
and as many different evaluations as people evaluating. 

## Decision
All answers evaluated by a person will also be evaluated by the model. If an
answer doesn't have at least 100 human evaluations to calculate the accuracy, the model answer won't 
be used to grade the question.

## Consequences
New questions will always be evaluated by humans. Once the process is working at full scale,
with humans and AI grading, replacing all available questions with new 
questions could break the promise of 2 weeks for evaluation, since there will be not enough
experts to evaluate, and not enough evaluations to asses the accuracy of the model. 
Therefore, the process of adding new questions and removing old ones should be handled in small increments.

## Compliance
The process of adding new questions should have guidelines, both written and in a system. A
human should be able to override the decision, but the system should issue the warning.

## Notes
The specific threshold must be evaluated experimentally and negociated with the stakeholders.
Evaluating the tipping point where the system would get stressed should be easy to calculate given 
the number of evaluations and experts available to evaluate in any given moment.