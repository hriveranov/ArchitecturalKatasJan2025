# We want to have insights about the model
We want to have insights about why our model behaves when it works correctly,
and expecially when it doesn't.

## Status
Proposed

## Context
The LLM is largely a black box. However, we have control on the prompt and
context. The LLM itself can be subject of updates.

## Decision
We will store and version the LLM, prompt and context. Each evaluation generated by
the model should have a reference to those elements and the associated answer, for 
reproduction and evaluation purposes.

## Consequences
Storing those elements has a cost impact, which, idealy, should be nominal. 
However, the benefits of having an observable model outweight the costs.

## Compliance

## Notes
The tentative retention time for the data is 1 year. This decision should be 
reevaluated every six months.
