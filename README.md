# Trivia-Quiz-Project
A trivia quiz is a game or activity that tests participants' knowledge across a wide range of topics, including history, science, literature, entertainment, sports, and popular culture. It typically involves answering questions posed by a quizmaster or through a digital platform.

# Trivia Quiz Game

Welcome to the Trivia Quiz Game! This is a console-based quiz game where you can test your knowledge with a variety of questions. The game will present questions with multiple-choice options, and you need to select the correct answer to score points.

## Features

- Multiple-choice questions
- Randomized answer options
- Score tracking
- Instant feedback on answers

## How to Play

1. The game will present a question with four possible answers.
2. Type the number corresponding to your choice and press Enter.
3. The game will tell you whether your answer was correct or incorrect.
4. After all questions are answered, your total score will be displayed.

## Getting Started

### Prerequisites

- Python 3.x

### Running the Game

1. Clone the repository or download the `quiz.py` file.
2. Open a terminal or command prompt.
3. Navigate to the directory containing the `quiz.py` file.
4. Run the game by typing:

    ```sh
    python quiz.py
    ```

5. Follow the on-screen instructions to play the game.

## Code Overview

### `Question` Class

Represents a single quiz question.

- `__init__(self, question, correct_answer, options)`: Initializes the question with the question text, the correct answer, and a list of options.

### `Quiz` Class

Manages the quiz, including presenting questions, evaluating answers, and tracking the score.

- `__init__(self, questions)`: Initializes the quiz with a list of `Question` objects and sets the initial score to 0.
- `present_question(self, question)`: Displays a question and its shuffled answer options, then prompts the user for their answer.
- `evaluate_answers(self)`: Iterates through all questions, presents each one, and checks the user's answer.
- `start_quiz(self)`: Starts the quiz, welcomes the user, and evaluates all answers.

### Example Usage

```python
import random

class Question:
    def __init__(self, question, correct_answer, options):
        self.question = question
        self.correct_answer = correct_answer
        self.options = options

class Quiz:
    def __init__(self, questions):
        self.questions = questions
        self.score = 0

    def present_question(self, question):
        print(question.question)
        options = question.options.copy()
        random.shuffle(options)
        for i, option in enumerate(options):
            print(f"{i + 1}. {option}")

        user_answer = input("Enter your choice (1-4): ")
        if user_answer.isdigit() and 1 <= int(user_answer) <= 4:
            return options[int(user_answer) - 1]
        else:
            print("Invalid choice. Please enter a number between 1 and 4.")
            return self.present_question(question)

    def evaluate_answers(self):
        for question in self.questions:
            user_answer = self.present_question(question)
            if user_answer == question.correct_answer:
                print("Correct!")
                self.score += 1
            else:
                print(f"Wrong! The correct answer is: {question.correct_answer}")
            print("----------------------")

    def start_quiz(self):
        print("Welcome to the Trivia Quiz Game!")
        print("Answer the following questions:")
        self.evaluate_answers()
        print(f"Your score: {self.score}/{len(self.questions)}")

if __name__ == "__main__":
    questions = [
        Question("What is the capital of France?", "Paris", ["London", "Berlin", "Paris", "Rome"]),
        Question("What keyword is used to define a function in Python?", "def", ["function", "void", "def", "define"]),
        Question("What does the 'self' keyword refer to in Python?", "Instance of the class", ["Global variable", "Local variable", "Instance of the class", "Class itself"]),
        Question("What is the largest mammal in the world?", "Blue Whale", ["African Elephant", "Blue Whale", "Giraffe", "Hippopotamus"]),
        Question("Who is known as the father of modern physics?", "Albert Einstein", ["Isaac Newton", "Galileo Galilei", "Albert Einstein", "Nikola Tesla"]),
        Question("Which planet is known as the Red Planet?", "Mars", ["Venus", "Mars", "Jupiter", "Saturn"]),
        Question("Which country is known as the Land of the Rising Sun?", "Japan", ["China", "Japan", "South Korea", "Vietnam"]),
    ]

    quiz = Quiz(questions)
    quiz.start_quiz()
