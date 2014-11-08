pathfinding - APACHE LICENSE 2.0
==========

<p>
A java pathfinding library meant to be used for games.
It is generic enough to be used in different kind of graphs (though, right now it only has implementation for grid graphs).

It was heavily inspired by [this](https://github.com/qiao/PathFinding.js/ "Pathfinding.js") javascript library. Code initially was adapted, then
some modifications were made.

This library works with Libgdx's html5 backend, it was even used in my [#1GAM january entry](https://github.com/xaguzman/shiftingislands/ "Shifting Islands Source").

Current stable version is 0.2.4

__________

## Installing
The library has been uploaded to sonatype oss repository.
If you are using libgdx you can install it via graddle adding this dependency to your core project:

>	compile "com.github.xaguzman:pathfinding:0.2.4"

If you want to try the gdx-bridge, add another dependency to your project.

>	compile "com.github.xaguzman:pathfinding-gdx-bridge:0.2.4"

Right now there's no documentation for using the gdx-bridge. For a quick reference on how to use the gdx-bridge, please see this [test](https://github.com/xaguzman/pathfinding/blob/master/tests/src/main/org/xguzm/pathfinding/tests/MapLoadingTest.java "MapLoadingTest")

## Intro
The library works on a bunch of interfaces:
* NavigationNode: this basically just represents a node of a graph. contains some getters and setters meant for navigation. Right now, only implementation is GridCell
* NavigationGrap: a group of navigation nodes. Right now, only implementation is NavigationGrid
* PathFinder: the implementation for the pathfinding algorithm, current options are:
	* AStarFinder
	* AStarGridFinder
	* JumpPointFinder
	* ThetaStarFinder
	* ThetaStarGridFinder

Finders are fed with so called PathFinderOptions, which determine how the pathfinding will work (allowing diagonal movement, for example).

## How to use
You need to create a graph.
Be aware the the NavigationGrid class, expects a bidimensional array of GridCell stored as [x][y]

	//these should be stored as [x][y]
	GridCell[][] cells = new GridCell[5][5];
	
	//create your cells with whatever data you need
	cells = createCells();
	
	//create a navigation grid with the cells you just created
	NavigationGrid<GridCell> navGrid = new NavigationGrid(cells);

Now, you need a finder which can work on your graph.

	//create a finder either using the default options
	AStarGridFinder<GridCell> finder = new AStarGridFinder(GridCell.class);
	
	//or create your own pathfinder options:
	GridFinderOptions opt = new GridFinderOptions();
	opt.allowDiagonal = false;
	
	AStarGridFinder<GridCell> finder = new AStarGridFinder(GridCell.class, opt);

Once you have both, a graph and a finder, you can find paths within your graph at any time.

	List<GridCell> pathToEnd = finder.findPath(0, 0, 4, 3, navGrid);
	
That's pretty much all there is to using the library.



