# When a user enters an URL in the browser, how does the browser fetch the desired result.

- looks up the location of the server hosting the website
- makes the connection to the server
- sends a request to get the specific page
- handles the response from the server and
- how it renders the page so you, the viewer, can interact with the website



## What is the main functionality of the browser?

- Browser initiates a TCP (Transfer Control Protocol) connection with the server using synchronize(SYN) and acknowledge(ACK) messages.

- Browser sends an HTTP request to the web server. GET or POST request.
- Server on the host computer handles that request and sends back a response. - It assembles a response in some format like JSON, XML and HTML.
- Server sends out an HTTP response along with the status of response.
- Browser displays HTML content


## High Level Components of a browser.

- User interface
- browser engine
- rendering engine
- Networking: netwroking call HTTP requests
- UI backend: uses operating system user interface methods
- JavaScript interpreter. Used to parse and execute JavaScript code
- Data storage

![alt text](https://user-images.githubusercontent.com/56916664/208243276-e905b88a-cb01-4ae8-9926-fcdd0f0a664c.png)

## Rendering engine and its use

- Rendering engine displays the requested contents on the browser screen.
- By default the rendering engine can display HTML and XML documents and images. It can also display other types of data as well.
- Different browsers use different rendering engines: 
  - Internet Explorer uses Trident. 
  - Firefox uses Gecko. 
  - Safari uses WebKit. 
  - Chrome and Opera (from version 15) use Blink, a fork of WebKit
- Rendering engine will start parsing the HTML document and convert elements to DOM nodes.


![alt text](https://user-images.githubusercontent.com/56916664/208243701-7a504265-6f7e-465f-9032-fdf913f2d1e7.png)

## Parsers (HTML, CSS, etc)

- Parsing a document means translating it. 
- The result is usually a tree of nodes that represent the structure of the document. Called a syntax tree.
- Parsing can be separated into two sub processes: lexical analysis and syntax analysis
- Lexical analysis is the process of breaking the input into tokens.
- Syntax analysis is the applying of the language syntax rules.
- HTML parser is to parse the HTML markup into a parse tree.
- CSS file is parsed into a StyleSheet object. Each object contains CSS rules.

## Script Processors

- script processor executes Javascript code to process an event
- The parsing of the document halts until the script has been executed.
-  If the script is external then the resource must first be fetched from the network - this is also done synchronously.


## Tree constructing

- While the DOM tree is being constructed, the browser constructs another tree, the render tree. This tree is of visual elements in the order in which they will be displayed.
- The purpose of this tree is to enable painting the contents in their correct order.
- Firefox calls the elements in the render tree "frames". WebKit uses the term renderer or render object.
- A renderer knows how to lay out and paint itself and its children.

## Order of script processing

- Scripts
- Speculative parsing
- Style sheets

## Layout and Painting

### Layout
- Dirty bit system : A renderer that is changed or added marks itself and its children as "dirty": needing layout.

- Global and incremental layout : Incremental layout is triggered (asynchronously) when renderers are dirty.
- Asynchronous and Synchronous layout
- Optimizations : only a sub tree is modified and layout does not start from the root.
- The layout process
  - Parent renderer determines its own width.
  - Parent goes over children
  - Parent uses children's accumulative heights and the heights of margins and padding to set its own height
- Width calculation :The renderer's width is calculated using the container block's width, the renderer's style "width" property, the margins and borders.
- Line Breaking : When a renderer in the middle of a layout decides that it needs to break, the renderer stops and propagates to the layout's parent that it needs to be broken. 

### Painting

In the painting stage, the render tree is traversed and the renderer's "paint()" method is called to display content on the screen. Painting uses the UI infrastructure component.

- Global and Incremental
  - Like layout, painting can also be global - the entire tree is painted - or incremental. 
  - In incremental painting, some of the renderers change in a way that does not affect the entire tree. The cha

- The painting order
  - This is actually the order in which the elements are stacked in the stacking contexts.
  - background color
  - background image
  - border
  - children
  - outline

- Dynamic changes
  - The browsers try to do the minimal possible actions in response to a change. So changes to an element's color will cause only repaint of the element.

- The rendering engine's threads
  - The browsers try to do the minimal possible actions in response to a change. So changes to an element's color will cause only repaint of the element.

- Event loop
  - The browser main thread is an event loop. It's an infinite loop that keeps the process alive. It waits for events (like layout and paint events) and processes them.

![Event loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop/the_javascript_runtime_environment_example.svg)

## License

[MIT](https://choosealicense.com/licenses/mit/)