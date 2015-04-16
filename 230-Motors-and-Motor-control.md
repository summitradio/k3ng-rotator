The rotor software accommodates several different motor types each requiring unique interface 
hardware depending on motor type. Capacitor run single phase AC (typical CDE rotor), permanent 
magnet DC (has brushes), synchronous AC motor and stepping motors. The motor controller must be 
selected to match the motor type. For a PMDC motor either relays or a dual half-bridge PWM controller 
(search ebay for BTS7960) is suitable. For Capacitor run single phase AC relays are usual. With relays 
you need a separate speed controller if speed control is desired. With a typical electronic motor control 
PWM speed control is built in. The controller has variable frequency outputs suitable for driving a 
synchronous AC motor but for a driver you are on your own. Step motors are typically 2/4 phase and 
require suitable micro stepping driver such as the DIV268N (search ebay) 

In the K3NG rotor controller all motors are operated in a simple servo loop with the motor speed and 
stopping point determined by feedback from a positioning device. This is usual in all the above cases 
with the exception of step motors. In the K3NG application the step motor us used as a brushless DC 
motor (BLDC) which has maximum torque at zero RPM (stall). Most DC motors that have PWM speed 
control have near zero torque at very low motor RPM.
