# Use of guardrails
We don't want to process obscene, racist, discriminatory, etc. entries, and we
dont want the model to produce it

## Status
Accepted

## Context
Since the model is in essence a black box, it could potentially produce offensive
output. This situation could be aggravated if it receives offensive inputs 

## Decision
The model will have guardrails analyzing the inputs, and on the output.

## Consequences
This will add extra processing (but that's not too expensive).
This also means that some answers will have to be routed to a person even after
they have been routed to the LLM

## Compliance

## Notes
