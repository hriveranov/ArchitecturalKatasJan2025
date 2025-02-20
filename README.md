# ArchitecturalKatasJan2025
Repo for the project for Architectural Katas Jan 2025

The Architecture characteristics that we detected as most important 
were 

- Accuracy
- Scalability

These characteristics drive the architecture decisions and tradeoffs.

Another consideration was to reuse as much as the current architecture as possible, without limiting
the new features we want to introduce.

### Accuracy
Not only the reputation of the company, but also people's jobs depend on the accuracy of the evaluations
of the model. However, the definition of accuracy is especially difficult, because there could be as
many answers as people taking the test, and as many evaluations as experts. We landed on a definition
of accuracy as "As close as a human would evaluate".

### Scalability
The main problem we try to solve is scalability. Not in the sense of big data or massive multiprocess,
but in the sense of increasing the evaluation process beyond its current capacity.


## Architecture Decision Records

Can be found in the /adr folder

## Architecture Diagrams

Can be found in the /diagrams folder.
