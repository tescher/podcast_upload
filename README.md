Podcast Upload
=============

This is a bash script that automates upload of podcast mp3 posts to your WordPress site. It assumes the WordPress add-on mp3-to-post is
installed and will take files from the wp-content/uploads/mp3-to-post directory and actually make posts out of them.

Setup
=====

The following environment variables should be set up:
* PU_FTP_SERVER - The FTP location for your WordPress server (NOTE: "scp" will actually be used for the copying, so a scp certificate relationship needs to be set up)
* PU_FTP_USER - Your FTP user login
* PU_FTP_DIR - Where to put the files, e.g. html/wp-content/uploads/mp3-to-post
* PU_LOCALDIR - The parent direcotry for the local files to send. 
* PU_MID3_PATH - This script uses the mid3v2 mp3 modification program. This is where to find that program.
* PU_TEMP_DIR - Local temporary directory where files can be copied and modified
* PU_PODCAST_GENRE_DEFAULT - The default genre to use if there is none in the data file for a podcast. This becomes the category for the Wordpress post
* PU_MARKER_COMMENT - The comment added to the mp3 file that marks it as having been uploaded
* PU_PODCAST_DATA_FILE - The file that lists the podcasts you want to uploaded, Default is podcast_data.txt
* PU_START_AFTER_DATE - Date after which to start sending files. Files before this date are ignored. YYYY-MM-DD format

Podcast Data
============
The file specified in PU_PODCAST_DATA_FILE is a text file with a line for each show formatted as follows:

local_subdirectory|show_title|description|genre

* local_subdirectory is the directory on your local machine where files should be found for that podcast
* show_title is the title of the podcast. It will be used in the WordPress post title
* description is the podcast description. It will be the post content
* genre is turned into the post category on WordPress

Mid3v2 Setup
==========
Get it here: https://mutagen.readthedocs.io/en/latest/

WordPress Setup
===============
Install the mp3-to-post plugin. Unfortunately it has a bug in it that needs fixing after you add it.

In WordPress Admin, go to Plugins, find Mp3 to Post, and click Edit.

On the right side of the screen under Plugin Files, find mp3-to-post/getid3/getid3.lib.php and open it. Copy all the code and put into a different editor like Notepad++.

Find line 282 (a "break" command) and comment it out by putting two forward slashes in front of it, like this:

      //break;
      
Copy all the code and replace it back into the file in WordPress and click Update File to save it.

Podcast Setup
=============
How to hook the resulting Wordpress feed to podcast directories (like iTunes) is outside the scope of this document (because it is constantly evolving), but you can start here:

https://codex.wordpress.org/WordPress_Feeds
https://codex.wordpress.org/Using_FeedBurner

