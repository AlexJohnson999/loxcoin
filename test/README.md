	public void addCelebrity(String name, String guess, String type)
	{
		if(validateCelebrity(name) && validateClue(guess, "")) {
			
		if(type.equals("Celebrity")) celebrityList.add(new Celebrity(name, guess));
			else if(guess.indexOf(',') !=-1 && type.equals("Literature"))
				
            celebrityList.add(new LiteratureCelebrity(name, guess, ""));
			else
				celebrityList.add(new LiteratureCelebrity(name, guess.substring(0, guess.indexOf(',')), 
            guess.substring(guess.indexOf(','))));
		}
			
	}
 

 // Simplest Way Possible Claude
 public void addCelebrity(String name, String guess, String type) {
   if(!validateCelebrity(name) || !validateClue(guess, "")) return;
   
   int i = guess.indexOf(',');
   celebrityList.add(type.equals("Celebrity") ? 
       new Celebrity(name, guess) : 
       new LiteratureCelebrity(name, 
           i > -1 && type.equals("Literature") ? guess.substring(0, i) : guess, 
           i > -1 && type.equals("Literature") ? guess.substring(i+1) : ""));
}

//Shortest code possible according to claude
public void addCelebrity(String name, String guess, String type) {
   if(!validateCelebrity(name) || !validateClue(guess, "")) return;
   if(type.equals("Celebrity")) celebrityList.add(new Celebrity(name, guess));
   else if(type.equals("Literature") && guess.indexOf(',') != -1) {
       int i = guess.indexOf(',');
       celebrityList.add(new LiteratureCelebrity(name, guess.substring(0, i), guess.substring(i+1)));
   } else celebrityList.add(new LiteratureCelebrity(name, guess, ""));
}
Will have to repaste other dudes stuff to test what is making multiple exceptions
Entire code for the gamefile itself:
import java.util.ArrayList;
import java.util.List;


/**
 * The framework for the Celebrity Game project
 * 
 * @author cody.henrichsen
 * @version 2.3 25/09/2018 refactored the prepareGame and play methods
 */
public class CelebrityGame
{
	private Celebrity subCeleb;
	private ArrayList<Celebrity> celebrityList;
   private CelebrityFrame celebrityGameFrame;
	
	public CelebrityGame()
	{
		celebrityGameFrame = new CelebrityFrame(this);
      celebrityList =new ArrayList<Celebrity>();
	
	}

	/**
	 * Prepares the game to start by re-initializing the celebGameList and having the gameFrame open the start screen.
	 */
	public void prepareGame()
	{
		celebrityGameFrame.replaceScreen("Begin!");
      celebrityList= new ArrayList<Celebrity>();
	}
	
	//Closes the current game window. Used for the reset button functionality under CelebrityPanel
	public void closeGame()
	{
		celebrityGameFrame.dispose();
	}

	/**
	 * Determines if the supplied guess is correct.
	 * 
	 * @param guess
	 *            The supplied String
	 * @return Whether it matches regardless of case or extraneous external
	 *         spaces.
	 */
	public boolean processGuess(String guess)
	{
		if(guessCheck(guess, subCeleb.getAnswer())) {
			celebrityList.remove(subCeleb);
			
			if(celebrityList.size() > 0)
            subCeleb= celebrityList.get(0);
			
         else
            subCeleb= new Celebrity(" "," ");
			
			return true;
		}
		else
			return false;
	}
   private boolean guessCheck(String guess, String answer) {
    return guess.trim().equalsIgnoreCase(answer);
   }
	/**
	 * Asserts that the list is initialized and contains at least one Celebrity.
	 * Sets the current celebrity as the first item in the list. Opens the game
	 * play screen.
	 */
	public void play()
	{
		if (isListValid(celebrityList))  {
			
			subCeleb = celebrityList.get(0);
			celebrityGameFrame.replaceScreen("Celebrity");
		}
		else 
			{
			celebrityGameFrame =new CelebrityFrame(this);
			celebrityGameFrame.replaceScreen("Begin!");
		}
	}
   private boolean isListValid(List<?> list){
    return list != null && !list.isEmpty();
}
	/**
	 * Adds a Celebrity of specified type to the game list
	 * 
	 * @param name
	 *            The name of the celebrity
	 * @param guess
	 *            The clue(s) for the celebrity
	 * @param type
	 *            What type of celebrity
	 */
	public void addCelebrity(String name, String guess, String type)
	{
		if(validateCelebrity(name) && validateClue(guess, "")) {
			
		if(type.equals("Celebrity")) celebrityList.add(new Celebrity(name, guess));
			else if(guess.indexOf(',') !=-1 && type.equals("Literature"))
				
            celebrityList.add(new LiteratureCelebrity(name, guess, ""));
			else
				celebrityList.add(new LiteratureCelebrity(name, guess.substring(0, guess.indexOf(',')), 
            guess.substring(guess.indexOf(','))));
		}
			
	}
	

	/**
	 * Validates the name of the celebrity. It must have at least 4 characters.
	 * @param name The name of the Celebrity
	 * @return If the supplied Celebrity is valid
	 */
	public boolean validateCelebrity(String name)
	{
    return name.length() >= 4;

	}

	/**
	 * Checks that the supplied clue has at least 10 characters or is a series of clues
	 * This method would be expanded based on your subclass of Celebrity.
	 * @param clue The text of the clue(s)
	 * @param type Supports a subclass of Celebrity 
	 * @return If the clue is valid.
	 */
	public boolean validateClue(String clue, String type)
	{
   return clue.length() >= 10;

	}

	/**
	 * Accessor method for the current size of the list of celebrities
	 * 
	 * @return Remaining number of celebrities
	 */
	public int getCelebrityGameSize()
	{
		return celebrityList.size();
	}

	/**
	 * Accessor method for the games clue to maintain low coupling between
	 * classes
	 * 
	 * @return The String clue from the current celebrity.
	 */
	public String sendClue()
	{
		return subCeleb.getClue();
	}

	/**
	 * Accessor method for the games answer to maintain low coupling between
	 * classes
	 * 
	 * @return The String answer from the current celebrity.
	 */
	public String sendAnswer()
	{
	return subCeleb.getAnswer();
	}
	
}













