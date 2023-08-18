---
tags: k8s

---

### Promql
promql is the programming language used in prometheus 

Data Types:

scalar
string 
instant vector
range vector

### Selectors and matchers
![[Pasted image 20230629181138.png]]
we used selector to match only job of node Exporter
![[Pasted image 20230629175902.png]]
![[Pasted image 20230629180505.png]]
![[Pasted image 20230629180624.png]]

Aggregation Operator
it calculates the overall metrics over time
add()
count()
etc
![[Pasted image 20230629180950.png]]
![[Pasted image 20230629181007.png]]


## Function
![[Pasted image 20230629181449.png]]
function to check how many times the process restarted

### Funnction For gauge metrics

Rules

![[Pasted image 20230629191546.png]]

we cn create rules.yml file and add it to prometheus using