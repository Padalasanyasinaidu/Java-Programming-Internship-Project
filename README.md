import java.util.ArrayList;
import java.util.Scanner;

class Question {
    private String text;
    private String[] options;
    private int correctAnswer;

    public Question(String text, String[] options, int correctAnswer) {
        this.text = text;
        this.options = options;
        this.correctAnswer = correctAnswer;
    }

    public void display() {
        System.out.println(text);
        for (int i = 0; i < options.length; i++) {
            System.out.println((i + 1) + ". " + options[i]);
        }
    }

    public boolean isCorrect(int userAnswer) {
        return userAnswer == correctAnswer;
    }
}

class Quiz {
    private ArrayList<Question> questions;

    public Quiz() {
        this.questions = new ArrayList<>();
    }

    public void addQuestion(Question question) {
        questions.add(question);
    }

    public int takeQuiz() {
        int score = 0;
        for (Question question : questions) {
            question.display();
            int userAnswer = getUserInput();
            if (question.isCorrect(userAnswer)) {
                score++;
            }
        }
        return score;
    }

    public int size() {
        return questions.size();
    }

    private static int getUserInput() {
        Scanner scanner = new Scanner(System.in);
        while (true) {
            try {
                int userAnswer = Integer.parseInt(scanner.nextLine());
                if (userAnswer >= 1 && userAnswer <= 4) {
                    return userAnswer;
                } else {
                    System.out.println("Invalid input. Please enter a number between 1 and 4.");
                }
            } catch (NumberFormatException e) {
                System.out.println("Invalid input. Please enter a number.");
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        // Create Questions
        Question question1 = new Question("What is the capital of France?", new String[]{"Paris", "Berlin", "London", "Rome"}, 1);
        Question question2 = new Question("Which planet is known as the Red Planet?", new String[]{"Mars", "Venus", "Jupiter", "Saturn"}, 1);
        Question question3 = new Question("What is the largest mammal?", new String[]{"Elephant", "Whale Shark", "Blue Whale", "Giraffe"}, 3);

        // Create Quiz
        Quiz quiz = new Quiz();
        quiz.addQuestion(question1);
        quiz.addQuestion(question2);
        quiz.addQuestion(question3);

        // Take Quiz
        int userScore = quiz.takeQuiz();

        // Display Score
        System.out.println("\nYour score: " + userScore + "/" + quiz.size());
    }
}
