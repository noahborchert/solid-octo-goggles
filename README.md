# GPA calculator

import java.io.*;

import java.util.*;

import java.math.RoundingMode;

import java.text.DecimalFormat;

/**
 * This class is used to take input from the user via a scanner class, store and
 * calculate inputs, and tell the user their GPA based on the 7 inputs given
 *
 * @Noah Borchert
 * @1-13-2020
 */

public class Calc
{
    
    /**
     * I first initiate all variables including 
     * - each letter grade set to a double
     * - three grade variables that alternate to add and divide the grades
     * - a string taking in the grade
     * - a boolean for honors
     * - a decimal format variable to round the final grade to the nearest thousandth
     */
    public static double A = 4.0;
    public static double B = 3.0;
    public static double C = 2.0;
    public static double D = 1.0;
    public static double F = 0.0;
    public static double finalGrade = 0.0;
    public static double numGrade;
    public static double addedGrade = 0.0;
    public static String grade;
    public static boolean isHonors = false;
    private static DecimalFormat df = new DecimalFormat("0.00");

    /**
     * This class does just what it's name suggests. It asks the user for the grade
     * in their classes one at a time.
     * After each ask it runs the honors method and then the calculator method,
     * so it knows if to add to the grade as an honors class, and then it adds the
     * grade to the changing grade variable used to calculate.
     * After it has asked for and received a grade 7 times, the method takes the
     * latest version of final grade and outputs a response to the user based
     * on their GPA
     * If the user does not input a capital letter A-F (excluding E), the user
     * is prompted for a valid input
     */
    public static String askForInput()
    {

        System.out.println("What is your current letter grade in your first class of the day?");
        grade = UserInput.getString();
        if(grade.equals("A") || grade.equals("B") || grade.equals("C") 
        || grade.equals("D") || grade.equals("F"))
        {
            honors();
            calculator();
        }
        else
        {
            System.out.println("I'm sorry, I don't understand. Please enter a valid input");
            askForInput();
        }
        for(int i = 0; i < 5; i++)
        {
            System.out.println("What is your current letter grade in your next class? ");
            grade = UserInput.getString();
            if(grade.equals("A") || grade.equals("B") || grade.equals("C") 
            || grade.equals("D") || grade.equals("F"))
            {
                honors();
                calculator();
            }
            else
            {
                System.out.println("I'm sorry I dont understand, could you try a different answer?");
                System.out.println("");
                i--;
            }
        }

        System.out.println("What is your current letter grade in your last class of the day?");
        grade = UserInput.getString();
        if(grade.equals("A") || grade.equals("B") || grade.equals("C") 
        || grade.equals("D") || grade.equals("F"))
        {
            honors();
            calculator();
        }
        else
        {
            System.out.println("I'm afraid I dont understand. Please try again.");
            System.out.println("");
            while(!(grade.equals("A") || grade.equals("B") || grade.equals("C") 
                || grade.equals("D") || grade.equals("F")))
            {
                System.out.println("What is your current letter grade in your last class of the day?");
                grade = UserInput.getString();
                honors();
                calculator();
            }
        }

        double GPA = finalGrade / 7;
        if(GPA > 4.0)
        {
            System.out.println("Wow you might actually suceeed in life with a " + df.format(GPA));
        }
        else if(GPA <= 4.0 && GPA >= 3.5)
        {
            System.out.println("Congrats; with a " + df.format(GPA) + ", you can get into most colleges. But never the top teir ones...");
        }
        else if(GPA <= 3.5 && GPA >=2.0)
        {
            System.out.println("Your GPA is a " + df.format(GPA) + "...Maybe you can get into Penn State or something...");
        }
        else if(GPA < 2.0 && GPA >= 1.5)
        {
            System.out.println(df.format(GPA) + ", huh...Maybe you'll get good SAT scores?");
        }
        else if(GPA < 1.5 && GPA >= 1.0)
        {
            System.out.println("A " + df.format(GPA) + " is something even I can't help you with.");
        }
        else if(GPA < 1.0)
        {
            System.out.println("A " + df.format(GPA) + "? Did you only take a semester PE class?");
        }
        return grade;
    }

    /**
     * simple boolean method that looks for a string input and sets "yes" to
     * true (is an honors class) and "no" to false
     */
    public static boolean honors()
    {
        System.out.println("Is this a weighted class?(honors?) ");

        String honors = UserInput.getString();

        if(honors.equals("yes") || honors.equals("Yes"))
        {
            isHonors = true;
        }
        else if(honors.equals("no") || honors.equals("No"))
        {
            isHonors = false;
        }
        else
        {
            System.out.println("It would be most efficient if the user did not dodge the question.");
            honors();
        }

        return isHonors;
    }

    /**
     * This method takes a String and sets each letter grade to a double with the
     * same letter that holds a double value coorisponding to the grade. If it's
     * and honors class, and the grade is higher than a D, the calculator adds 
     * 1.0 and then adds the final grade of that class to addedGrade which then 
     * equals final grade.
     */
    public static double calculator()
    {
        if(grade.equals("A"))
        {
            numGrade = A;
        }
        else if(grade.equals("B"))
        {
            numGrade = B;
        }
        else if(grade.equals("C"))
        {
            numGrade = C;
        }
        else if(grade.equals("D"))
        {
            numGrade = D;
        }
        else if(grade.equals("F"))
        {
            numGrade = F;
        }
        if(isHonors && numGrade != D && numGrade != F)
        {
            numGrade += 1.0;
        }
        addedGrade += numGrade;
        finalGrade = addedGrade;

        return finalGrade;
    }

    /**
     * The main method prints the program header, disclaimer, and directions, 
     * and then calls the askForInput method to start the GPA claculator
     */
    public static void main()
    {
        System.out.println("      GGGGGGGGGGGGG  PPPPPPPPPPPPPPPPP         AAA                                                      lllllll                -----_    _" );
        System.out.println("    GGG::::::::::::G  P::::::::::::::::P       A:::A                                                     l:::::l                  |  |\\  /|" );
        System.out.println("  GG:::::::::::::::G  P::::::PPPPPP:::::P     A:::::A                                                    l:::::l                  |  | \\/ | " );        
        System.out.println(" G:::::GGGGGGGG::::G  PP:::::P     P:::::P   A:::::::A                                                   l:::::l                     " );
        System.out.println("G:::::G       GGGGGG    P::::P     P:::::P  A:::::::::A               cccccccccccccccc  aaaaaaaaaaaaa     l::::l     cccccccccccccccc" );
        System.out.println("G:::::G                 P::::P     P:::::P A:::::A:::::A            cc:::::::::::::::c  a::::::::::::a    l::::l   cc:::::::::::::::c" );
        System.out.println("G:::::G                 P::::PPPPPP:::::P A:::::A A:::::A          c:::::::::::::::::c  aaaaaaaaa:::::a   l::::l  c:::::::::::::::::c" );
        System.out.println("G:::::G    GGGGGGGGGG   P:::::::::::::PP A:::::A   A:::::A        c:::::::cccccc:::::c           a::::a   l::::l c:::::::cccccc:::::c" );
        System.out.println("G:::::G    G::::::::G   P::::PPPPPPPPP  A:::::A     A:::::A       c::::::c     ccccccc    aaaaaaa:::::a   l::::l c::::::c     ccccccc" );
        System.out.println("G:::::G    GGGGG::::G   P::::P         A:::::AAAAAAAAA:::::A      c:::::c               aa::::::::::::a   l::::l c:::::c            " ); 
        System.out.println("G:::::G        G::::G   P::::P        A:::::::::::::::::::::A     c:::::c              a::::aaaa::::::a   l::::l c:::::c            " ); 
        System.out.println(" G:::::G       G::::G   P::::P       A:::::AAAAAAAAAAAAA:::::A    c::::::c     ccccccca::::a    a:::::a   l::::l c::::::c     ccccccc" );
        System.out.println("  G:::::GGGGGGGG::::G PP::::::PP    A:::::A             A:::::A   c:::::::cccccc:::::ca::::a    a:::::a  l::::::lc:::::::cccccc:::::c" );
        System.out.println("   GG:::::::::::::::G P::::::::P   A:::::A               A:::::A   c:::::::::::::::::ca:::::aaaa::::::a  l::::::l c:::::::::::::::::c" );
        System.out.println("     GGG::::::GGG:::G P::::::::P  A:::::A                 A:::::A   cc:::::::::::::::c a::::::::::aa:::a l::::::l  cc:::::::::::::::c" );
        System.out.println("        GGGGGG   GGGG PPPPPPPPPP AAAAAAA                   AAAAAAA    cccccccccccccccc  aaaaaaaaaa  aaaa llllllll    cccccccccccccccc");
        System.out.println("");
        System.out.println("                                               ---Presented to you by ACME IQ inc.--- ");
        System.out.println("");
        System.out.println("                                     * --------------------------------------------------------- *");
        System.out.println("                                     | Disclaimer:                                               |");
        System.out.println("                                     |     Any information involving low grades and GPA may      |");
        System.out.println("                                     |     be sent to every single person you know via email.    |");
        System.out.println("                                     |     In this event, ACME™ will not be held legally         |");
        System.out.println("                                     |     responsible for damage to self-esteem.                |");
        System.out.println("                                     * --------------------------------------------------------- *");
        System.out.println("");
        System.out.println(" ➣ I will need to know the current letter grade (as a capital letter) of each class");
        System.out.println("    as weather or not it's a wieghted class in order to calculate as well");
        System.out.println("    your GPA. All information provided will maybe remain anonymous.");
        System.out.println("");
        System.out.println("");

        askForInput();
    }
}




**** UserInput Class ******



import java.util.Scanner;

/**
 * class for getting input from a user
 */
 
public class UserInput
{
    /**
     * This scanner enables user to input through text
     */
     
    public static String getString()
    
    {
    
        Scanner input = new Scanner(System.in);
        
        return input.next();
        
    }
    
    
}

