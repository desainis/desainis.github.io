---
title: "Welcome to my Humble Abode"
published: true
---

**Hello world**, it's astonishing to think that there was a time when I didn't know what I wanted to do. My friend was an avid computer science geek and when I was supposed to deciding on a college, I was thinking "What the hell do I do now?". In comes my good friend, playing around with `Python`. As a highschool kid, I was intrigued by the simple tic tac toe games he was making as a part of an assignment. The thought of games blew my average sized brains out and that was it. I was going to be a programmer. I took Grade 11 Computer Science in Grade 12 (because of course I was late) and then made my way into University of Toronto as a Computer Science student. 

College, what felt like the longest six years of my life was over in 2018. In all honesty, I didn't realize how easy I had it then. The structured courses, assignments, and most of all my friends were one the highlights of my life. Real life seems to have too many choices for any rational human being to make. After several years of pure developer work, someone said that magic word. **Containers**.

Containers changed the way I thought about building applications. They morphed a whole new realm of possibilites of the famous "Continuous Integration / Delivery" topic we know of today. Over the past year I have been transitioning myself into a Site Reliabiity Engineering (SRE) role and living/breathing Docker & Kubernetes. I never thought I would finally live a world where spinning up a server would be as simple as:

```json
provider "aws" {
  access_key = "ZKIAITH7YUGAZZIYYSZA"
  secret_key = "UlNapYqUCg2m4MDPT9Tlq+64BWnITspR93fMNc0Y"
  region = "ap-southeast-1"
}

resource "aws_instance" "example" {
  ami = "ami-83a713e0"
  instance_type = "t2.micro"
  tags {
  Name = "your-instance"
}
```

Don't worry, those are not real keys of course. :-) 

Infrastructure as a code has been the most impactful stream of computer science I've ever delved into not only because of its challenge but because I have a steady stream of friends, mentors and colleagues to help guide me through this journey.

I hope you enjoyed this one. Coming up: ChatOps. 
