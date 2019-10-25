#include <kipr/botball.h>
int l_motor = 0; 
int r_motor = 3;
int forward = -15;
int backward = 35;
int infared = 5;
int range_front = 1;
int infared_spot = 2000;
int f_average = 2910;
int v_speed = -95;
int servo = 2;
int l_wave = 1400;
int r_wave = 700;
int pause = 750;
int reset = 1030;
int main()
{
    find_line();
    printf("found line/n");
	find_wall();
    printf("found wall/n");
    wave();
    printf("hello/n");
    return 0;
}
void forwards(){
    motor(l_motor,forward);
    motor(r_motor,forward);
}
void l_veer(){
    motor(l_motor,v_speed);
}
void r_veer(){
    motor(r_motor,v_speed);
}
void find_line(){
    while (analog(infared) < infared_spot){
    forwards();
    }
    ao();
}
void find_wall(){
    while (analog(range_front) <= f_average){
     	forwards();
    if (analog(infared) < infared_spot){
        l_veer();
    }
    if (analog(infared) > infared_spot){
        r_veer();
    }
    ao();
  }
}
void wave(){
    enable_servos();
	set_servo_position(servo,l_wave);
    msleep(pause);
	set_servo_position(servo,r_wave);
    msleep(pause);
    set_servo_position(servo,l_wave);
    msleep(pause);
	set_servo_position(servo,r_wave);
    msleep(pause);
    set_servo_position(servo,l_wave);
    msleep(pause);
	set_servo_position(servo,r_wave);
    msleep(pause);
    set_servo_position(servo,l_wave);
    msleep(pause);
	set_servo_position(servo,r_wave);
    msleep(pause);
    set_servo_position(servo,reset);
    msleep(pause);
	disable_servos();
    ao();
}
