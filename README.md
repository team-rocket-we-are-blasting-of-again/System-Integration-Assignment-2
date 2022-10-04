# System Integration Assignment 2 - Mini Project BPM

## Group Members

- Frederik Johnsen, cph-fj111@cphbusiness.dk
- Jean-Poul Leth-Møller, cph-jl360@cphbusiness.dk
- Mathias Parking, cph-mp525@cphbusiness.dk
- Magdalena Wawrzak cph-mw216@cphbusiness.dk
- Tobias Zimmermann cph-tz11@cphbusiness.dk

## Services

We make use of a microservice architecture, these services can be found here:

- [Complaint Service With BPM](https://github.com/team-rocket-we-are-blasting-of-again/complaint_service_with_bpm)
- [Case management](https://github.com/team-rocket-we-are-blasting-of-again/case-management)
- [Email service](https://github.com/team-rocket-we-are-blasting-of-again/Simple-Email-Service)

Each microservice is compleatly independent, this is done by each service having their own database as well as their own API / REST endpoints

## BPMN Diagram

To view our full XML representation follow this [link](https://github.com/team-rocket-we-are-blasting-of-again/complaint_service_with_bpm/blob/main/src/main/resources/process.bpmn)

![process model](https://raw.githubusercontent.com/team-rocket-we-are-blasting-of-again/complaint_service_with_bpm/main/docs/process.bmp)

## Integration Patterns

- Process Manager

  We use Camunda to model our business process.

- Pub/Sub

  We use rabbit as our Message Broker. This allows us to emit events of specific things that happen during our camunda process.

## Business Rules

We use conditional expressions, since our conditions are very simple.

[Example conditional expression](https://github.com/team-rocket-we-are-blasting-of-again/complaint_service_with_bpm/blob/main/src/main/resources/process.bpmn#L29)

This business rule checks if a complaint contains any bad words, if it does we simply deny the complaint and send pass them to a new service which will tell the complaintent that their complaint was denied.

Alternatively, if we were to have some more in depth business rules with a bunch of edge cases, we would have implemented these using a Decision Table.

## Human Tasks

We use human tasks to allow the employee to review the opened complaint. This review involves figuring out if the complaint is a new case in our system or if the complaint is similar to an already existing case, it will be added to the pile of messages relevant to that case.
