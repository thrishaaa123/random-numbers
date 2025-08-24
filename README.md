import tkinter as tk
import random

class GuessGame:
    def __init__(self, root):
        self.root = root
        self.root.title("🎯 Number Guessing Game")
        self.root.geometry("400x300")
        
        self.secret_number = random.randint(1, 50)
        self.attempts = 0

        # Title
        self.title_label = tk.Label(root, text="Guess the Number!", font=("Arial", 16, "bold"))
        self.title_label.pack(pady=10)

        # Instructions
        self.instruction_label = tk.Label(root, text="I'm thinking of a number between 1 and 50")
        self.instruction_label.pack()

        # Entry box
        self.entry = tk.Entry(root, font=("Arial", 14))
        self.entry.pack(pady=5)

        # Submit button
        self.submit_button = tk.Button(root, text="Submit Guess", command=self.check_guess, bg="green", fg="white")
        self.submit_button.pack(pady=5)

        # Result label
        self.result_label = tk.Label(root, text="", font=("Arial", 12))
        self.result_label.pack(pady=5)

        # Attempts label
        self.attempt_label = tk.Label(root, text="Attempts: 0")
        self.attempt_label.pack()

        # Restart button
        self.restart_button = tk.Button(root, text="Restart Game", command=self.restart_game, bg="red", fg="white")
        self.restart_button.pack(pady=10)

    def check_guess(self):
        try:
            guess = int(self.entry.get())
            self.attempts += 1
            self.attempt_label.config(text=f"Attempts: {self.attempts}")

            if guess < self.secret_number:
                self.result_label.config(text="Too low! Try again.", fg="blue")
            elif guess > self.secret_number:
                self.result_label.config(text="Too high! Try again.", fg="orange")
            else:
                self.result_label.config(text=f"🎉 Correct! The number was {self.secret_number}", fg="green")
        except ValueError:
            self.result_label.config(text="Please enter a valid number.", fg="red")

    def restart_game(self):
        self.secret_number = random.randint(1, 50)
        self.attempts = 0
        self.attempt_label.config(text="Attempts: 0")
        self.result_label.config(text="")
        self.entry.delete(0, tk.END)


# Run the game
if __name__ == "__main__":
    root = tk.Tk()
    game = GuessGame(root)
    root.mainloop()
