# PrisonersDilemma
Directions and code to play Prisoners Dilemma

Central Question in Prisoners Dilemma - 
When playing against opponent (co-worker/business/country) do you try to help them or not.

               Prisoners Dilemma has applications in Cold War, economy, social sciences ...

In class we listen to the first 10 minutes of the radiolab mp3 which sets up the motivation for this game and how it is played.

Prisoners Dilemma is a standard example of a game analyzed in game theory
 
  From https://en.wikipedia.org/wiki/Prisoner%27s_dilemma
 Albert W. Tucker formalized the game with prison sentence rewards and named it "prisoner's dilemma" presenting it as follows:
 
 Two members of a criminal gang are arrested and imprisoned. Each prisoner is in solitary confinement with no means of communicating with the other. The prosecutors lack sufficient evidence to convict the pair on the principal charge, but they have enough to convict both on a lesser charge. Simultaneously, the prosecutors offer each prisoner a bargain. Each prisoner is given the opportunity either to betray the other by testifying that the other committed the crime, or to cooperate with the other by remaining silent. The offer is:

    If A and B each betray the other, each of them serves two years in prison
    If A betrays B but B remains silent, A will be set free and B will serve three years in prison (and vice versa)
    If A and B both remain silent, both of them will serve only one year in prison (on the lesser charge).



The Director code which runs this tournament was modeled after Robert Axelrod's Prisoners Dilemma tournament where every program plays every other program 200 times in a round robin tournamet. The team with the most overall points after playing all other teams is the winner.   https://plato.stanford.edu/entries/prisoner-dilemma/#AxelTitForTat

Here is the scoring for YOUR program versus the other team's program:

public class ScoreConstant {

	public static final double COOPERATE_COOPERATE = 3;
	public static final double COOPERATE_DEFECT = 0;
	public static final double DEFECT_COOPERATE = 5;
	public static final double DEFECT_DEFECT = 1;
}

   
   For example if you cooperate when the other team defects you earn 0 points. If you defect when the other team cooperates you get 5 points. If both teams defect, they each earn 1 point. If both teams cooperate, they each earn 3 points.
   
Each team must implement the Entry interface:

public interface Entry {
	
	 /* Returns this entry's move for the given round.
	 * @param round the integer round number
	 * @return the Move made for this round by this entry*/
	public Move getMove(int round);
	
	 /* Sets the moves made for the given round by this entry and the opponent.
	 * 
	 * @param round the integer round number
	 * @param yourMove the Move this entry  made for this round
	 * @param opponentMove the Move the opponent made for this round*/
	public void setResult(int round, Move yourMove, Move opponentMove);
}

 getMove(...)  returns your Move     ->  either Move.DEFECT  or Move.COOPERATE
 setResult(int r, Move you, Move opp)  -> called after your program and opponents program have made a move and it tells you what each of your moves were for that round.   Your program can keep track of all the moves, some of the moves, ...  and set instance variable(s) appropriately to have a strategy in your getMove method.

public enum Move {
	DEFECT,
	COOPERATE
}

The Director program plays two programs against each other (and eventually all teams agains all other teams in a round robin). It first calls getMove(int round) from each program to get the move of each. It then calls setResult(int round, Move yourMove, Move opponentMove) to tell each program what just happened. This repeats 200 times with the Director keeping track of each program's score.

Students get the following files when writing their program:  Move.java,   Entry.java, ScoreConstant.java

An example program which always cooperates is included.   Jesus.java  
