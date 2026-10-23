# CanSat for the UK CanSat Competition 2026-27
## Overview 
### This is TKA's Orbital's programming repository
Which may or may not be submitted alongside the PDR, CDR, FDR I don't know as it has our names tied to it which is a big nono in the rules soooo.  
I decided to evaporate the other repo and only have one as i made two without understanding both github and how development would work on the pi pico. As of now the repo is very bare bones as we have not finalised the core language yet and everything depends on that. So for that reason I have left it intentionally ambiguous as to fit any structure and will work on the Docs as the hardware is somewhat finalised.  

repo layout: (some folders are not included yet because I am a clown but they are written down here)  
cansat/  
├── flight/            # code that runs on the CanSat Pico  
│   ├── code.py  
│   └── lib/           # contains the libraries for the modules  
├── ground_station/    # code for the receiving Pico and GUI  
├── tests/             # scripts that test one module each  
├── docs/              # wiring diagram, pin table, PDR notes  
└── README.md        
## Part list
The part list can be found [here](https://docs.google.com/spreadsheets/d/1fmi5YQzSYtQBcR9bM0utwFKDUaHqM_v9Lo2z1Qys7S8/edit?gid=943090944#gid=943090944)  
The pin out for everything is detailed in its own file [wiring.md](docs/wiring.md)

I'm just as new to github as anyone else is (probably) so just as I am doing can others attempt to learn how to use it as this will be a large boost to productivity in the future. 
