#include <vector>
#include <unordered_set>
#include <algorithm>

class Solution {
public:
    // This method simulates the movement of a robot according to given commands and obstacles.
    // Returns the maximum squared Euclidean distance from the origin a robot reaches.
    int robotSim(std::vector<int>& commands, std::vector<std::vector<int>>& obstacles) {
        // Direction vectors for north, east, south, west.
        int directions[5] = {0, 1, 0, -1, 0}; // last '0' is to allow easy access to 'y' direction with directions[k+1]

        // Function to encode a pair of coordinates into a single integer.
        auto hashFunction = [](int x, int y) {
            return x * 60010 + y;
        };
      
        // Set to hold the hashed locations of the obstacles.
        std::unordered_set<int> obstacleSet;
        for (const auto& obstacle : obstacles) {
            obstacleSet.insert(hashFunction(obstacle[0], obstacle[1]));
        }
      
        // Initialize variables to track the maximum Euclidean distance squared
        // and the current direction index and coordinates of the robot.
        int maxDistanceSquared = 0, directionIndex = 0;
        int x = 0, y = 0; // Robot starts at the origin (0,0)

        // Iterate through each command to move the robot.
        for (int command : commands) {
            if (command == -2) { // -2 means turn left 90 degrees
                directionIndex = (directionIndex + 3) % 4; // rotate left in the directions array
            } else if (command == -1) { // -1 means turn right 90 degrees
                directionIndex = (directionIndex + 1) % 4; // rotate right in the directions array
            } else {
                // Move forward by 'command' steps.
                while (command--) { // Loop over each step.
                    // Calculate the next x and y after moving a step in the current direction.
                    int nextX = x + directions[directionIndex];
                    int nextY = y + directions[directionIndex + 1];

                    // Check if next position is an obstacle.
                    if (obstacleSet.count(hashFunction(nextX, nextY))) {
                        break; // An obstacle blocks further movement in this direction.
                    }

                    // Update the robot's current position.
                    x = nextX;
                    y = nextY;

                    // Update the max distance squared if necessary.
                    maxDistanceSquared = std::max(maxDistanceSquared, x * x + y * y);
                }
            }
        }
      
        // Return the maximum Euclidean distance squared that the robot has been from the origin.
        return maxDistanceSquared;
    }
};
