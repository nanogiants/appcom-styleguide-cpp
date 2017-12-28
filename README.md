# Appcom C++ Style Guide

This document describes the style guide applied to C++ projects for appcom interactive GmbH. It describes rules how to organize your project, dependencies and files, so that some best practises are held.

So use it in your favor if you want to and/or override the style guide in any way you want.

<a name="table-of-contents"></a>
## Table of Contents

1. [Dependencies](#dependencies)
1. [Comments / Doxygen](#comments)
1. [File Names](#file-names)
1. [Asset Naming Conventions](#asset-naming-conventions)
1. [Roadmap](#roadmap)
1. [Resources](#resources)
1. [License](#license)

<a name="dependencies"></a>
## [0](#dependencies) Dependencies

<a name="dependencies-library-version"></a>
### [0.1](#dependencies-library-version) Library version

Always use the latest stable version of a library if possible.
Make sure to migrate also major releases if possible.

<a name="dependencies-library-provision"></a>
### [0.2](#dependencies-library-provision) Library provision

Libraries must be included using git submodules if compiled within the project itself or using an artefact repository (like sonatype nexus) if precompiled. Provide a script for installing these if needed. The name of the script must be install-deps.sh and placed at the source root.

<a name="dependencies-folder"></a>
### [0.3](#dependencies-folder) Folder

Dependencies should be found and structured at a well known place. Therefore these must be placed under the `deps` folder at the souce root. Precompiled libraries must be placed under the subfolder `lib` and the corresponding header files must be under the subfolder `include`.

**[back to top](#table-of-contents)**

<a name="comments"></a>
## [0](#comments) Comments / Doxygen

<a name="comments-documentation"></a>
### [0.1](#comments-documentation) Documentation

Every class and it's methods must contain a description of what it is for and how it does it's task. To utilize IDEs with doxygen support and to be able to generate a documentation, these descriptions must use the doxygen syntax. To be uniformly the `!` is used to mark a doxygen comment and `@` to mark commands like `@brief` and `@param`.

```
// good

/*!
* @brief This does something.
* @details A more detailed description ...
* @param tag The tag that is used to do something.
* @return true if done successfully, false on failure.
* @sa doSomethingRelated()
*/
bool doSomething(string* tag);

// bad

/**
* \brief This does something.
* \param tag The tag that is used to do something.
*/
void doSomething(string* tag);
```

<a name="comments-multiline-comments"></a>
### [0.2](#comments-multiline-comments) Multiline comments

Use `/*! ... */` for block comments.

```
// good

/*!
* @brief This does something.
* @param tag The tag.
*/
bool doSomething(string* tag);

// bad

// @brief This does something.
// @param tag The tag.
bool doSomething(string* tag);
```

<a name="comments-singleline-comment"></a>
### [0.3](#comments-singleline-comment) Singleline comment

Use `//` for single line comments.
Place single line comments on a newline above the subject of the comment. Put an empty line before the comment unless it's on the first line of a block.

```
// good
// is current tab
int active = true;

// bad
int active = true; // is current tab

// good
int getType()
{
    BOOST_LOG_TRIVIAL(debug) << __FILE__ << "(" << __LINE__ << "): " << "Fetching type...";

    // set the default type to 'no type'
    int typeOut = _type ? _type : -1;

    return typeOut;
}

// bad
int getType()
{
    BOOST_LOG_TRIVIAL(debug) << __FILE__ << "(" << __LINE__ << "): " << "Fetching type...";
    // set the default type to 'no type'
    int typeOut = _type ? _type : -1;
    
    return typeOut;
}

// also good
int getType()
{
    // set the default type to 'no type'
    int typeOut = _type ? _type : -1;
    
    return type;
}
```

<a name="comments-spaces"></a>
### [0.4](#comments-spaces) Spaces

Start all comments with a space to make it easier to read.

```
// good
// is current tab
int active = true;

// bad
//is current tab
int active = true;
```

<a name="comments-fixme"></a>
### [0.5](#comments-fixme) Fixme

Use `// FIXME:` to annotate problems.

```
Calculator::Calculator()
{
    // FIXME: shouldn't use a global here
    _total = 0;
}
```

<a name="comments-todo"></a>
### [0.6](#comments-todo) Todo

Use `// TODO:` to annotate solutions to problems.

```
Calculator::Calculator()
{
    // TODO: total should be configurable by an options param
    _total = 0;
}
```

**[back to top](#table-of-contents)**

<a name="file-names"></a>
## [5](#file-names) File Names

File names must reflect the name of the class implementation that they contain, including case.
Follow the convention that your project uses. File extensions must be as follows:

| Extension | Type |
|---|---|
| .h | C header file |
| .hpp | C++ header file |
| .c | C implementation file |
| .cpp | C++ implementation file |

Files containing code that may be shared across projects or used in a large project must have a clearly unique name, typically including the project.

**[back to top](#table-of-contents)**

<a name="asset-naming-conventions"></a>
## [0](#asset-naming-conventions) Asset Naming Conventions

<a name="asset-naming-conventions-image-naming"></a>
### [0.1](#asset-naming-conventions-image-naming) Image Naming

Images must be named after the following pattern:

```
<WHAT>_<WHERE>_<DESCRIPTION>[_<SIZE>][_STATE]
```

```
// example
bg_login_background
ic_login_button_small_pressed
```

The `WHAT` denodes the type of the drawable. It can be one of the following:

* ic (Icons)
* bg (Backgrounds)
* shape (Shapes)

The `WHERE` describes in which part of the app the drawable is used. If the drawable is used in more than one screen use `all`.
The `DESCRIPTION` must tell the reader what the actual purpose of the drawable is.
The `SIZE` part is optional and describes the size of the drawable. This can either be a measurable (e.g. 24dp) or a generic term (e.g. small).
`STATE` indicates optionally the state of the drawable. It can be one of the following:

* normal (can be omitted)
* disabled
* selected
* pressed

**[back to top](#table-of-contents)**

<a name="roadmap"></a>
## [0](#roadmap) Roadmap

This section describes items, which will be added to this style guide in the future.
These items are categorized in two sections namely `next` for items added in the next release and `future` for items added in future releases without a fixed date.

<a name="roadmap-next"></a>
### [0.1](#roadmap-next) Next

<a name="roadmap-future"></a>
### [0.2](#roadmap-future) Future

* Linter for continuous integration based on this style guide

**[back to top](#table-of-contents)**

<a name="resources"></a>
## [0](#resources) Resources

<a name="resources-documentation"></a>
### [0.1](#resources-documentation) Documentation

* [http://www.stack.nl/~dimitri/doxygen/manual/docblocks.html](http://www.stack.nl/~dimitri/doxygen/manual/docblocks.html)

<a name="resources-related-work"></a>
### [0.2](#resources-related-work) Related Work

This Style Guide is inspired by the following Style Guides:

* [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)
* [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html)

**[back to top](#table-of-contents)**

<a name="license"></a>
## [0](#license) License

(The MIT License)

Copyright (c) 2017 appcom interactive GmbH

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
