import random
import csv

def main():
    '''main'''
    with open("pokemon.csv", "r") as file:
        try:
            reader = csv.DictReader(file)
        except Exception:
            print("File not found.")

    info = select(reader)
    game(info)


def select(reader):
    '''Randomly selected pokemon information is saved to a dictionary'''
    pokemon = {
        "Name":[],
        "FirstType": [],
        "SecondType": [],
        "Height": [],
        "Weight": [],
        "Generation": [],
    }
    # Randomly select a pokemon from database
    row = random.randint(2, 802)
    for row in reader:
        name = row['name']
        type1 = row['type1']
        type2 = row['type2']
        height = row['height']
        weight = row['weight']
        generation = row['generation']

    # Randomly selected pokemon info is stored
    pokemon['Name'].append(name)
    pokemon['FirstType'].append(type1)
    pokemon['SecondType'].append(type2)
    pokemon['Height'].append(height)
    pokemon['Weight'].append(weight)
    pokemon['Generation'].append(generation)

    return pokemon


def game(info):
    '''Loops for entirety of game'''
    count = 0

    # Number of guesses user has
    while count < 10:
        # Initialize empty dictionary
        guesser = {
            "Name":[],
            "FirstType": [],
            "SecondType": [],
            "Height": [],
            "Weight": [],
            "Generation": [],
        }

        guess = input("Enter pokemon name: ")
        count = count + 1

        # Used to break out of nested loop if conditions are met
        break_flag = False

        with open("pokemon.csv", "r") as file:
            reader = csv.DictReader(file)
                 
            for row in reader:
                for field in row:
                    if field == guess:
                        name = row['name']
                        type1 = row['type1']
                        type2 = row['type2']
                        height = row['height']
                        weight = row['weight']
                        generation = row['generation']

                        guesser['Name'].append(name)
                        guesser['FirstType'].append(type1)
                        guesser['SecondType'].append(type2)
                        guesser['Height'].append(height)
                        guesser['Weight'].append(weight)
                        guesser['Generation'].append(generation)

                        break_flag = True
                        break
                if break_flag is True:
                    break
            else:
                print("ERROR: Pokemon not found. Please enter a valid Pokemon name.")
                count = count - 1
                continue

        check = response(guesser, info)

        # If guess is correct
        if check is True:
            print(guess + " is correct! It took " + count + "guess(es).")
            break


def response(guesser, info):
    '''Outputs advice for user's next input'''
    # Initialize an array for comparisons
    advice = ['Name', 'FirstType', 'SecondType', 'Height', 'Weight', 'Generation']

    # Change all elements to lowercase for comparison
    lower(guesser, advice)
    lower(info, advice)
  
    for i in len(info):
        if i == 0:
            if guesser.get(advice[i]) == info.get(advice[i]):
                return True
        if i in (1,2):
            if guesser.get(advice[i]) != info.get(advice[i]):
                print(advice[i] + ": Incorrect")
            else:
                print(advice[i] + ": Correct")
        if i in (3,4,5):
            if guesser.get(advice[i]) != info.get(advice[i]):
                print(advice[i] + ": Incorrect.", end = "")
                if guesser.get(advice[i]) > info.get(advice[i]):
                    print(advice[i] + " is less")
                else:
                    print(advice[i] + " is greater")
            else:
                print(advice[i] + ": Correct")


def lower(dictionary, advice):
    '''Converts dictionary to lowercase''' 

    for i in len(dictionary):
        dictionary[advice[i]] = dictionary[advice[i]].str.lower()
    return dictionary
