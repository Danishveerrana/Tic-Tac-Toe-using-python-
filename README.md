# Tic-Tac-Toe-using-python-
The Python code uses `tkinter` to make a Tic Tac Toe game GUI with buttons, player clicks, and win/draw handling.

# Tic Tac Toe GUI using tkinter

import tkinter as tk
from tkinter import messagebox

class TicTacToeGUI:
    def __init__(self):
        self.window = tk.Tk()
        self.window.title("Tic Tac Toe")
        self.current_player = "X"
        self.buttons = []

        for i in range(3):
            for j in range(3):
                button = tk.Button(self.window, text="", font=('normal', 20), width=8, height=4,
                                   command=lambda row=i, col=j: self.on_button_click(row, col))
                button.grid(row=i, column=j)
                self.buttons.append(button)

    def on_button_click(self, row, col):
        button = self.buttons[row * 3 + col]

        if button["text"] == "":
            button["text"] = self.current_player
            button["state"] = "disabled"

            if self.check_winner(row, col):
                messagebox.showinfo("Tic Tac Toe", f"Player {self.current_player} wins!")
                self.reset_game()
            elif self.is_board_full():
                messagebox.showinfo("Tic Tac Toe", "It's a draw!")
                self.reset_game()
            else:
                self.current_player = "O" if self.current_player == "X" else "X"

    def check_winner(self, row, col):
        # Check row
        if all(self.buttons[row * 3 + i]["text"] == self.current_player for i in range(3)):
            return True
        # Check column
        if all(self.buttons[i * 3 + col]["text"] == self.current_player for i in range(3)):
            return True
        # Check diagonals
        if row == col and all(self.buttons[i * 3 + i]["text"] == self.current_player for i in range(3)):
            return True
        if row + col == 2 and all(self.buttons[i * 3 + (2 - i)]["text"] == self.current_player for i in range(3)):
            return True
        return False

    def is_board_full(self):
        return all(button["text"] != "" for button in self.buttons)

    def reset_game(self):
        for button in self.buttons:
            button["text"] = ""
            button["state"] = "normal"

        self.current_player = "X"

    def run(self):
        self.window.mainloop()

# Create an instance of the TicTacToeGUI class and run the GUI
tictactoe_gui = TicTacToeGUI()
tictactoe_gui.run()
