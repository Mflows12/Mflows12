import random
import sys

# Function to display the road with obstacles and the car position
def display_road(road_length, car_position):
    road = [' '] * road_length
    road[car_position] = 'C'  # Car represented by 'C'
    road_with_obstacles = add_obstacles(road)
    print(''.join(road_with_obstacles))

# Function to add random obstacles on the road
def add_obstacles(road):
    for i in range(len(road)):
        if random.random() < 0.2:  # Adjust obstacle frequency as needed
            road[i] = 'X'  # Obstacle represented by 'X'
    return road

# Function to move the car left
def move_left(car_position):
    return max(0, car_position - 1)

# Function to move the car right
def move_right(car_position, road_length):
    return min(road_length - 1, car_position + 1)

# Main function to run the game
def main():
    road_length = 20
    car_position = road_length // 2  # Start the car in the middle of the road
    game_over = False

    print("Welcome to the Driving Game!")
    print("Use WASD keys to move the car. Press Q to quit.")

    while not game_over:
        display_road(road_length, car_position)

        # Get user input to move the car
        move = input("Move left (A) or right (D)? Press Q to quit: ").lower()

        if move == 'a':
            car_position = move_left(car_position)
        elif move == 'd':
            car_position = move_right(car_position, road_length)
        elif move == 'q':
            print("Thanks for playing!")
            game_over = True
        else:
            print("Invalid input! Please use WASD keys to move the car or Q to quit.")

        # Check for collision with obstacle
        if 'X' in display_road(road_length, car_position):
            print("Game Over! You crashed into an obstacle!")
            game_over = True

if __name__ == "__main__":
    main()
