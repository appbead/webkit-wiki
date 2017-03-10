### WebKit 1 (QWebView or QGraphicsWebView)

The main class is GraphicsContext (Qt-specific code is mostly located in GraphicsContextQt.cpp). Think of it as QPainter that provides even more fancy drawing operations, e.g. it can fill rectangle with round hole with a single call. In Qt port GraphicsContext is actually implemented on top of QPainter, it "lowers" complex operations of GraphicsContext API (that sometimes have peculiar behavior that directly affects how web pages look if implemented improperly) to QPainter calls. GraphicsContext also supports transparency layers, that are currently implemented as a stack of QPixmap's drawn on top of main layer. Pointer to QPainter can always be obtained from GraphicsContext via platfromContext() method.

So, if you see visual artifacts in web page that don't disappear when AcceleratedCompositing (AC from now on) is disabled, chances are high that it is GraphicsContextQt bug.

Point of entry for drawing is QWebFrameAdapter::renderRelativeCoords. It creates new GraphicsContext from given QPainter (that may be created by QWebView, or be supplied by user), and renders all visible parts of page that need update.

QWebFrameAdapter::renderCompositedLayers() is used to draw additional layers when AC is enabled. Point of AC is that parts of page, e.g. those that are animated, are drawn in separate layers. TextureMapper is used to composite them, it can use raster images in case of software mode (and draw them with GraphicsContext, see TextureMapperImageBuffer), or use OpenGL directly (TextureMapperGL).

### WebKit 2

Here AC is always on, and TextureMapper is always in use. However, additional system called CoordinatedGraphics is working on top of TextureMapper. It supports breaking layer into tiles (TiledBackingStore), and also supports working in multiprocess environment.

Read https://trac.webkit.org/wiki/CoordinatedGraphicsSystem

Actual backing store (pixels where GraphicsContext paints) is owned by WebCoordinatedSurface