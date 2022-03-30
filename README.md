# OBS_Dump_Button
The goal of this project is to provide instructions on how to setup a nested streaming solution to provide an intentional stream delay to mute live callers or inappropriate content before it gets show to an audience  

# Goal
The goal of this write up is to create a virtual dump solution when streaming to twitch, youtube, etc without purchasing expensive audio equipment.

# Summary
Using MonaTiny RTMP server the user can stream localy to VLC with a delay and upload the stream directly to the streaming platform. With some configuration the switch is seamless and adds very little latency. Your use may vary. 

Write up V1.0 

# Requirements 

Software Required
1. 2 streaming softwares or multiple instances of OBS (I will be showing OBS and stream labs)
2. MonaTiny Server https://www.monaserver.ovh/  https://sourceforge.net/projects/monaserver/files/MonaTiny/
3. VLC - https://www.videolan.org/vlc/download-windows.html
4. Virtual Audio cable - https://vb-audio.com/Cable/

Hardware
1. Decent streaming machines

Optional
1. Windows 10/11 for virtual desktops
2. Multiple monitors

# MonTiny Setup

MonaTiny setup
MonaTiny is a small self-contained streaming server. Your secondary PCs will be streaming to your own private MonaTiny server rather than streaming to Twitch.

Download and unzip MonaTiny on one of your PCs. In my setup, I use the secondary for this; it should only be needed on one system. Note there is no install or configuration process.

Start MonaTiny. Windows will probably prompt you about firewall permissions, allow it. It should pop up a console window which you can mostly ignore. Keep this running for the duration of your stream.
Note: MonaTiny has no authentication mechanism. You'll want to find another option if you don't trust your internal network/firewall setup.

Configure secondary OBS
Perform all of these steps on the secondary PC(s):

Install OBS if it is not already installed.

Edit your settings in OBS (gear icon in the lower left)

Under "Video", ensure Base (Canvas) Resolution and Output (Scaled) Resolution are set to the same value for best quality. If you know exactly how much space will be used on the final output, you change these resolutions to match -- i.e. if you're one vertical half of a 1920x1080 stream, set these to 960x1080

Under "Stream", change "Stream Type" to "Custom Streaming Server"

For URL, use rtmp://127.0.0.1 if the secondary PC is running MonaTiny. Replace 127.0.0.1 with the correct IP address if the primary PC (or some other computer) is running MonaTiny.
For Stream Key, enter a key to identify your stream. Unlike Twitch, this is not like a password and does not need to be secret. Don't use your Twitch stream key. You'll want something simple to remember.
If you are using multiple secondary PCs, they need different keys.
For the rest of this guide, I assume your key is key.

Click Done to finish editing settings.

Build a scene in OBS.
This only needs to capture whatever window(s) and other devices (cameras?) you want to share.
Adding pretty background effects and other things is unneccessary and only adds to how much bandwidth you need between the primary and secondary PCs. Do all that on the primary PC instead and just use a plain black background (or another solid color)
Click "Go Live"
If you look at the MonaTiny console window, there should be a message that says something like
MonaTiny.cpp[157] Client publish key, where key is the stream key you chose earlier.
Testing
Open VLC on whichever system MonaTiny is on.

Choose Media -> Open Network String.

For the network URL, use rtmp://127.0.0.1/key/key. Replace both copies of key with the stream key you chose earlier

Yes, the URL begins with rtmp not rtfmp here.
Yes, the stream key is in the URL twice.
Choose Play. You should see your secondary PC's stream.

If MonaTiny isn't on the primary PC, repeat this test there -- replacing 127.0.0.1 with the secondary PC's IP address.

# VLC setup

VLC will need a few settings changed 

1. Browse to Tools -> Prefrences -> Output -> OpenGL video output //this allows streaming to OBS 
2. Browse to Tools -> Prefrences -> subtitles/OSD -> Disable OSD //Remove play/pause/mute from the screen
3.  Browse to Tools -> Prefrences -> Hotkeys -> mute -> under global setting enter a global key (f12 or anything you want NOTE global key make the key unuseable while VLC is open). //set a custom mute button globally
4.  Place VLC in a virtual window using win+tab and creating a new desktop, VLC when minimzed stops working. 

# Stream setup
1. open your other first streaming software. This is the main software which has all you scense and 
2. Set your delay to a custom amount (this is how much time you have to stop profanity)
3. Start your stream uploading to MonaRTMP server
4. Launch VLC and stream you video to VLC
5. Launch you seconds OBS instance and take VLC as an input
6. Stream away! press your mute key when bad stuff happens and wait until it catches up to the live stream!


