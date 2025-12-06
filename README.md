// RLCore.h

#include <iostream>
#include <map>
#include <string>

/**
 * Defines a simplified structure for the agent's state in the game.
 * Used as the key in the Q-table.
 */
struct GameState {
    int currentRank;
    bool isUnderAttack;
    std::string keyObjectiveStatus;
    
    // Allows the struct to be used as a map key
    bool operator<(const GameState& other) const {
        if (currentRank != other.currentRank) return currentRank < other.currentRank;
        if (isUnderAttack != other.isUnderAttack) return isUnderAttack < other.isUnderAttack;
        return keyObjectiveStatus < other.keyObjectiveStatus;
    }
};

/**
 * Defines the Reinforcement Learning Core class.
 */
class RLCore {
private:
    // Q-Table structure: State -> Action -> Q-Value (Expected Reward)
    std::map<GameState, std::map<std::string, double>> qTable;
    double learningRate = 0.1;
    double discountFactor = 0.9; 

public:
    RLCore() {}

    /**
     * Gets the current Q-Value for a given State-Action pair.
     */
    double getQValue(const GameState& state, const std::string& action) {
        // Returns 0.0 for unexplored states/actions
        return qTable[state][action];
    }
    
    // Placeholder for the core update logic
    void updateQValue(const GameState& state, const std::string& action, double reward, const GameState& nextState) {
        // Core RL update logic will be implemented here later.
    }
};

// Example Usage (for compilation test)
void testRLCore() {
    RLCore core;
    GameState state = {2, false, "Available"};
    std::string action = "AggressivePush";
    
    // Initial check
    std::cout << "Initial Q-Value for Rank 2 / AggressivePush: " 
              << core.getQValue(state, action) << std::endl;
}
