# Day 1 — Linux

## Commands I learned
- pwd — shows where I am
- ls — shows files
- cd — moves between folders
- cat — reads a file
- mkdir - creates a directory/folder
- touch - creates an empty file
- find — finds files
- grep — searches for text
- cp - copies something
- mv - moves or renames files
- rm - removes or deletes something (should be cautious with it because Linux doesn't have a recycle bin)
I reviewed most of them and also created flashcards for them. e.g 
  & -- Runs the command, but does not wait for it to finish before you can do anything else. The command runs in the background and is helpful for commands that might take a while to complete, or ones that you want to keep running
  && -- Runs both commands, but waits for the first command to finish first, before the next. Like a set of dominoes.
  > -- Used to redirect output. We can take a command's output and send it to a file. This operator will overwrite anything that exists in the file.
  >> -- This redirector does the same thing, but instead of overwriting, it appends the output to the bottom of the file.
Also learned about permissions
  - r read
  - w write
  - x  execute
and modes to set,
- chmod -- change the permissions mode
- chown -- change onwership

## TryHackMe

Completed Linux Fundamentals Part 1.
Also completed the trotorail room and vpnopen room

## OverTheWire Bandit

Reached Level 5-6

## What confused me
Did every level easily, but I got stuck on level 4 because it uses the word human-readable file, just a word confusion. Otherwise, I did very well

## What I learned
In level 1, I learned that the files can be executed by ./.
In level 2, I had to use "" if the file has spaces in its name
Level 3 was simple, and in level 4, I learned that the human-readable files have the word ' text ' in them
In level 5, I learned to use the command find
