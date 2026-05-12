================================================================
  Thermodynamic Resonance
  
  A Max for Live Instrument
================================================================
 
OVERVIEW
--------
Thermodynamic Resonance is a Max for Live instrument in which
nitrogen (N2), oxygen (O2), and carbon dioxide (CO2) molecules
move freely inside a cubic space, producing sound each time they
collide with the walls or with one another.
 
Temperature is the sole parameter that drives everything —
the motion of molecules, the state of matter, and the resulting
sound. Inspired by thermodynamics, this instrument attempts to
translate physical phenomena into musical expression.
 
 
REQUIREMENTS
------------
- Ableton Live 11 or later
- Max for Live 8.6 or later (Max 9 recommended)
 
 
INSTALLATION
------------
1. Place the entire "ThermodynamicResonance" folder in your
   Ableton User Library or any location of your choice.
 
2. In Ableton Live, drag "ThermodynamicResonance.amxd" onto
   a MIDI track.
 
3. Press the power button on the device to initialize.
 
 
HOW IT WORKS
------------
Molecules
  - N2 (Nitrogen)  : 39 molecules / Blue  / 1760 Hz
  - O2 (Oxygen)    : 10 molecules / Red   / 1540 Hz
  - CO2            :  1 molecule  / Yellow/ 1120 Hz
 
  The total of 50 molecules reflects the approximate composition
  of air (N2: 78%, O2: 21%, CO2: 1%).
 
  Pitch is derived from molecular weight using the formula:
    f = 440 x (M_N2 / M_x) x 4
 
Sound Generation
  Sound is produced using [mc.cycle~] and [mc.adsr~ 5 1.54 0. 308],
  creating a percussive, popping texture. The strength of each
  collision (impulse) is applied to the velocity of the note.
 
Physics
  - Gravity    : None (in gas state)
  - Restitution: 1.0 (perfect elastic collision)
  - Friction   : 0.0
  - Force is applied every frame, proportional to temperature,
    causing molecules to move as if they have their own will.
  - Damping 0.1 is applied to prevent chaotic motion from force.
  - At 0K, damping becomes 1.0 and all molecules come to rest.
 
 
STATE OF MATTER
---------------
As temperature decreases, molecules undergo phase transitions,
and the physics parameters change accordingly.
 
  N2  : Gas above 77K / Liquid 63-77K  / Solid below 63K
  O2  : Gas above 90K / Liquid 54-90K  / Solid below 54K
  CO2 : Gas above 194K                 / Solid below 194K
        (No liquid state at 1 atm — sublimates directly)
 
  Gas State   : gravity OFF / damping 0.1 0.1 / restitution 1.0
  Liquid & Solid State : gravity ON / damping 0. 0. / restitution 0.0
 
  When molecules enter liquid or solid state, gravity pulls them
  downward. At low temperatures, molecules that have settled on
  the floor continue to vibrate slightly — an unintentional but
  physically accurate representation of thermal vibration.
 
 
UI GUIDE
--------
Temperature Slider
  - Range  : 0K to 1000K
  - A lag is applied to prevent abrupt transitions.
  - Celsius (°C) and Fahrenheit (°F) are displayed simultaneously.
 
Meters (Blue / Red / Yellow)
  - Correspond to N2 / O2 / CO2 respectively.
  - Show the velocity and number of molecules sounding
    at any given moment.
 
Visualization
  - The right panel shows molecules moving in real time.
  - Pink lines appear at the moment of collision.
  - Each molecule type has a different sphere size and mass.
  - Press [▲ Open] to open a larger window.
  - Press [▼ Close] to close it.
 
 
TECHNICAL NOTES
---------------
Collision Detection
  Collision data is retrieved from [jit.world] dumpout via
  [route collisions] → [dict]. Each collision pair contains
  body1, body2, impulse, duration, and contact information
  in dictionary format.
 
  A key challenge was that most impulse values were reported
  as 0.0, even during actual collisions. This occurs because
  Bullet Physics reports impulse only at the instant of impact,
  while all subsequent frames output 0. The solution was to use
  the right outlet of [select 0], which passes only non-zero
  values — filtering out the noise and capturing only genuine
  collision impulses.
 
  Impulse values are passed through a quadratic curve
  (x squared) before being applied to amplitude, in order to
  suppress the noise caused by thermal vibration at low
  temperatures while preserving the loudness of strong
  collisions.
 
Panning
  The x-coordinate of each molecule group is continuously
  retrieved from [jit.phys.multiple] outlet 0 and used
  to control stereo panning.
 
 
KNOWN LIMITATIONS
-----------------
- The physics simulation is not a perfect representation of
  real thermodynamic behavior. It is an artistic interpretation.
- At very low temperatures, thermal vibration may produce
  dense, high-frequency collisions that result in noisy output.
  This is partially mitigated by the quadratic amplitude curve.
- Adding reverb is recommended for a more polished sound.
 
 
CREDITS
-------
Created by Vanadi(1void_)
Created with Max 9 / Max for Live
Physics engine: Bullet Physics via jit.phys.world
Inspired by thermodynamics and the kinetic theory of gases.
 
 
LICENSE
-------
Free to use and modify for personal and educational purposes.
Please credit the author if shared or performed publicly.
 
================================================================
  "At absolute zero, there is no sound.
   Turn up the temperature, and the universe begins to sing."
================================================================
