# Learn to Code HTML & CSS
review of the basics
source : http://learn.shayhowe.com/html-css/

## further reading

## notes
HTML - hypertext markup language - content
CSS - cascading style sheets - appearance of content

## common terms
http://www.scriptingmaster.com/html/HTML-terms-glossary.asp

<b>Alt text</b> - text description of a graphic that appears before the graphic is loaded, rollover

<b>Anchor</b> - <a></a> - used to define a hypertext link
Angle brackets - < > to surround an element to create a tag
Attribute - property of html element (in the start of the html tag) provide instructions to an html tag

Broken links - that do not work because destination has been deleted or path has changed

Browser - program used to access and display HTML

CGI (common gateway interface) - programming standard that defines how programs communciate with each other and with the web server (generally called a script)

Clickable map - aka imagemap

Closing tag - html instruction that tells the browser to turn off a specific feature of an opening tag

Comments - info for future reference <!-- -->

Deprecated element - element that will be obsolete in the future and needs to be replaced

Document content - text and graphics of a web doc that you want the user to see

Document Type Definition (DTD) - specification for a markup language

Domain name - alphabetic name for a computer host mapped to a computer's numeric IP address

Elements - an element in html = tag (e.g. <head>, <body>, <p>) or element of structure of a document (body, title, paragraph)

Entities - characters that do not appear on the keyboard(i.e., ™ ©, ®, etc.) or characters that have special meaning in HTML (i.e., <, >, &, etc.).

Form
A mechanism that enables a user to supply input to the web page author.

Footer text
The text that is not specifically related to the content of the webpage and that appears on every webpage is referred to as footer text. The most notable example of footer text is the copyright statements at the bottom of webpages.

Frames - HTML supports frames to divide a web page into independent and scrollable sections. Having two frames on a web page is like loading three separate pages in the browser. A common use for frames is to place the navigation on the left, and content on the right.

Frames (used at the top of a web page to specify HTML version) - A frames document type definition indicates that the document uses frames and it also supports deprecated elements. This is the most flexible document type definition.

FTP stands for File Transfer Protocol. FTP is a robust method for transferring files between computers using TCP/IP. TCP stands for Transmission Control Protocol and 

IP stands for Internet Protocol. TCP is responsible for transporting data and IP is responsible for making sure data goes to the correct address.

GIF (Graphics Interchange Format) - A file format (commonly used for web pages) used for storing image files.

Hotspot - A defined area on an image that acts as a hyperlink.

HTML (Hypertext Markup Language)
A web scripting language used for creating web page documents.

HTML converter
A software that converts text to HTML code.

HTML editor
A software that inserts HTML code as you work to create an HTML file.

Hypermedia - Hypertext that may include multimedia like text, images, sound, and video.

Imagemap - A graphic that has clickable areas (or hotspots) defined to allow a user to move to another URL.

Inline - Elements those that are supported directly by HTML are known as inline. Also, another characteristic of inline element is that their output can be seen or heard without the user taking any additional action (such as clicking, and installing of a plug-in) because the output is directly placed on the webpage. Inline elements include, for instance, animated graphics, graphics, and sound.

JPEG or JPG (Joint Photographic Experts Group)
A common cross-platform image format that is used on the web.

Line break - Line break simply refers to stop of the current line and continuation to the next line. In HTML documents, the <br> tag is used to end a line.

Link - A hypertext link used to connect one document with another document or file.

Mirror site - A mirror site is a copy of a publicly available website.

Nesting/nested tags - Nesting occurs when you place tags within other tags. Anytime you create an HTML document, you will end-up using nested tags. For example, the <title>, and <body>, tags are nested inside the root <html> tag. The <body> tag is likely to also nest inside of itself other tags.

Navigating - The act of observing the content of web for some purpose.

Obsoleted element - An element that won't necessarily work in the future versions of browsers. Any obsolete element that you may be using in your website should be removed; otherwise, newer browsers would ignore that element.

Opening tag - An HTML instruction that tells the browser to turn on the feature and apply it to the document content that follows.

Out-of-line - those elements that require the user to take some additional action to see or hear the output of the element. The additional action could consist of clicking or installing of a plug-in. Examples of out-of-line elements include video, 3-D models, animations, etc.

Pixel - A collection of dots that make up a monitor's display. On color monitors, a pixel contains three dots: red, green, and blue. On monochrome monitors, a pixel contains only one dot.

Robot - A software that automatically explores the web.

Server - A software application that serves requests initiated by client programs.

Strict (used at the top of a web page to specify HTML version) The strict version indicates that the web document does not use frames or any deprecated elements. If a web document is based on a strict definition, it must have clean HTML (meaning all opened tags must be closed, attribute values surrounded by double quotation marks, etc.).

Style sheet - A style sheet includes styling syntax (rules) that dictates how your web page will look. Style sheets are very useful as they help web developers create uniform (or consistent) presentation of web pages.

Syntax - Syntax basically refers to the rules a computer language uses to perform a task. Without syntax, a computer language would not be functional or useful at all. HTML syntax dictates what and how a web page will display.

Syntax error - A syntax error basically refers to a situation in which the rules (or a rule) of the computer language are (is) broken. In HTML, depending on the syntax error you produce, the web page may look completely different than what you had intended.

Tags = the HTML code that controls the appearance of an HTML document's content.

Transitional (used at the top of a web page to specify HTML version) A document defined as transitional may include deprecated elements and all the new HTML elements. However, the document cannot contain frames.

Uploading - Think of uploading as just opposite of downloading. While uploading simply means moving/sending files to the server, downloading means getting/receiving files from the server.

World Wide Web Consortium (W3C) - An organization consisting of representatives from member companies and responsible for making rules for the World Wide Web.

## concepts
elements - designators that define the structure and content of objects within a page
  h1, p, a, div, span, strong, em

tags - <> surrounding an element
  opening tag <div> marks the beginning of an element
  closing tag </div> marks the end of an element
  between the elements = the content of the element

attributes - properties used to provide additional info about an element
  id, class, src, href 
  defined within the opening tag after the element name
  have a name and value

minimum required
  <!DOCTYPE html> - informs web browsers which version of HTML is used - default latest
  <html lang="en"> 
    <head>
      identifies the top of the doc and metadata, links to external files 
      <meta charset="utf-8">  character encoding of the page
      <title> this is the title </title> title of the document
    </head>
    <body>all visible content</body>
  </html>

