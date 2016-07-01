If you are planning to use some modern Web feature with QtWebKit, or you are using it already and suspect that it does not work at all, this guide is for you.

Note that it can be applied to any WebKit port, not only QtWebKit. All you need is git repository, checked out at appropriate branch or tag.

For example, we will find out if QtWebKit supports CSS property `initial-letter`.

### Step 1. Determine if WebKit engine have code to support your feature

If feature is supported, it has to be mentioned in source code. Let's check:

`git grep initial-letter Source/ ':!*ChangeLog*'`

Results:
```
Source/WebCore/css/CSSLineBoxContainValue.cpp:73:        text.appendLiteral("initial-letter");
Source/WebCore/css/CSSPropertyNames.in:523:-webkit-initial-letter [Converter=InitialLetter]
Source/WebCore/css/CSSValueKeywords.in:1055:initial-letter
Source/WebCore/features.json:437:        "url": "http://dev.w3.org/csswg/css-inline/#propdef-initial-letter",
Source/WebCore/rendering/RenderBlockLineLayout.cpp:1745:        // We have to reset the cap-height alignment done by the first-letter floats when initial-letter is set, so just always treat first-letter floats
Source/WebCore/rendering/line/LineWidth.cpp:85:    // initial-letter float always shrinks the first line.
```
OK, we see that it is recognized by CSS paraser and is prefixed (`-webkit-initial-letter`). To be sure that it is actually working in QtWebKit you might also want to check if it is not under some `#if` condition in `CSSPropertyNames.in` file.

Even if you haven not found anything, proceed to step 2.

Also https://webkit.org/status/ may be useful, but it does not have information about every feature you may be interested in.

### Step 2. Check if there are tests for your feature

`git grep initial-letter LayoutTests ':!*ChangeLog*'`

Results:

```
LayoutTests/fast/css-generated-content/initial-letter-basic.html:5:div::first-letter { -webkit-initial-letter: 3; margin-right:2px; margin-left:2px }
LayoutTests/fast/css-generated-content/initial-letter-border-padding.html:5:div::first-letter { color:red; border:2px solid red; padding:1px; -webkit-initial-letter: 3 2; margin-right:2px; margin-left:2px }
LayoutTests/fast/css-generated-content/initial-letter-clearance.html:5:div::first-letter { font-family: Zapfino; -webkit-initial-letter: 4 2; margin-right:2px; margin-left:2; }
LayoutTests/fast/css-generated-content/initial-letter-descender.html:5:div::first-letter { font-family: Zapfino; -webkit-initial-letter: 4 2; margin-right:2px; margin-left:2 }
LayoutTests/fast/css-generated-content/initial-letter-first-line-wrapping.html:15:        -webkit-initial-letter: 5;
LayoutTests/fast/css-generated-content/initial-letter-raised.html:5:div::first-letter { -webkit-initial-letter: 3 2; margin-right:2px; margin-left:2px }
LayoutTests/fast/css-generated-content/initial-letter-sunken.html:5:div::first-letter { -webkit-initial-letter: 2 3; margin-right:2px; margin-left:2px }
```

We've found that it has several layout tests. Proceed to step 3.

### Step 3. Try out layout tests you've just found

For example,

`Tools/Scripts/run-minibrowser --qt LayoutTests/fast/css-generated-content/initial-letter-basic.html`

You see that it is not rendered properly. Proceed to step 4.

**WARNING**: Some tests won't work if simply opened in browser, because they rely on testing infrastructure support. See [[Running Layout Tests]]

### Step 4. See what other WebKit ports do in this test.

You can run the same tests in different WebKit port available for your platform, but if it is not available, there is easier way.

Search for expected results of test:

`find LayoutTests/ -name 'initial-letter-basic*'`

Results:

```
LayoutTests/fast/css-generated-content/initial-letter-basic.html
LayoutTests/platform/gtk/fast/css-generated-content/initial-letter-basic-expected.txt
LayoutTests/platform/ios-simulator/fast/css-generated-content/initial-letter-basic-expected.txt
LayoutTests/platform/efl/fast/css-generated-content/initial-letter-basic-expected.txt
LayoutTests/platform/mac/fast/css-generated-content/initial-letter-basic-expected.txt
LayoutTests/platform/mac/fast/css-generated-content/initial-letter-basic-expected.png
LayoutTests/platform/win/fast/css-generated-content/initial-letter-basic-expected.txt
```

Great, there is one PNG file! Open `LayoutTests/platform/mac/fast/css-generated-content/initial-letter-basic-expected.png` in any image viewer to see, how does Mac port render this test.