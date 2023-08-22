# Artificial-Intelligence-Based-Safety-Solution-for-Accident

[![Watch the video](https://img.youtube.com/vi/H3dZqzgsovI/0.jpg)](https://youtu.be/H3dZqzgsovI)

    #define trigPin 2            //sensor A
    #define echoPin 3          //sensor A
    #define btrigPin 7          //sensor B
    #define bechoPin 8         //sensor B
    #define LED 13
    #define LED2green 12

    long d1;                  // sensor 1 distance                
    long d2;                  // sensor 2 distance
    long t1 = 0;              // sensor 1 timestamp; initialize as 0
    long t2 = 0;              // sensor 2 timestamp; initialize as 0
    unsigned long start_time; // time since program start
    float max_distance = 10;  // movement sensing range (in cm)
    long sensor1=0;
    long sensor2=0;
    long sensorno=0;
    void setup() 
      {
        Serial.begin (115200);
        pinMode(trigPin, OUTPUT);
        pinMode(echoPin, INPUT);
        pinMode(btrigPin, OUTPUT);
        pinMode(bechoPin, INPUT);
        pinMode(LED, OUTPUT);
        pinMode(LED2green, OUTPUT);
      start_time = millis();  // get program start time
    }

    void loop()
      {
        int  walid=0;
        int bduration, bdistance;
        digitalWrite(btrigPin, HIGH);
        delayMicroseconds(1000);
        digitalWrite(btrigPin, LOW);
        bduration = pulseIn(bechoPin, HIGH);
        bdistance = (bduration/2) / 29.1;
  
        int duration, distance;
        digitalWrite(trigPin, HIGH);
        delayMicroseconds(1000);
        digitalWrite(trigPin, LOW);
        duration = pulseIn(echoPin, HIGH);
        distance = (duration/2) / 29.1;
  
  
        if (distance >= 3 && distance <= 10)
          {
            t1 = millis();
           Serial.print(distance);
           Serial.println(" cm");
           sensor1=1;

                if (t2 < t1) 
                  {  
                    // if left sensor triggered first
                    Serial.println("Left to right");    // direction is left to right
                  } 
               else if (t1 < t2) 
                  {    
                    // if right sensor triggered first
                     Serial.println("Right to left");    // direction is right to left

                   }
                   delay(1000);
      
          }
           
            else if (bdistance >= 3 && bdistance <= 10)
                {
                  Serial.print(bdistance);
                  Serial.println(" cm");
                  t2 = millis();
                  sensor2=1;

                      if (t2 < t1) 
                        {                      
                        // if left sensor triggered first
                        Serial.println("Left to right");    // direction is left to right
                        } 
                       else if (t1 < t2) 
                       {                 
                       // if right sensor triggered first
                      Serial.println("Right to left");    // direction is right to left
                       }
                     delay(1000);      
             }   

    if (sensor2==1 )
        {
         Serial.println("two"); 
        Serial.println(sensor2); 
        Serial.println(sensor1); 
        digitalWrite(LED, HIGH);
        digitalWrite(LED2green, LOW);
            if (sensor1==1)
               {
             sensor1=0;
             sensor2=0;
               }
      }
    else if (sensor1==1)
      {
       Serial.println("one"); 
      Serial.println(sensor2); 
      Serial.println(sensor1); 
      digitalWrite(LED, HIGH);
      digitalWrite(LED2green, LOW);

        if (sensor2==1)
       {
           sensor1=0;
           sensor2=0;
       }
      
    }
     else if (sensor2 ==0 && sensor1==0)
      {
   
      digitalWrite(LED, LOW);
      digitalWrite(LED2green, HIGH); 
        }

      delay(1000);
    }
