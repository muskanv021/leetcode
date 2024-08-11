class Solution {
public:
    // Direction array to facilitate grid traversal.
    const vector<int> directions = {-1, 0, 1, 0, -1};
    // Variables to store grid dimensions.
    int rows, cols;

    // Function that returns the minimum number of days to isolate part of the grid.
    int minDays(vector<vector<int>>& grid) {
        // Initialize the dimensions.
        rows = grid.size();
        cols = grid[0].size();
      
        // Check if the grid is already disconnected or not connected at all.
        if (countIslands(grid) != 1) {
            return 0;  // A 0 will indicate no day required to isolate.
        }
      
        // Attempt removing each land piece to check if it can isolate an area.
        for (int i = 0; i < rows; ++i) {
            for (int j = 0; j < cols; ++j) {
                // If the current cell is land.
                if (grid[i][j] == 1) {
                    grid[i][j] = 0;  // Temporarily remove the land piece.
                    // Check if removing this piece disconnects the grid.
                    if (countIslands(grid) != 1) {
                        return 1;  // Returning 1 day required to isolate.
                    }
                    grid[i][j] = 1;  // Restore the land piece.
                }
            }
        }
      
        // If no single piece removal leads to isolation, return 2 days.
        return 2; // 
    }

    // Helper function to count the number of islands (distinct connected components).
    int countIslands(vector<vector<int>>& grid) {
        int islandCount = 0;
        // Iterate over the grid to find starting points of islands.
        for (int i = 0; i < rows; ++i) {
            for (int j = 0; j < cols; ++j) {
                // If a cell is land, start DFS.
                if (grid[i][j] == 1) {
                    dfs(i, j, grid);
                    ++islandCount;  // Increment island count after a full DFS.
                }
            }
        }
        // Reset the grid to its original state after counting.
        for (int i = 0; i < rows; ++i) {
            for (int j = 0; j < cols; ++j) {
                if (grid[i][j] == 2) {
                    grid[i][j] = 1;  // Reset the state from temporary 2 to land (1).
                }
            }
        }
        return islandCount;  // Return the total count of islands.
    }

    // Depth-first search to mark all cells of a single connected component.
    void dfs(int row, int col, vector<vector<int>>& grid) {
        grid[row][col] = 2;  // Temporarily mark the cell as part of an island.
        // Explore all four adjacent directions.
        for (int k = 0; k < 4; ++k) {
            int newRow = row + directions[k], newCol = col + directions[k + 1];
            // If adjacent cell is in bounds and land, continue the DFS.
            if (newRow >= 0 && newRow < rows && newCol >= 0 && newCol < cols && grid[newRow][newCol] == 1) {
                dfs(newRow, newCol, grid);
            }
        }
    }
};
