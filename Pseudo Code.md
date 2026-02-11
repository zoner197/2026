---
subject: Digital Solutions
term: 1
date: 2026-02-11
topic: Pseudo Code
difficulty: Low/Medium/High
status: Needs Review/In Progress/Mastered
source: "[[U1 Lesson 03 - Developing User Experiences and Interfaces.pdf]]"
worksheet: "[[]]"
tags:
  - "#note"
  - "#class"
---
# Activity 3.3 A
Write an algorithm in pseudocode that keeps track of the sum of numbers entered by a user until the total is more than 100. A user will only enter one number at a time. 

```pseudo
BEGIN
	SET total = 0
	WHILE total >!= to 100 DO
		INPUT number
		SET total += number
	ENDWHILE
	OUTPUT "You have reached 100."
END
```

# Activity 3.3 B
Write an algorithm in pseudocode that a teacher could use to work out the average score for a class. The teacher will enter the value -1 when all grades have been entered for the class. 
```pseudo
BEGIN
	SET grade = 0
	SET total = 0
	SET n     = 0
	
	REPEAT
		INPUT grade
		
		SET n += 1
		set total += grade
	UNTIL grade != -1
	
	OUTPUT "Average is: "
	OUTPUT total/n
END
```

# Activity 3.3 C
Convert the flow chart into pseudocode.
![[Pseudo Code.png]]

```pseudo
BEGIN
	A
	N
	IF X = 5 THEN
		A
	ELSE
		S
	ENDIF
END
```

# Activity 3.3 D
Convert the flow chart into pseudocode.
![[Pseudo Code-1.png]]

```pseudo
BEGIN
	A
	LABEL goto_n
	N
	IF X != 5 THEN
		S
	ELSE
		GOTO goto_n
	ENDIF
END
```

# Activity 3.3 E
Convert the flow chart into pseudocode.
![[Pseudo Code-2.png]]

```pseudo
BEGIN
	P
	IF x = 0 THEN
		S
	ELSE IF 
END
```