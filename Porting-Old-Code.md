### Smart pointers
* `OwnPtr` and `PassOwnPtr` should be replaced with `std::unique_ptr`
* Replace `adoptPtr(new Something(...))` with `std::make_unique<Something>(...)`
* `adoptPtr` which use existing pointer instead of `new` should be transformed to usage of `std::unique_ptr` constructor
* Replace `OwnPtr::clear()` with `= nullptr`

### JSC and its usage (bridge, WebKit)
* `FooBar* fb = static_cast<JSFooBar*>(object)->impl()` becomes `FooBar* fb = JSFooBar::toWrapped(object)`

### WebCore
* These classes are now commonly passed by reference, not by pointer: `GraphicsContext`, `RenderObject`, `RenderStyle`, `StyleResolver`
* `Font` class was renamed to `FontCascade`, `SimpleFontData` to `Font`
* Replace `toClassName()` invocations with `downcast<ClassName>`
* Many enums were converted to C++11 enum classes, slightly changing their names and usage