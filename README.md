# Problem-Classes
//Problem Class. A class with a question and an answer.

public class Problem{
	
	private String question;
	private String[] answers;
	private int level;
	private int index = 0;
	
	//Constructors
	
	public Problem(){
		question = "";
		answers = new String[5];
		level = 1;
		createQuestion();
	}
	
	public Problem(int l){
		question = "";
		answers = new String[5];
		level = l;
		createQuestion();
	}
	
	public Problem(String q, String[] a, int l){
		question = q;
		answers = new String[5];
		for(int i = 0; i < 5; i++){
			answers[i] = a[i];
		}
		level = l;
	}
	
	//Methods
	
	public void createQuestion(){
		Questions q;
		switch (level) {
			case 2: q = new LevelTwoQuestion();
				break;
			case 3: q = new LevelThreeQuestion();
				break;
			case 4: q = new LevelFourQuestion();
				break;
			//case 5: q = new LevelFiveQuestion();
				//break;
			default: q = new LevelOneQuestion();
				break;
		}
		question = q.getQuestion();
		index = (int)(Math.random()*5);
		for(int i = 0; i < 5; i++){
			if(i == index)
				answers[i] = q.getRightAnswer();
			else
				answers[i] = q.getWrongAnswer();
		}
	}
	
	//Modifying Methods
	
	public void setQuestion(String q){
		question = q;
	}
	
	public void setAnswers(String[] a){
		for(int i = 0; i < 5; i++){
			answers[i] = a[i];
		}
	}
	
	public void setLevel(int l){
		level = l;
		Questions q;
		switch (level) {
			case 2: q = new LevelTwoQuestion();
				break;
			case 3: q = new LevelThreeQuestion();
				break;
			case 4: q = new LevelFourQuestion();
				break;
			//case 5: q = new LevelFiveQuestion();
				//break;
			default: q = new LevelOneQuestion();
				break;
		}
		question = q.getQuestion();
		index = (int)(Math.random()*5);
		for(int i = 0; i < 5; i++){
			if(i == index)
				answers[i] = q.getRightAnswer();
			else
				answers[i] = q.getWrongAnswer();
		}
	}
	
	//Accessor Methods
	
	public String getQuestion(){ return question; }
	
	public String[] getAnswers(){ return answers; }
	
	public int getLevel(){ return level; }
	
	public int getRightAnswerIndex(){ return index; }
	
}


//Creats a level 1 question Addition/Subtraction

public class LevelOneQuestion extends Questions{
	
	private int x;
	private int y;
	private int answer;
	private String n;
	
	//constructors
	
	public LevelOneQuestion(){
		x = (int)(Math.random()*100);
		y = (int)(Math.random()*100);
		if(y % 2 == 0){
			n = " - ";
			answer = x - y;
		} else {
			n = " + ";
			answer = x + y;
		}
	}
	
	//accessor methods
	
	public String getQuestion(){
		return (x + n + y + " = ");
	}
	
	public String getRightAnswer(){
		return ("" + answer);
	}
	
	public String getWrongAnswer(){
		return ("" + (int)(Math.random()*150));
	}
	
}


//Creats a level 2 question Multiplication/Division

public class LevelTwoQuestion extends Questions{ 
	
	private int x;
	private int y;
	private String answer;
	private String n;
	private int rem;
	
	//constructors
	
	public LevelTwoQuestion(){
		x = (int)(Math.random()*20);
		y = (int)(Math.random()*20);
		if(y % 2 == 0){
			n = " * ";
			answer = ("" + (x * y));
		} else {
			n = " / ";
			rem = x % y;
			answer = ("" + (x / y) + " R: " + rem);
		}
	}
	
	//accessor methods
	
	public String getQuestion(){
		return (x + n + y + " = ");
	}
	
	public String getRightAnswer(){
		return answer;
	}
	
	public String getWrongAnswer(){
		if(y % 2 == 0){
			return("" + (int)(Math.random()*20)*(int)(Math.random()*20));
		} else {
			return("" + (x / y) + " R: " + ((int)(Math.random()*y)));
		}
	}
	
}


//Creats a level 3 question Simple Algebra

public class LevelThreeQuestion extends Questions{ 
	
	private int x;
	private int y;
	private int answer;
	private String question;
	
	//constructors
	
	public LevelThreeQuestion(){
		x = (int)(Math.random()*20);
		y = (int)(Math.random()*20);
		if((y - x) % 2 == 0){
			answer = (y - x)/2;
			question = ("2x + " + x + " = " + y);
		} else if(x % 2 == 0){
			answer = (y - x);
			question = ("x + " + x + " = " + y);
		} else if(y % 2 == 0){
			answer = (y - x);
			question = (x + " + x = " + y);
		} else {
			answer = -1 * (y-x);
			question = (x + " - x = " + y);
		}
	}
	
	//accessor methods
	
	public String getQuestion(){
		return (question + ". Find x.");
	}
	
	public String getRightAnswer(){
		return ("" + answer);
	}
	
	public String getWrongAnswer(){
		return ("" + (int)(Math.random()*30));
	}
	
}


//Creats a level 4 question Algebra 1

public class LevelFourQuestion extends Questions{
	
	private int x;
	private int y;
	private String answer;
	private String question;
	
	//constructors
	
	public LevelFourQuestion(){
		x = (int)(Math.random()*20);
		y = (int)(Math.pow((double)(x / 2), 2.0));
		question = ("x^2 + " + x + "x + " + y);
		if(x % 2 == 0)
			answer = ("(x + " + (x / 2) + ")^2");
		else
			answer = ("(x + " + (x / 2) + ")(x + " + (x / 2 + 1) + ")");
	}
	
	//accessor methods
	
	public String getQuestion(){
		return (question + ". Simplify.");
	}
	
	public String getRightAnswer(){
		return answer;
	}
	
	public String getWrongAnswer(){
		int a = (int)(Math.random()*15);
		if(x % 2 == 0)
			return ("(x + " + a + ")^2");
		else
			return ("(x + " + a + ")(x + " + (a + 1) + ")");
	}
	
}


//Creats a level 5 question. Trig

/*public class LevelFiveQuestion extends Questions{
	
	private String[] x = new String[]{"0", (String)227};
	private String[][] y;
	private String answer;
	private String question;
	
	//constructors
	
	public LevelFiveQuestion(){
		
	}
	
	//accessor methods
	
	public String getQuestion(){
		return (question + ". Simplify.");
	}
	
	public String getRightAnswer(){
		return answer;
	}
	
	public String getWrongAnswer(){
		
	}
	
}*/
