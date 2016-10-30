<div class="contents">

<div class="header">

<div id="label">SuperCollider CLASSES (extension)</div>

<div id="categories">[GUI>Views](./../Browse.html#GUI>Views)</div>

# TabbedView2

<div id="summary">A Tabbed View which holds TabbedViewTabs</div>

</div>

<div class="subheader">

<div id="filename">Source: /Users/fuo/Library/Application Support/SuperCollider/downloaded-quarks/TabbedView2/[TabbedView2.sc](file:///Users/fuo/Library/Application Support/SuperCollider/downloaded-quarks/TabbedView2/TabbedView2.sc)</div>

<div id="superclasses">Inherits from: [Object](../Classes/Object.html)</div>

<div id="related">See also: [TabbedViewTab](./../Classes/TabbedViewTab.html), [CompositeView](./../Classes/CompositeView.html)</div>

</div>


## <a class="anchor" name="description">Description</a>

There are extensive explanations in the [Examples](#Examples) section on how to use TabbedView2 with its many configuration options .

### <a class="anchor" name="Version and Author">Version and Author</a>

version: 1.05 , Oct 28, 2016

author: Jost Muxfeldt

### <a class="anchor" name="New Features">New Features</a>

TabbedView2 has a number of new features compared with TabbedView.

*   Tabs are draggable, both for their order and view position.
*   Under QtGUI, tabs can be dragged (using cmd/ctrl-drag) to other TabbedView2s, even between windows.
*   Under QtGUI tabs can be detached.
*   Double-clicking tabs changes their orientation.
*   Tabs can be set to be closable.
*   Tabs are individually configurable, not just globally, though global defaults are settable.
*   Tab states can be automatically archived. See [Auto-Archiving a TabbedView2 State](#Auto-Archiving a TabbedView2 State)

<div class="note"><span class="notelabel">NOTE:</span> Try the [DEMO](#Demo) Code to test all the features, and go through the [EXAMPLES](#Examples).</div>

### <a class="anchor" name="Differences to older TabbedView">Differences to older TabbedView</a>

The new TabbedView2 now holds an Array of TabbedViewTab instances. The creation syntax is just like other Views:

<pre class="code prettyprint lang-sc"> *new(parent, bounds);</pre>

You then add defaults, followed by the individual tabs, setting their individual instance variables.

<div class="note"><span class="notelabel">NOTE:</span> You never dierectly create TabbedViewTab instances, but rather use TabbedView2.add to add tabs. Many instance variables for TabbedView, are now (arrays of) default values for TabbedViewTab instances. TabbedViewTab instances can in turn override those defaults. This way you can customize individual tabs.

See [TabbedViewTab](./../Classes/TabbedViewTab.html) .

</div>

**Example**:

**Old Syntax**

<pre class="code prettyprint lang-sc">(
// create the TabbedView, tabs,color, etc.
t=TabbedView.new(nil,nil,
    ["test1","test2","test3"],
    [Color.red.alpha_(0.1), Color.blue.alpha_(0.1),Color.green.alpha_(0.1)],
    "test window",
    scroll:true);

//add defaults
t.tabHeight_(20).tabCurve_(3);

//populate view
v=t.views[0];
Slider(v, Rect(20,20,320,20));

//add more views
t.add("extraTab, but not custom")
)</pre>

**New Syntax**

<pre class="code prettyprint lang-sc">(
// create the TabbedView2
t=TabbedView2.new;

//add defaults, before creating tabs
t.backgrounds_([Color(0.9,0.85,0.85),Color(0.85,0.85,0.9),Color(0.9,0.9,0.85)]);
t.unfocusedColors_([Color(0.9,0.75,0.75),Color(0.75,0.75,0.9),Color(0.9,0.9,0.75)]);
t.labelColors_([Color.red,Color.blue,Color.yellow]);

t.tabHeight_(20);

// now add a tab and populate it with a slider;
v=t.add("test1", scroll:true); //scroll must be decided upon creation.
Slider(v, Rect(20,20,320,20));

//add some closable tabs
t.add("test2", scroll:true).closable_(true);
t.add("test3", scroll:true).closable_(true);
t.add("test4", scroll:true).closable_(true);

// override defaults in a custom tab
m=t.add("Custom Configured Tab", scroll:true);
m.labelColor=Color.green.alpha_(1);
m.unfocusedColor=Color.green.alpha_(0.4);
m.background=Color.green.alpha_(0.1);

t.refresh;
)</pre>

## <a class="anchor" name="classmethods">Class Methods</a>

### <span class="methprefix">*</span>[new](./../Overviews/Methods.html#new) (<span class="argstr">parent</span>, <span class="argstr">bounds</span>)

<div class="method">

create a Tabbed View

#### Arguments:

| parent | 

a parent view. if nil, then a new window is created

 |
| bounds | 

Rect . if nil then the parent Rect is used

 |

#### Returns:

<div class="returnvalue">

returns a TabbedView2

</div>

</div>

### <a class="anchor" name="Convenience Creation Methods">Convenience Creation Methods</a>

<pre class="code prettyprint lang-sc">// choose one.   .demo adds some tabs automatically
TabbedView2.newPacked.demo;    //create a very space efficient TabbedView2
TabbedView2.newFlat.demo;    // create a  flat  TabbedView2
TabbedView2.newTall.demo;    // create a tall TabbedView2
TabbedView2.newColor.demo;    // create a Tabbed View with  rgb tabs
TabbedView2.newColorLabels.demo;    // create a Tabbed View with  rgb labels
TabbedView2.newBasic.demo;    // create a very basic TabbedView2
TabbedView2.newTransparent.demo;    // create a transparent TabbedView2</pre>

### <a class="anchor" name="Inherited class methods">Inherited class methods</a>

### <a class="anchor" name="Undocumented class methods">Undocumented class methods</a>

### <span class="methprefix">*</span>[newIDEdefault](./../Overviews/Methods.html#newIDEdefault) (<span class="argstr">w</span>, <span class="argstr">bounds</span>)

<div class="extmethod">From extension in [/Users/fuo/Documents/SC3_IDE/QT_only/SystemOverwrites//Overrides.sc](file:///Users/fuo/Documents/SC3_IDE/QT_only/SystemOverwrites//Overrides.sc)</div>

## <a class="anchor" name="instancemethods">Instance Methods</a>

### <a class="anchor" name="Views and Windows">Views and Windows</a>

### <span class="methprefix">-</span>[view](./../Overviews/Methods.html#view)

<div class="method">

#### Returns:

<div class="returnvalue">

the container for all the views

</div>

</div>

### <span class="methprefix">-</span>[alwaysOnTop](./../Overviews/Methods.html#alwaysOnTop)

### <span class="methprefix">-</span>[alwaysOnTop](./../Overviews/Methods.html#alwaysOnTop) = value

<div class="method">

#### Arguments:

| (boolean) | 

If a window was created automatically, then this sets whether it is always on top.

 |

</div>

### <span class="methprefix">-</span>[window](./../Overviews/Methods.html#window)

<div class="method">

If a window was created automatically, then this returns the window.

<div class="note"><span class="notelabel">NOTE:</span> If the last tab of this window is closed or dragged (under QT only), then the window closes as well.</div>

</div>

### <span class="methprefix">-</span>[tabAt](./../Overviews/Methods.html#tabAt) (<span class="argstr">index</span>)

<div class="method">

get the TabbedViewTab instance at index.

#### Returns:

<div class="returnvalue">

a TabbedViewTab instance. A TabbedViewTab instance responds to .asView, so it can be used to fill a parent argument, just like any other view can.

</div>

</div>

### <span class="methprefix">-</span>[tabViews](./../Overviews/Methods.html#tabViews)

### <span class="methprefix">-</span>[tabViews](./../Overviews/Methods.html#tabViews) = value

<div class="method">

#### Returns:

<div class="returnvalue">

an array of TabbedViewTab instances.

</div>

</div>

### <span class="methprefix">-</span>[resize](./../Overviews/Methods.html#resize)

### <span class="methprefix">-</span>[resize](./../Overviews/Methods.html#resize) = <span class="argstr">int</span>

<div class="method">

sets the resize flag (1-9 ) of the enclosing view. see [Resize behaviour](./../Reference/Resize.html)

</div>

### <span class="methprefix">-</span>[clone](./../Overviews/Methods.html#clone) (<span class="argstr">parent</span>, <span class="argstr">x: 0</span>, <span class="argstr">y: 0</span>)

<div class="method">

Creates a new TabbedView2, copying all of the settings of the current on, other that the tabs. This method is also used internally when detaching tabs under QT.

#### Arguments:

| parent | 

a parent view. if none, a new window is created.

 |
| x | 

If a new window is created, it will be created offset from this x position by 20px (mainly for internal use)

 |
| y | 

If a new window is created, it will be created offset from this y position by 20px (mainly for internal use)

 |

#### Returns:

<div class="returnvalue">

The new TabbedView2 instance.

</div>

</div>

### <a class="anchor" name="Adding, Removing, Dragging, and Detaching Tabs">Adding, Removing, Dragging, and Detaching Tabs</a>

<div class="note"><span class="notelabel">NOTE:</span> **Double-Clicking and Dragging.**Double-clicking or dragging a tab widget within its view will change the tab followEdges or position (\left, \top, \right, or \bottom), as well as changing the order of the tabs; You can use methods tabPosition and followEdges to do the same programmatically. To prevent dragging or double clicking, use lockPosition and followEdges=false, or dragTabs=false.</div>

<div class="note"><span class="notelabel">NOTE:</span> **DraggingTabs between Views and Windows.**Under QT, you can cmd-drag (or ctrl-drag) a tab between different TabbedView2 instances, even if they are in different window.</div>

<div class="note"><span class="notelabel">NOTE:</span> **DetachingTabs.**Under QT, you can right click to detach a tab. In reality, this clones the parent TabbedView2, places the clone in its own window, and then migrates the tab into the new view, using Qt's set Parent. If the last Tab of this window is closed or dragged, then the window closes as well.</div>

### <span class="methprefix">-</span>[add](./../Overviews/Methods.html#add) (<span class="argstr">label</span>, <span class="argstr">index</span>, <span class="argstr">scroll: false</span>)

<div class="method">

adds a TabbedViewTab instance

#### Arguments:

| label | 

string, the label

 |
| index | 

int, (optional) the index at which the tab is inserted (if nil, add to the end)

 |
| scroll | 

Boolean, default false. Must be set before creation of tab.

 |

#### Returns:

<div class="returnvalue">

the new TabbedViewTab

</div>

</div>

### <span class="methprefix">-</span>[insert](./../Overviews/Methods.html#insert) (<span class="argstr">index</span>, <span class="argstr">label</span>, <span class="argstr">scroll: false</span>)

<div class="method">

inserts a TabbedViewTab instance at index

#### Arguments:

| index | 

the index at which the tab is inserted

 |
| label | 

(describe argument here)

 |
| scroll | 

Boolean, default false. Must be set before creation of tab.

 |

#### Returns:

<div class="returnvalue">

the new TabbedViewTab

</div>

</div>

### <span class="methprefix">-</span>[dragTabs](./../Overviews/Methods.html#dragTabs)

### <span class="methprefix">-</span>[dragTabs](./../Overviews/Methods.html#dragTabs) = value

<div class="method">

Boolean or Function: {arg thisView; return boolean}. default: true; Set to false to disable regular tab dragging (position or order changing by drag);

</div>

### <span class="methprefix">-</span>[detachedClosable](./../Overviews/Methods.html#detachedClosable)

### <span class="methprefix">-</span>[detachedClosable](./../Overviews/Methods.html#detachedClosable) = value

<div class="method">

if tabs are detached, you can lose a tab if you close its window. so this allows you to prevent that by setting it to false. The window will still close when the last tab has been dragged out of it.

</div>

### <span class="methprefix">-</span>[demo](./../Overviews/Methods.html#demo) (<span class="argstr">i: 3</span>, <span class="argstr">string: "tab"</span>)

<div class="extmethod">From extension in [/Users/fuo/Library/Application Support/SuperCollider/downloaded-quarks/TabbedView2/TabbedView2plus.sc](file:///Users/fuo/Library/Application Support/SuperCollider/downloaded-quarks/TabbedView2/TabbedView2plus.sc)</div>

<div class="method">

quickly creates a bunch of tabs. for texting TabbedView2 settings Tab labels will be i++string

#### Arguments:

| i |
| string |

</div>

### <span class="methprefix">-</span>[removeAt](./../Overviews/Methods.html#removeAt) (<span class="argstr">index</span>)

<div class="method">

remove tab at Index

#### Arguments:

| index | 

the index of the tab to be removed

 |

</div>

### <span class="methprefix">-</span>[focus](./../Overviews/Methods.html#focus) (<span class="argstr">index</span>)

<div class="method">

selects one of the tabs

#### Arguments:

| index | 

int, the index to focus

 |

</div>

### <span class="methprefix">-</span>[activeTab](./../Overviews/Methods.html#activeTab)

<div class="method">

#### Returns:

<div class="returnvalue">

returns the focused tab

</div>

</div>

### <a class="anchor" name="Set tabPosition and followEdges">Set tabPosition and followEdges</a>

<div class="note"><span class="notelabel">NOTE:</span> Double-clicking or dragging a tab widget will change the tab followEdges or position (\left, \top, \right, or \bottom), or the order of the tabs. You can use methods tabPosition and followEdges to do the same programmatically.</div>

### <span class="methprefix">-</span>[tabPosition](./../Overviews/Methods.html#tabPosition)

### <span class="methprefix">-</span>[tabPosition](./../Overviews/Methods.html#tabPosition) = <span class="argstr">symbol</span>

<div class="method">

#### Arguments:

| symbol | 

\left, \top, \right, or \bottom.

 |

</div>

### <span class="methprefix">-</span>[lockPosition](./../Overviews/Methods.html#lockPosition)

### <span class="methprefix">-</span>[lockPosition](./../Overviews/Methods.html#lockPosition) = value

<div class="method">

Lockes the \left, \top, \right, or \bottom position of the tabs. You still can change the order of the tabs themselves by dragging.

#### Arguments:

| (bool) | 

default false.

 |

</div>

### <span class="methprefix">-</span>[followEdges](./../Overviews/Methods.html#followEdges)

### <span class="methprefix">-</span>[followEdges](./../Overviews/Methods.html#followEdges) = <span class="argstr">bool</span>

<div class="method">

Boolean or Function: {arg thisView; return boolean}. Set tabs parallel or perpendicular to container edges. default true. (Set tabs parallel);

</div>

### <span class="methprefix">-</span>[lockEdges](./../Overviews/Methods.html#lockEdges)

### <span class="methprefix">-</span>[lockEdges](./../Overviews/Methods.html#lockEdges) = value

<div class="method">

Prevents Double-Click changing of followEdges.

#### Arguments:

| (bool) | 

default false.

 |

</div>

### <a class="anchor" name="Examples: Set tabPosition and followEdges">Examples: Set tabPosition and followEdges</a>

**Setting the position or followEdges instance variables**

<pre class="code prettyprint lang-sc">(
v=TabbedView2.newColorLabels; //default
v.tabHeight = 25;
5.do{arg i; var q="aa"; i.do{q=q++"a"}; v.add(q) };
v.tabViews[0].flow({arg w;
    Button(w,360@50).states_([["tabs top (or drag tab to top)"]]).action_({v.tabPosition_(\top)});
    w.startRow;
    Button(w,178@50).states_([["tabs left (or drag tab to left)"]]).action_({v.tabPosition_(\left)});
    Button(w,178@50).states_([["tabs right (or drag tab to right)"]]).action_({v.tabPosition_(\right)});
    w.startRow;
    Button(w,360@50).states_([["tabs top (or drag tab to botom)"]]).action_({v.tabPosition_(\bottom)});

    Button(w,360@50)
    .states_([["set followEdges=false \n(or double-click on tabs)",Color.black,Color.red.alpha_(0.2)],
        ["set followEdges=true \n(or double-click on tabs)",Color.black,Color.green.alpha_(0.2)]])
    .action_({arg b;(b.value==1).if{v.followEdges_(false)}{v.followEdges_(true)};});
});
)
(
TabbedView2.newColorLabels.tabPosition_(\right).followEdges_(false).demo(25,"");
TabbedView2.newTall.tabPosition_(\left).demo(25,"test");
TabbedView2.newTall(nil,Rect(100,500,400,100)).tabPosition_(\bottom).demo(5,"test");

)</pre>

### <a class="anchor" name="Auto-Archiving a TabbedView2 State">Auto-Archiving a TabbedView2 State</a>

<div class="note"><span class="notelabel">NOTE:</span> In order to archive tab positions, their labels must be unique.</div>

<div class="note"><span class="notelabel">NOTE:</span> Does not support detached Tabs</div>

### <span class="methprefix">-</span>[autoArchive](./../Overviews/Methods.html#autoArchive) ( <span class="argstr">... args</span>)

<div class="method">

Automatically saves the state of the TabbedView2 to given path in the Archive.

<div class="note"><span class="notelabel">NOTE:</span> If the number of saved \indexes is different than the number of tabs, the saved \indexes array will be ignored and reset.</div>

#### Arguments:

| symbols | 

symbol1, symbol2, symbol3, ...

<pre class="code prettyprint lang-sc">v=TabbedView2.new;
v.add("tab1"); // tab names must be unique
v.add("tab2");
v.add("tab3");
// call autoArchive **after** adding the tabs;
v.autoArchive(\myStorageProject, \myStorageSubsection, \myTabbedViewStorageName);</pre>

 |

</div>

### <span class="methprefix">-</span>[archiveKeys](./../Overviews/Methods.html#archiveKeys)

### <span class="methprefix">-</span>[archiveKeys](./../Overviews/Methods.html#archiveKeys) = value

<div class="method">

Array: Determines which keys will be archived when autoArchive is enabled.

`default=[\indexes, \followEdges, \tabPosition, \tabFocus]`

#### Arguments:

| (array) | 

Array of Symbols, may include only `[\indexes, \followEdges, \tabPosition, \tabFocus]`

 |

</div>

### <span class="methprefix">-</span>[saveStateToArchive](./../Overviews/Methods.html#saveStateToArchive) ( <span class="argstr">... args</span>)

<div class="method">

Saves the state of the TabbedView2 to given path in the Archive.

#### Arguments:

| symbols | 

symbol1, symbol2, symbol3, ...

 |

</div>

### <span class="methprefix">-</span>[restoreStateFromArchive](./../Overviews/Methods.html#restoreStateFromArchive) ( <span class="argstr">... args</span>)

<div class="method">

Restores the state of the TabbedView2 from given path in the Archive.

<div class="note"><span class="notelabel">NOTE:</span> If the number of saved \indexes is different than the number of tabs, the saved \indexes array will be ignored and reset.</div>

#### Arguments:

| symbols | 

symbol1, symbol2, symbol3, ...

 |

</div>

### <a class="anchor" name="Setting Colors">Setting Colors</a>

<div class="note"><span class="notelabel">NOTE:</span> Many of these methods take arrays of Color instances. These colors are used as the defaults for new tabs. If the array is shorter than the amount of tabs, then the color choice will cycle through the array. However, TabbedViewTab instances will retain their color when their positions change, and they can also have individual color definitions, which override the defaults. These defaults are only there in order to prevent repeating code when creating new tabs.</div>

### <span class="methprefix">-</span>[resetColors](./../Overviews/Methods.html#resetColors)

<div class="method">

reset the tab colors, cycling through default color arrays.

<div class="warning"><span class="warninglabel">WARNING:</span> This will reset individual colors that were overriden in the tab instances!</div>

</div>

### <span class="methprefix">-</span>[labelColors](./../Overviews/Methods.html#labelColors)

### <span class="methprefix">-</span>[labelColors](./../Overviews/Methods.html#labelColors) = <span class="argstr">colorArray</span>

<div class="method">

#### Arguments:

| colorArray | 

Array of Colors sets the default colors of the tab widgets. New tabs will cycle through these colors, though these can be overridden in the TabbedViewTab instance.

 |

</div>

### <span class="methprefix">-</span>[unfocusedColors](./../Overviews/Methods.html#unfocusedColors)

### <span class="methprefix">-</span>[unfocusedColors](./../Overviews/Methods.html#unfocusedColors) = <span class="argstr">colorArray</span>

<div class="method">

#### Arguments:

| colorArray | 

Array of Colors sets the default unfocusedColors colors of the tab widgets. New tabs will cycle through these colors, though these can be overridden in the TabbedViewTab instance.

 |

</div>

### <span class="methprefix">-</span>[backgrounds](./../Overviews/Methods.html#backgrounds)

### <span class="methprefix">-</span>[backgrounds](./../Overviews/Methods.html#backgrounds) = <span class="argstr">colorArray</span>

<div class="method">

#### Arguments:

| colorArray | 

Array of Colors sets the default background colors of the Composite/Scroll Views. New tabs will cycle through these colors, though these can be overridden in the TabbedViewTab instance.

 |

</div>

### <span class="methprefix">-</span>[stringColors](./../Overviews/Methods.html#stringColors)

### <span class="methprefix">-</span>[stringColors](./../Overviews/Methods.html#stringColors) = <span class="argstr">colorArray</span>

<div class="method">

#### Arguments:

| colorArray | 

Array of Colors sets the default label string colors. New tabs will cycle through these colors, though these can be overridden in the TabbedViewTab instance.

 |

</div>

### <span class="methprefix">-</span>[stringFocusedColors](./../Overviews/Methods.html#stringFocusedColors)

### <span class="methprefix">-</span>[stringFocusedColors](./../Overviews/Methods.html#stringFocusedColors) = <span class="argstr">colorArray</span>

<div class="method">

#### Arguments:

| colorArray | 

Array of Colors sets the default focused label string colors. New tabs will cycle through these colors, though these can be overridden in the TabbedViewTab instance.

 |

</div>

### <a class="anchor" name="Setting Geometry and Fonts">Setting Geometry and Fonts</a>

<div class="note"><span class="notelabel">NOTE:</span> tabWidth and labelPadding are defaults which can be overridden in individual tabs</div>

### <span class="methprefix">-</span>[refresh](./../Overviews/Methods.html#refresh)

<div class="method">

recalculate all geometry values and redraw tabs

</div>

### <span class="methprefix">-</span>[tabWidth](./../Overviews/Methods.html#tabWidth)

### <span class="methprefix">-</span>[tabWidth](./../Overviews/Methods.html#tabWidth) = <span class="argstr">int</span>

<div class="method">

#### Arguments:

| int | 

int or \auto ; a fixed tab width, or "auto" for automatic tab width (default "auto", unless using themes). Can be overridden in in the TabbedViewTab instance.

 |

</div>

### <span class="methprefix">-</span>[labelPadding](./../Overviews/Methods.html#labelPadding)

### <span class="methprefix">-</span>[labelPadding](./../Overviews/Methods.html#labelPadding) = <span class="argstr">int</span>

<div class="method">

#### Arguments:

| int | 

if autosizing is on, then this determines left and right padding from the label text. Can be overridden in in the TabbedViewTab instance.

 |

</div>

### <span class="methprefix">-</span>[tabHeight](./../Overviews/Methods.html#tabHeight)

### <span class="methprefix">-</span>[tabHeight](./../Overviews/Methods.html#tabHeight) = <span class="argstr">val</span>

<div class="method">

#### Arguments:

| int | 

int or \auto . a fixed tab height, or "auto" for automatic tab height (default "auto", unless using themes)

 |

</div>

### <span class="methprefix">-</span>[tabCurve](./../Overviews/Methods.html#tabCurve)

### <span class="methprefix">-</span>[tabCurve](./../Overviews/Methods.html#tabCurve) = <span class="argstr">int</span>

<div class="method">

#### Arguments:

| int | 

the radius in pixels of the rounded tab corners

 |

</div>

### <span class="methprefix">-</span>[clickbox](./../Overviews/Methods.html#clickbox)

### <span class="methprefix">-</span>[clickbox](./../Overviews/Methods.html#clickbox) = value

<div class="method">

#### Arguments:

| (int) | 

set the size of the clickbox and detach icons in pixels. default is 15

 |

</div>

### <span class="methprefix">-</span>[swingFactor](./../Overviews/Methods.html#swingFactor)

### <span class="methprefix">-</span>[swingFactor](./../Overviews/Methods.html#swingFactor) = value

<div class="method">

#### Arguments:

| (point) | 

Point ; a multiplication factor for a string/tab width for GUI.swing only. default Point(0.52146,1.25)

 |

</div>

### <span class="methprefix">-</span>[font](./../Overviews/Methods.html#font)

### <span class="methprefix">-</span>[font](./../Overviews/Methods.html#font) = <span class="argstr">fnt</span>

<div class="method">

set the font

</div>

### <a class="anchor" name="Inherited instance methods">Inherited instance methods</a>

### <a class="anchor" name="Undocumented instance methods">Undocumented instance methods</a>

### <span class="methprefix">-</span>[changeAction](./../Overviews/Methods.html#changeAction)

### <span class="methprefix">-</span>[changeAction](./../Overviews/Methods.html#changeAction) = value

### <span class="methprefix">-</span>[hasDuplicates](./../Overviews/Methods.html#hasDuplicates)

## <a class="anchor" name="examples">Examples</a>

### <a class="anchor" name="Usage:">Usage:</a>

**use CompositeView style GUI**

<pre class="code prettyprint lang-sc">(
t=TabbedView2.new;
v=t.add("tab1");
 Button( v,Rect(50,50,200,100)).states_([["go to next tab "]]).action_({t.focus(1)});
t.add("tab2");
t.add("tab3");
)</pre>

**use FlowView style GUI**

<pre class="code prettyprint lang-sc">(
t=TabbedView2.new; // use Flow Style

    t.add("test1").flow({|w|
        GUI.button.new(w,Rect(50,50,250,50))
        .states_([["control the tab with method 'focus' -->"]]).action_({t.focus(1)})
    });

    t.add("test2").flow({|w|
        GUI.button.new(w,Rect(50,50,200,100))
        .states_([["go to last tab"]]).action_({t.focus(2)})
    });
    t.add("test2");
)</pre>

### <a class="anchor" name="Quick styling with variations on *new:">Quick styling with variations on *new:</a>

(There are some color differences for swing)

<pre class="code prettyprint lang-sc">//.demo automatically adds 3 tabs.

TabbedView2.newBasic.demo
TabbedView2.newColor.demo
TabbedView2.newColorLabels.demo
TabbedView2.newFlat.demo
TabbedView2.newTall.demo
TabbedView2.newTransparent.demo
(
t = TabbedView2.newPacked;
20.do{|i| t.add(i.asString)}; //very good for tons of tabs :
)</pre>

### <a class="anchor" name="Drag objects from one tab to another (under cocoa and qt only at the moment):">Drag objects from one tab to another (under cocoa and qt only at the moment):</a>

<pre class="code prettyprint lang-sc">(
v=TabbedView2.newColorLabels.demo;
n = GUI.dragSource.new(v.tabViews[0], Rect(50, 50, 140, 24));
            n.object = "Drag me to Tab2";
 GUI.textView.new (v.views[1], Rect(50, 50, 140, 80));
)</pre>

### <a class="anchor" name="Add, removeAt, insert tabs">Add, removeAt, insert tabs</a>

defaults on *new, but other themes use fixed widths:

<pre class="code prettyprint lang-sc">v=TabbedView2.newTall.demo(3)

v.add("I am last")

v.insert(2,"squeeze me in")

v.removeAt(2)</pre>

### <a class="anchor" name="Auto-Archiving Tabs">Auto-Archiving Tabs</a>

<div class="note"><span class="notelabel">NOTE:</span> Does not support detached Tabs</div>

<pre class="code prettyprint lang-sc">v.add("tab1"); // tab names must be unique
v.add("tab2");
v.add("tab3");
// call autoArchive **after** adding the tabs;
v.autoArchive(\myStorageProject, \myStorageSubsection, \myTabbedViewStorageName);
// v's state will now be stored in the archive,
// and will be restored if you execte the above code again.</pre>

### <a class="anchor" name="resize">resize</a>

<pre class="code prettyprint lang-sc">(
w=GUI.window.new.front;
v=TabbedView2.newTall(w,Rect(40,40,280,280)).demo(8)
    .tabPosition_(\right).followEdges_(false);
v.resize_(5);
GUI.slider.new(v.views[0],Rect(10,80,200,30)).resize_(2);
)</pre>

### <a class="anchor" name="Nest TabbedView2 &amp; use scrolling">Nest TabbedView2 & use scrolling</a>

uses scroll:true in the inner tab

<pre class="code prettyprint lang-sc">(
v=TabbedView2.newPacked(nil,Rect(200,200,600,400).insetBy(20,20)).demo(3,"")
        .tabHeight_(40).tabPosition_(\right).followEdges_(false);

q=TabbedView2.newColorLabels(v.tabViews[0],nil)
    .tabPosition_(\right).resize_(5).followEdges_(false);
["tab1.1","tab1.2","tab1.3"].do{arg text; q.add(text, scroll: true)};

q.tabViews[0].flow({ arg w;
    78.do({ arg i;
        b = Button(w, Rect(rrand(20,300),rrand(20,300), 75, 24));
        b.states = [["Start "++i, Color.black, Color.rand],
        ["Stop "++i, Color.white, Color.red]];
    });
});
GUI.slider.new(q.tabViews[1], Rect(20,20,200,20));
)</pre>

### <a class="anchor" name="User functions: focus and unfocus">User functions: focus and unfocus</a>

turn on/off scopes , e.g.

<pre class="code prettyprint lang-sc">(
v=TabbedView2.new;
v.add("test1").focusAction={"tab2 is focused".postln};
v.add("test2").unfocusAction={"tab2 just unfocused".postln};
v.add("test3");
)</pre>

### <a class="anchor" name="Swing Special: focusFrameColor_(color) and unfocusTabs_(bool)">Swing Special: focusFrameColor_(color) and unfocusTabs_(bool)</a>

The tabs are drawn with user view which have a clear focus frame on Cocoa. On Swing, the frame cannot be made clear, so by default the tabs are unfocused after clicking. You can change this if it interferes with your tabbing scheme.

<pre class="code prettyprint lang-sc">(
v=TabbedView2.new.demo;

v.unfocusTabs_(false);  // default is false on Cocoa and QT, true otherwise;
v.focusFrameColor_(Color.red); //cocoa only

)</pre>

### <a class="anchor" name="Fixed tab widths and \auto tab widths">Fixed tab widths and \auto tab widths</a>

tabWidth defaults to \auto on *new, but other themes use fixed widths:

<pre class="code prettyprint lang-sc">( // *newFlat has fixed width, so you might need to adjust it
t = TabbedView2.newFlat(nil,Rect(150,100,400,500));
t.tabWidth_(\auto); //change default width to auto
t.add("1");
t.add("two");
t.add("threeeeeeeeeeee");
t.add("four");
t.add("5");
)

// Or you can keep the tab width fixed, but adjust the individual tab

( // newFlat has fixed width, so you might need to adjust it
t = TabbedView2.newFlat(nil,Rect(150,100,400,500));
t.add("1");
t.add("two");
t.add("threeeeeeeeeeee").tabWidth_(110); // adjust width of this tab only
t.add("four");
t.add("5");
t.tabWidth_(\auto);
)</pre>

### <a class="anchor" name="Set Font">Set Font</a>

Swing fonts only work within certain limits for now. use swingFactor_ to adjust the conversion.

<pre class="code prettyprint lang-sc">TabbedView2.newBasic.font_(GUI.font.new("Monaco",9)).tabHeight_(18).demo;
TabbedView2.newBasic.font_(GUI.font.new("Monaco",36)).demo;
TabbedView2.newBasic.font_(GUI.font.new("Helvetica",14)).tabHeight_(\auto).demo;
TabbedView2.newTall.font_(GUI.font.new("Helvetica",18)).tabPosition_(\left).demo;
TabbedView2.newTall.font_(GUI.font.new("Helvetica",36)).tabHeight_(\auto).tabWidth_(\auto).demo;</pre>

### <a class="anchor" name="Set colors very specifically to your own taste using set methods">Set colors very specifically to your own taste using set methods</a>

<pre class="code prettyprint lang-sc">(
t=TabbedView2.new;
//set default colors
c=[Color.rand,Color.rand,Color.rand];
t.labelColors_(c);
t.unfocusedColors_(c.collect{|c| c.alpha_(0.4)});
t.backgrounds_(c.collect{|c| c.alpha_(0.4)});
t.stringColors_([Color.black,Color.blue]);
t.stringFocusedColors_([Color.white]);
t.demo(8);  // make tabs

// set colors of tab7 to yellow
t.tabAt(6).labelColor_(Color.red)
    .unfocusedColor_(Color.blue)
    .background_(Color.yellow.alpha_(0.1));
t.refresh;
)

t.resetColors;  //resets individual tabs to default. ( use this, e.g., if you dragged a tab (under QT) to another TabbedView2 that has different default colors).</pre>

### <a class="anchor" name="Adjust padding and curves">Adjust padding and curves</a>

labelPadding only has an effect on auto width

<pre class="code prettyprint lang-sc">(
v=TabbedView2.new;
v.labelPadding_(8);      //tighter padding
v.tabCurve_(0);           //sharper curves
v.stringColors_([Color.black]);
v.backgrounds_([Color.white.alpha_(0.3)]);
v.demo(20,"")
)

// or simply use *newPacked:

(
v=TabbedView2.newPacked.demo(20,"");
)</pre>

### <a class="anchor" name="Adjust tab height and curves">Adjust tab height and curves</a>

<pre class="code prettyprint lang-sc">// super flat and elegant

(
v=TabbedView2.new.tabWidth_(70).tabHeight_(13).tabCurve_(0).demo(5);
)

// super tall and clear

(
TabbedView2.new.tabWidth_(70).tabHeight_(30).demo(5);
)</pre>

## <a class="anchor" name="Demo">Demo</a>

Execute the code below to test all the features and parameters.

### <a class="anchor" name="All Features and Parameters">All Features and Parameters</a>

<pre class="code prettyprint lang-sc">(
w=Window.new("TabbedView Examples").front.setTopLeftBounds(Rect(50,50,1050,700));
// setup views
~t1v=TabbedView2.newTall(w.view, Rect(50,50,450,600));
~t1t1= ~t1v.add("Tab 1.1");
~t1t2= ~t1v.add("Tab 1.2").closable_(true);
~t1t3= ~t1v.add("Tab 1.3").useDetachIcon_(true);

~t2v=TabbedView2.newTall(w.view, Rect(550,50,450,600));
~t2t1= ~t2v.add("Tab 2.1");
~t2t2= ~t2v.add("Tab 2.2").closable_(true);
~t2t3= ~t2v.add("Tab 2.3").closable_(true);

// populate
~t1t1.flow({arg w;

Button(w,Rect(0,0,360,22)).states_([["Add Tab"]]).action_({~t1t1.tabbedView.add("extra"+~t1t1.tabbedView.tabViews.size).closable_(true)});

StaticText(w,Rect(0,0,360,130)).string_("
- Drag the index position of the tags (no cmd key needed).
- Drag the top,left,botom,right postion of the tabs.
- Double-click on tabs to change followEdges option
- Under QT, right-click on tab to detach it.
- Under QT, Cmd/ctrl-drag tabs between tab views, even between windows.");
StaticText(w,Rect(0,0,360,22)).string_(" TabbedViewTab color variables:").background_(Color.grey(0.85));
Button(w,Rect(0,0,360,22))
    .states_([["background_ of this tab Color.blue.alpha_(0.1)"]])
    .action_({~t1t1.background_(Color.blue.alpha_(0.1));~t1t1.focus});
Button(w,Rect(0,0,360,22))
    .states_([["labelColor_ of this tab Color.blue.alpha_(0.1)"]])
    .action_({~t1t1.labelColor_(Color.blue.alpha_(0.1));~t1t1.focus});
Button(w,Rect(0,0,360,22))
    .states_([["unfocusedColor_ of this tab Color.blue"]])
    .action_({~t1t1.unfocusedColor_(Color.blue);~t1t2.focus;{{~t1t1.focus}.defer(1)}.fork});
Button(w,Rect(0,0,360,22))
    .states_([["stringFocusedColor_ of this tab Color.red"]])
    .action_({~t1t1.stringFocusedColor_(Color.red);~t1t1.focus});
Button(w,Rect(0,0,360,22))
    .states_([["stringColor_ of this tab Color.green"]])
    .action_({~t1t1.stringColor_(Color.green);~t1t2.focus;{{~t1t1.focus}.defer(1)}.fork});
Button(w,Rect(0,0,360,22))
    .states_([[".resetColors"]])
    .action_({~t1t1.tabbedView.resetColors;~t1t2.focus;~t1t1.focus});
StaticText(w,Rect(0,0,360,22)).string_(" TabbedView2 color variables:").background_(Color.grey(0.85));

StaticText(w,Rect(0,0,360,88)).string_("Use the same variable names as above, but in plural, to set defaults before adding tabs. All default colors are set as arrays of colors, and tabs cylcle though the colors upon being created.");
},~t1t1.bounds.insetBy(15,0));

~t2t1.flow({arg w;
    Button(w,Rect(0,0,360,22))
        .states_([["Add Tab"]])
        .action_({~t2t1.tabbedView.add("extra"+ ~t2t1.tabbedView.tabViews.size).closable_(true)});
    StaticText(w,Rect(0,0,360,22)).string_(" TabbedView2 instance variables").background_(Color.grey(0.85));
    //CheckBox(w,Rect(0,0,179,22)).string_("followEdges_").action_{|b| ~t2v.followEdges=b.value}.value_(true);
    EZPopUpMenu(w,Rect(0,0,177,22),"followEdges_:",[ \true ->{~t2v.followEdges=true}, \false ->{~t2v.followEdges=false}],labelWidth:100)
         .labelView.align_(\left);

    EZPopUpMenu(w,Rect(0,0,177,22),"tabPosition_:",
         [
             \top ->{~t2v. tabPosition_(\top)},
                \right ->{~t2v. tabPosition_(\right)},
                \bottom ->{~t2v. tabPosition_(\bottom)},
                \left ->{~t2v. tabPosition_(\left)},
         ],labelWidth:100);
    StaticText(w,Rect(0,0,360,22)).string_("Prevent dragging:");
    EZPopUpMenu(w,Rect(0,0,177,22),"lockEdges_:",[ \false ->{~t2v.lockEdges=false}, \true ->{~t2v.lockEdges=true}],labelWidth:100)
         .labelView.align_(\left);
    EZPopUpMenu(w,Rect(0,0,177,22),"dragTabs_:",[ \true ->{~t2v.dragTabs=true}, \false ->{~t2v.dragTabs=false}],labelWidth:100);

    EZPopUpMenu(w,Rect(0,0,177,22),"lockPosition_:",[ \false ->{~t2v.lockPosition=false}, \true ->{~t2v.lockPosition=true}],labelWidth:100)
        .labelView.align_(\left);
    CompositeView(w,Rect(0,0,177,22));

    EZPopUpMenu(w,Rect(0,0,177,22),"tabHeight_:",[
         \30 ->{~t2v.tabHeight=30;~t2v.refresh},
         \40 ->{~t2v.tabHeight=40;~t2v.refresh},
         \20 ->{~t2v.tabHeight=20;~t2v.refresh},
         \auto ->{~t2v.tabHeight=\auto;~t2v.refresh}],
        labelWidth:100).labelView.align_(\left);
    EZPopUpMenu(w,Rect(0,0,177,22),"labelPadding_:",[
         \20 ->{~t2v.labelPadding=20;~t2v.refresh},
         \40 ->{~t2v.labelPadding=40;~t2v.refresh},
         \60 ->{~t2v.labelPadding=60;~t2v.refresh}],
        labelWidth:100);
    EZPopUpMenu(w,Rect(0,0,360,22),"font_:",[
         'Helvetica 12' ->{~t2v.font=Font("Helvetica",12);~t2v.refresh},
         'Helvetica 14' ->{~t2v.font=Font("Helvetica",14);~t2v.refresh},
         'Helvetica 18' ->{~t2v.font=Font("Helvetica",18);~t2v.refresh},
         'Helvetica 24' ->{~t2v.font=Font("Helvetica",24);~t2v.refresh}],
        labelWidth:100).labelView.align_(\left);

    StaticText(w,Rect(0,0,360,22)).string_(" labelPadding_ only effects tabWidth:\\auto .");

    StaticText(w,Rect(0,0,360,22)).string_(" TabbedViewTab instance variables").background_(Color.grey(0.85));
    EZPopUpMenu(w,Rect(0,0,177,22),"closable_:",[ \false ->{~t2t1.closable=false;~t2v.refresh}, \true ->{~t2t1.closable=true;~t2v.refresh}],
        labelWidth:100).labelView.align_(\left);
    EZPopUpMenu(w,Rect(0,0,177,22),"useDetachIcon_:",[ \false ->{~t2t1.useDetachIcon=false;~t2v.refresh}, \true ->{~t2t1.useDetachIcon=true;~t2v.refresh}],
        labelWidth:100).labelView.align_(\left);
    EZPopUpMenu(w,Rect(0,0,177,22),"tabWidth_:",[
         \70 ->{~t2t1.tabWidth=70;~t2v.refresh},
         \100 ->{~t2t1.tabWidth=100;~t2v.refresh},
         \120 ->{~t2t1.tabWidth=120;~t2v.refresh},
         \auto ->{~t2t1.tabWidth=\auto;~t2v.refresh}],
        labelWidth:100).labelView.align_(\left);

},~t2t1.bounds.insetBy(15,0));

StaticText(~t1t2,Rect(20,60,360,40))
    .string_("- I am closable: .closable_(true)");

StaticText(~t1t3,Rect(20,60,360,40))
    .string_("- Under QT, I have a detach icon: .useDetachIcon_(true)");
)</pre>

<div class="doclink">source: [/Users/fuo/Library/Application Support/SuperCollider/downloaded-quarks/TabbedView2/HelpSource/Classes/TabbedView2.schelp](file:///Users/fuo/Library/Application Support/SuperCollider/downloaded-quarks/TabbedView2/HelpSource/Classes/TabbedView2.schelp)
link::Classes/TabbedView2::
sc version: 3.7.2</div>

</div>