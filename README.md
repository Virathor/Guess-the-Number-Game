# Guess-the-Number-Game

import random

def get_user_guess():
    while True:
        try:
            guess = int(input("Enter your guess: "))
            return guess
        except ValueError:
            print("Please enter a valid number!")

def play_game(difficulty):
    if difficulty == 'easy':
        upper_limit = 50
        attempts = 10
    elif difficulty == 'medium':
        upper_limit = 100
        attempts = 8
    else:
        upper_limit = 1000
        attempts = 12

    secret_number = random.randint(1, upper_limit)
    print(f"Guess the number between 1 and {upper_limit}. You have {attempts} attempts.")

    for attempt in range(attempts):
        guess = get_user_guess()

        if guess == secret_number:
            print(f"Congratulations! You guessed it in {attempt + 1} attempts.")
            score = upper_limit - attempt * (upper_limit // attempts)
            print(f"Your score: {score}")
            return

        elif guess < secret_number:
            print("Higher!")

        else:
            print("Lower!")

        remaining_attempts = attempts - attempt - 1
        if remaining_attempts > 0:
            print(f"You have {remaining_attempts} attempts left.")
        else:
            print("Sorry, you're out of attempts!")
            print(f"The number was: {secret_number}")

def main():
    print("Welcome to the Guess the Number game!")

    while True:
        print("\nChoose difficulty: (easy, medium, hard)")
        difficulty = input().lower()

        if difficulty not in ['easy', 'medium', 'hard']:
            print("Invalid choice. Please choose 'easy', 'medium', or 'hard'.")
            continue

        play_game(difficulty)

        play_again = input("Do you want to play again? (yes/no): ").lower()
        if play_again != 'yes':
            print("Thanks for playing!")
            break

if __name__ == "__main__":
    main()
