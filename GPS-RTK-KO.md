# KnoxKang-Research

## Basic principal of GPS-RTK. 

  RTK(Real Time Kinematic) is a technology to enhance acurracy of GNSS system.
  It uses measurements of the phase of GPS signal's carrier wave, not the informational content of the signal.
  Theoretically, accuracy of RTK system could reach 2mm.
  
## Why is technology like GPS-RTK needed?

  Because with conventional way, locating accuracy can only be around 3m('civialian' code) to 30cm('military' code).

## How does independant GPS-RTK work?
  
  GPS-RTK works based on Carrier-wave-tracking. This method uses carrier wave unlikly to DGPS(Dual GPS) to calculate distance between at least 5(one for spare) satalites and the point where the user is. 
  
  Although RTK system has a same problem as with carrier wave tracking([integer ambiguity](https://github.com/KnoxKang/KnoxKang-Research/blob/master/GPS-RTK.md#q2-what-is-integer-ambiguity)), RTK solves this problem within about 10 seconds if all conditions(no multi-path, large number of satalites available, receviers are multi-frequncy, etc..) are optimal.
  
  Standard RTK system is composed of two GPS recevers, one for 'base'(which stays stationary) purpose, and one for 'rover'(which moves around) purpose.
  
  With two recivers, one of them will work as a 'base station', which stays in a predefined static location while the other receiver works as a 'rover', which retrives correction data from the base station to define where the rover is.
  
  Since RTK needs at least 2.4kbps updated in about every half a second, good network quality is necessary for a accurate locating.
  
  If the base location is not predefined, once the base is in a static place and powered, the base will start calculating its own coordinate with method called PPP(Precise Point Positioning), and start to 'stabilize' its location.
  
  If condidion is optimal, after about 3~5 minutes, PPP calculation will be done, and rover will be able to loacte it self correctly.


  
## How does GPS-RTK with NTRIP(which is Network Tranport of RTCM)?

  In this case user don't need a base to start a RTK system, so, minimal requirement is reduced to a single RTK-able GPS reciver attached to a internet accesable device.
  
  Procedure to use NTRIP is actually very easy, user only need to know, or register ID/PW to any NTRIP caster, and type that information in to the rover.
  
  If the rover has a correct information, rover will connect through network device to NTRIP caster to retrive list of connection points and let user to choose one, or just choose what's the closest based on roughly estimated position of it self.
  
  
  
## Q&A

### Q1. why does NTRIP require users ID/PW to 'listen' to their broadcast?
A1. it is not NTRIP protocol that requires ID/PW. it is required when connecting to NTRIP caster(which controls data flow from multiple base stations to multiple rovers)

### Q2. what is 'integer ambiguity'?
A2. it means that carrier wave's ambiguity is always integer. reason for this is when GPS reciver is mesuring distance between the satalite and the antenea, it uses NCO(numerically controlled oscillator)to generate a signal with same frequency and phase to the incoming signal. However, becuase of inablilty of NCO to recognize between one carrier wave cycle and the other, signal generated from NCO converges to the nearest cycle. This makes the ambiguity of carrier wave always integer, thus remains as a potential error.

