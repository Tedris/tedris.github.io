---
layout: post
date: '2017-03-12 09:21:53'
title: Open Source
---

As much as I would like to make some extra money off this project, I feel like I could really give something back to the community.  I've been meaning to join projects and start fixing stuff, but I felt like I could get at least some learning in trying a small project on my own first.

As of now I'm trying to keep it simple with Javascript.  Definitely not thinking about using any frameworks, I may want to try and make the app reactive at some point, and maybe see if I can make it work on mobile, but right now I have code that pretty much uses electron for file input/output.

May make code to change that, but for now this is how I have it:

```
const electron = require('electron');
var dialog = electron.remote.dialog;
var fs = require('fs');
var character = {};

function loadCharacter() {
    dialog.showOpenDialog(function(fileNames) {
        if (fileNames === undefined) {
            console.log("Select a file");
        } else {
            readFile(fileNames[0]);
        }
    });
}

function readFile(path) {
    fs.readFile(path, 'utf-8', function(err, data) {
        if (err) {
            console.log("File read failed: " + err.message);
            return;
        }

        saveToCharacterObject(data);
        console.log(character);
    });
}

function saveToCharacterObject(data) {
    character = JSON.parse(data);
}
```

Pretty much got that from a tutorial, but it works.  Also for the save files I'm using JSON.  Yes that means that people can read that easily, I kind of want people to write their own things that reads the data.  If people want to edit, then fine, whatever, this isn't a multiplayer game.

If I do make something multiplayer, I will need to make some kind of save auditing, since I know I can't stop people from editing files or editing what they're sending to a server.  For now I'll keep it simple.