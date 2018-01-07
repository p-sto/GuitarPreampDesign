Guitar Jazz Preamp
==================

Repo contains schematic and description of guitar Jazz preamp which I have been working on for some time. I really enjoy
playing guitar and electronics has always been my greatest interest among engineering, especially - guitar and audio amplifiers.
Working on this design I was mostly inspired by:

1. Polytone Mini Brute `schematic <http://www.murchmusic.com/Polytone%20Info/Schem1.JPG>`_
2. Fender Jazz King `schematic <http://www.nodevice.com/manual/jazz-king/get126263.html>`_
3. Music Man's HD series (hybrid amplifiers from 80s) `schematic <http://drtube.com/schematics/musicman/gb2.gif>`_

My plan is to build whole amplifier though I still have not decided what kind of power amplifier should I choose.
Two possibilities are:

1. Class D power stage
2. Class AB tube stage (2xEL84 since I've got a bunch of them)

First option would be cheaper and weights less. Also whole power stage could be acquired easily since there are doznes
of kits or assembled units on ebay (I'm too lazy to design it by myself, though - class D is an interesting example of engineering).
Second option would be definitely a bit uncommon (refer to Music Man's amp) and that's why it's worth trying it.

Design goals and considerations
-------------------------------

.. image:: https://raw.githubusercontent.com/stovorov/GuitarPreampDesign/master/docs/schematic.png

My goal was to design fairly simple preamp with equaliser incorporated in gain stage feedback circuit. EQ is based
on classic Baxandall approach which delivers flat frequency response with knobs in center position and up to 10dB boost/scope
for particular frequency range. ``BASS`` and ``MIDDLE`` controls uses op-amp based gyrators to fake inductance circuit. This allow
creating band pass/stop filtering. ``TREBLE`` works as a simple first order cut/boost filter. To extend ability of tone shaping,
`PRESENCE <https://www.teachmeaudio.com/mixing/techniques/audio-spectrum/>`_ control was added. Circuit uses ``Twin-T`` filter in negative feedback with center frequency set around 5.5k Hz.
Additional capacitor (C28) was added to impact frequencies ranges exceeding Twin T filter range - it works as additional
high frequencies cutoff - good for getting rid of unpleasant higher order harmonics.
Reverb circuit is an improved Polytone's circuit driving 600 ohm reverb tank from Accutronics (``4eb3c1b`` model).
In presented schematic ``phase inverter`` circuit was added after ``VOLUME`` potentiometer (added as a fixed resistor) to
provide 180 degree phase shift for driving AB class tube power stage. For class D amplifier such circuit is not needed.

Tools
~~~~~

Preamp was designed using LTSpice.

Simulations
-----------

Transistor models where downloaded from Bob Cordell's `site <http://www.cordellaudio.com/book/spice_models.shtml>`_

Transient
~~~~~~~~~

.. image:: https://raw.githubusercontent.com/stovorov/GuitarPreampDesign/master/docs/tran_1khz.png

AC
~~

Frequency response for flat settings:

.. image:: https://raw.githubusercontent.com/stovorov/GuitarPreampDesign/master/docs/ac_sim.png

Observed ripple at around 5.5kHz is due to ``PRESENCE`` control:

.. image:: https://raw.githubusercontent.com/stovorov/GuitarPreampDesign/master/docs/presence_circuit.png

The same circuit without 470p cap:

.. image:: https://raw.githubusercontent.com/stovorov/GuitarPreampDesign/master/docs/presence_no_cap.png

Achieved THD (normalised) is at the level of 0.47% - however, ideal op-amps models where used. On the other hand,
this circuit is not intended to be hi-fi preamp and it's more than enough for guitar applications.
