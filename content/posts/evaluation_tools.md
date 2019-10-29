---
title: "Smart Contract Evaluation Tools"
date: 2019-10-24T22:02:37+02:00
#draft: true
---


Program analysis distinguishes between *static* and *dynamic*. In dynamics, the execution of the program is required (unit testing, integration testing, ...); on the contrary, in static analysis, the execution of the program is not required. Some of the most used techniques for static analysis are the formal methods (symbolic executions, data-flow analysis, model checking, ...).  

Performing dynamic program analysis is difficult in a blockchain scenario because it requires a very big effort to simulate the execution environment. This is very difficult given # Smart Contract evaluation tools

Program analysis distinguishes between *static* and *dynamic*. In dynamics, the execution of the program is required (unit testing, integration testing, ...); on the contrary, in static analysis, the execution of the program is not required. Some of the most used techniques for static analysis are the formal methods (symbolic executions, data-flow analysis, model checking, ...).  

Performing dynamic program analysis is difficult in a blockchain scenario because it requires a very big effort to simulate the execution environment. This is very difficult given the non-determinism (transaction ordering) and complexity of blockchain behaviors.

For this reason, the use of static techniques is gaining ground in the development of tools for the evaluation of smart contracts.

## Catalogue of tool

### [Securify](https://github.com/eth-sri/securify)
Securify statically analyzes the EVM code of the smart contract to infer important semantic information (including control-flow and data-flow facts) about the contract. This step is fully automated using [Soufflé](https://souffle-lang.github.io/), a scalable Datalog solver that defines patterns which through them Securify analyses the semantics of the code. Then, Securify checks the inferred facts to discover security violations or prove the compliance of security-relevant instructions. The full technical details behind the Securify scanner are available in the [research paper](https://files.sri.inf.ethz.ch/website/papers/ccs18-securify.pdf).

#### Datalog
A Datalog program [1] consists of an extensional database, which is defined by facts, and an intensional database, which is defined by rules. In a setup for static program analysis, the extensional database represents an input program in relational form. The relational representation of an input program is obtained from an **extractor** describing the relevant semantics of the input program for a given program analysis. The intensional database represents the program analysis specification phrased as Horn clause formula over finite domains. The query result of the Datalog execution represents the actual result of the program analysis. 
**One of the major challenges in logic programming, such as datalog, is scalability.**

![alt-image](https://d3i71xaburhd42.cloudfront.net/450f586425a1f8753379a23e12651b1594c0722d/2-Figure1-1.png)

#### [Soufflè](https://souffle-lang.github.io/index.html)
Soufflé is a variant of Datalog for tool designers crafting static analyses. Soufflé provides the ability to rapid prototype and make deep design space explorations possible.
![alt-image](https://souffle-lang.github.io/img/souffle-compiler.png)

### [Oyente](https://github.com/melonproject/oyente)
Oyente analysis tool is based upon symbolic execution. It uses the Control Flow Graph (CFG) of a program which is a directed graph whose paths model the execution traces of the program. 

![alt-image](https://upload.wikimedia.org/wikipedia/commons/thumb/3/30/Some_types_of_control_flow_graphs.svg/220px-Some_types_of_control_flow_graphs.svg.png)

### [Mythril](https://github.com/ConsenSys/mythril)
Mythril is a security analysis tool for EVM bytecode. It detects security vulnerabilities in smart contracts built for Ethereum, Quorum, Vechain, Roostock, Tron and other EVM-compatible blockchains. It uses *symbolic execution*, SMT solving and taint analysis detect a variety of security vulnerabilities. It's also used (in combination with other tools and techniques) in the MythX security analysis platform.

### [Mayan](https://github.com/MAIAN-tool/MAIAN)
Tool for automatic detection of buggy Ethereum smart contracts of three different types: prodigal, suicidal and greedy. Maian processes contract's bytecode and tries to build a trace of transactions to find and confirm bugs. It uses *Symbolic Executions*.

### [Why3](http://why3.lri.fr/#publications)
Why3 is a platform for deductive program verification. It provides a rich language for specification and programming, called WhyML, and relies on external theorem provers, both automated and interactive, to discharge verification conditions.

## Classification

Every tools uses *static program analysis*:

| Tool | *Formal method*  |  Technique |
|------------|--------------------------------------|-------------------------------|
| Oyente | *symbolic execution*  |  control-flow graph  |
|  Mythril | *symbolic execution*  |   |
|   Mayan | *symbolic execution*  |   |
|  Securify | *symbolic execution* + *data-flow analysis*  | control-flow graph  + Soufflè (datalog) |
| Zeus | *symbolic model checking* | |
| Why3 | | |





## Note

*Datalog* is a DSL (*domain specific language, i.e.  a computer language specialized to a particular application domain).

*Symbolic execution* is a way of analyzing a program to determine what inputs cause each part of a program to execute. An interpreter follows the program, assuming symbolic values for inputs rather than obtaining actual inputs as normal execution of the program would, a case of abstract interpretation. *Control-flow graph* is a technique 

*Data-flow analysis* is a lattice-based techniques for gathering information about the possible set of values at various points in a computer program.

In *symbolic model checking* , the verified system is modeled as a finite state transition system, and the specifications are expressed in a propositional temporal logic. Then, by exhaustively exploring the state space of the state transition system, it is possible to check automatically if the specifications are satisfied. The termination of model checking is guaranteed by the finiteness of the model. One of the most important features of model checking is that, when a specification is found not to hold, a counterexample (i.e., a witness of the offending behavior of the system) is produced.

------------------------------------------------------------------

Descrivere lo stato del sistema in maniera formale in modo da poter capire che se eseguo due transazioni diverse con ordine diverso queste possono violare la fairness del sistema

Sezione 2 - 3 - 14 del libro --> formal model of execution

Costruire un modello in modo tale da poter introdurre i problemi formalmente
Problema con cio che è fairness e cio che è corretto nei paper
	Admissible bound of messages  -> per definire correctness 
	tutti i processi devono fare computation allo stesso modo -> definire fairness

In paper state both received that coming msgs.

Calculus goes into the details of a protocol
formal models of execution aim to describe any execution

https://blog.ethereum.org/2015/11/15/merkling-in-ethereum/
the non-determinism (transaction ordering) and complexity of blockchain behaviors.

For this reason, the use of static techniques is gaining ground in the development of tools for the evaluation of smart contracts.
