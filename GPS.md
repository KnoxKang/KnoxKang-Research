  GPS is a shortened word for "Global positioning system", which is one of GNSS( global navigation satellite system ). 
  
  GPS satelite trasmits mainly on L1, L2 frequency, but some of the latest satelite transmits on L5 as well.
  while L1 is 1575.42MHz, information it contains(C/A code) are only transmitted at 1.023MBPS, equals to 1.023MHz.
  with this slow bit rate, only using this code will result in unsatisfiably low accuracy(around 30m CEP).
  to solve this low accuracy, things like GPS_RTK(https://github.com/KnoxKang/KnoxKang-Research/blob/master/GPS-RTK.md), DGPS(Dual-GPS), PPP(Precision Point Positioning), using multiple bands, etc had emerged.
  in this document, the focus will be on GNSS system with single antenea.
  
  #using multi-bands
    This method can erase ionosphear-error(an error that happens because when GPS signal goes through the ionosphear, the signal can't go straight.) which consists up to 50% of inaccuracy when its the worst.
    method is simple enough. by comparing two or more carrier wave's phase and its pesudo ranges calculated from each signals, state of ionosphear could be caulculated, and error could be removed.
