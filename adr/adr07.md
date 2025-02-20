# The model should not be allowed to grade if it's accuracy is below the threshold
This ADR is related to ADR 05

## Status
Proposed

## Context
Even if a model is deemed accurate in the intial evaluations, its accuracy, defined as
"how close to a human evaluation", could diminish. 

## Decision
All answers evaluated by a person will also be evaluated by the model. These will 
provide a constant evaluation of the accuracy of the model. We will include monitors to stop the 
model from answering a specific question if the accuracy is below a threshold.

## Consequences
We will have to add observability and monitoring to several parts of the process.

## Compliance

## Notes
The specific threshold must be evaluated experimentally and negociated with the stakeholders.
