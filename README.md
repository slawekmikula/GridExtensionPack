# GridExtensionPack Add-on for Vaadin 7.5

GridExtensionPack is a collection of more or less useful extensions for tweaking 
Grid UX.

## Online demo

Online demos for extensions are not available right now.

## Download release

Official releases of this add-on are available at Vaadin Directory. For Maven 
instructions, download and reviews, go to http://vaadin.com/addon/GridExtensionPack

## Building and running demo

- git clone https://github.com/tsuoanttila/GridExtensionPack.git
- mvn clean install
- cd GridExtensionPack-demo
- mvn jetty:run

To see the demo, navigate to http://localhost:8080/

## Development with Eclipse IDE

For further development of this add-on, the following tool-chain is recommended:
- Eclipse IDE
- m2e wtp plug-in (install it from Eclipse Marketplace)
- Vaadin Eclipse plug-in (install it from Eclipse Marketplace)
- Chrome browser

### Importing project

Choose File > Import... > Existing Maven Projects

Note that Eclipse may give "Plugin execution not covered by lifecycle 
configuration" errors for pom.xml. Use "Permanently mark goal resources in 
pom.xml as ignored in Eclipse build" quick-fix to mark these errors as 
permanently ignored in your project. Do not worry, the project still works fine. 

## Release notes

### 0.2.4
- ContextClick and SidebarMenu bug fixes
- Header wrapping extension

### Version 0.2.3
- Bug fixes

### Version 0.2.2
- Server-side ContextClickEvent
- Table-like client-side selection UX
- PagedContainer
- SidebarMenuExtension

## Roadmap

This component is developed as a hobby with no public roadmap or any guarantees 
of upcoming releases. That said, the following features are planned for upcoming 
releases:
- Not much for now

## Issue tracking

The issues for this add-on are tracked on its GitHub page. All bug reports and feature requests are appreciated. 

## Contributions

Contributions are welcome, but there are no guarantees that they are accepted as 
such. Process for contributing is the following:
- Fork this project
- Create an issue to this project about the contribution (bug or feature) if there is no such issue about it already. Try to keep the scope minimal.
- Develop and test the fix or functionality carefully. Only include minimum amount of code needed to fix the issue.
- Refer to the fixed issue in commit
- Send a pull request for the original project
- Comment on the original issue that you have implemented a fix for it

## License & Author

Add-on is distributed under Apache License 2.0. For license terms, see LICENSE.txt.

GridExtensionPack is written by Teemu Suo-Anttila

SidebarMenuExtension is written by Anna Koskinen

# Developer Guide

## Getting started

Here is a simple example on how to try out an extension in this add-on:

```java
Grid grid = new Grid();
ContextClickExtension.extend(grid).addContextClickListener(/* Insert 
context click listener here */);
```

Using the PagedContainer needs an existing Indexed container to wrap:

```java
// This is your existing container
Container.Indexed myContainer;
PagedContainer container = new PagedContainer(myContainer);
Grid grid = new Grid(container);

// PagedContainer has a helper class for page manipulation
PagingControls controls = container.setGrid(grid);

// Set container (and grid with it) to certain size
controls.setPageLength(5);

// Jump to fourth page (0-based indexing)
controls.setPage(3);

// Jump to next (fifth) page
controls.nextPage();
```

For a more comprehensive example, see DemoUI.java in GridExtensionPack-demo

## Features

### ContextClickExtension

ContextClickExtension catches the context menu events targeting the body 
of Grid, and sends events similar to ItemClickEvent.

This extension can be relatively easily made to work with ContextMenu 
addon for displaying a custom context menu for the Grid.

### TableSelectionModel

TableSelectionModel gives you client-side selection UX similar 
to Table. It supports Multiple selection in simple mode and with ctrl + 
click.

### PagedContainer

A simple Container wrap on top of any indexed container. Works through 
paging and provides its own PagingControls for a cleaner API.

This also works with Table, but I don't intend to track any possible 
issues with it.

### SidebarMenuExtension

This extension provides a way to add custom items in the Grids 
SidebarMenu. Setting styles and custom captions along with running 
certain code when the menu item is clicked, this is the easiest way to 
get your special actions in to said menu.

### WrappingGridExtension

This extension makes possible to wrap text in headers. Sometimes you
need long header description in columns where the data content is short
(e.g. number). With this extension you can enable wrapping text in
header row and it auto adjusts the header row height accordingly. If 
you use this extension, you need to set fixed widths to columns, since 
otherwise it is not possible reliably calculate needed height of the 
header row. 

### GridRefresher

A simple helper extension that gives you an API that you can use to
force the repaint of a row.

## API

No online JavaDoc available (for now at least).

## Changes since 0.2
### Version 0.3-SNAPSHOT
- Table-like selection now in a SelectionModel, not an extension
- ContextClickExtension dropped, since the functionality is now present in the Framework
- GridRefresher extension that gives a helper to force repaint rows
