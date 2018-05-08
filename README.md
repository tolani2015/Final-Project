const int buttonPin1 = 4; //buttonPin1 to arduino pin 4
const int buttonPin2 = 3; //buttonPin2 to arduino pin 3
const int buttonPin3 = 2; //buttonPin3 to arduino pin 2
const int ledPin1 =  13; //ledPin1 to arduino pin 13
const int ledPin2 =  12; //ledPin2 to arduino pin 12
const int ledPin3 =  11; //ledPin3 to arduino pin 11
const int ledPinWrong =  7; //ledPinWrong to arduino pin 7
const int buzzer = 9; //buzzer to arduino pin 9
int start = 0; // initial game level
int randArray[9]; // Array for random ouput
int userArray{9]; // Array for user input
int y;

int buttonState1 = 0; // variable for reading the buttonPin1
int buttonState2 = 0; // variable for reading the buttonPin2
int buttonState3 = 0; // variable for reading the buttonPin3
void fail(); // function for losing tone
void win(); // function for winning tone


void setup() 
{
  pinMode(ledPin1, OUTPUT); // Set ledPin1 - pin 13 as an output
  pinMode(ledPin2, OUTPUT); // Set ledPin2 - pin 12 as an output
  pinMode(ledPin3, OUTPUT); // Set ledPin3 - pin 11 as an output
  pinMode(ledPinWrong, OUTPUT); // Set buttonPinWrong - pin 7 as an output
  pinMode(buttonPin1, INPUT); // Set buttonPin1 - pin 4 as an output
  pinMode(buttonPin2, INPUT); // Set buttonPin2 - pin 3 as an output
  pinMode(buttonPin3, INPUT); // Set buttonPin3 - pin 2 as an output
  pinMode(buzzer, OUTPUT); // Set buzzer - pin 9 as an output
  randomSeed(analogRead(0)); // Initializes pseudo-random number generator
  for(int w=0;w<10;w++) // For loop for random number
  {
      randArray[w] = random(1, 4); // Array up to 10 random inputs from 1 to 3
   
  }
}
void loop() 
{  
   buttonState1 = digitalRead(buttonPin1); //Sets the status of buttonPin1 to buttonState1 
   buttonState2 = digitalRead(buttonPin2); //Sets the status of buttonPin2 to buttonState2 
   buttonState3 = digitalRead(buttonPin3); //Sets the status of buttonPin3 to buttonState3
  if (buttonState2==HIGH&&buttonState3==HIGH)// Game starts when buttonPin2 & 3 are pressed
  {
  for(y=0;y<=start;y++)//limited by start
  {
    while (start == 9)//while start is equal to 9 
    {
      for(int w = 0; w < 100; w--)// infinite loop
      {
       win();//play winning tone infinitly until game is manually reset
      }
    } 
    digitalWrite(ledPin1, HIGH);// Turns on ledPin1
    digitalWrite(ledPin2, HIGH);// Turns on ledPin2
    digitalWrite(ledPin3, HIGH);// Turns on ledPin3
    delay(300);                 //  ...for .3 sec
    digitalWrite(ledPin3, LOW);// Turns off ledPin1
    digitalWrite(ledPin2, LOW);// Turns off ledPin2
    digitalWrite(ledPin1, LOW);// Turns off ledPin3
    delay(300);                //...for 1 sec
    for (int x=0;x<=y;x++)//limited by y variable
    
    {
     if (randArray[x]== 1)// If randArray is 3 at x
       {
        digitalWrite(ledPin1, HIGH);// turns on ledPin1
        tone(buzzer, 500); // Send 500Hz sound signal...
        delay(100);        // ...for .1 sec
        noTone(buzzer);     // Stop sound...
        delay(100);        // ...for .1sec
        digitalWrite(ledPin1, LOW);// turns off ledPin1
        delay(1000);// ...for 1 sec
       }
       if (randArray[x] == 2)// If randArray is 2 at x
       {
        digitalWrite(ledPin2, HIGH);// turns on ledPin2
        tone(buzzer, 2000); // Send 2KHz sound signal...
        delay(100);        // ...for .1 sec
        noTone(buzzer);     // Stop sound...
        delay(100);        // ...for .1sec
        digitalWrite(ledPin2, LOW);// turns off ledPin2
        delay(1000);// ...for 1 sec
       }
       if (randArray[x] == 3)// If randArray is 3 at x
       {
        digitalWrite(ledPin3, HIGH);// turns on ledPin3
        tone(buzzer, 4000); // Send 4KHz sound signal...
        delay(100);        // ...for .1 sec
        noTone(buzzer);     // Stop sound...
        delay(100);        // ...for .1 sec
        digitalWrite(ledPin3, LOW);// turns off ledPin3
        delay(1000);// ...for 1 sec
       }

     } // for x
    if(input()<0)
    {
     y=0;
     start=0;// resets game level
     break;// breaks for(y) statement
    }
    else
    {
    start++;// increases game level by 1
    }
  }// for y
 }//if

}

int input()
{
        
   for (int x=0; x <= start;x++)
   {
   buttonState1 = digitalRead(buttonPin1); //Sets the status of buttonPin1 to buttonState1 
   buttonState2 = digitalRead(buttonPin2); //Sets the status of buttonPin2 to buttonState2
   buttonState3 = digitalRead(buttonPin3); //Sets the status of buttonPin3 to buttonState3 
    while (buttonState1==LOW&&buttonState2==LOW&&buttonState3==LOW)//while buttonPin1, 2 & 3 are on
    {
     buttonState1 = digitalRead(buttonPin1); //Sets the status of buttonPin1 to buttonState1 
     buttonState2 = digitalRead(buttonPin2); //Sets the status of buttonPin2 to buttonState2 
     buttonState3 = digitalRead(buttonPin3); //Sets the status of buttonPin3 to buttonState3
      delay(20);
    } // while
 
     while (buttonState1==HIGH)// while buttonPin1 is on
     {
       userArray[x] = 1;// Places value of 1 for the array at x
       if (userArray[x]== randArray[x])// If the choice is correct, ledPin1 lights up & plays tone
       {
       buttonState1=LOW;// Turns buttonPin1 off
       digitalWrite(ledPin1, HIGH);// Turns on ledPin1
       tone(buzzer, 2500); // Send 6.5KHz sound signal...
       delay(300);        // ...for .3 sec
       noTone(buzzer);     // Stop sound...    
       tone(buzzer, 1000); // Send 2KHz sound signal...
       delay(300);        // ...for .3 sec*/
       noTone(buzzer);     // Stop sound...    
       digitalWrite(ledPin1, LOW);// Turns off ledPin1
       }
       else
       {
         fail();// Plays failing tone when the user loses
         return -1;// Returns negative value to so that the game resets
       }
     } // while ( buttonState1 ) 
     
    while (buttonState2==HIGH)// while buttonPin2 is on
     {
       userArray[x] = 2;// Places value of 2 for the array at x
       if (userArray[x]== randArray[x])// If the choice is correct, ledPin2 lights up & plays tone
       {
       buttonState2=LOW;// Turns buttonPin2 off
       digitalWrite(ledPin2, HIGH);// Turns on ledPin2
       tone(buzzer, 6500); // Send 6.5KHz sound signal...
       delay(300);        // ...for .1 sec
       noTone(buzzer);     // Stop sound...    
       tone(buzzer, 2000); // Send 2KHz sound signal...
       delay(300);        // ...for .1 sec
       noTone(buzzer);     // Stop sound...  
       digitalWrite(ledPin2, LOW);// Turns off ledPin2
       }
       else
       {
         fail();// Plays failing tone when the user loses
         return -2;// Returns negative value to so that the game resets.
       }
     } // while( buttonState2 ) 
     while (buttonState3==HIGH)// while buttonPin3 is on
     {
       userArray[x] = 3;// Places value of 3 for the array at x
       if (userArray[x]== randArray[x])// If the choice is correct, ledPin3 lights up & plays tone
       {
       buttonState3=LOW;// Turns buttonPin1 off
       digitalWrite(ledPin3, HIGH);// Turns on ledPin3
       tone(buzzer, 6500); // Send 6.5KHz sound signal...
       delay(300);        // ...for .1 sec
       noTone(buzzer);     // Stop sound...    
       tone(buzzer, 2000); // Send 2KHz sound signal...
       delay(300);        // ...for .1 sec
       noTone(buzzer);     // Stop sound...    
       digitalWrite(ledPin3, LOW);// Turns off ledPin3
       }
       else
       {
         fail();// Plays failing tone when the user loses
         return -3;// Returns negative value to so that the game resets.
       }
     } // while( buttonState3 ) 
      
   
   } // end for x
return 1; 
}  // end function input()
  
void fail() //Function used if the player fails to match the sequence
 { 
  tone(buzzer, 300); // Send .3 KHz sound signal...
  delay(500);        // ...for .5 sec
  digitalWrite(ledPinWrong, HIGH);// Turns on ledPinWrong
  delay(500);                     // ...for .5 sec
  digitalWrite(ledPinWrong, LOW);// Turns off ledPinWrong
  delay(500);                    // ...for .5 sec
  tone(buzzer, 300); // Send .3 KHz sound signal...
  delay(500);        // ...for .5 sec
  digitalWrite(ledPinWrong, HIGH);// Turns on ledPinWrong
  delay(500);                     // ...for .5 sec
  digitalWrite(ledPinWrong, LOW);// Turns off ledPinWrong
  delay(500);                    // ...for .5 sec
  noTone(buzzer);    // Stop sound...    
 }
 void win()
  {
  tone(buzzer, 300); // Send .3 KHz sound signal...
  delay(500);        // ...for .5 sec
  digitalWrite(ledPin1, HIGH);// turns on ledPin1
  digitalWrite(ledPin2, HIGH);// turns on ledPin2
  digitalWrite(ledPin3, HIGH);// turns on ledPin3
  delay(500);                 // ...for .5 sec
  digitalWrite(ledPin1, LOW);// turns off ledPin1
  digitalWrite(ledPin2, LOW);// turns off ledPin2
  digitalWrite(ledPin3, LOW);// turns off ledPin3
  delay(500);                // ...for .5 sec
  tone(buzzer, 300); // Send .3 KHz sound signal...
  delay(500);        // ...for .5 sec
  digitalWrite(ledPin1, HIGH);// turns on ledPin1
  digitalWrite(ledPin2, HIGH);// turns on ledPin2
  digitalWrite(ledPin3, HIGH);// turns on ledPin3
  delay(500);                 // ...for .5 sec
  digitalWrite(ledPin1, LOW);// turns off ledPin1
  digitalWrite(ledPin2, LOW);// turns off ledPin2
  digitalWrite(ledPin3, LOW);// turns off ledPin3
  delay(500);                // ...for .5 sec
  noTone(buzzer);    // Stop sound...    
  }
