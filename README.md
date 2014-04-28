#wcat
## cat tool for windows, works for linux as well

I did not know how to print a file to the screen in windows, so I made this familiar command to do it.
This is a module that prints a file's contents, and appends line numbers to each line on the way to process.stdout

## to install

(the -g means you can call this from anywhere on your system)

    npm install -g wcat
    
## to use , pass in a filename as a cmd line argument

    wcat filename.txt
    
## example terminal output

    mark@squirtle:~/wcat$ wcat ./lib/wcat.js
    1	 //wcat.js
    2	 exports.wcat = function(filename){
    3	 
    4	 	if(!filename){
    5	 		console.log("Please supply a filename as a command line argument.");
    6	 		process.exit(0);
    7	 	}
    8	 
    9	 	var fs = require("fs");
    10	 	var through = require("through");
    11	 	var split = require("split");
    12	 	var lineNum = 0;
    13	 	var prependLineWithNumber = function(buf){
    14	 		lineNum++;
    15	 		this.queue( lineNum + "\t " + buf.toString() + "\n");
    16	 	}
    17	 	var readable = fs.createReadStream(filename)
    18	 		.pipe(split())
    19	 		.pipe(through(prependLineWithNumber))
    20	 		.pipe(process.stdout);
    21	 
    22	 }

