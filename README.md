# Vert.x - From zero to (micro-) hero.

This repository is a lab about vert.x explaining how to build distributed _microservice_ reactive applications using
Vert.x.

Instructions are available on http://escoffier.me/vertx-hol

Complete code is available in the `solution` directory.

## Teasing

Vert.x is a toolkit to create reactive distributed applications running on the top of the Java Virtual Machine. Vert.x
exhibits very good performances, and a very simple and small API based on the asynchronous, non-blocking
development model.  With vert.x, you can developed microservices in Java, but also in JavaScript, Groovy, Ruby and
Ceylon. Vert.x also lets you interact with Node.JS, .NET or C applications.  

This lab is an introduction to microservice development using Vert.x. The application is a fake _trading_
application, and maybe you are going to become (virtually) rich! The applications is a federation of interaction microservices packaged as _fat-jar_ and creating a cluster.

## Content

 * Vert.x
 * Microservices
 * Asynchronous non-blocking development model
 * Composition of async operations
 * Distributed event bus
 * Database access
 * Providing and Consuming REST APIs
 * Async RPC on the event bus
 * Microservice discovery

## Want to improve this lab ?

Forks and PRs are definitely welcome !

## Building

To build the code:

    mvn clean install

To build the documentation:

    cd docs
    docker run -it -v `pwd`:/documents/ asciidoctor/docker-asciidoctor "./build.sh" "html"
    # or for fish
    docker run -it -v (pwd):/documents/ asciidoctor/docker-asciidoctor "./build.sh" "html"

## OpenShift

```
oc new-project vertx-trader
oc policy add-role-to-user view system:serviceaccount:$(oc project -q):default

cd virt:~/git/vertx-microservices-workshop/trader-dashboard
oc new-build --name=trader-dashboard --strategy=docker --binary
oc start-build trader-dashboard --from-file=. --follow
oc new-app trader-dashboard
oc expose svc trader-dashboard

cd ~/git/vertx-microservices-workshop/quote-generator
oc new-build --name=quote-generator --strategy=docker --binary
oc start-build quote-generator --from-file=. --follow
oc new-app quote-generator

cd ~/git/vertx-microservices-workshop/portfolio-service
oc new-build --name=portfolio-service --strategy=docker --binary
oc start-build portfolio-service --from-file=. --follow
oc new-app portfolio-service

cd ~/git/vertx-microservices-workshop/compulsive-traders
oc new-build --name=compulsive-traders --strategy=docker --binary
oc start-build compulsive-traders --from-file=. --follow
oc new-app compulsive-traders

cd ~/git/vertx-microservices-workshop/audit-service
oc new-build --name=audit-service --strategy=docker --binary
oc start-build audit-service --from-file=. --follow
oc new-app audit-service
```