Reformatting for github is ongoing.

Please refer to the original document:
https://docs.google.com/document/d/1LdyXb5AyqV8_A_CFeOp9DE0SkhXPEn3VPQhPJVOdUv0/edit?usp=sharing

# Teamdrive/Service Account setup for Cloudbox:

NOTE: This is the work of a random cloudbox user, not one of the core dev team.  This setup works for me, though.

So, you want to add a teamdrive to your cloudbox setup and configure cloudplow to upload to that teamdrive?  And you’re interested in doing this so you can circumvent Google’s 750Gb daily upload limit?

Here’s a description of how I configured cloudbox to do that.  There’s an outline, and then a detailed section with screenshots and more detail on exactly WHY I’m asking you to do this and that.

PLEASE, READ THROUGH THIS ENTIRE THING BEFORE YOU DO ANYTHING. That way you’ll have a handle on what things you’ll need from earlier steps and the later steps may influence your decisions about earlier steps.  Also, it’s always better to clear up questions before you’re in the middle of it.

This document is written as if you are adding a single teamdrive.  There are some notes herein describing what parts need to be repeated for multiple teamdrives.

### Outline:
1.  Create service accounts
    
    - Typically, the reason for doing this is to get around the 750Gb upload limit, so you’ll probably want to create more than one.
    
    - Save the JSON for the service accounts somewhere that cloudplow will be able to see them.  For the examples below, I will assume you put them in: `/opt/sa-json`
    
1.  Create a new OAuth user for use with this teamdrive
    
    - Use the same method as you did initially for Cloudbox
    
    - Maybe not strictly necessary, but they are free so why not?
    
    - Helps avoid API bans
    
    - You will use the Client ID and Secret for rclone later.

1. Create the Teamdrive
    - Chances are you want the file structure here to match the cloudbox-related portion of My Drive, since you probably want this stuff to just show up in Plex automagically without adding new folders to your library configs.  i.e.:
      `/Media/Movies`
      `/Media/TV`
      and so forth...
    - I added a folder to the root of each teamdrive so I can tell at a glance if the teamdrive has been successfully merged into the mergerfs at /mnt/unionfs, for example:
      `/TD-Teamdrive`

1. Share the teamdrive with the service accounts using their email address
    - I gave all the service accounts “Manager” privileges, since they will be used in very limited circumstances all entirely under my control and I figure why not give them *All The Privs* so they can do whatever they may need to do behind the scenes.
    - If you have a lot of service accounts [I have 100], you may wish to create a Google Group, add all the service account emails to the Google Group, then share the teamdrive with the group’s email address.

1. Create an rclone remote for the teamdrive.
    - Enter the clientID and secret from the user you created above.
    - Go through the rclone setup just the same as you did for the original rclone remote you created for Cloudbox.
    - After authorizing, you’ll be asked if you want to set this drive up as a teamdrive.  Answer “yes”; you’ll be shown a list of teamdrives from which to choose.
    - You will need the name of this remote when you set up the rclone_vfs mount.
    - In the examples below, I will assume you called it “teamdrive”.
    - _I STRONGLY SUGGEST that you make this name all lower case with no spaces and use it from now on throughout this setup wherever you refer to this teamdrive.  Something like “teamdrive-books”, “teamdrive-shared-movies”, etc._
