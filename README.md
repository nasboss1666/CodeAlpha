# CodeAlpha
"A terminal-based Python Hangman game that features random word selection, interactive letter guessing, and custom input validation within a 6-attempt limi
import random


def play_hangman():
  # 1. A small list of 5 predefined words
  words = ["python", "coding", "hangman", "developer", "abubaka Yusuf Maitama "]

  # Select a random word from the list
  word_to_guess = random.choice(words)
  guessed_letters = []
  incorrect_guesses_left = 6

  print("========================================")
  print("         WELCOME TO HANGMAN!            ")
  print("========================================")
  print(f"You have {incorrect_guesses_left} incorrect guesses allowed.\n")

  # Game loop
  while incorrect_guesses_left > 0:
    # Build the current word display (revealing guessed letters, hiding others with underscores)
    display_word = ""
    for letter in word_to_guess:
      if letter in guessed_letters:
        display_word += letter + " "
      else:
        display_word += "_ "

    print(f"Word: {display_word.strip()}")

    # Check if the player has won
    if "_" not in display_word:
      print("\n🎉 Congratulations! You guessed the word correctly! 🎉")
      break

    print(f"Guessed letters: {', '.join(sorted(guessed_letters))}")
    print(f"Incorrect guesses remaining: {incorrect_guesses_left}")

    # Get player input
    guess = input("\nGuess a letter: ").lower()

    # Input validation
    if len(guess) != 1 or not guess.isalpha():
      print("⚠️ Please enter a single alphabetical letter.\n")
      continue

    if guess in guessed_letters:
      print(f"⚠️ You already guessed '{guess}'. Try a different letter.\n")
      continue

    # Record the guess
    guessed_letters.append(guess)

    # Evaluate the guess using if-else
    if guess in word_to_guess:
      print(f"✅ Good job! '{guess}' is in the word.\n")
    else:
      incorrect_guesses_left -= 1
      print(f"❌ Sorry, '{guess}' is not in the word.\n")

  # Loss condition check
  if incorrect_guesses_left == 0:
    print("========================================")
    print("      GAME OVER! You ran out of lives.  ")
    print("========================================")
    print(f"The secret word was: {word_to_guess}")


if __name__ == "__main__":
  play_hangman()
