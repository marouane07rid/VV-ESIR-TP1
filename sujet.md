# Practical Session #1: Introduction

1. Find in news sources a general public article reporting the discovery of a software bug. Describe the bug. If possible, say whether the bug is local or global and describe the failure that manifested its presence. Explain the repercussions of the bug for clients/consumers and the company or entity behind the faulty program. Speculate whether, in your opinion, testing the right scenario would have helped to discover the fault.

2. Apache Commons projects are known for the quality of their code and development practices. They use dedicated issue tracking systems to discuss and follow the evolution of bugs and new features. The following link https://issues.apache.org/jira/projects/COLLECTIONS/issues/COLLECTIONS-794?filter=doneissues points to the issues considered as solved for the Apache Commons Collections project. Among those issues find one that corresponds to a bug that has been solved. Classify the bug as local or global. Explain the bug and the solution. Did the contributors of the project add new tests to ensure that the bug is detected if it reappears in the future?

3. Netflix is famous, among other things we love, for the popularization of *Chaos Engineering*, a fault-tolerance verification technique. The company has implemented protocols to test their entire system in production by simulating faults such as a server shutdown. During these experiments they evaluate the system's capabilities of delivering content under different conditions. The technique was described in [a paper](https://arxiv.org/ftp/arxiv/papers/1702/1702.05843.pdf) published in 2016. Read the paper and briefly explain what are the concrete experiments they perform, what are the requirements for these experiments, what are the variables they observe and what are the main results they obtained. Is Netflix the only company performing these experiments? Speculate how these experiments could be carried in other organizations in terms of the kind of experiment that could be performed and the system variables to observe during the experiments.

4. [WebAssembly](https://webassembly.org/) has become the fourth official language supported by web browsers. The language was born from a joint effort of the major players in the Web. Its creators presented their design decisions and the formal specification in [a scientific paper](https://people.mpi-sws.org/~rossberg/papers/Haas,%20Rossberg,%20Schuff,%20Titzer,%20Gohman,%20Wagner,%20Zakai,%20Bastien,%20Holman%20-%20Bringing%20the%20Web%20up%20to%20Speed%20with%20WebAssembly.pdf) published in 2018. The goal of the language is to be a low level, safe and portable compilation target for the Web and other embedding environments. The authors say that it is the first industrial strength language designed with formal semantics from the start. This evidences the feasibility of constructive approaches in this area. Read the paper and explain what are the main advantages of having a formal specification for WebAssembly. In your opinion, does this mean that WebAssembly implementations should not be tested? 

5.  Shortly after the appearance of WebAssembly another paper proposed a mechanized specification of the language using Isabelle. The paper can be consulted here: https://www.cl.cam.ac.uk/~caw77/papers/mechanising-and-verifying-the-webassembly-specification.pdf. This mechanized specification complements the first formalization attempt from the paper. According to the author of this second paper, what are the main advantages of the mechanized specification? Did it help improving the original formal specification of the language? What other artifacts were derived from this mechanized specification? How did the author verify the specification? Does this new specification removes the need for testing?

## Answers

#### 1 - 1985-1987 – Therac-25 medical accelerator.

A radiation therapy device malfunctions and delivers lethal radiation doses at several medical facilities. Based upon a previous design, the Therac-25 was an "improved" therapy system that could deliver two different kinds of radiation: either a low-power electron beam (beta particles) or X-rays.

Two software faults were to blame. One, when the operator incorrectly selected X-ray mode before quickly changing to electron mode, which allowed the electron beam to be set for X-ray mode without the X-ray target being in place. A second fault allowed the electron beam to activate during field-light mode, during which no beam scanner was active or target was in place. 

What engineers didn't know was that both the 20 and the 25 were built upon an operating system that had been kludged together by a programmer with no formal training. Because of a subtle bug called a "race condition," a quick-fingered typist could accidentally configure the Therac-25 so the electron beam would fire in high-power mode but with the metal X-ray target out of position. At least five patients die; others are seriously injured.

Testing the right scenario would have prevented selecting involuntarily X-ray mode. 


#### 2 - Apache bug resolution: HasherCollection

A local bug reported by an Apache forum member comes from the HasherCollection. Indeed, the HasherCollection should implement the Hasher interface, which was not the case. The developers were not able to use the library correctly. Consequently, the HasherCollection code and all its corresponding tests were deleted on the repository.

#### 3 - 
The concrete experiments they perform are :

 - Build a hypothesis around steady state behavior
 - Vary real-word events
 - Run experiments to run continuously

 The requirements for these experiments are :
 
 - Hypotheses
 - Independent variables
 - Dependent variables
 - Context

Is Netflix the only company performing these experiments? 

We can not say if Netflix is the only company performing these experiments because other organizations don’t document how they are applying Chaos Engineering.



#### 4 - Web Assembly

Web Assembly is a portable format for executable programs. The goal is to enable high-performance applications on web pages. It uses formal specification and it has some advantages :
 - It does not contain ambiguity. The code is clear and design with several patterns which increase understanding
 - It allows a good understanding of every problem 
 - Encourages for a global view of the system and is less technical as the formal specification is clear and helps the developers to code. So they can focus more on the “what…for” and “why” than on the “how”
 - It clearly defines correctness for a program. The specification defines what is correct and what is not. A correct program should not have any bug, according to the specification.

However, a webassembly program should also be tested. As we say, the only code without bugs is an empty code. Even if the language prevents most of the common bugs, there is still a risk. The main risks remain in the code of the web assembly language. A bug in the source code would be catastrophic as everyone would also have this bug if they use web assembly.

#### 5 - Mechanising and Verifying the WebAssembly Specification
How did the author verify the specification?

```Our executable interpreter, suitably augmented with the ref-
erence parser and linker, successfully passes all core language
conformance tests available in the WebAssembly reposi-
tory. Due to the
soundness result we have with respect to our mechanised
specification, these tests also serve to validate our model.```

Does this new specification removes the need for testing?
No,
Our work in proving WebAssembly’s type soundness
properties identified several important issues with the official
specification which we could not have discovered without
embarking on such a “deep" proof of a language property,
and might not have been so immediately actionable by the
official specification authors had we not maintained eyeball
closeness. Furthermore, we can now guarantee, through our
proofs, that the type system is sound in a way that would
not be possible for a “light-weight" specification
