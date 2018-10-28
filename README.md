
Retro Audiophile Design distrubutes a specialized playback software running on Debian Jessie operating system (Linux) and configured for Raspberry Pi 3 and Pi-DigiAMP+. The software is free open source licensed under GNU General Public License version 3.

The software is a modified redistribution of the Raspberry Pi Audio Linux distribution developed by the Volumio 2 project. It is an open source software and licensed under Gnu General Public License version 3. Volumio is a registered trademark of INTUITU di Michelangelo Guarise.

The Github depository for Volumiuo2 can be found here: https://github.com/volumio/Volumio2

Modified files are kept in this depository.

=======================
RETRO AUDIOPHILE DESIGNS 		Patch specification	2018-08-26
Volumio 2.444 Patch Revision A

Fixes
1. first fix – install Balbuze’s Volspotconnect2 dev version 
Download and install the plugin, go to:
 https://github.com/balbuze/volumio-plugins/tree/master/plugins/music_service/volspotconnect2

Type the following commands to download and install plugin), done in Putty:
wget https://github.com/balbuze/volumio-plugins/raw/master/plugins/music_service/volspotconnect2/volspotconnect2.zip
mkdir ./volspotconnect2
miniunzip volspotconnect2.zip -d ./volspotconnect2
cd ./volspotconnect2
volumio plugin install

2. second fix – playlist is added to Queue and Played (Play-option in menu)
Changes made in source code file: Volumio/app/playlistManager.js. If Play is chosen for a playlist it is now added to the Queue instead of being cleared and the first track in the newly added list is played.
In method PlaylistManager.prototype.commonPlayPlaylist.

The code when the Queue is emptied by mistake is now a comment. 
/*Retro Audiophile Design modification: …*/

Introduce new variable indexToBePlayed to hold next index. Key code statement let indexToBePlayed = self.commandRouter.volumioGetQueue().length;   this is the thing that sets current position to the first added track, the position where the list is added. Index is used in the call of self.commandRouter.volumioPlay(indexToBePlayed);

Comments added:
/*Retro Audiophile Design modification: cannot clear queue as above */
/* Retro Audiophile Designs modification: Play the first track in the ADDED list. Index is then the length of the queue before adding.*/
