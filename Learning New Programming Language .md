
## Overview

In this exercise, you will learn a new programming language using structured AI prompting techniques. You will plan your learning, develop understanding, and build a mini project.

---

## Prerequisites

* A language you already understand (source language)
* A new language you want to learn (target language)
* Skills in using an AI tool (ChatGPT, Claude, etc.)
* A working development environment

---

## Exercise Structure

You will work through 4 sections:

* Create a learning plan
* Practice thinking and reasoning skills
* Practice advanced prompting
* Build a mini-project

---

# Create a Learning Journey Plan (Part 1)

## Define your goals

Set 2–3 clear goals for your target language.

Example:

* Create a REST API using Go
* Create data visualisations using Julia

---

## Develop a learning strategy

Use AI to help create a plan.

Example prompt:

I know [SOURCE LANGUAGE] and want to learn [TARGET LANGUAGE] to reach [GOAL].

Create a learning plan with:

* 3–4 learning phases
* Prerequisites for each phase
* 4–5 steps per phase
* Verification tasks

---

## Refine your plan

* Review the AI plan
* Modify it if needed

---

# Apply the 4 Step Prompting Strategy (Part 2)

Choose one topic from your plan.

---

## Step 1: Conceptual Understanding

Discuss the concept at a high level:

* Main differences between source and target language
* What problem the language solves
* Required mental model changes
* Common misunderstandings

---

## Step 2: Step-by-Step Breakdown

Ask AI to explain a concept:

* How it works in the target language
* Comparison with source language
* Key syntax
* Best practices

Do not code yet (wait for next step)

---

## Step 3: Guided Implementation

Ask AI to guide you:

* Create a simple example
* Explain each step
* Show differences from source language

---

## Step 4: Understanding Verification

Write the code yourself, then ask AI to check it:

Ask:

* Is it correct and idiomatic?
* How can it be improved?
* What should I learn next?
* Am I using old language habits?

---

# Advanced Prompting Techniques

Use at least 2 of these:

---

## Using Context Effectively

Compare both languages to improve understanding.

---

## Promoting Deep Understanding

Ask about:

* Performance
* Alternative solutions
* Scaling
* Different approaches

---

## Learning Through Teaching

Explain the concept and ask AI to review it:

* What is correct
* What is missing
* What is wrong

---

## Using a Tutor

Ask AI to act as a tutor:

* Give hints instead of answers
* Ask guiding questions
* Break concepts into smaller parts
* Correct mistakes gently

---

# Part 4: Create a Mini-Project

Got it — here is your **Part 4 added into the exercise**, kept simple and aligned with your format:

---

## Part 4: Build a Mini-Project

For this exercise, I built a simple Python project: a **Number Guessing Game**.

### Project Description

A program where the computer selects a random number between 1 and 100, and the user has to guess it within a limited number of attempts.

---

### Code Implementation

```python
import random

def number_guessing_game():
    print("Welcome to the Number Guessing Game!")
    print("I'm thinking of a number between 1 and 100.")

    secret_number = random.randint(1, 100)
    attempts = 0
    max_attempts = 10

    while attempts < max_attempts:
        try:
            guess = int(input("Enter your guess: "))
            attempts += 1

            if guess < secret_number:
                print("Too low!")
            elif guess > secret_number:
                print("Too high!")
            else:
                print(f"Correct! You guessed it in {attempts} attempts.")
                break

        except ValueError:
            print("Please enter a valid number.")

    if attempts == max_attempts and guess != secret_number:
        print(f"Game over! The correct number was {secret_number}.")

if __name__ == "__main__":
    number_guessing_game()
```

---

### How it works

* The computer generates a random number
* The user gets up to 10 attempts
* After each guess, feedback is given:

  * Too high
  * Too low
  * Correct
* The game ends when the user wins or runs out of attempts

---

### Reflection Questions

* This project helped me understand how loops and conditionals work together.
* I learned how to handle user input safely using `try/except`.
* I improved my understanding of basic game logic in Python.

---
