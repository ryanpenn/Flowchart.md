# Markdown Flowchart

## Types of Flowcharts

- `mermaid` chart
- `flow` chart
- `sequence` chart

## Mermaid

- [Mermaid](https://github.com/mermaid-js/mermaid) is a JavaScript-based drawing tool that uses a syntax similar to Markdown, allowing users to easily create charts through code.

### What types of charts can Mermaid draw?

- **Pie chart**: Use the `pie` keyword
- **Flowchart**: Use the `graph` or `flowchart` keyword
- **Sequence diagram**: Use the `sequenceDiagram` keyword
- **Gantt chart**: Use the `gantt` keyword
- **Class diagram**: Use the `classDiagram` keyword
- **State diagram**: Use the `stateDiagram` keyword
- **User journey diagram**: Use the `journey` keyword

#### Pie Chart

- The first line specifies the keyword `pie`
- The title keyword is `title`, which is optional
- Comments: `%%` + `comment text` at the beginning of the line

```mermaid
pie
title What to eat tonight?
"Hotpot" : 8
"Takeout" : 60
"Cook by myself" : 8
"Haidilao" : 9
"Seafood" : 5
"Barbecue" : 5
"Not eat" : 5
%% Comment text
```

#### Flowchart

- The first line: `graph` + `direction`
- Direction options:
  - From top to bottom `TD` or `TB`
  - From bottom to top `BT` or `DT`
  - From left to right `LR`
  - From right to left `RL`
- Shapes
  - `[Rectangle]` `(Rounded rectangle)` `{Diamond}` `((Circle))`
  - `([Stadium shape])` `[[Subroutine shape]]` `[(Cylinder)]` `{{Hexagon}}`
  - `[/Parallelogram/]` `[\Reverse parallelogram\]` `[/Trapezoid\]` `[\Reverse trapezoid/]`
- Lines
  - Dashed arrow: `-.->`
  - Solid arrow: `-->`
  - Thick solid arrow: `==>`
  - Text arrow:
    - `-.text.->`
    - `--text-->`
    - `==text==>`
  - Arrowless: remove `>`
  - Connection symbols: `o` `x` `<` `>`
- `graph` flowchart

```mermaid
graph LR
A[Rectangle] -.->B(Rounded rectangle) --> C{Diamond} ==> D((Circle)) 
E([Stadium shape])--Solid line text--> F[[Subroutine shape]]==Thick solid line text==>G[(Cylinder)]-.Dashed line text.->H{{Hexagon}}
I[/Parallelogram/]-.-J[\Reverse parallelogram\]---K[/Trapezoid\]===L[\Reverse trapezoid/]
```

- `flowchart` flowchart

```mermaid
flowchart LR
A1[Rectangle] o--o B1(Rounded rectangle) <--> C1{Diamond} x--x D1((Circle))
A2[Rectangle] o-.-o B2(Rounded rectangle) <-.-> C2{Diamond} x-.-x D2((Circle))
A3[Rectangle] o==o B3(Rounded rectangle) <==> C3{Diamond} x==x D3((Circle))
```

- `subgraph` sub-process `end`

```mermaid
graph RL
        User((User))--1.User login-->Login(Login)
        Login --2.Query-->SERVER(Server)
        
subgraph Query Database
        SERVER--3.Query data-->DB[(Database)]
        DB--4.Return result-->SERVER
end

        SERVER--5.Check data-->Condition{Judgment}
        Condition -->|Check success| OK(Login success)
        Condition -->|Check failure| ERR(Login failure)
        OK-->SYS(Enter system)

        ERR -->|Return login page, re-login| Login
```

#### Sequence Diagram

- Use `sequenceDiagram`
- `autonumber` can automatically label the sequence
- Use aliases: `participant alias as display name`
- Comment annotations:
  - Format: `Note over participant1,participant2: comment content` displayed between two participants
  - Format: `Note left of participant1: comment content` displayed on the left of participant1
  - Format: `Note right of participant1: comment content` displayed on the right of participant1
- Lines: `-> solid line`, `->> solid line arrow`, `--> dashed line`, `-->> dashed line + arrow`, `-x line with a cross`
- Background highlighting can use: `rect rgb(0, 255, 0) ... end`
- Self-loop use `loop ... end`
- Judgment use `alt ... else ...else ... end`, if there is no else, you can use: `opt .... end`

```mermaid
%% Sequence diagram example,-> solid line,--> dashed line,->> solid line arrow
sequenceDiagram
autonumber
  participant Z as Zhang San
  participant L as Li Si
  participant W as Wang Wu

  Note over Z,W: Zhang San, Li Si, Wang Wu,<br/>were the best playmates when they were young, now 80 years have passed...
  Z->>W: How are you, Old Wang?
  Note left of Z: Besides Old Zhang, who has been a soldier,<br/>and is in relatively good health, the other two are not doing so well

  loop Health check
      W->>W: Fighting the disease
  end

  Note right of W: Eat reasonably <br/>See a doctor<br/>Get an IV...
  W-->>Z: Not bad, just can't walk well now!!
  L->>Z: How about you, Old Zhang?

  alt Healthy#9829;
  Z-->>L: Very good!
  else Passed away
  Z-->>L: I'm sorry, Old Zhang has already gone!!!
  end
```

#### Gantt Chart

- Gantt charts are a type of bar chart, proposed by Karol Adamiechi in 1896, and independently proposed by Henry Gantt in 1910.
- They are usually used to describe the start and completion times of project terminal elements and summary elements.

| Mark       | Introduction                                          |
| ---------- | ----------------------------------------------------- |
| title      | Title                                                 |
| dateFormat | Date format                                           |
| section    | Module, defines the vertical direction                |
| done       | Already completed                                     |
| active     | Currently ongoing                                     |
| crit       | Critical phase, urgent, will be highlighted           |
| after      | Default starts from the end time of the previous item |

```mermaid
gantt

dateFormat YYYY-MM-DD
title Development Plan

section Requirements Document
	Login Registration:done,login,2021-06-25,2021-06-28
	Add friends and groups:add, 2021-06-29,3d
	Single chat :active ,chat, 2021-07-01,2d
	Group chat :groupChat,after chat,5d
	Moment :crit,5d
	Others:3d
section Development
	Develop login registration:done,d-login,2021-06-25,24h
	Develop add friends and groups:active,d-add,after d-login,5d
	Develop single chat and group chat:crit,d-chat,after d-add,7d
	Develop moment:d-friend,after d-chat,7d
	
section Testing
	Test cases and play:active,test,2021-06-25,10d
	Start testing some interfaces:crit,start-test,after test,11d
```

#### Class Diagram

- Use the `classDiagram` keyword
- Then define the class, its properties, and methods like writing Java code
- Then connect the relationships between them with lines
- Format: `Class1 line Class2: note`
- Lines: `<|--`、`*--`、`o--`、`..`、`<-->`、`--|>`
- Types:
  - `<<Interface>>` represents an interface class
  - `<<abstract>>` represents an abstract class
  - `<<Service>>` represents a service class
  - `<<enumeration>>` represents an enumeration

```mermaid
classDiagram

class Serializable{
<<interface>>
}
class Throwable{
<<class>>
 String detailMessage;
 Object backtrace;
 Throwable();
}

class Exception{
<<class>>
Exception()
Exception(String message)
}
class IOException{
	<<class>>
}

class SocketException{
	
}

class RuntimeException{
<<class>>
}

class IndexOutOfBoundsException{
	
}

class ArithmeticException{
	
}

Serializable <|.. Throwable:Serializable interface
Throwable *--Exception
Exception <-- RuntimeException:Runtime exception
Exception <-- IOException:IO stream related exception
IOException o-- SocketException
RuntimeException o-- IndexOutOfBoundsException
RuntimeException o-- ArithmeticException
```

#### State Diagram

- Use the `stateDiagram` keyword
- There are two special state indicators for the start and stop of the chart.
- These are written with the `[*]` syntax, and the direction of the transition defines them as start or stop states.
- A transition is the path from one state to another, represented by the arrow "–>".
- In practical use of state diagrams, you often get multi-dimensional diagrams because a state can have multiple internal states. These are called composite states in this terminology.
- To define a composite state, you need to use the `state` keyword, followed by an `id` and `{}` containing the body of the composite state.

```mermaid
stateDiagram-v2

[*] --> Idle
Idle --> [*]
Idle --> Walking
Walking --> Idle
Walking --> Running
Running --> Walking : Running can stop to be idle, or slow down to Walking
Running --> [*]

state if_state <<choice>>
[*] --> IsPositive
IsPositive --> if_state
if_state --> False: if n < 0
if_state --> True : if n >= 0


state fork_state <<fork>>
  [*] --> fork_state
  fork_state --> State2
  fork_state --> State3

  state join_state <<join>>
  State2 --> join_state
  State3 --> join_state
  join_state --> State4
  State4 --> [*]

[*] --> First
First --> Second
First --> Third

state First {
    [*] --> fir
    fir --> [*]
}
state Second {
    [*] --> sec
    sec --> [*]
}
state Third {
    [*] --> thi
    thi --> [*]
}
```

#### User Journey Diagram

- Use the `journey` keyword
- Format: `Task:Score:Role list (multiple separated by commas)`

```mermaid
journey
title My Day
section Morning
  Eat: 5: Me,Her
  Run: 3: Me
section Work Time
   Take the subway to work: 5 :Me
   Work: 1:Me
section Evening
  Sleep: 5: Me,Her
```

## Flow

- Standard flowchart
- The code mainly consists of two parts:
  - The first part: Define elements
    - **start** # Start
    - **end** # End
    - **operation** # Operation
    - **subroutine** # Subroutine
    - **condition** # Condition
    - **inputoutput** # Input or output
  - The second part: Define the direction of elements
    - Format: `Element name=>Element type: Display node content` (There must be a space after the colon)
    - Define element type use `=>`
    - Connect two elements use `->`
    - The direction of elements can use: `left`、`right`、`top`、 `bottom`

```flow
st=>start: Start box
op=>operation: Process box
cond=>condition: Decision box (Yes or no?)
sub1=>subroutine: Subroutine
io=>inputoutput: Input/output box
e=>end: End box
st->op->cond
cond(yes)->io->e
cond(no)->sub1(right)->op
```

## Sequence

- Sequence diagram
- The syntax is the same as Mermaid's sequence diagram, but the generated diagram is more concise.

### Simple Example

```sequence
Object A->Object B: Are you okay, Object B? (Request)
Note right of Object B: Description of Object B
Note left of Object A: Description of Object A (Hint)
Object B-->Object A: I'm fine (Response)
Object A->Object B: Are you really okay?
```

### Complex Example

```sequence
Object A->Object B: Are you okay, Object B? (Request)
Note right of Object B: Description of Object B
Note left of Object A: Description of Object A (Hint)
Object B-->Object A: I'm fine (Response)
Object B->Object C: Are you okay
Object C-->>Object A: Object B is looking for me
Object A->Object B: Are you really okay?
Note over Object C,Object B: We are friends
participant D
Note right of D: No one plays with me
```

