# Game
class Room:
    def __init__(self, name, description):
        self.name = name
        self.description = description
        self.exits = {}

    def add_exit(self, direction, room):
        self.exits[direction] = room

    def get_exit(self, direction):
        return self.exits.get(direction)


class Player:
    def __init__(self, name):
        self.name = name
        self.current_room = None

    def move(self, direction):
        if direction in self.current_room.exits:
            self.current_room = self.current_room.get_exit(direction)
            print("You move to", self.current_room.name)
            print(self.current_room.description)
        else:
            print("You cannot go that way.")


# Define the rooms
kitchen = Room("Kitchen", "You are in a spacious kitchen. You see a table and some chairs.")
living_room = Room("Living Room", "You are in a cozy living room with a fireplace.")
bedroom = Room("Bedroom", "You are in a comfortable bedroom with a large bed.")

# Set up the exits between rooms
kitchen.add_exit("north", living_room)
living_room.add_exit("south", kitchen)
living_room.add_exit("east", bedroom)
bedroom.add_exit("west", living_room)

# Create the player
player_name = input("Enter your name: ")
player = Player(player_name)
player.current_room = kitchen

# Start the game loop
print("Welcome to the Text-based Adventure Game!")
print("Type 'quit' to exit the game.")

while True:
    print("\n" + player.current_room.name)
    print(player.current_room.description)
    
    command = input("What do you want to do? (Type 'north', 'south', 'east', 'west', or 'quit'): ").lower()
    
    if command == "quit":
        print("Thanks for playing!")
        break
    elif command in ["north", "south", "east", "west"]:
        player.move(command)
    else:
        print("Invalid command. Please try again.")
