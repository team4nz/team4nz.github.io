---
layout: post
categories: posts
title: 3. Development Log
tags: [dev]
date-string: DECEMBER 02, 2019
---

# Task #1 - Line Tracing ( PID )

```c++

while ( bt ) {

    cl = getColorName(c2);
    
    if ( (cl==last) && (cl!=laston) ) {
        if ( cnt == 50 ){
            on = cl;
            laston = cl;
        } else {
            cnt++;
        }
    } else {
        cnt = 0;
    }
    
    last = cl;
    
    switch ( on ) {
        
        case 4:
            setMotorSpeed(lm,0);
            setMotorSpeed(rm,0);
            int temp = roomptr;
            for ( ; roomptr < MAX; roomptr++ ) {
                if ( roomlist[temp].rbi != roomlist[roomptr].rbi ) {
                    break;
                }
            }
            sleep(500);
            on = -1;
            break;
        
        case 3:
            setMotorSpeed(lm,0);
            setMotorSpeed(rm,0);
            roomcnt++;
            sleep(500);
            on = -1;
            break;
        
        case 5:
            setMotorSpeed(lm,0);
            setMotorSpeed(rm,0);
            sleep(2000);
            on = -1;
            roomptr += roomcnt;
            sleep(500);
            for ( int i = 0; i < roomlist[roomptr].ri+1; i++ ) {
                playSoundFile("Dog bark 2")
                sleep(750);
            }
            bt = False;
            roomcnt = 0;
            break;
    }

    error = getColorReflected(c1) - getColorReflected(c3);
    sum = sum + error;
    diff = error - last_error;
    setMotorSpeed(lm, v + (error*kp + sum*ki + diff*kd));
    setMotorSpeed(rm, v - (error*kp + sum*ki + diff*kd));
    last_error = error;

}

turn();

while ( !bt ) {

    cl = getColorName(c2);

    if ( (cl==last) && (cl!=laston) ) {
        if( cnt == 170 ){
            on = cl;
            laston = cl;
        } else {
            cnt++;
        }
    } else {
        cnt = 0;
    }

    last = cl;
    
    switch ( on ) {
        case 5:
            bt = True;
            break;
    }

    error = getColorReflected(c1) - getColorReflected(c3);
    sum = sum + error;
    diff = error - last_error;
    setMotorSpeed(lm, v + (error*kp + sum*ki + diff*kd));
    setMotorSpeed(rm, v - (error*kp + sum*ki + diff*kd));
    last_error = error;
}

turn();

```

# Task #2 - Color Sensing

```c++

if ( (cl==last) && (cl!=laston) ) {
    if ( cnt == 50 ) {
        on = cl;
        laston = cl;
    } else {
        cnt++;
    }
} else {
    cnt = 0;
}

last = cl;

```

# Task #3 - Signal System

```c++

switch ( on ) {
    
    case 4:
        setMotorSpeed(lm,0);
        setMotorSpeed(rm,0);
        int temp = roomptr;
        for( ; roomptr < MAX; roomptr++ ) {
            if ( roomlist[temp].rbi != roomlist[roomptr].rbi ) {
                break;
            }
        }
        sleep(500);
        on = -1;
        break;
    
    case 3:
        setMotorSpeed(lm,0);
        setMotorSpeed(rm,0);
        roomcnt++;
        sleep(500);
        on = -1;
        break;
    
    case 5:
        setMotorSpeed(lm,0);
        setMotorSpeed(rm,0);
        sleep(2000);
        on = -1;
        roomptr += roomcnt;
        sleep(500);
        for ( int i = 0; i < roomlist[roomptr].ri+1; i++ ) {
            playSoundFile("Dog bark 2")
            sleep(750);
        }
        bt = False;
        roomcnt = 0;
        break;
}

```

# Original Full Code

```c++

#pragma config(Sensor, S1,     c1,             sensorEV3_Color)
#pragma config(Sensor, S2,     c2,             sensorEV3_Color, modeEV3Color_Color)
#pragma config(Sensor, S3,     c3,             sensorEV3_Color)
#pragma config(Motor,  motorB,          lm,            tmotorEV3_Large, PIDControl, encoder)
#pragma config(Motor,  motorC,          rm,            tmotorEV3_Large, PIDControl, encoder)
#define MAX 9

typedef struct rtype{
   int ri;
   int rbi;
}rtype;


rtype roomlist[MAX];

void turn(){
   setmotorspeed(lm,25);
   setmotorspeed(rm,-25);
   sleep(1450);
}


task main(){
    int v = 30, error = 0, sum = 0, diff = 0, last_error = 0;
    float kp = 0.8, kd = 200, ki = kp*kp/(4*kd);
    int cl;
    int last = -1;
    int on = 0;
    int laston = 0;
    int cnt = 0;
    int roomcnt = 0;
    int roomptr = 0;
    bool bt = True;
    for(int i = 0; i < MAX; i++){
       roomlist[i].ri = i;
   }
   roomlist[0].rbi=1;
   roomlist[1].rbi=1;
   roomlist[2].rbi=3;
   roomlist[3].rbi=3;
   roomlist[4].rbi=5;
   roomlist[5].rbi=6;
   roomlist[6].rbi=6;
   roomlist[7].rbi=7;
   roomlist[8].rbi=9;
   while(bt){
      cl = getColorName(c2);
      if((cl==last)&&(cl!=laston)){
        if(cnt == 50){
          on = cl;
          laston = cl;
        }
        else cnt++;
      }
      else{
        cnt = 0;
      }
      last = cl;
      switch(on){
        case 4:
              setMotorSpeed(lm,0);
            setMotorSpeed(rm,0);
            int temp = roomptr;
            for(;roomptr < MAX; roomptr++){
               if(roomlist[temp].rbi != roomlist[roomptr].rbi) break;
            }
            sleep(500);
            on = -1;
            break;
        case 3:
                  setMotorSpeed(lm,0);
              setMotorSpeed(rm,0);
              roomcnt++;
              sleep(500);
              on = -1;
              break;
        case 5:
           setMotorSpeed(lm,0);
           setMotorSpeed(rm,0);
           sleep(2000);
           on = -1;
           roomptr += roomcnt;
                sleep(500);
           for(int i = 0; i < roomlist[roomptr].ri+1; i++){
             playSoundFile("Dog bark 2")
             sleep(750);
           }
           bt = False;
           roomcnt = 0;
           break;
        }

      error = getColorReflected(c1) - getColorReflected(c3);
      sum = sum + error;
      diff = error - last_error;
      setMotorSpeed(lm, v + (error*kp + sum*ki + diff*kd));
      setMotorSpeed(rm, v - (error*kp + sum*ki + diff*kd));
      last_error = error;
   }

   turn();

   while(!bt){
      cl = getColorName(c2);
      if((cl==last)&&(cl!=laston)){
        if(cnt == 170){
          on = cl;
          laston = cl;
        }
        else cnt++;
      }
      else{
        cnt = 0;
      }
      last = cl;
      switch(on){
        case 5:
           bt = True;
           break;
        }

      error = getColorReflected(c1) - getColorReflected(c3);
      sum = sum + error;
      diff = error - last_error;
      setMotorSpeed(lm, v + (error*kp + sum*ki + diff*kd));
      setMotorSpeed(rm, v - (error*kp + sum*ki + diff*kd));
      last_error = error;
   }
   turn();
}

```


#### Next

> link : <a target="_blank" href="https://team4nz.github.io//posts/2019-12-01/Plans-Presentation.html"> 04. Plans and Presentation