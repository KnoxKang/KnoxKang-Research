# KnoxKang-Research

Basic principal of GPS-RTK.
  RTK(Real Time Kinematic) is a technology to enhance acurracy of GNSS system.
  It uses measurements of the phase of GPS signal's carrier wave, not the informational content of the signal.
  Theoretically, accuracy of RTK system could reach 2mm.
  
Why is technology like GPS-RTK is needed?
  Because with conventional way, loaction accuracy can only be around 3m('civialian' code) to 30cm('military' code).
  
How does GPS-RTK work?
  GPS-RTK works based on Carrier-wave-tracking. This method uses carrier wave unlikly to DGPS(Dual GPS) to calculate distance between at least 5(one for spare) satalites and the point where the user is. 
  Although RTK system has a same problem as with carrier wave tracking(integer ambiguity), RTK solves this problem within about 10 seconds if all conditions(no multi-path, large number of satalites available, receviers are multi-frequncy, etc..) are optimal.
  Standard RTK system is composed of two GPS recevers, one for 'base'(which stays stationary) purpose, and one for 'rover'(which moves around) purpose. 
  Since RTK needs at least 2.4kbps updated in about every half a second, good network quality is necessary for a accurate locating.
  
  
  
Q1. why does NTRIP require users ID/PW to 'listen' to their broadcast?
A1. it is not NTRIP protocol that requires ID/PW. it is required when connecting to NTRIP caster(which controls data flow from multiple base stations to multiple rovers)
