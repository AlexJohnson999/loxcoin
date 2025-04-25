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
