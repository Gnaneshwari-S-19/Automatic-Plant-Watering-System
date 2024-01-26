class plant
{
  int pump; //LED
  int pot;  //Potentiometer
  int s;  //State i.e assign 1 if ON and 0 if OFF
  public:
    plant(){} //Default Constructor
    plant(int x, int y) //Initializing pin values per plant
    {
      pump = x;
      pot = y;
    }
    void pump_on(void);
    void pump_off(void);
    void state(void);
    void moisture(void);
};

void setup() 
{
  pinMode(A0, INPUT);
  pinMode(A1, INPUT);
  pinMode(A2, INPUT);
  pinMode(6, OUTPUT);
  pinMode(7, OUTPUT);
  pinMode(8, OUTPUT);
  pinMode(4, OUTPUT);
  pinMode(5, OUTPUT);
  pinMode(13, OUTPUT);
  pinMode(12, INPUT);
  Serial.begin(115200);
  Serial.println("Automatic Plant Watering System\nCommands:");
  Serial.println("1.Print State of Pumps");
  Serial.println("2.Override\n");
}

plant p1(6, A0);  //Plant 1
plant p2(7, A1);  //Plant 2
plant p3(8, A2);  //Plant 3

void loop() 
{
  int com = Serial.parseInt();
    if(com == 1)  //Print pump state
    {
      p1.state();
      p2.state();
      p3.state();
      Serial.println("\n\n");
      delay(3000);
      start();
    }
    else if(com == 2) //Override
    {
      p1.pump_off();
      p2.pump_off();
      p3.pump_off();
      screen();
      Serial.print("\n");
      while(com !=3)
      {
        int c = Serial.parseInt();
        switch(c)
        {
          case 10: p1.pump_off();
                    break;
          case 11: p1.pump_on();
                    break;
          case 20: p2.pump_off();
                    break;
          case 21: p2.pump_on();
                    break; 
          case 30: p3.pump_off();
                    break;
          case 31: p3.pump_on();
                    break;
          case 3: com = 3;
                  start();
                  break;
        }
      }
    }
    else
    {
      p1.moisture();
      p2.moisture();
      p3.moisture();
    }
}

////////********To Print the state of the pumps********////////
void plant::state()
{
  if(pump == 6)
    Serial.print("Plant 1 ");
  else if(pump == 7)
    Serial.print("Plant 2 ");
  else
    Serial.print("Plant 3 ");
  if(s == 1)
    Serial.print("Pump is on.\n");
  else if(s == 0)
    Serial.print("Pump is off.\n");  
}

////////********Turn on the pump & set state to 1********////////
void plant::pump_on()
{
  digitalWrite(pump, HIGH);
  s = 1;
}

////////********Turn off the pump & set state to 0********////////
void plant::pump_off()
{
  digitalWrite(pump, LOW);
  s = 0;
}

/////////*********Check moisture level in the soil********////////
void plant::moisture()
{
  if (tank() == 0 )
  { 
    float m = analogRead(pot);
    m = map(m, 0, 1023, 0, 300);
    if(m > 250.0)
      pump_off();
    else if(m < 100.0)
      pump_on();  
  }
}

//////////**********Check water level in the tank**********//////////
int tank()
{
  digitalWrite(13, HIGH);
  delayMicroseconds(10);
  
  digitalWrite(13, LOW);
  
  int duration = pulseIn(12, HIGH);
  float level = (duration/58);
  if(level > 350)
  {
    Serial.println("Low Water Level!");
    digitalWrite(4, HIGH);
    tone(5, 500, 200);
    p1.pump_off();
    p2.pump_off();
    p3.pump_off();
    delay(2000);
    return 1;
  }
  else
  {
    digitalWrite(4, LOW);
    digitalWrite(5, LOW);
    return 0;
  }
}

//////////**********Command Screen for Override**********//////////
void screen()
{
  Serial.println("Override!\nCommands:");
  Serial.println("11.Turn plant1 pump on      10.Turn plant1 pump off");
  Serial.println("21.Turn plant2 pump on      20.Turn plant2 pump off");
  Serial.println("31.Turn plant3 pump on      30.Turn plant3 pump off");
  Serial.println("3.Switch to automatic");
}

///////////***********Initial Command Screen***********///////////
void start()
{
  Serial.println("\n");
  Serial.println("Automatic Plant Watering System\nCommands:");
  Serial.println("1.Print State of Pumps");
  Serial.println("2.Override\n\n");
}

//////////////**************End of Code**************//////////////
