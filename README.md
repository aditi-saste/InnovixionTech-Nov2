# InnovixionTech-Nov2(task 1)
import random
import tkinter as tk
from tkinter import messagebox

def check_guess(guess_entry, result_label, guess_button, secret_number, attempts_left):
    try:
        guess = int(guess_entry.get())
        if guess < secret_number:
            result_label.config(text="Too low! Try a higher number.")
        elif guess > secret_number:
            result_label.config(text="Too high! Try a lower number.")
        else:
            result_label.config(text=f"Congratulations! You've guessed the number ({secret_number}) correctly!")
            guess_button.config(state=tk.DISABLED)
        attempts_left[0] -= 1
        if attempts_left[0] == 0:
            result_label.config(text=f"Sorry, you've run out of attempts. The number was {secret_number}.")
            guess_button.config(state=tk.DISABLED)
    except ValueError:
        result_label.config(text="Please enter a valid number.")

def start_game(level):
    root = tk.Tk()
    root.title("Number Guessing Game")
    root.configure(bg="pink")

    if level == "Easy":
        secret_number = random.randint(1, 50)
        attempts_left = [5]  # Mutable object to store attempts
    elif level == "Medium":
        secret_number = random.randint(1, 100)
        attempts_left = [7]
    else:
        secret_number = random.randint(1, 200)
        attempts_left = [10]

    instructions_label = tk.Label(root, text=f"I'm thinking of a number between 1 and {'50' if level == 'Easy' else '100' if level == 'Medium' else '200'}. You have {attempts_left[0]} attempts to guess it.",font=("Arial", 14), padx=20, pady=20, bg="lightblue")
    instructions_label.pack()

    guess_entry = tk.Entry(root, width=10)
    guess_entry.pack()

    guess_button = tk.Button(root, text="Guess", padx=20, pady=20, bg="lightblue",font=("Arial", 14), command=lambda: check_guess(guess_entry, result_label, guess_button, secret_number, attempts_left))
    guess_button.pack()

    result_label = tk.Label(root, text="", padx=20, pady=20, bg="pink",font=("Arial", 14))
    result_label.pack()

def lets_play():
    root = tk.Tk()
    root.configure(bg="pink")
    root.title("Number Guessing Game")

    welcome_label = tk.Label(root, text="Welcome to the Number Guessing Game!", padx=20, pady=20, bg="lightblue",font=("Arial", 14))
    welcome_label.pack()

    level_label = tk.Label(root, text="Choose the level of the game:", padx=20, pady=20, bg="lightblue",font=("Arial", 14))
    level_label.pack()

    level_var = tk.StringVar()
    easy_button = tk.Radiobutton(root,font=("Arial", 14), text="Easy", variable=level_var, value="Easy")
    medium_button = tk.Radiobutton(root,font=("Arial", 14), text="Medium", variable=level_var, value="Medium")
    hard_button = tk.Radiobutton(root,font=("Arial", 14), text="Hard", variable=level_var, value="Hard")

    easy_button.pack()
    medium_button.pack()
    hard_button.pack()

    lets_button = tk.Button(root, text="Let's Play", padx=20, pady=20, bg="lightblue",font=("Arial", 14), command=lambda: start_game(level_var.get()))
    lets_button.pack()

    root.mainloop()

# Run the game
lets_play()
