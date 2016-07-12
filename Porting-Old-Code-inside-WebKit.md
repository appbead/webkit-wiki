* Replace `OVERRIDE` with `override`. (You may want to do the same with `Q_DECL_OVERRIDE` in non-API code as well)

### Smart pointers
* `OwnPtr` and `PassOwnPtr` should be replaced with `std::unique_ptr`
* Replace `adoptPtr(new Something(...))` with `std::make_unique<Something>(...)`
* `adoptPtr` which use existing pointer instead of `new` should be transformed to usage of `std::unique_ptr` constructor
* Replace `OwnPtr::clear()` with `= nullptr`

### JSC and its usage (bridge, WebKit)
* `FooBar* fb = static_cast<JSFooBar*>(object)->impl()` becomes `FooBar* fb = JSFooBar::toWrapped(object)`
* `JSC::Identifier` constructors should probably be replaced with `JSC::Identifier::fromString`

### WebCore
* These classes are now commonly passed by reference, not by pointer: `GraphicsContext`, `RenderObject`, `RenderStyle`, `StyleResolver`
* `Clipboard` was renamed to `DataTransfer`
* `Font` class was renamed to `FontCascade`, `SimpleFontData` to `Font`
* Replace invocations of `toClassName()` **non-method** functions with `downcast<ClassName>`
* If code uses virtual method like `Node::toInputElement()`, use `is<ClassName>` before `downcast<ClassName>`, because old methods were forgivingly returning `0` in case of wrong type.
* Timer is not template anymore, see https://github.com/annulen/webkit/commit/50862feb41477701a0daee3dda170e9ac139c3d3
* Many enums were converted to C++11 enum classes, slightly changing their names and usage

### Modernization TODO
The next items don't cause compiler errors right now, but should be replaced to make code future-proof:
* Eleminate PassRefPtr [#18](https://github.com/annulen/webkit/issues/18)
* Replace DEPRECATED_DEFINE_STATIC_LOCAL with NeverDestroyed [#19](https://github.com/annulen/webkit/issues/19)
* Use references for types which are commonly passed by reference in WebCore
* Where possible, avoid conversion of 8-bit Strings to QStrings