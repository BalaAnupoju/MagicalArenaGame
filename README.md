# MagicalArenaGame
This project implements a simple Magical Arena game where two players battle each other by attacking and defending in turns. 
The game continues until one player's health reaches zero, and the player with remaining health wins. 
Players use dice rolls to determine the effectiveness of their attacks and defenses.

Requirements :
--> Java 11 or later (for the provided Java implementation)
--> JUnit 5 for unit testing

magical-arena/
├── src/
│   ├── Arena.java      // Contains the game loop and logic for the battle
│   ├── Player.java     // Defines the Player class with attributes and methods
│   ├── Main.java       
├── junit5/src/magicalArenaGame/java
│   ├── ArenaTest.java  // Unit tests for the Arena class
│  
├── README.md          // Project documentation

--> src/ contains the core implementation of the game.
--> junit5/src/magicalArenaGame/java contains unit tests for verifying the logic of the game.
--> README.md provides documentation for how to set up and run the project.

How to Run :-
Process 1 :

1) Clone the Repository
2) Compile the Java code: If you have Java installed, you can compile the source files using the javac command
   javac -d bin src/*.java
3)Run the Game: After compiling, you can run the game:
   java -cp bin Arena
4)If you're using Maven, you can run:
   mvn test

Process 2 :
   If you're using an IDE (e.g., IntelliJ IDEA, Eclipse), you can run the files directly in the IDE.



   

How the game works :- 
Initialization of Players
When the game starts, two players are created:
Player 1: Player player1 = new Player(50, 5, 10);
Health = 50
Strength = 5
Attack = 10
Player 2: Player player2 = new Player(100, 10, 5);
Health = 100
Strength = 10
Attack = 5
Arena Creation

These two players are then passed into an Arena object:

Arena arena = new Arena(player1, player2);
The arena will handle the combat between these two players, deciding who attacks first and managing the turns.
Determining the First Attacker

In the startFight() method in the Arena class, the game determines which player will attack first based on their health:

Player attacker = player1.getHealth() <= player2.getHealth() ? player1 : player2;
Player defender = attacker == player1 ? player2 : player1;
Player with lower or equal health attacks first.
Player 1 has 50 health, and Player 2 has 100 health. Since Player 1 has the lower health, Player 1 will attack first.
Turn-Based Combat (Attack and Defense)

On each turn, the attacker will:

Roll the Attack Die: This is a random value between 1 and 6.
Roll the Defense Die: The defender also rolls a defense die, a random value between 1 and 6.
Attack Calculation: The attack damage is calculated by multiplying the attack die roll by the attack attribute of the attacking player.

For example, if Player 1 attacks:
Assume Player 1 rolls a 5 on the attack die.
Attack damage = Player 1's attack * Attack die roll = 10 * 5 = 50.
Defense Calculation: The defender rolls the defense die and multiplies it by their strength attribute to calculate how much damage they block.

For example, if Player 2 rolls a 2 on the defense die:
Defense damage = Player 2's strength * Defense die roll = 10 * 2 = 20.
Effective Damage: The net damage is the difference between the attack damage and the defense damage. If the result is negative (i.e., the defense is higher than the attack), the damage is set to zero.

Effective damage = max(attackDamage - defenseDamage, 0).
In this case: 50 - 20 = 30 (so Player 2 takes 30 damage).
Player Health Reduction: The opponent (defender) takes the effective damage:

Player 2’s health reduces by 30. So, Player 2's health is now 100 - 30 = 70.
Swapping Roles: After each turn, the attacker and defender swap roles, and the next player attacks:

Player temp = attacker;
attacker = defender;
defender = temp;
After Player 1 attacks and Player 2’s health is reduced, Player 2 will now attack and Player 1 will defend on the next turn.
Repeat the Combat Loop: The game continues to alternate turns between the players until one player's health reaches zero. The game loop looks like this:

while (player1.isAlive() && player2.isAlive()) {
    attacker.attack(defender); // Attacker attacks defender
    Player temp = attacker;
    attacker = defender;
    defender = temp;
}
Game Over: When one player's health reaches zero, the loop ends, and the winner is declared:

if (player1.isAlive()) {
    System.out.println("Player 1 wins!");
} else {
    System.out.println("Player 2 wins!");
}


Example Walkthrough of One Round
Let’s walk through an example with the following setup:

Player 1: Health = 50, Strength = 5, Attack = 10
Player 2: Health = 100, Strength = 10, Attack = 5
Round 1: Player 1 Attacks
Player 1 rolls the attack die: 5.
Player 2 rolls the defense die: 2.
Attack damage: 5 (attack die roll) * 10 (Player 1's attack) = 50
Defense damage: 2 (defense die roll) * 10 (Player 2's strength) = 20
Effective damage: 50 (attack) - 20 (defense) = 30
Player 2’s health: 100 - 30 = 70
Round 2: Player 2 Attacks
Player 2 rolls the attack die: 4.
Player 1 rolls the defense die: 3.
Attack damage: 4 (attack die roll) * 5 (Player 2's attack) = 20
Defense damage: 3 (defense die roll) * 5 (Player 1's strength) = 15
Effective damage: 20 (attack) - 15 (defense) = 5
Player 1’s health: 50 - 5 = 45
At this point, Player 1’s health is 45, and Player 2’s health is 70.

The game continues like this, alternating turns until one player’s health reaches 0.

Key Notes:
First Attack: The player with the lower health attacks first.
Dice Rolls: Both the attacker and defender roll a 6-sided die to determine the effectiveness of their actions (attack and defense).
Health Reduction: The defender’s health is reduced by the net damage (attack damage minus defense damage).
Winner: The game ends when one player's health reaches zero, and the other player is declared the winner.
Final Thoughts
The game continues to alternate between players until one of them loses all health.
The randomness of the dice rolls ensures that no two fights are exactly the same, adding variety and unpredictability to the game.
The Arena class manages the entire flow of the game, including determining which player attacks first, swapping roles after each turn, and ending the game when a player's health reaches zero.




   

   
