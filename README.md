# Functional Tetris

[You can play the newest version from this repo right here on GitHub.](https://xdracam.github.io/functional-tetris/)

The original NES Tetris written in a style that adheres 
to haskell's paradigms as much as possible.

Featuring clear separation of data and program logic, 
all-out immutability, some Monads and a platform independent
thread-safe core logic. All bundled with a simple ScalaJS GUI
for playing in the browser. 

I wrote this as an exercise to get more used to functional 
programming with the cats framework in particular and
with the whole style in general. 

It further helped me get acquainted with frontend web
programming techniques since the UI slightly escalated in v2.0.

### Usage

Just download the html and compiled JS files from one of the 
release folders and open with your browser. There are no ads
and I do not collect any data. In fact, you can just play offline.
The highscore is stored using the browser's local storage. 

From 1.5 onwards, the code uses `img/gameover.png` to signal the
default game over. While it might work without, having the image
available does grant you a slight style bonus.

### Building yourself

Clone the project and treat as a usual ScalaJS project:

    cd path/to/FunctionalTetris
    sbt "~fastOptJS" # recompiles on every source change
    sbt fullOptJS    # for a compressed release version
    
You might have to change the import in the html from `...fastOpt.js` to `...opt.js`.
    
### Can I include this in my webpage?

Sure. The easiest way would be to just embed the 
[live version](https://xdracam.github.io/functional-tetris/)
inside of an `iframe` to use my nice HTML UI.  

If you just want the logic, include one of the JS files found inside the 
release folders inside of a `<script>` tag. Then you 
can use the JS 'API' by passing a proper config object:

    FTetris.startGame({
        mainCanvas: html.Canvas,
        nextTileCanvas: html.Canvas,
        onpointchange: Int => Void,
        onlevelchange: Int => Void,
        onlineclear: Int => Void,
        touchRootNode: [OPT] dom.Node,
        ongameend: [OPT] () => Void,
        onpausestart: [OPT] () => Void,
        onpauseend: [OPT] () => Void,
        simpleRenderingMode: [OPT] () => Boolean,
        guidelineColors: [OPT] () => Boolean,
    }); 
    
Where `mainCanvas` is a reference to the canvas you want the game 
to render in, e.g. `document.getElementByID('myCanvas')`.
The game fits itself into the canvas dimensions, but it 
assumes that the equation `height = 2 * width` holds, for
aesthetic reasons.

The same goes for `nextTileCanvas`, which should provide 
`height = width` in order to properly show the next
spawning tile. 

`touchRootNode` enables the user to specify the dom node 
which receives all touch event handlers. If not specified,
the canvas is used. This should encompass the whole area
which allows touch input, but not the `<body>` tag itself.

`simpleRenderingMode` can be explicitly set to `true` in 
order to enable a less beautiful but far more efficient
rendering mode suitable for poor hardware or alternative 
browsers. It's a function to allow changes during runtime.

`guidelineColors` specifies whether the official guideline
colors should be used instead of my beloved shades of green.
It's a function to allow changes during runtime.

The others are callbacks that either take an `int` - the
updated value - or no arguments and they all return nothing.
The pause callbacks are optional since the canvas has
a built-in pause effect.


### License

Use at your own risk. Tetris is a licensed product owned
by the [Tetris Company](https://tetris.com/).

This project is completely non-commercial and only intended
for educational purposes.

If you plan on using this code somewhere, just include 
a reference to this project or my GitHub account.
   
