## 1.
Gulp is a javascript task runner (that can be used as a build system) that will automate and enhance your workflow.
Gulp provides some streams and a basic task system.

## 2.
Gulp is written in Javascript, and is used mainly by front-end engineers, so it needs to be super easy to start with.
Gulp uses node.js streams.
Streams come to us from the earliest days of UNIX and have proven themselves over the decades as a dependable way to compose large systems out of small components that do one thing well. The output of one program is piped to the input of another.
Using node best practices and maintaining a minimal API surface, your build works exactly as you would imagine and by enforcing strict plugin guidelines, plugins stay simple and work as expected.

## 3.
At the beginning you have to create a "gulpfile" in your root directory. Here's an example.
This simple task will get all Javascript files inside scripts directory.
Then these files are piped to the jshint to check the javascript syntax.
After that we concat all the files into one single file, so the stream contains only this one file.
To this single file we pipe uglify to minify it, and after that the file is finally written to disc.
As you can see, there was no interaction with file system between any of those plugins.

## 4.
In classic build systems like grunt the workflow is like this.
You have to write to disk after every step that some plugin makes, due to bad flow control.
This is very inefficient and sometimes can result in very long build times, because it writes to disk between every plugin.

## 5.
In Gulp, the build system works the way you expect it to.
Streams are what make gulp so powerful.
The whole build system is just a series of small components piped to each other as you saw in the example.

## 6.
By preferring code over configuration, gulp keeps things simple and makes complex tasks manageable.
Using node.js streams you can pipe one plugin to another, so the plugins can communicate between each other.
You can use any standard node.js library, inside your task, as in the end it's just a function.
By enforcing strict plugin guidelines, plugins stay simple and work as expected. For example, in grunt there are several ways how to get files passed to your plugin, in gulp there's always just a stream piped in.

## 7.
The lack of plugins might make you think that Grunt is better, when in fact it just needs more plugins to be useful. When you need static web server, you can directly use one; for example, http or express. If you need live-reload, you can directly use the live-reload module. In grunt you would need plugins for all of these.
All plugins should do only one thing. The guidelines are quite strict. Every plugin needs to have a tests, so all available plugins are quite high quality. Not tests and your plugin will get blacklisted.
Making tests is very easy as simple plugins don’t need even fixtures. You can just simulate a file in a stream, and you can use any testing framework like mocha.

## 8.
Node.js streams might take little bit longer to get familiar with, but documentation is very good.
Tasks running in maximal concurrency can sometimes be a disadvantage. There is good dependency system, where you can specify that one task is dependant on another (and it will wait for that task to finish) but in real life this isn't always possible.
Mainly because a task has to return a stream, promise or call a callback so that gulp will know when it has ended, but if your task contains more than one stream, you can’t do it as you don’t know which one to return.

## 9.
This is the simple example of gulp task that will generate the sprites.
This task dynamically checks all the folders in the assets directory, and generates the sprites for the images (grouped by folder).

## 10.
So we have a sprite for features, a sprite for icons ...
The 2x folder contains the same icons but in double size for retina displays.
Every time we have some new image to add to sprite, we just need to place it in corresponding folder, regenerate sprites and its ready to use.

## 11.
The Mustache files are just templates for generating the final css file, so we can have the structure that suits us.
This is big advantage when compared with other sprites libraries like compass, as we can very easilly automate retina sprites without any manual work.
2x mustache contains the same code as regular one, just wrapped in retina media query.

## 12.
As you can see there, the spritesmith library returns two streams, one for image and one for css.
The css is directly output into assets, but for the image we also pipe it through imagemin so our sprite is also minified before we output it.