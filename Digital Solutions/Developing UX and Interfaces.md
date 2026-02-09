---
subject: Digital Solutions
term: 1
date: 2026-02-09
topic: Developing UX and Interfaces
difficulty: Low
status: Needs Review/In Progress/Mastered
source: "[[U1 Lesson 03 - Developing User Experiences and Interfaces.pdf]]"
worksheet: "[[]]"
tags:
  - "#note"
  - "#class"
---
# Unit 1: Creating with Code

## 3. Developing User Experiences and Interfaces

> [!abstract] Learning Goals (WALT & WILF)
> 
> **WALT (We Are Learning To):**
> 
> - Examine a problem to determine achievable outcomes within deadlines.
>     
> - Determine features to include in an app.
>     
> - Communicate planning through detailed mind maps.
>     
> 
> **WILF (What I'm Looking For):**
> 
> - Exploring and developing a hypothetical app concept (Café Loco).
>     
> - Creating a detailed mind map.
>     
> - Distinguishing between app goals and user goals.
>     
> 
> **TIB (This Is Because):** Technologies transform and sustain our world; they are created to improve quality of life.

---

## 3.1 Determining the Scope of a Solution

### Case Study: Café Loco

**The Problem:** Café Loco wants to offer customers an easy way to order lunch deliveries via mobile devices.

#### 1. Brainstorming Users

- **Demographics:** 18–65+, time-poor, health-conscious.
    
- **Needs:** Quick meals, convenience, accessibility (disability/illness), late workers.
    

#### 2. Feature Brainstorming

- **Core:** Menu (food/drink), Payment, Select delivery times, Save profile, Allergy alerts.
    
- **Secondary:** Favorite orders, "Surprise Me," Map location, Eco-friendly packaging, Loyalty rewards, Group orders.
    

#### 3. Minimum Viable Product (MVP)

The MVP is the combination of essential features from both the **User Goals** (easy ordering, nutritional info) and **App Goals** (payment processing, delivery tracking).

---

### Activity 3.1 B: The Mind Map

For FIA1/IA1, your mind map should include these branches:

1. **Client Problem:** What the business needs.
    
2. **User Problems:** Proto-personas and user pain points.
    
3. **Features:** What the app actually does.
    
4. **Usability Principles:** Accessibility, Effectiveness, Safety, Utility, Learnability.
    
5. **Code (Key Algorithms):** Expected calculations (e.g., total cost).
    
6. **Impacts:** Personal, Social, and Economic (Focus on positive solutions).
    
7. **Competitors:** Existing market solutions.
    
8. **Data Storage/Selection:** (Not required for FIA1).
    

---

### Activity 3.1 D: Success Criteria

Use these checkboxes to define what "success" looks like for the project:

#### Features

- [ ] User must be able to order menu items
    
- [ ] Menu must have photos of popular meals
    
- [ ] User must be able to see location of store on Google maps
    
- [ ] Must be able to calculate invoice amount for orders
    
- [ ] Must be able to process payments and generate receipts
    
- [ ] User must receive delivery and pickup notifications
    

#### Usability

- [ ] Inclusive language and terms used throughout.
    
- [ ] Layout must be consistent and intuitive.
    
- [ ] Restrict invalid input (e.g., using dropdowns instead of text for quantities).
    
- [ ] Secure connection icons (padlock) to reassure users during payment.
    

#### Impacts

- [ ] **Personal:** Dietary/Allergy alerts to prevent life-threatening reactions.
    
- [ ] **Economic:** Data security to protect the business reputation and customer profit.
    

---

## 3.2 Developing the User Interface (UI)

### 5 Key Principles of Sketching

When developing wireframes, you must include:

1. **Titles:** Clear names for every screen.
    
2. **Annotations:** Names/notes for elements that are hard to draw.
    
3. **User Flow:** Use arrows to show how screens link together.
    
4. **Gestures:** Indicate taps, swipes, or long-presses with symbols or notes.
    
5. **Notes:** Explain how **Usability Principles** are integrated at the bottom of the wireframe.
    

---

## 3.3 Identifying Key Algorithms

### Defining Algorithms

Algorithms are the "calculations" the app performs.

- **Input:** What data is collected? (User input/Sensors)
    
- **Process:** How is it manipulated? (Calculations/Sorting)
    
- **Output:** What is the result? (Display results/Adjust settings)
    

### Pseudocode Conventions

- Use **CAPITALS** for keywords (`BEGIN`, `END`, `INPUT`, `OUTPUT`, `IF`, `WHILE`).
    
- Use **Indentation** for code inside loops or if-statements.
    
- Every `IF` or `LOOP` must have a matching `END IF` or `END LOOP`.
    

#### Example 1: Grade Checker

```pseudo
BEGIN
    INPUT grade
    IF grade >= 50 THEN
        OUTPUT pass
    ELSE
        OUTPUT fail
    END IF
END
```

#### Example 2: Rectangle Calculations (Looping)

```pseudo
BEGIN
    INPUT width
    INPUT length
    area = width * length
    perimeter = 2 * (width + length)
    REPEAT 5
        OUTPUT area
        OUTPUT perimeter
    END REPEAT
END
```

---

## Activity 3.3 Workspace

> [!todo] Activity 3.3 A
> 
> Write an algorithm that keeps track of a sum of numbers until the total is > 100.
> 
> `(Draft your pseudocode here)`

> [!todo] Activity 3.3 B
> 
> Write an algorithm for a teacher to find a class average. Enter -1 to finish.
> 
> `(Draft your pseudocode here)`