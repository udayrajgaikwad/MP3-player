import pygame
import os
import tkinter as tk
from tkinter import filedialog

class MP3Player:
    def __init__(self):
        self.root = tk.Tk()
        self.root.title("MP3 Player")
        self.root.geometry("400x200")

        self.current_file = None
        self.paused = False

        self.initialize_ui()

    def initialize_ui(self):
        # Buttons
        self.play_button = tk.Button(self.root, text="Play", command=self.play_pause)
        self.play_button.pack(pady=10)

        self.stop_button = tk.Button(self.root, text="Stop", command=self.stop)
        self.stop_button.pack(pady=5)

        self.forward_button = tk.Button(self.root, text="Forward", command=self.forward)
        self.forward_button.pack(pady=5)

        self.rewind_button = tk.Button(self.root, text="Rewind", command=self.rewind)
        self.rewind_button.pack(pady=5)

        self.select_button = tk.Button(self.root, text="Select MP3", command=self.select_mp3)
        self.select_button.pack(pady=10)

        # Initialize Pygame
        pygame.mixer.init()

        self.root.mainloop()

    def play_pause(self):
        if self.current_file:
            if not self.paused:
                pygame.mixer.music.load(self.current_file)
                pygame.mixer.music.play()
                self.play_button.config(text="Pause")
            else:
                pygame.mixer.music.pause()
                self.play_button.config(text="Play")
            self.paused = not self.paused

    def stop(self):
        pygame.mixer.music.stop()
        self.play_button.config(text="Play")
        self.paused = False

    def forward(self):
        # You can implement your own logic for forwarding the track
        pass

    def rewind(self):
        # You can implement your own logic for rewinding the track
        pass

    def select_mp3(self):
        file_path = filedialog.askopenfilename(title="Select MP3 file", filetypes=[("MP3 files", "*.mp3")])
        if file_path:
            self.current_file = file_path
            self.stop()
            self.play_pause()

if __name__ == "__main__":
    mp3_player = MP3Player()
