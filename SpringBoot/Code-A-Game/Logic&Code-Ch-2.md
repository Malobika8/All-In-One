## Goal
<img width="1131" alt="Screenshot 2024-06-23 at 9 39 45 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/17dcb40a-6ebd-45a0-987c-314db60ee5de">
<img width="904" alt="Screenshot 2024-06-23 at 11 10 33 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/7c74c86c-2cde-49ce-82d2-0d24a644999d">

## GameController

    @Controller
    public class GameController {

    @Autowired
    GameService gameService;

    @Autowired
    GameUtils gameUtils;

    @RequestMapping("/game-home")
    String showGameHomePage(@RequestParam(value = "guessedChar", required = false) String guessedChar, Model model) {

        if (guessedChar != null && gameUtils.getTriesRemaining()>0) {
            Boolean isGuessCorrect = gameService.addGuess(guessedChar.toLowerCase().charAt(0));
            if(!isGuessCorrect)
                gameUtils.reduceTry();
        }

        if(Arrays.equals(gameService.getRandomlyChosenWord().toCharArray(), gameService.getCharactersOfTheWord())){
            model.addAttribute("result", "You won!!!");
        }

        String randomWord = gameService.toString();

        model.addAttribute("randomWord", randomWord);
        model.addAttribute("triesLeft",gameUtils.getTriesRemaining());

        return "game-home";
    }

    @GetMapping("/reload")
    public String reloadGame(){

        gameService = gameUtils.reload();

        //reset the no of tries
        gameUtils.resetTries();

        return "redirect:/game-home";
    }
    }

## GameService

Default scope of a Bean is Singleton. We need to create object on demand. We can use prototype scope for the same.

    @Service
    @Scope("prototype")
    public class GameService {

    private String[] randomWords = {"father", "mother", "sister", "brother", "hi", "hello", "food"};
    private  String randomlyChosenWord =null;
    private char[] charactersOfTheWord;
    Random random = new Random();

    public GameService() {

        randomlyChosenWord = randomWords[random.nextInt(randomWords.length)];
        charactersOfTheWord = new char[randomlyChosenWord.length()];
        System.out.println("******************" + randomlyChosenWord);
    }

    public String getRandomlyChosenWord() {
        return randomlyChosenWord;
    }

    public char[] getCharactersOfTheWord() {
        return charactersOfTheWord;
    }

    public Boolean addGuess(char chr){
        Boolean isCorrect = false;

        for(int i = 0; i< randomlyChosenWord.length(); i++){
            if(charactersOfTheWord[i]=='\u0000' && chr == randomlyChosenWord.charAt(i)){
                charactersOfTheWord[i] = chr;
                isCorrect = true;
            }
        }
        return isCorrect;
    }

    @Override
    public String toString() {
        String ret = "";

        for(int i=0; i<charactersOfTheWord.length;i++){
            if(charactersOfTheWord[i] == '\u0000')
                ret = ret + " _";
            else
                ret = ret + charactersOfTheWord[i];
        }

        return ret;
    }
    }

## GameUtils

    @Component
    public class GameUtils {

    @Autowired
    ConfigurableApplicationContext applicationContext;
    private static int MAX_TRIES = 5;

    public void reduceTry(){
        MAX_TRIES = MAX_TRIES - 1;
    }

    public int getTriesRemaining(){
        return MAX_TRIES;
    }

    public void resetTries(){
        MAX_TRIES = 5;
    }

    public GameService reload(){
        GameService gameService = applicationContext.getBean(GameService.class);

        return gameService;
    }
    }

## game-home.html

    <!DOCTYPE html>
    <html lang="en" xmlns:th="http://www.thymeleaf.org">
    <head>
    <meta charset="UTF-8">
    <title>Guess the Word</title>
    <script th:inline="javascript">
        window.onload = function checkIfGameOver(){
            var numOfTriesRemaining = [[${triesLeft}]];
            if(numOfTriesRemaining == 0){
                alert("Game Over");
                document.getElementById('guessedChar').disabled = true;
                document.getElementById('try').disabled = true;
            }
        }
        function reloadGame(){
            window.location.href = "http://localhost:8080/reload";
        }
    </script>
    </head>
    <body>
    <h1 align="center ">Guess the Word</h1>
    <h2 align="center" th:text="${randomWord}">Show some random word</h2>
    <h2 align="right" th:text="'Attempts Remaining : ' + ${triesLeft}">Number of tries left</h2>
    <hr/>
    <div>
        <input type="button" value="reload" id="reload" style="float:right" onclick="reloadGame()">
    </div>
    <div align="center">
        <form action="game-home" method="get">
            <label>Guess a Character</label>
            <input type="text" name="guessedChar" id="guessedChar">
            <input type="submit" name="Try" id="try">
        </form>
    </div>
    <hr/>
    <h2 align="center" th:text="${result}">Show result</h2>
    </body>
    </html>

## GuessTheWordApplication

    @SpringBootApplication
    public class GuessTheWordApplication {
    public static void main(String[] args) {

        SpringApplication.run(GuessTheWordApplication.class, args);
    }
    }






