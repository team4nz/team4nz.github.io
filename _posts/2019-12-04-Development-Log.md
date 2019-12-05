---
layout: post
categories: posts
title: 1. Development Log
tags: [dev]
date-string: November 01, 2019
---
<script src="//ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
<script>window.jQuery || document.write('<script src="_/js/libs/jquery-1.9.1.min.js"><\/script>')</script>

# Task #1 - Line Tracing ( PID )

# Task #2 - Color Sensing

# Task #3 - Signal System

# Full Code
```c++
#pragma config(Sensor, S1,     c1,             sensorEV3_Color)
#pragma config(Sensor, S2,     c2,             sensorEV3_Color, modeEV3Color_Color)
#pragma config(Sensor, S3,     c3,             sensorEV3_Color)
#pragma config(Motor,  motorB,          lm,            tmotorEV3_Large, PIDControl, encoder)
#pragma config(Motor,  motorC,          rm,            tmotorEV3_Large, PIDControl, encoder)
#define MAX 9
/*3 = green/+ 4 = yello/select 5 = red 2 = blue/-*/

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
   /*roomlist[0].rbi=1;
   roomlist[1].rbi=1;
   roomlist[2].rbi=0;
   roomlist[3].rbi=3;
   roomlist[4].rbi=3;
   roomlist[5].rbi=5;
   roomlist[6].rbi=6;
   roomlist[7].rbi=6;
   roomlist[8].rbi=7;
   roomlist[9].rbi=9;*/
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


<center>
    <div class="photoset-grid-custom" data-layout="213">
        <img src="/images/intro/manz-intro1.jpg">
    </div>
</center>

 Sit mollis consectetuer tempor in, sociosqu mi in ornare et, placerat in eget ac, praesent pellentesque, mollis est natoque. Quis quis, ac ac pretium sed fusce sollicitudin cursus, magna vitae placerat tincidunt sed dictumst, nullam rutrum pharetra consectetuer. Erat libero odio venenatis, et id ac ultrices convallis, ac iaculis nec vestibulum etiam nec metus, integer velit dictum. Inceptos laoreet at wisi libero dolor, id scelerisque vulputate a amet amet dapibus, at et vitae nec aliquam, fringilla vitae quam. Mauris felis nec sagittis posuere mauris, penatibus ullamcorper, tristique aliquet, vel posuere class placerat. Ornare et non magnis fusce.

<script src="/assets/js/jquery.photoset-grid.js"></script>

<script type="text/javascript">
    $('.photoset-grid-custom').photosetGrid({
    // Set the gutter between columns and rows
    gutter: '5px',
  
    // Wrap the images in links
    highresLinks: true,
  
    // Asign a common rel attribute
    rel: 'print-gallery',

    onInit: function(){},
    
    onComplete: function(){
        // Show the grid after it renders
        $('.photoset-grid-custom').attr('style', '');
    }
});
</script>