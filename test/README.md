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
